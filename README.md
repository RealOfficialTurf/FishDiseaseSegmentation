# FishDiseaseSegmentation

This is the code that is used in the paper "Incorporating Transfer Learning Strategy for improving Semantic Segmentation of Epizootic Ulcerative Syndrome Disease Using Deep Learning Model"

## How to use

Create a conda environment first,

```
conda create -n eseg2
conda activate eseg2
```

Then install the following libraries.

```
conda install pytorch==2.3.1 torchvision==0.16.1 torchaudio==2.1.1 pytorch-cuda=12.1 -c pytorch -c nvidia
conda install -c conda-forge jupyter
conda install -c conda-forge matplotlib
pip install pycocotools
```

Run the .ipynb notebook file through the Jupyter Notebook installed in the environment.

## How to run

You will need to obtain the datasets first. The following datasets are used in the paper.

Classification dataset: https://www.kaggle.com/datasets/subirbiswas19/freshwater-fish-disease-aquaculture-in-south-asia/versions/2
Segmentation dataset: https://universe.roboflow.com/testing-dgymd/fish-disease-2

Note that the code that are used for deduplication and preprocessing is not included in this repo.

Modify the `dataset_dir` variable in the notebook file to the file path pointing to the dataset folder.

Select the model and optimizer that will be used for training with the `MODELNAME` and `OPTIMIZERNAME` variable, respectively. The following models are used in this paper:

|Classification Model String|Model Name in Paper|
|-|-|
|VGG16|VGG16|
|PRE_VGG16|VGG16-P|
|ResNet50|ResNet50|
|PRE_ResNet50|ResNet50-P|

|Segmentation Model String|Model Name in Paper|
|-|-|
|UNet|UNet|
|UNet+VGG16|U-Net+VGG16|
|UNet+Pretrained_VGG16|U-Net+VGG16-I|
|UNet+Pre_CLS_VGG16|U-Net+VGG16-IC|
|UNet+CLS_VGG16|U-Net+VGG16-C|
|UNet+ResNet50|U-Net+ResNet50|
|UNet+Pretrained_ResNet50|U-Net+ResNet50-I|
|UNet+Pre_CLS_ResNet50|U-Net+ResNet50-IC|
|UNet+CLS_ResNet50|U-Net+ResNet50-C|
|SegNet16|SegNet|
|Pretrained_SegNet16|SegNet-I|
|Pre_CLS_SegNet16|SegNet-IC|
|CLS_SegNet16|SegNet-C|

Then run the notebook.

### Two Stage Transfer Learning

The classification notebook file outputs the classification model weight file in the form of `<Name>-<Size>^2-<DatasetName>+CutMixUp-<Optimizer>-CE_wprop-BS8-E<EpochCount>-<TrainAcc>_<ValAcc>_<TestAcc>.pth` as well as various loss curve plots. As part of the two stage transfer learning method in the paper, The classification model weight files are subsequently used in the segmentation notebook file.

In the segmentation notebook file, the following variables need to be modified and filled with the file path pointing to the classification model weight files.

```
VGG16_Path
PRE_VGG16_Path
ResNet50_Path
PRE_ResNet50_Path
```
