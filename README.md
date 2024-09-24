# Outfit_Swapping_Final

## Overview
This is a implementation for text-prompt based outfit swapping for human avatar images, it consists of two components: (1) a segmentation model ([SegFormer](https://huggingface.co/mattmdjaga/segformer_b2_clothes)) that is used to extract mask corresponding to the dress region of the avatar image; (2) a text-guided inpainting model ([HD-Painter](https://github.com/Picsart-AI-Research/HD-Painter)) that is used to realistically inpaint the masked region of the avatar with user-specified outfit.


![1727206388815-802c448b-74f6-4bab-aae8-c0c13624ef7f_1](https://github.com/user-attachments/assets/5d15a11e-9ff4-4b80-8ba6-31474d0831a3)

