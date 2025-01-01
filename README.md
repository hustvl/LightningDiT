<div align="center">

## ⚡Taming Optimization Dilemma in Latent Diffusion via Vision Foundation Model Aligned VAE

**_FID=1.35 on ImageNet-256 & 21.8x faster training than DiT!_**

[Jingfeng Yao](https://github.com/JingfengYao), [Xinggang Wang](https://xwcv.github.io/index.htm)*

Huazhong University of Science and Technology (HUST)

*Corresponding author: xgwang@hust.edu.cn

[![arXiv](https://img.shields.io/badge/arXiv-VA_VAE-b31b1b.svg)]()
[![arXiv](https://img.shields.io/badge/arXiv-FasterDiT-b31b1b.svg)](https://arxiv.org/abs/2410.10356)
[![license](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
[![authors](https://img.shields.io/badge/by-hustvl-green)](https://github.com/hustvl)

</div>
<div align="center">
<img src="images/vis.png" alt="Visualization">
</div>

## ✨ Highlights

- Latent diffusion system with 0.28 rFID and **1.35 FID on ImageNet-256** generation, **surpassing all published state-of-the-art**!

- **More than 21.8× faster** convergence with **VA-VAE** and **LightningDiT** than original DiT!

- **Surpass DiT （FID=2.11） with only 8 GPUs in 10 hours**. Let's make diffusion transformers research more affordable!

## 📰 News

- **[2025.01.02]** 🎉 We release the code and paper for VA-VAE and LightningDiT! The weights and pre-extracted latents will be released soon.

## 📄 Introduction

Latent diffusion models (LDMs) with Transformer architectures excel at generating high-fidelity images. However, recent studies reveal an **optimization dilemma** in this two-stage design: while increasing the per-token feature dimension in visual tokenizers improves reconstruction quality, it requires substantially larger diffusion models and more training iterations to achieve comparable generation performance.
Consequently, existing systems often settle for sub-optimal solutions, either producing visual artifacts due to information loss within tokenizers or failing to converge fully due to expensive computation costs.

We argue that this dilemma stems from the inherent difficulty in learning unconstrained high-dimensional latent spaces. To address this, we propose aligning the latent space with pre-trained vision foundation models when training the visual tokenizers. Our proposed VA-VAE (Vision foundation model Aligned Variational AutoEncoder) significantly expands the reconstruction-generation frontier of latent diffusion models, enabling faster convergence of Diffusion Transformers (DiT) in high-dimensional latent spaces.
To exploit the full potential of VA-VAE, we build an enhanced DiT baseline with improved training strategies and architecture designs, termed LightningDiT.
The integrated system demonstrates remarkable training efficiency by reaching FID=2.11 in just 64 epochs -- an over 21× convergence speedup over the original DiT implementations, while achieving state-of-the-art performance on ImageNet-256 image generation with FID=1.35.

## 📝 Results

- State-of-the-art Performance on ImageNet 256x256 with FID=1.35.
- Surpass DiT within only 64 epochs training, achieving 21.8x speedup.

<div align="center">
<img src="images/results.png" alt="Results">
</div>

## 🎯 How to Use

### Installation

```
conda create -n lightningdit python=3.10.12
conda activate lightningdit
pip install -r requirements.txt
```


### Inference with Pre-trained Models

- Download pre-trained DiT weights and [VA-VAE weights]() (to be released), pre-computed [latent infos]() (to be released soon).
<!-- 
    |    Gen Model     |    Training Epochs    | FID-50k (w/o cfg) | FID-50k (w/ cfg) |  Download  |
    |:----------------:|:---------------------:|:-----------------:|:----------------:|:----------:|
    | LightningDiT-XL  |          64           |       5.15        |       2.11       | [checkpoint]() (to be released) |
    |                  |          800          |       2.21        |       1.35       | [checkpoint]() (to be released) |

    Modify ``configs/lightningdit_xl_vavae_f16d32.yaml`` and ``tokenizer/configs/vavae_f16d32.yaml``. -->

- Fast sample demo images:

    Run:
    ```
    bash bash run_fast_inference.sh configs/lightningdit_xl_vavae_f16d32.yaml
    ```
    Images will be saved into ``demo_images/demo_samples.png``, e.g. the following one:
    <div align="center">
    <img src="images/demo_samples.png" alt="Demo Samples" width="600">
    </div>

- Sample for FID-50k evaluation:
    
    Run:
    ```
    bash run_inference.sh configs/lightningdit_xl_vavae_f16d32.yaml
    ```
    NOTE: The FID result reported by the script serves as a reference value. The final FID-50k reported in paper is evaluated with ADM:

    ```
    git clone https://github.com/openai/guided-diffusion.git
    
    # save your npz file with tools/save_npz.py
    bash run_fid_eval.sh /path/to/your.npz
    ```

## 🎮 Train Your Own Models

 
- **We provide a 👆[detailed tutorial](docs/tutorial.md) for training your own models of 2.05 FID score within only 64 epochs. It takes only about 10 hours with 8 x H800 GPUs.** 


<!-- - Extract feature first. LightninDiT could alse get great performance with SD-VAE. We will integrated this feature later.

    ```
    bash run_extract_feature.sh tokenizer/configs/vavae_f16d32.yaml
    ```

- Run the following command to start training. 
    
    We provide a reference log of our training process. With 8 x H800 GPUs, it takes about **only 10 hours** to surpass the performance of original DiT. Hope you enjoy it.

    ```
    bash run_train.sh tokenizer/configs/vavae_f16d32.yaml
    ```

- Run the following command to start inference.

    ```
    bash run_inference.sh tokenizer/configs/vavae_f16d32.yaml
    ``` -->

## ❤️ Acknowledgements

- This repo is mainly built on [DiT](https://github.com/facebookresearch/DiT), [FastDiT](https://github.com/chuanyangjin/fast-DiT) and [SiT](https://github.com/willisma/SiT). Our VAVAE codes are mainly built with [LDM](https://github.com/CompVis/latent-diffusion) and [MAR](https://github.com/LTH14/mar). Thanks for all these great works.

## 📝 Citation

If you find our work useful, please consider to cite our related paper:

```
# arxiv preprint TODO
@article{vavae,
  title={Taming Optimization Dilemma in Latent Diffusion via Vision Foundation Model Aligned VAE},
  author={Yao, Jingfeng and Wang, Xinggang},
  journal={to be released},
  year={2025}
}

# NeurIPS 24
@article{fasterdit,
  title={FasterDiT: Towards Faster Diffusion Transformers Training without Architecture Modification},
  author={Yao, Jingfeng and Wang, Cheng and Liu, Wenyu and Wang, Xinggang},
  journal={arXiv preprint arXiv:2410.10356},
  year={2024}
}
```