# HyperIQA Implementation
- 논문 저자들이 demo.py를 만들어 놓음.
- 실행할 경우 demo image의 predict score를 output함.
- 이번 프로젝트에서 사용하기 위해 demo.ipynb 생성
- koniq_pretrained.pkl 파일 필요
- pretrained 폴더 생성 후 koniq_pretrained.pkl 파일을 넣음.
- 1번 셀 실행 후 2번 셀에서 torch.load 경로 확인 후 실행
- filenames에 predict 하고자하는 이미지 폴더 경로를 넣음.
- 결과를 저장하기 위한 dataframe을 생성
- im_path = f'./data/{filename}' 에 이미지 폴더 경로를 넣음.
- dataframe 이름 확인 후 셀 실행 시 dataframe에 결과가 삽입.



# HyperIQA

This is the source code for the CVPR'20 paper "[Blindly Assess Image Quality in the Wild Guided by A Self-Adaptive Hyper Network](https://openaccess.thecvf.com/content_CVPR_2020/papers/Su_Blindly_Assess_Image_Quality_in_the_Wild_Guided_by_a_CVPR_2020_paper.pdf)".

## Dependencies

- Python 3.6+
- PyTorch 0.4+
- TorchVision
- scipy

(optional for loading specific IQA Datasets)
- csv (KonIQ-10k Dataset)
- openpyxl (BID Dataset)

## Usages

### Testing a single image

Predicting image quality with our model trained on the Koniq-10k Dataset.

To run the demo, please download the pre-trained model at [Google drive](https://drive.google.com/file/d/1OOUmnbvpGea0LIGpIWEbOyxfWx6UCiiE/view?usp=sharing) or [Baidu cloud](https://pan.baidu.com/s/1yY3O8DbfTTtUwXn14Mtr8Q) (password: 1ty8), put it in 'pretrained' folder, then run:

```
python demo.py
```

You will get a quality score ranging from 0-100, and a higher value indicates better image quality.

### Training & Testing on IQA databases

Training and testing our model on the LIVE Challenge Dataset.

```
python train_test_IQA.py
```

Some available options:
* `--dataset`: Training and testing dataset, support datasets: livec | koniq-10k | bid | live | csiq | tid2013.
* `--train_patch_num`: Sampled image patch number per training image.
* `--test_patch_num`: Sampled image patch number per testing image.
* `--batch_size`: Batch size.

When training or testing on CSIQ dataset, please put 'csiq_label.txt' in your own CSIQ folder.

## Citation
If you find this work useful for your research, please cite our paper:
```
@InProceedings{Su_2020_CVPR,
author = {Su, Shaolin and Yan, Qingsen and Zhu, Yu and Zhang, Cheng and Ge, Xin and Sun, Jinqiu and Zhang, Yanning},
title = {Blindly Assess Image Quality in the Wild Guided by a Self-Adaptive Hyper Network},
booktitle = {IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
month = {June},
year = {2020}
}
```





