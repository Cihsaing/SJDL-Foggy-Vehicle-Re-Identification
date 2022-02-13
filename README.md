# SJDL-Foggy-Vehicle-Re-Identification--AAAI2022

<!-- ![image](https://github.com/Cihsaing/SJDL-Foggy-Vehicle-Re-Identification--AAAI2022/blob/master/Poster.png) -->
<!-- ![image](https://github.com/Cihsaing/SJDL-Foggy-Vehicle-Re-Identification--AAAI2022/blob/master/fig/teasor_fig_1.png)
![image](https://github.com/Cihsaing/SJDL-Foggy-Vehicle-Re-Identification--AAAI2022/blob/master/fig/teasor_fig_2.png)
![image](https://github.com/Cihsaing/SJDL-Foggy-Vehicle-Re-Identification--AAAI2022/blob/master/fig/teasor_fig_3.png) -->

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



# Setup and environment

To implement our method you need:

1. Python 3
2. pytorch 1.7.0+
3. torchvision 0.8.0+

# Data Preparation
Since the policy of Veri-1M, we can only provide the codes to synthesize the foggy data and the index of the real-world foggy data. Please follow the steps to generate the data:
See https://github.com/Cihsaing/SJDL-Foggy-Vehicle-Re-Identification--AAAI2022/tree/master/Datasets

# Train SJDL
Run following command to train the SJDL model
```
python ./train.py --logPath ./your_log_path --dataPath /path_to_data/data.npy --gtPath /path_to_gt/gt.npy --batchsize batchsize --epochs epochs --modelPath ./path_to_exist_model/model_to_load.h5 --validation_num number_of_validation_image --steps_per_epoch steps_per_epoch
```

*data.npy should be numpy of training image whose shape is (number_of_image, 480, 640, 3). The range is (0, 255) and the datatype is uint8 or int.<br>
*gt.npy should be numpy of ground truth image, whose shape is (number_of_image, 480, 640, 3). The range is (0, 255) and datatype is uint8 or int.

Example:
```
python ./train.py --logPath ./log --dataPath ./training_data.npy --gtPath ./training_gt.npy --batchsize 3 --epochs 1500 --modelPath ./previous_log/preivious_model.h5 --validation_num 200 --steps_per_epoch 80
```

Testing
```
$ python ./predict.py -dataroot ./your_dataroot -datatype datatype -predictpath ./output_path -batch_size batchsize
```
*datatype default: tif, jpg ,png

Examples
```
$ 
python ./predict.py -dataroot ./testImg -predictpath ./p -batch_size 3
python ./predict.py -dataroot ./testImg -datatype tif -predictpath ./p -batch_size 3
```

The pre-trained model can be downloaded from: https://ntucc365-my.sharepoint.com/:u:/g/personal/f05943089_ntu_edu_tw/EZtus9ex-GtNukLuSxWGmPIBEJIzRFMbEl0dFeZ_oTQnVQ?e=xnfqFL. 
Put the "finalmodel.h5" to the 'modelParam'.

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
