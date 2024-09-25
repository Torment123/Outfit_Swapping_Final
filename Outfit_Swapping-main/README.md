# Outfit_Swapping

## Overview
This is a implementation for text-prompt based outfit swapping for human avatar images, it consists of two components: (1) a text prompt-based segmentation model ([ClipSeg](https://github.com/timojl/clipseg)) that is used to extract mask corresponding to the dress region of the avatar image; (2) a text-guided inpainting model ([HD-Painter](https://github.com/Picsart-AI-Research/HD-Painter)) that is used to realistically inpaint the masked region of the avatar with user-specified outfit 

![workflow](https://github.com/user-attachments/assets/db2f26dd-ef61-4289-a2c8-bc83c64903cf)

## Data Preparationg and Preprocessing
The avatar images used in this implementation are from the 'Studio Avatar' tab in [link](https://app.heygen.com/avatars). And based on [heygen-generative-outfit-instruction](https://help.heygen.com/en/articles/8181925-heygen-generative-outfit-instructions) the images are cropped to close-up view, and individuals whose hair fall on the shoulder are not selected.

## Execution
1. Implement the code in get_seg.ipynb to get the segmentation mask, saved as mask.png
2. Get the outfit-swapped image by implementing

```
python hd_inpaint.py \
  --model-id ONE_OF[ds8_inp, sd2_inp, sd15_inp] \
  --method ONE_OF[baseline, painta, rasg, painta+rasg] \
  --image-path HR_IMAGE_PATH \
  --mask-path HR_IMAGE_MASK \
  --prompt PROMPT_TXT \
  --output-dir OUTPUT_DIRECTORY
```
`--model-id` specifies the baseline model for text-guided image inpainting. The following baseline models are supported by the script:
- `ds8_inp` - DreamShaper 8 Inpainting
- `sd2_inp` - Stable Diffusion 2.0 Inpainting
- `sd15_inp` - Stable Diffusion 1.5 Inpainting

If not specified `--model-id` defaults to `ds8_inp`.

` --method` specifies the inpainting method. The available options are as such:
- `baseline` - Run the underlying baseline model.
- `painta` - Use PAIntA block as introduced in the paper.
- `rasg` - Use RASG guidance mechanism as introduced in the paper.
- `painta+rasg` - Use both PAIntA and RASG mechanisms.

## Results
### Ablation on Super-Resolution module of HD-Painter
1. Without super-reoslution module (no artifacts, but less facial details)
![Screenshot 2024-09-07 203428](https://github.com/user-attachments/assets/d40f4efd-7fb2-4f0a-a8a9-b7a4a71fc4d0)

2. With super-resolution module (better facial details, but with artifacts, might due to forced precision change (bf16 to float32), and imperfect segmentation mask

![Screenshot 2024-09-07 204927](https://github.com/user-attachments/assets/3a4c68bd-63a6-46f5-ad25-1adbcde06dc1)


### More results
![Screenshot 2024-09-07 211922](https://github.com/user-attachments/assets/0727bcad-d8a8-4208-9ae6-1b2dc9f0b7ed)


![Screenshot 2024-09-07 213452](https://github.com/user-attachments/assets/83322a15-c2c8-4040-b58a-06f3a3a6b69d)


![Screenshot 2024-09-07 221555](https://github.com/user-attachments/assets/7388aa35-d1bd-4dc1-8305-582bd9a4bd2d)

### Outof distribution cases


![Screenshot 2024-09-07 221045](https://github.com/user-attachments/assets/c4c41279-e270-4fcc-83a7-1fed7d5bfec4)

