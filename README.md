<table style="width:100%" text-align:center >
  <tr>
    <th>Original Layout (Mostly)</th>
    <th>Alternative Layout</th>
  </tr>
  <tr>
    <td>
      <a target="_blank" href="https://colab.research.google.com/github/yushan777/dbsd-dec-2022/blob/main/dbsd_dec_2022_original.ipynb">
      <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab" width="250"/></a>
    </td>
    <td>
      <a target="_blank" href="https://colab.research.google.com/github/yushan777/dbsd-dec-2022/blob/main/dbsd_dec_2022.ipynb">
      <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab" width="250"/><br></a>
    </td>
  </tr>

</table>

# Dreambooth Stable Diffusion Winter 2022 Edition
This colab is based on ShivamShrirao's repository and colab, modified to use older dependencies from late 2022.  
The diffusers repo itself will be locked to commit: `fbdf0a17055ffa34679cb34d986fabc1296d0785` 2022-03-02

https://github.com/ShivamShrirao/diffusers/ \
https://github.com/ShivamShrirao/diffusers/tree/main/examples/dreambooth

### Why? 
The performance of models trained on the original colab has occasionally been affected by sudden changes in dependencies, resulting in complaints about inconsistencies in the results. This issue seemed to have peaked in early January 2023 and although the situation seems to be back to normal, there are still occasional comments regarding this matter.

The aim of this colab is to lock-in dependencies from late 2022. Diffusers from the repo isbuilt and installed from Commit `fbdf0a17055ffa34679cb34d986fabc1296d0785`. 

train_dreambooth.py needs to be modified since there are calls to an updated `accelerator.unwrap_model()` that require Accelerate 0.14.0 but we are using 0.12.0.  

## Features?
For the most part the colab should be very familiar however I've made it a bit more wordy and verbose with the intention of making it easier for people new to it. A few added functionalities:

* Download diffusers, ckpt or safetensors
* Convert all weights to ckpt or safetensors

If you are more familiar with the original colab's layout, you can use the link to the one with the original layout.
