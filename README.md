# HSVC-Inpainting
Code for our paper "[ HSVC-Image Inpainting] 

### Introduction


##### Examples
![image](https://github.com/IPCSRG/HSVC-Inpainting/blob/main/Fig.1.png)
Example inpainting results on images of face, realistic street scene, and natural scene. Missing regions are shown in white. (From left to right) Input corrupted images, inpainting structure, ours final results, respectively.

##### Demo
![image](https://github.com/IPCSRG/HSVC-Inpainting/blob/main/HSVC-ImageInpainting.mp4)

### Requirements

1. Pytorch >= 1.0
2. Python 3
3. NVIDIA GPU + CUDA 11.0
4. Tensorboard


### Installation

1. Clone this repository

   ```bash
   git clone https://github.com/IPCSRG/HSVC-Inpainting
   ```
   
### Running

**1.   Image Prepare**

We train our model on three public datasets including Places2, Celeba, and Paris StreetView. We use the irregular mask dataset provided by [PConv](https://arxiv.org/abs/1804.07723). You can download these datasets from their project website.

1. [Places2](http://places2.csail.mit.edu)
2. [CelebA](http://mmlab.ie.cuhk.edu.hk/projects/CelebA.html) 
3. [Paris Street-View](https://github.com/pathak22/context-encoder) 
4. [Irregular Masks](http://masc.cs.gmu.edu/wiki/partialconv)

Finally, you can generate the image list using script  [`Dataset/flist.py`](scripts/flist.py) for training and testing.

**2.   Training**

To train our model, modify the model config file [model_config.yaml](model_config.yaml). You may need to change the path of dataset or the parameters of the networks etc. Then run the following code:

```bash
python train.py \
--name=[the name of your experiment] \
--path=[path save the results] 
```

**3.   Testing**

To output the generated results of the inputs, you can use the [test.py](test.py).  Please run the following code:

```bash
python test.py \
--name=[the name of your experiment] \
--path=[path of your experiments] \
--input=[input images] \
--mask=[mask images] \
--structure=[structure images] \
--output=[path to save the output images] \
--model=[which model to be tested]
```

**4.   Evaluate**

To evaluate the model performance over a dateset, you can use the provided script [./evaluate/metrics.py](evaluate/metrics.py). This script can provide the L1 loss, PSNR, SSIM and LPIPS of the results. Besides, you can use the provided script [./evaluate/FID.py](evaluate/FID.py). This FID can provide the Fréchet Inception Distance ([FID score](https://github.com/mseitzer/pytorch-fid)) of the results.

```bash
python ./scripts/metrics.py \
--g_path=[path to model outputs] \
--gt_path=[path to the real images using to calculate fid]
```

```bash
python ./scripts/FID.py \
--output_path=[path to model outputs] \
--fid_real_path=[path to the real images using to calculate fid]
```


**The pre-trained weights can be downloaded from [Places2](https://drive.google.com/drive/folders/1VXWnp3Cxl5r6yFf-GsPtYT-wMeqphwqu), [CelebA-HQ](https://drive.google.com/drive/folders/1iljc8iM5QiHDB5xUwS8xFv6wAmX9srWp), [Paris Street](https://drive.google.com/drive/folders/1CQXVuQht3f2EamEx9Bi7KR3e8tsGGLQX).**

Download the checkpoints and save them to './path_of_your_experiments/name_of_your_experiment/checkpoints'

For example you can download the checkpoints of Places2 and save them to './results/places2/checkpoints' and run the following code:

```bash
python test.py \
--name=places \
--path=results \
--input=./example/places/1.jpg \
--mask=./example/places/1_mask.png \
--structure=./example/places/1_tsmooth.png \
--output=./result_images \
--model=3
```

### Citation

We built our code based on [StructureFlow](https://github.com/RenYurui/StructureFlow).If you find this code is helpful for your research, please cite the following paper:

```
@inproceedings{ren2019structureflow,
      author = {Ren, Yurui and Yu, Xiaoming and Zhang, Ruonan and Li, Thomas H. and Liu, Shan and Li, Ge},
      title = {StructureFlow: Image Inpainting via Structure-aware Appearance Flow},
      booktitle={IEEE International Conference on Computer Vision (ICCV)},
      year = {2019}
}
```



### Acknowledgements

We built our code based on [StructureFlow](https://github.com/RenYurui/StructureFlow). Part of the code were derived from [Edge-Connect](https://github.com/knazeri/edge-connect) and [CA](https://github.com/JiahuiYu/generative_inpainting). Please consider to cite their papers. 
