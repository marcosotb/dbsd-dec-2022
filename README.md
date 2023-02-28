<a target="_blank" href="https://colab.research.google.com/github/yushan777/dbsd-xmas-edition/blob/main/DreamBooth_Stable_Diffusion_Xmas_Edition.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

# Dreambooth Stable Diffusion Xmas Edition
This colab is based on ShivamShrirao's repository, modified so that it will install diffusers of commit hash `47f456ea3dd3c6ba3f5cc1bcc0f69e79c787208b` from 25 December 2022.

### Why? 
The original colab has on occasion suffered from changes in dependencies affecting the models trained with numerous complaints that the results aren't quite the same as they were before. Anecdotally, this appeared to reach a peak at around early January 2023.  Though things seem to have settled, the occasional comment still arises. 

The aim of this colab is to :
1) Install diffusers and clone a few files in the state that they were on 25th December 2022. The only exception being the conversion scripts, since the up-to-date versions support the safetensors format. 
2) Install package dependencies, according to what was available at the time.  
