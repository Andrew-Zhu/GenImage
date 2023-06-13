# GenImage: A Million-Scale Benchmark for Detecting AI-Generated Image
**Mingjian Zhu, Hanting Chen, Qiangyu Yan, Xudong Huang, Guanyu Lin, Wei Li, Zhijun Tu, Hailin Hu, Jie Hu, Yunhe Wang**

This repository contains the GenImage dataset and the evaluated methods. GenImage is a million-scale AI-generated image detection dataset.
This dataset has the following advantages:
- Plenty of Images: Over one million <fake image, real image> pairs.
- Rich Image Content: Using the same classes in ImageNet, i.e., 1000 classes images.
- State-of-the-art Generators: Midjourney, Stable Diffusion, ADM, GLIDE, Wukong, VQDM, BigGAN.

<img src='https://github.com/Andrew-Zhu/GenImage/blob/main/Examples/visulization.png' width=1200>

## Dataset

The training set and testing set used in the paper can be downloaded in [Baidu Yunpan](https://pan.baidu.com/s/1i0OFqYN5i6oFAxeK6bIwRQ). The code is ztf1.

Each folder contains compressed files. After unzip the file, files under the data root directory can be organized as follows. The ai folder contains the AI-generated images, and the nature folder contains the collected images from ImageNet.

```
├── Midjourney
│   ├── train
│   │   ├── ai
│   │   ├── nature
│   ├── val
│   │   ├── ai
│   │   ├── nature
├── VQDM
│   ├── train
│   │   ├── ai
│   │   ├── nature
│   ├── val
│   │   ├── ai
│   │   ├── nature
├── Wukong
│   ├── ...
├── Stable Diffusion V1.4
│   ├── ...
├── Stable Diffusion V1.5
│   ├── ...
├── GLIDE
│   ├── ...
├── BigGAN
│   ├── ...
├── ADM
│   ├── ...
```

## Detection Methods

We use the codes of detection methods provided in the corresponding paper. 

- [ResNet-50](https://github.com/huggingface/pytorch-image-models/tree/v0.6.12/timm)
- [DeiT-S](https://github.com/facebookresearch/deit)
- [Swin-T](https://github.com/microsoft/Swin-Transformer)
- [CNNSpot](https://github.com/PeterWang512/CNNDetection)
- [Spec](https://github.com/ColumbiaDVMM/AutoGAN)
- [F3Net](https://github.com/yyk-wew/F3Net)
- [GramNet](https://github.com/liuzhengzhe/Global_Texture_Enhancement_for_Fake_Face_Detection_in_the-Wild)

## Benchmark
- Table 3: Results of different methods trained on SD V1.4 and evaluated on different testing subsets.

|   Method / Testing Subset  | Midjourney | SD V1.4 | SD V1.5 |  ADM | GLIDE | Wukong | VQDM | BigGAN | Avg Acc.(%) |
|:---------:|:----------:|:-------:|:-------:|:----:|:-----:|:------:|:----:|:------:|:-----------:|
| ResNet-50 |    54.9    |   99.9  |   99.7  | 53.5 |  61.9 |  98.2  | 56.6 |  52.0  |     72.1    |
|   DeiT-S  |    55.6    |   99.9  |   99.8  | 49.8 |  58.1 |  98.9  | 56.9 |  53.5  |     71.6    |
|   Swin-T  |    62.1    |   99.9  |   99.8  | 49.8 |  67.6 |  99.1  | 62.3 |  57.6  |     74.8    |
|  CNNSpot  |    52.8    |   96.3  |   95.9  | 50.1 |  39.8 |  78.6  | 53.4 |  46.8  |     64.2    |
|    Spec   |    52.0    |   99.4  |   99.2  | 49.7 |  49.8 |  94.8  | 55.6 |  49.8  |     68.8    |
|   F3Net   |    50.1    |   99.9  |   99.9  | 49.9 |  50.0 |  99.9  | 49.9 |  49.9  |     68.7    |
|  GramNet  |    54.2    |   99.2  |   99.1  | 50.3 |  54.6 |  98.9  | 50.8 |  51.7  |     69.9    |

- Table 4: Results of cross-validation on different training and test subsets using different methods. Eight models trained on eight generators are tested on one generator, and their average accuracy is each data point in the testing subset column.

|   Method / Testing Subset  | Midjourney | SD V1.4 | SD V1.5 |  ADM | GLIDE | Wukong | VQDM | BigGAN | Avg Acc.(%) |
|:---------:|:----------:|:-------:|:-------:|:----:|:-----:|:------:|:----:|:------:|:-----------:|
| ResNet-50 |    59.0    |   72.3  |   72.4  | 59.7 |  73.1 |  71.4  | 60.9 |  66.6  |     66.9   |
|   DeiT-S  |    60.7    |   74.2 |   74.2  | 59.5 |  71.1 |  73.1  | 61.7 |  66.3  |      67.6    |
|   Swin-T  |    61.7    |   76.0  |   76.1  | 61.3 |  76.9 |  75.1  | 65.8 |  69.5  |     70.3    |
|  CNNSpot  |    58.2    |   70.3  |   70.2  | 57.0 |  57.1 |  67.7  | 56.7 |  56.6  |     61.7    |
|    Spec   |    56.7    |   72.4  |   72.3  | 57.9 |  65.4 |  70.3  | 61.7 |  64.3  |     65.1    |
|   F3Net   |    55.1    |   73.1  |   73.1  | 66.5 |  57.8 |  72.3  | 62.1 |  56.5  |     64.6    |
|  GramNet  |    58.1    |   72.8  |   72.7  | 58.7 |  65.3 |  71.3  | 57.8 |  61.2  |     64.7    |

- Table 5: Model evaluation on degraded images. q denotes quality.

|   Method / Testing Subset  | LR (112) | LR (64) | JPEG (q=65)  | JPEG (q=30)  |  Blur ($\sigma$=3) |  Blur ($\sigma$=5) |  Avg Acc.(%) |
|:---------:|:----------:|:-------:|:-------:|:----:|:-----:|:------:|:----:|
| ResNet-50 |    96.2    |  57.4   |   51.9  |  51.2 | 97.9  | 69.4   | 70.6  |   
|   DeiT-S  |   97.1    |  54.0 |  55.6  | 50.5 |  94.4 |  67.2 | 69.8  | 
|   Swin-T  |    97.4    | 54.6   |  52.5  | 50.9 | 94.5  | 52.5   | 67.0 |  
|  CNNSpot  |   50.0    |   50.0  |  97.3  | 97.3 |  97.4 | 77.9   | 78.3 | 
|    Spec   |   50.0     | 49.9    |  50.8   | 50.4  | 49.9  | 49.9  | 50.1 |   
|   F3Net   |    50.0    | 50.0    | 89.0    | 74.4 | 57.9  |  51.7 | 62.1 |   
|  GramNet  |    98.8    |  94.9   | 68.8    | 53.4 | 95.9  | 81.6  | 82.2 |  
