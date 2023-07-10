# VGG-demo
This is our demo to reproduce VGG on pytorch, the dataset uses more than 4000 images in 5 categories.Here's [my blog] on some interpretations of the VGG paper.The VGG paper《[Very Deep Convolutional Networks for Large-Scale Image Recognition](https://arxiv.org/pdf/1409.1556.pdf)》.

These are the six different network structures of VGG given by the authors in the paper:：
![image](https://img2023.cnblogs.com/blog/3233343/202307/3233343-20230707164745328-1069969601.png)

VGG-16 schematic diagram is as follows, overall the whole network can be divided into 5 blocks, each block consists of convolution + pooling, and then into 3 fully connected layers and then connected to softmax to achieve classification：
![image](https://img2023.cnblogs.com/blog/3233343/202307/3233343-20230707164801578-188752917.png)

Let's take VGG-16 as an example to decipher its network structure：
- The convolutional layers within VGG-Block are all of the same structure, where they are all implemented uniformly by **size of 3×3 kernel size + stride1 + padding(same)**, meaning that the input and output sizes are the same and the convolutional layers can be stacked and reused.
- The MaxPool layer has a uniform **pool size=2,stride=2**, which plays the role of reducing the features of the previous convolutional layers by half, from 224-112-56-28-14-7.

## Dataset

The same dataset as [AlexNet-dem](https://github.com/Hjxin02AIsharing-Wust/AlexNet-demo) is used.The dataset uses more than 4000 images in 5 categories, you can download it [here](https://drive.google.com/drive/folders/1z2d7UejBR55QY8dc2GOmSkyfi8C-vUBs).

## Data Preprocess
You need to change the `root_file` parameter in the  `Data_Preprocess.py` file to the address of the dataset you downloaded. We follow the training set: validation set ratio of 9 to 1. You can also change this ratio, just change the `split_rate parameter`. Also we follow the data enhancement operation of the VGG paper, cropping the image to 224x224 at random and flipping it horizontally.

## Usage

### Train
You can use the following commands to train the model：
```shell
python train.py 
```
Here are some of our training settings: batchsize is set to 128, cross-entropy loss function is used, Adam is used for the optimizer, learning rate is set to 0.0002, and 20 epochs are trained.

## Test

We provide the test code：
```shell
python test.py
```
You can use our provided model weights [`VGG16.pth`](https://drive.google.com/drive/folders/1XOtcJu1q0rMejKc20wuYNi22-V7opl9c) and test image `roseflower.png`, of course, you can also use your own.


