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


## Cell 1. Google Drive & Build Environment
#### Mount Google Drive
* Will act like a local drive in the colab's filesystem. This isn't essential but you should mount the drive if: 
* You store training images, models and other resources needed for training.  
* You wish to quickly save trained models there so you can download at a later time.
#### Downloads and installs required dependencies. 
* These dependencies date back to late 2022.  
* Diffusers itself will be installed from commit `fbdf0a17055ffa34679cb34d986fabc1296d0785`.  
* Scripts to convert to and from Stable Diffusion Original (ckpt/safetensors) and Diffusers are also downloaded. 
* File train_dreambooth.py will be modified upon download to remove references to `keep_fp32_wrapper=True` when function `accelerator.unwrap_model()` is used since it is not available in Accelerate 0.12.0

## Cell 2. Token Word, Class Word & Class Prompt
#### Token Word.
* Can be anything but ideally it should be short.  
* Avoid common nouns and names since they are very likely to have a strong associations already in the model you are training on.
* Examples : `skf, lun, whoo, olis...`
#### Class Word. 
* Class word should represent the broad concept you are trying to train
* Examples: `person, man, woman, dog, cat, car`
* Token and Class word are used together to represent your subject being trained. \
* Example: `photo of [zwf] [person] sitting in a cafe.` \
#### Class Prompt 
* Used for generating class images used for regularization.  
* Generated from the base model that you are training on. 
* Can be the same as Class Word or more descriptive such as, `photo of a person`.  
* If you are providing your own set of class images, then this prompt will be ignored. 
* If empty, defaults will be used. 

## Cell 3. Download / Convert Model & Set Model Path
#### Only fill one field. If both fields are filled-in then the last field will be used. <br>
#### HUGGINGFACE_MODEL_PATH
* Use this field to point to the HuggingFace repo `user/repo-name` format.
  * `runwayml/stable-diffusion-v1-5`
* If it is local (on your Google Drive), you can just point it to that location
  * `drive/MyDrive/diffusers-models/sd15` (relative)
  * `/content/drive/MyDrive/diffusers-models/sd15` (absolute)
#### CKPT_SAFETENSOR_URL
* Use this field to directly download a ckpt/safetensor model which will then be converted to diffusers.
* Links from various sources are supported including HuggingFace, Civitai, Google Drive (that isn't mounted)
  * `https://huggingface.co/runwayml/stable-diffusion-v1-5/resolve/main/v1-5-pruned-emaonly.ckpt` \
  * `https://civitai.com/api/download/models/6987?type=Model&format=PickleTensor` \
  * `https://civitai.com/api/download/models/6987?type=Model&format=SafeTensor` \
  * `https://drive.google.com/file/d/1JEZCyW36ziz9Fn482MUG8T0_2P4FGG-/view?usp=share_link` _(google drive share link)_ \
* Model will be converted into directory `/content/diffusers-<name of model>`

## Cell 4. Instance, Class, Output Directory, Concepts List Settings
#### INSTANCE_DIR
* Directory for instance (training) images. Leave blank for default. 
* Default is `training_images/{TOKEN_WORD}` 
#### CLASS_DIR
* Directory for class images. Leave blank for default. 
* Default is `class_images/{CLASS_WORD}` 
* When training starts, if no class images exist in this directory then they will be created then (slower). 
#### SAVE_TO_GOOGLE_DRIVE
* Save trained models directly to google drive. 
* If you are saving multiple models at intervals as well as converting to ckpts or safetensors, you will need a lot of storage, so this is off by default.
* You can selectively save your model(s) to Google Drive after training.
#### OUTPUT_DIR
* Enter the directory to save trained model(s)okay in. Leave empty for default. 
* _Default is : 
* `stable_diffusion_weights/{TOKEN_WORD}` or..
* If you are saving to Google Drive then it will be: 
* `drive/MyDrive/stable_diffusion_weights/{TOKEN_WORD}`_
#### CONCEPTS LIST
* A file `concepts_list.json` will be created.
* To keep things simple, the list is only for one subject/concept, but can easily be adapted for multiple subjects. (see code)

## Cell 5. Upload Instance (Training) Images
* If the instance directory defined (in Cell 4) does not already contain images, manually upload instance images to the folder 

## Cell 6. Training!
Training cell contains quite a few parameters. A few that are likely to be changed most often have been have been presented on the colabl cell's form:
#### NUM_CLASS_IMAGES
* Number of Class images to generate and/or use.
#### MAX_TRAIN_STEPS
* Maximum number of steps to train.
#### SAVE_INTERVAL
* Save weights at every N steps. (set this to same as or greater than MAX_TRAIN_STEPS to only have one set of weights saved)
#### SAVE_MIN_STEPS
* Start saving weights at and after N steps.

## Cell 7. Generate Grid of Preview Images Generated During Training (Optional)
Generate an XY grid of the preview images that were generated at every saved weight interval.

## Cell 8a. Convert All Weights To ckpt / safetensors. 
Convert all the saved weights to either ckpt or safetensor
##### MODEL_NAME_PREFIX
* name of the model. if it is `Tom_zwx` then models will be `Tom_zwx_xxx.ckpt` or `Tom_zwx_xxx.safetensor` where xxx is the step value.
##### MODEL_FORMAT
* select format of the checkpoint file. 
##### fp16
* Whether to convert to half-precision fp16, (reduces filesize down to 2GB).

## Cell 8b. Convert Specific Weight To ckpt / safetensors
Same as 8a. but just for one weight. 
