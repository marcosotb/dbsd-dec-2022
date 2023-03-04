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

## Cell 1. Mount Google Drive
Mount Google Drive.  Will act like a local drive in the colab's filesystem. This isn't essential but you should mount the drive if: 
* You store training images, models and other resources needed for training.  
* You wish to quickly save trained models there so you can download at a later time.

## Cell 2. Build Environment
* Downloads and installs required dependencies. 
* These dependencies date back to late 2022.  
* Diffusers itself will be installed from commit `fbdf0a17055ffa34679cb34d986fabc1296d0785`.  
* Scripts to convert to and from Stable Diffusion Original (ckpt/safetensors) and Diffusers are also downloaded. 
* File train_dreambooth.py will be modified upon download to remove references to `keep_fp32_wrapper=True` when function `accelerator.unwrap_model()` is used since it is not available in Accelerate 0.12.0

## Cell 3. Token & Class
* Enter Token and Class words. 
* Token word can be anything but ideally it should be short.  Avoid common nouns and names since they are very likely to have a strong prior already in the model you are training on.
* Example tokens: `skff, rune, nlwx...`
* In my experience, if likeness of trained subject isn't quite right, using a different token might improve things. Some people use the same token for all their trained subjects. Some don't.  You can experiment and see what works best for you.
* Example class words : `person, man, woman, dog, cat, car`
* Class word should represent the broad concept you are trying to train
* If empty, defaults will be used. 
