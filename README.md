# SJDL-Vehicle: Semi-supervised Joint Defogging Learning for Foggy Vehicle Re-identification--AAAI2022

<!-- ![image](https://github.com/Cihsaing/SJDL-Foggy-Vehicle-Re-Identification--AAAI2022/blob/master/Poster.png) -->
<!-- ![image](https://github.com/Cihsaing/SJDL-Foggy-Vehicle-Re-Identification--AAAI2022/blob/master/fig/teasor_fig_1.png)
![image](https://github.com/Cihsaing/SJDL-Foggy-Vehicle-Re-Identification--AAAI2022/blob/master/fig/teasor_fig_2.png)
![image](https://github.com/Cihsaing/SJDL-Foggy-Vehicle-Re-Identification--AAAI2022/blob/master/fig/teasor_fig_3.png) -->
This is official implentation of the paper "SJDL-Vehicle: Semi-supervised Joint Defogging Learning for Foggy Vehicle Re-identification".

# Abstract:
Vehicle re-identification (ReID) has attracted considerable attention in computer vision. Although several methods have been proposed to achieve state-of-the-art performance on this topic, re-identifying vehicle in foggy scenes remains a great challenge due to the degradation of visibility. To our knowledge, this problem is still not well-addressed so far. In this paper, to address this problem, we propose a novel training framework called Semi-supervised Joint Defogging Learning (SJDL) framework. First, the fog removal branch and the re-identification branch are integrated to perform simultaneous training. With the collaborative training scheme, defogged features generated by the defogging branch from input images can be shared to learn better representation for the re-identification branch. However, since the fog-free image of real-world data is intractable, this architecture can only be trained on the synthetic data, which may cause the domain gap problem between real-world and synthetic scenarios. To solve this problem, we design a semi-supervised defogging training scheme that can train two kinds of data alternatively in each iteration. Due to the lack of a dataset specialized for vehicle ReID in the foggy weather, we construct a dataset called FVRID which consists of real-world and synthetic foggy images to train and evaluate the performance. Experimental results show that the proposed method is effective and outperforms other existing vehicle ReID methods in the foggy weather.


<!-- [[Paper Download]](https://openaccess.thecvf.com/content/ICCV2021/papers/Chen_ALL_Snow_Removed_Single_Image_Desnowing_Algorithm_Using_Hierarchical_Dual-Tree_ICCV_2021_paper.pdf)
[[Dataset Download]](https://ccncuedutw-my.sharepoint.com/:u:/g/personal/104501531_cc_ncu_edu_tw/EfCooq0sZxxNkB7F8HgCyKwB-sJQtVE59_Gpb9soatYi5A?e=5NjDhb)
[[Poster Download]](https://ntucc365-my.sharepoint.com/:b:/g/personal/f05943089_ntu_edu_tw/EXjU8U85nMZMkoHwqVCO_QEBlWvz9U803iinqfkLv3QrZg?e=3k0diD)
[[Slide Download]](https://ntucc365-my.sharepoint.com/:b:/g/personal/f05943089_ntu_edu_tw/EVUaKr-l1UNDoUeuInao0RkB6kv5MDMfUcUCNp96rRZeTA?e=5LYZSC) -->

You can also refer our previous works on other low-level vision applications!

Desnowing-[[JSTASR]](https://github.com/weitingchen83/JSTASR-DesnowNet-ECCV-2020)(ECCV'20) and [[HDCWNet]](https://github.com/weitingchen83/ICCV2021-Single-Image-Desnowing-HDCWNet)(ICCV'21)<br>
Dehazing-[[PMS-Net]](https://github.com/weitingchen83/PMS-Net)(CVPR'19) and [[PMHLD]](https://github.com/weitingchen83/Dehazing-PMHLD-Patch-Map-Based-Hybrid-Learning-DehazeNet-for-Single-Image-Haze-Removal-TIP-2020)(TIP'20)<br>
Image Relighting-[[MB-Net]](https://github.com/weitingchen83/NTIRE2021-Depth-Guided-Image-Relighting-MBNet) (NTIRE'21 1st solution) and [[S3Net]](https://github.com/dectrfov/NTIRE-2021-Depth-Guided-Image-Any-to-Any-relighting) (NTIRE'21 3 rd solution)<br>


# Network Architecture
## Joint Defogging Learning (JDL)
![image](https://github.com/Cihsaing/SJDL-Foggy-Vehicle-Re-Identification--AAAI2022/blob/master/fig/architecture.png)

## Semi-supervised Joint Defogging Learning (SJDL)
![image](https://github.com/Cihsaing/SJDL-Foggy-Vehicle-Re-Identification--AAAI2022/blob/master/fig/semi.png)


# Dataset
Both synthetic data and real-world data are adopted in this paper:<br><br><br>
Example of synthetic data:<br>
![image](https://github.com/Cihsaing/SJDL-Foggy-Vehicle-Re-Identification--AAAI2022/blob/master/fig/dataset_syn.png)

Example of real-world data:<br>
![image](https://github.com/Cihsaing/SJDL-Foggy-Vehicle-Re-Identification--AAAI2022/blob/master/fig/dataset_real.png)

<!-- 
[[Dataset Download]](https://ccncuedutw-my.sharepoint.com/:u:/g/personal/104501531_cc_ncu_edu_tw/EfCooq0sZxxNkB7F8HgCyKwB-sJQtVE59_Gpb9soatYi5A?e=5NjDhb)
![image](folder/csd.png)
 -->

# Result
![image](https://github.com/Cihsaing/SJDL-Foggy-Vehicle-Re-Identification--AAAI2022/blob/master/fig/quantitative.png)


## Setup and environment

To implement our method you need:
> 1. Python 3.10
> 2. pytorch 1.8.0+
> 3. torchvision 0.13.0+
> 4. yacs
> 5. tqdm

**As the device was updated, I changed the environment parameters for the RTX3090 and provided the final version, which can be generated with** ```conda env create -f environment.yml```. In 08/26/2022.

## Data Preparation
Since the policy of Veri-1M, we can only provide the codes to synthesize the foggy data and the index of the real-world foggy data. Please follow the steps to generate the data:
See [Data Preparation](https://github.com/Cihsaing/SJDL-Foggy-Vehicle-Re-Identification--AAAI2022/tree/master/Datasets).

## Train SJDL
Run following command to train the SJDL model
```
cd SJDL/
CUDA_VISIBLE_DEVICES=0 python trainer.py -c configs/FVRID_syn.yml MODEL.NAME "resnet50" TEST.VIS True OUTPUT_DIR "./output/SJDL/" MODEL.TENSORBOARDX False
```
where ```CUDA_VISIBLE_DEVICES``` defines usable GPU. <br> 
where the ```configs/FVRID_syn.yml``` is the default SJDL training config. <br> 
where the ```MODEL.NAME``` select the backbone. eg. 'resnet50', 'resnet101'... <br>
where the ```TEST.VIS``` enable resotration result plot. <br>
where the ```OUTPUT_DIR``` define the output path. <br>
where the ```MODEL.TENSORBOARDX``` enable tensorboard. <br>

### Common problem
1. If the gpu memory is insufficient, please lower the number of "configs/FVRID_syn.yml":
   ```DATALOADER.NUM_WORKERS``` and ```SOLVER.IMS_PER_BATCH  # Must be a multiple of DATALOADER.NUM_INSTANCE``` .
2. If you encounter an amp conflict, there are two possibilities: torch version problem and the device must have support.
   If your device not support, please keep the ```"configs/FVRID_syn.yml": SOLVER.FP16 = False```.
3. If you encounter the loss.py line:242 torch.fft problem, please check the torch version and find the corresponding version of the fft.

## Pretrained Models
We provide the pretrained SJDL, training on FVRID for your convinient. You can download it from the following link: 
https://drive.google.com/file/d/1WhsvYQP-qg1R-BcpH5lonjxh4DYp2ouv/view?usp=sharing

## Testing
```
cd SJDL/
CUDA_VISIBLE_DEVICES=0 python inference.py -t -c <Configs> TEST.WEIGHT <PTH_PATH> OUTPUT_DIR <OUTPUT_PATH>
```
where the ```<Configs>``` is the testing configs file. <br>
where the ```<PTH_PATH>``` is the test weight. <br>
where the ```<OUTPUT_PATH>``` is the output paths. <br>

The pre-trained model can be downloaded from Link: <br>
https://drive.google.com/file/d/1WhsvYQP-qg1R-BcpH5lonjxh4DYp2ouv/view?usp=sharing. <br>
and you can put it at the dir ```'./SJLD/output/'```

Examples
```
cd SJDL/
# For FVRID_real
CUDA_VISIBLE_DEVICES=0 python inference.py -t -c ./configs/FVRID_real.yml TEST.WEIGHT ./output/best.pth OUTPUT_DIR ./output/Test_on_FVRID_real/
# For FVRID_syn
CUDA_VISIBLE_DEVICES=0 python inference.py -t -c ./configs/FVRID_syn.yml TEST.WEIGHT ./output/best.pth OUTPUT_DIR ./output/Test_on_FVRID_syn/
```
And you can also create the new config at dir ```'./configs'``` for another application.
If you train another weights, please change the ```TEST.WEIGHT```.

# Citations
Please cite this paper in your publications if it is helpful for your tasks:    

Bibtex:
```
@inproceedings{chen2021all,
  title={SJDL-Vehicle: Semi-supervised Joint Defogging Learning for Foggy Vehicle Re-identification},
  author={Chen, Wei-Ting and Chen, I-Hsiang and Yeh, Chih-Yuan and Yang, Hao-Hsiang and Ding, Jian-Jiun and Kuo, Sy-Yen},
  booktitle={Proceedings of the AAAI conference on artificial intelligence},
}
```
