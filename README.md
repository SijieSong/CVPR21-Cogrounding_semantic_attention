# CVPR21-Cogrounding_semantic_attention

### Co-Grounding Networks with Semantic Attention for Referring ExpressionComprehension in Videos (CVPR 2021).

Project page: https://sijiesong.github.io/co-grounding/

Check out our [paper](<https://arxiv.org/abs/2103.12346>) here.


### Prerequisites
* Python 3
* Pytorch >= 0.4.1
* Others (OpenCV, scipy, etc.)

### Data Preparation
* Please download the files from [BaiduYun](<https://pan.baidu.com/s/1IMy9aISnsxw_wY8siEyEYg>)(Extraction code：p98p) or [GoogleDrive](<https://drive.google.com/drive/folders/1VM_ScHIBKXb7pkgBizRJYtZL7UsC4NR1?usp=sharing>)[./data], then put the files under ./data.
* Download VID Dataset from this [link](<https://bvisionweb1.cs.unc.edu/ilsvrc2015/>) and put it into ./data/VID.
* Download RefCOCO Dataset following this [link](<https://github.com/lichengunc/refer>) and put it into ./data/unc.


### Getting started
* Train CG-SL-Att. on VID 
```
python train_semantic_attention_cogrounding.py  --data_root  ./data  --dataset VID --gpu GPUID --savename SAVENAME_FOR_YOUR_MODEL  --batch_size BATCHSIZE --lstm
```

* Test CG-SL-Att. on VID (model acc: 59.48):

Please download trained models from [BaiduYun](<https://pan.baidu.com/s/1IMy9aISnsxw_wY8siEyEYg>)(Extraction code：p98p) or [GoogleDrive](<https://drive.google.com/drive/folders/1VM_ScHIBKXb7pkgBizRJYtZL7UsC4NR1?usp=sharing>)[./saved_models], then put the models under ./saved_models.

```
python test_semantic_attention_cogrounding.py  --data_root  ./data  --dataset VID --gpu GPUID --savename VID_cogrounding_semantic_attn  --batch_size BATCHSIZE --lstm --test --resume ./saved_models/VID_cogrounding_semantic_attn.pth.tar
```

* Post processing based on CG-SL-Att. on VID (model acc: 60.03):
1. Generate cache files (or download the file from [BaiduYun](<https://pan.baidu.com/s/1IMy9aISnsxw_wY8siEyEYg>)(Extraction code：p98p)/[Google Drive](<https://drive.google.com/drive/folders/1VM_ScHIBKXb7pkgBizRJYtZL7UsC4NR1?usp=sharing>) [cache.zip])
```
python test_semantic_attention_cogrounding.py  --data_root  ./data  --dataset VID --gpu GPUID --savename VID_cogrounding_semantic_attn  --batch_size BATCHSIZE --lstm --cache --resume ./saved_models/VID_cogrounding_semantic_attn.pth.tar
```
2. Post-process the initial results
```
python post_processing.py --data_root ./data/ --dataset VID --gpu GPUID --savename model_post_processing --batch_size 16 --lstm --test --cache_dir CACHE_FILE_PATH
```

* Train SL-Att. on RefCOCO
```
python train_semantic_attention_visual_grounding.py --data_root  ./data  --dataset unc --gpu GPUID --savename SAVENAME_FOR_YOUR_MODEL --batch_size BATCHSIZE --lstm
```

* Test SL-Att. on RefCOCO (model acc: val/testA/testB 77.65/80.75/73.37):

Please download trained models and the put the models under ./saved_models as above.
```
python train_semantic_attention_visual_grounding.py --data_root  ./data  --dataset unc --gpu GPUID --savename Refcoco_grounding_semantic_attn --batch_size BATCHSIZE --lstm --test --resume ./saved_models/RefCOCO_semantic_attn.pth.tar
```



### Related projects

* [One-stage visual grounding](<https://github.com/zyang-ur/onestage_grounding>)


### Citation
If you use this code for your research, please cite our paper:

```
@inproceedings{cogrounding_2021_CVPR,
author = {Song, Sijie and Lin, Xudong and Liu, Jiaying and Guo, Zongming and Chang, Shih-Fu},
title = {Co-Grounding Networks with Semantic Attention for Referring Expression Comprehension in Videos},
booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
month = {June},
year = {2021}
}
```
