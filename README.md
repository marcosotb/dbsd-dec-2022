<a target="_blank" href="https://colab.research.google.com/github/yushan777/dbsd-xmas-edition/blob/main/dbsd_dec_2022.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab" width="300"/>
</a>

# Dreambooth Stable Diffusion Winter 2022 Edition
This colab is based on ShivamShrirao's repository and colab, modified to use older dependencies from late 2022.  
The diffusers repo itself will be locked to commit: `fbdf0a17055ffa34679cb34d986fabc1296d0785` 2022-03-02

https://github.com/ShivamShrirao/diffusers/ \
https://github.com/ShivamShrirao/diffusers/tree/main/examples/dreambooth

This also serves as an exercise of me to to learn a bit of Python, Jupyter and git, as all are kinda new for me. 

### Why? 
The performance of models trained on the original colab has occasionally been affected by sudden changes in dependencies, resulting in complaints about inconsistencies in the results. This issue seemed to have peaked in early January 2023, according to anecdotal evidence. Although the situation has stabilized, there are still sporadic comments regarding this matter.

The aim of this colab is to lock-in dependencies from late 2022. Diffusers from the repo will be built and installed from Commit `fbdf0a17055ffa34679cb34d986fabc1296d0785`. 

train_dreambooth.py needs to be modified since calls (introduced Jan 5th 2023) are made that require Accelerate 0.14.0 but we are using 0.12.0.  Specifically, references to the use of `accelerator.unwrap_model(model, keep_fp32_wrapper=True)`. need to be changed to just `accelerator.unwrap_model(model)`

# Cell 1
Mount Google Drive.  This isn't essential but if you store training images, models there then you need to mount it. 

# Cell 2
Build Environment. Downloads and installs required dependencies. 

