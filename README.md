# Outfit_Swapping_Final

## Overview
This is a implementation for text-prompt based outfit swapping for human avatar images, it consists of two components: (1) a segmentation model ([SegFormer](https://huggingface.co/mattmdjaga/segformer_b2_clothes)) that is used to extract mask corresponding to the dress region of the avatar image; (2) a text-guided inpainting model ([HD-Painter](https://github.com/Picsart-AI-Research/HD-Painter)) that is used to realistically inpaint the masked region of the avatar with user-specified outfit.


[workflow.pdf](https://github.com/user-attachments/files/17119919/workflow.pdf)
