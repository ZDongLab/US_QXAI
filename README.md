# Innovative Redefinition of Ultrasound Features Using Explainable Artificial Intelligence: A Dual-Center Validation Highlighting Clinical Advantages in Thyroid Nodule ACR TI-RADS Management
<center>
<img src='.\demo\Figure1.framework.png', width='600'>
</center>

[It will be activated at: 2025_Radio_US_QXAI.pdf]( ) 

Before implementing the code, you need to configure and setup some libraries required by the following [Requirements](requirements.txt):

* [Inplace-abn-1.1.1](https://github.com/mapillary/inplace_abn)
* pytorch-1.11 (CUDA.11.2)
* OpenCV-4.6, ...


# 1. Methods and materials
## 1.1 Methods: The flowchart of patients’ enrollment and study design
<center>
<img src='.\demo\figure1.png', width='600'>
</center>

## 1.2 Methods: Redefinition and quantification of traditional US features of thyroid nodules
<center>
<img src='.\demo\figure3.png', width='600'>
</center>

## 1.4 Database Setting
Before using the US_QXAI codes to train the model, you need to prepare the training dataset, validation dataset and testing  dataset in the following format:
```
datasets
   └──SSL_dataset6120
      └──train
         └──xxxx_thyroid.jpg
      └──val
         └──xxxx_thyroid.jpg
      └──test
         └──xxxx_thyroid.jpg
      |──train.csv
      |──val.csv
      |──test.csv
   └──Seg_dataset2992
      └──train
         └──xxxx_thyroid.jpg
      └──val
         └──xxxx_thyroid.jpg
      └──test
         └──xxxx_thyroid.jpg
      |──train.csv
      |──val.csv
      |──test.csv
   └──Quant_dataset873
      └──train
         └──xxxx_thyroid.jpg
      └──val
         └──xxxx_thyroid.jpg
      └──test
         └──xxxx_thyroid.jpg
      |──train.csv
      |──val.csv
      |──test.csv      
```
The information in the CSV file includes:  
* SSL_dataset6120: name_id
* Seg_dataset2992: name_id, GT (begin-->0, malignant-->1) 
* Quant_dataset873: name_id, GT (begin-->0, malignant-->1) , aspect ratio(>=1, <1), margin, Echogenicity, Components, Calcification information (based on CTI-RADS) and Each image is paired with a masked nodule image.

#  Experiment
## Experimental results
We provide [Some experimental results]()
<center>
<img src='.\demo\figure4.png', width='600'>
</center>
<center>
<img src='.\demo\figure5.png', width='600'>
</center>

## [Training and Validation](US_QXAI_SSL.train.py)
We provide [US_QXAI_SSL.train code](US_QXAI_SSL.train.py), and you can perform it by the following command:
```
CUDA_VISIBLE_DEVICES=0 python US_QXAI_SSL.train.py \
--model_name "US_QXAI_SSL.train" \
--batch-size 16
```
We provide [US_QXAI_Seg.train/test code](US_QXAI_Seg.train.py), and you can perform it by the following command:
```
CUDA_VISIBLE_DEVICES=0 python US_QXAI_Seg.train.py \
--model_name "US_QXAI_Seg.train" \
--batch-size 16
```

## [Quantization Inference ](US_QXAI_Quant.py)
We provide [Quantization Inference](US_QXAI_Quant.py), and you can perform it by the following command:
```
CUDA_VISIBLE_DEVICES=0 python US_QXAI_Quant.py \
--model_name "US_QXAI_Seg" \
--model_path "./models/US_QXAI_Quant/US_QXAI_Seg.xxx.ckpt" \
--batch-size 16
```

## Citation
If you use US_QXAI in your research, please cite:
```bibtex
@ARTICLE{Dong2025,
  author  = {xxx,xxx,xxx,xxx},
  title   = {Innovative Redefinition of Ultrasound Features Using Explainable Artificial Intelligence: A Dual-Center Validation Highlighting Clinical Advantages in Thyroid Nodule ACR TI-RADS Management},
  journal = {Radiology (Under Review)}, 
  volume  = {0},
  year    = {2025},
  pages   = {0}
}
```