# pix2pix 风格迁移

![PyTorch](https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?style=for-the-badge&logo=PyTorch&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.6%2B-blue.svg)

基于PyTorch实现的Pix2pix条件对抗生成网络(cGAN)，用于图像到图像的转换任务。

## 项目概述

本项目实现了Pix2pix网络，能够进行图像风格迁移

## 数据集准备

### 数据来源
- 使用StyleGAN公开的FFHQ数据集
- 选取500张亚洲人脸，经ArcaneGAN处理
- 数据集组成：
  - 训练集：400张图片
  - 测试集：100张图片

## 模型构建：
使用pix2pix网络结构，构建生成器和判别器模型。生成器将输入图像转换为风格化图像，判别器将评估生成图像的真实性。选择使用U-Net结构作为生成器，使用PatchGAN作为判别器。

## 模型训练：
-（1）输入数据：输入成对的图像数据，即一个输入图像和其对应的目标图像。
-（2）训练判别器：用生成图像和真实图像对判别器进行训练，使其区分真假图像。通过最小化判别器的损失，让其输出接近 1 表示真实，接近 0 表示虚假。
-（3）训练生成器：在保持判别器参数不变的情况下，训练生成器使其生成的图像能够“欺骗”判别器，即判别器误认为生成的图像是真实的，同时最小化 L1 损失。
-（4）迭代训练判别器和生成器，直到损失函数收敛或达到设定的训练轮数。

损失函数包含对抗性损失函数和L1损失：
Loss=GAN Loss+λ×L1 Loss，λ是一个权重系数，通常设置为100。

## 生成图像：
使用训练好的模型对新的内容图像进行风格迁移，生成风格化图像。

## 技术栈：
- PyTorch: 深度学习框架
- Torchvision: 图像数据集和变换
- NumPy: 数值计算
- PIL (Pillow): 图像处理
- Matplotlib: 图像可视化
- tqdm: 进度条显示
- glob: 文件路径查找

## 效果展示
![image](https://github.com/user-attachments/assets/ce633313-7ded-49e5-9b83-8c4e93566282)
![image](https://github.com/user-attachments/assets/2f6b01b0-5cc4-4a13-9ab7-45bd857d65dd)


