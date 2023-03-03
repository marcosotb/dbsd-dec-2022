<a target="_blank" href="https://colab.research.google.com/github/yushan777/dbsd-xmas-edition/blob/main/DreamBooth_Stable_Diffusion_Xmas_Edition.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

# Dreambooth Stable Diffusion Winter 2022 Edition
This colab is based on ShivamShrirao's repository, modified to use older dependencies from late 2022.  
The diffusers repo will be locked to commit: `xxxxxxxxxxxxxxxxx` 2022-03-03

### Why? 
The performance of models trained on the original colab has occasionally been affected by sudden changes in dependencies, resulting in complaints about inconsistencies in the results. This issue seemed to have peaked in early January 2023, according to anecdotal evidence. Although the situation has stabilized, there are still sporadic comments regarding this matter.

The aim of this colab is to lock-in dependencies from around the time as well as build and install diffusers from that commit. 

train_dreambooth.py needs to be modified since calls (introduced Jan 5th 2023) are made that require Accelerate 0.14.0 but we are using 0.12.0.  Specifically, references to the use of `accelerator.unwrap_model(model, keep_fp32_wrapper=True)`. need to be changed to just `accelerator.unwrap_model(model)`

