<a target="_blank" href="https://colab.research.google.com/github/yushan777/dbsd-xmas-edition/blob/main/DreamBooth_Stable_Diffusion_Xmas_Edition.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

# Dreambooth Stable Diffusion Xmas Edition
This colab is based on ShivamShrirao's repository, modified so that it will install diffusers of commit hash `47f456ea3dd3c6ba3f5cc1bcc0f69e79c787208b` from 25 December 2022.

### Why? 
The performance of models trained on the original colab has occasionally been affected by sudden changes in dependencies, resulting in complaints about inconsistencies in the results. This issue seemed to have peaked in early January 2023, according to anecdotal evidence. Although the situation has stabilized, there are still sporadic comments regarding this matter.

The aim of this colab is to lock-in dependencies from around the time as well as build and install diffusers from that commit. 
The only exception being the conversion scripts, since the up-to-date versions support the safetensors format. 
