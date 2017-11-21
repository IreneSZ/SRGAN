# FCCapsNet
A PyTorch implementation of FCCapsNet based on IJCAI2018 paper [xxxxx](xxxxx)

## Requirements
- [Anaconda](https://www.anaconda.com/download/)
- PyTorch
```
conda install pytorch torchvision -c soumith
conda install pytorch torchvision cuda80 -c soumith # install it if you have installed cuda
```
- tqdm
```
pip install tqdm
```

## Datasets

### Train、Val Dataset
The train and val datasets are sampled from [VOC2012](http://cvlab.postech.ac.kr/~mooyeol/pascal_voc_2012/).
Train dataset has 16700 images and Val dataset has 425 images.
Download the datasets from [here](https://pan.baidu.com/s/1c17nfeo), and then extract it into `data` directory. Finally run
```
python data_utils.py

optional arguments:
--upscale_factor      super resolution upscale factor [default value is 3]
```
to generate train and val datasets from VOC2012 with given upscale factors(options: 2、3、4、8).

### Test Dataset
The test dataset are sampled from 
| **Set 5** |  [Bevilacqua et al. BMVC 2012](http://people.rennes.inria.fr/Aline.Roumy/results/SR_BMVC12.html)
| **Set 14** |  [Zeyde et al. LNCS 2010](https://sites.google.com/site/romanzeyde/research-interests)
| **BSD 100** | [Martin et al. ICCV 2001](https://www.eecs.berkeley.edu/Research/Projects/CS/vision/bsds/)
| **Sun-Hays 80** | [Sun and Hays ICCP 2012](http://cs.brown.edu/~lbsun/SRproj2012/SR_iccp2012.html)
| **Urban 100** | [Huang et al. CVPR 2015](https://sites.google.com/site/jbhuang0604/publications/struct_sr).
Download the dataset from [here](https://pan.baidu.com/s/1nuGyn8l), and then extract it into `data` directory.

## Usage

### Train

```
python train.py

optional arguments:
--upscale_factor      super resolution upscale factor [default value is 3](choices:[2, 3, 4, 8])
--g_threshold         super resolution generator update threshold [default value is 0.2](choices:[0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9])
--g_stop_threshold    super resolution generator update stop threshold [default value is 10](choices:[10, 20, 30])
--g_loss_type         super resolution generator loss function type [default value is GACL](choices:['GAL', 'GAML', 'GACL', 'GACLL', 'GACLV', 'GACLLV'])
--num_epochs          super resolution epochs number [default value is 100]
```
The output val super resolution images are on `images` directory.

### Test
```
python test.py

optional arguments:
--upscale_factor      super resolution upscale factor [default value is 3]
--model_name          super resolution model name [default value is netG_epoch_3_100.pth]
```
The output super resolution images are on `results` directory.

## Benchmarks
The reconstructions of the digit numbers are showed at right and the ground truth at left.
<table>
  <tr>
    <td>
     <img src="results/ground_truth.jpg"/>
    </td>
    <td>
     <img src="results/reconstruction.jpg"/>
    </td>
  </tr>
</table>

Default PyTorch Adam optimizer hyperparameters were used with no learning rate scheduling. 
Epochs with batch size of 100 takes ~2 minutes on a NVIDIA GTX 1070 GPU. 

