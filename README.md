# Outfit_Swapping_Final

## Overview
This is a implementation for text-prompt based outfit swapping for human avatar images, it consists of two components: (1) a segmentation model ([SegFormer](https://huggingface.co/mattmdjaga/segformer_b2_clothes)) that is used to extract mask corresponding to the dress region of the avatar image; (2) a text-guided inpainting model ([HD-Painter](https://github.com/Picsart-AI-Research/HD-Painter)) that is used to realistically inpaint the masked region of the avatar with user-specified outfit.


![1727206388815-802c448b-74f6-4bab-aae8-c0c13624ef7f_1](https://github.com/user-attachments/assets/5d15a11e-9ff4-4b80-8ba6-31474d0831a3)

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

### More results
![example_one](https://github.com/user-attachments/assets/48384b8a-9cea-4c8f-86d2-3a587b7d2c7a)


![example_two](https://github.com/user-attachments/assets/930012e9-5a83-481d-8985-69d97888a0bd)
