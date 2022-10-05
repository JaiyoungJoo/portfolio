# 프로젝트 주제(진행중)
## Face Image Quality Assessment
- 얼굴 이미지 혹은 영상의 퀄리티(선명도)를 평가하는 태스크
- 화질을 평가하는 많은 방식들이 Reference(원본 이미지 혹은 영상)가 필요한 경우가 많음.
- 그러나 실제로 원본 영상, 저화질 영상이 항상 세트로 존재하는 것이 아니어서 full reference 방식의 평가 지표는 사용하기 어려움. 
- 임의의 이미지나 영상의 퀄리티를 평가하기 위해 No reference로 평가할 필요가 있음.  
## 1. 문제 정의
- Image Quality Assessment는 Full-Reference(FR)와 No-Reference(NR) 방식으로 나뉜다.
- NR-IQA 방식은 많지만 FIQA는 대부분 Full-Reference(FR) 방법을 사용한다.
- 하지만 Reference가 있는 데이터는 구하기 어렵다.
- 따라서 No-Reference 방식을 적용한 NR-FIQA 모델을 만들자.

## 2. 데이터 수집
- KonIQ-10k IQA Database
- Flickr-Faces-HQ (FFHQ) (512 * 512)
- Tampere Image Database (TID2013)
- MS-Celeb-1M
- 한국인 안면 이미지 데이터베이스(https://www.aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&aihubDataSe=realm&dataSetSn=83)

## 3. 기존 문제 해결방법 탐색 및 전략 수립
- NR-IQA 모델(MANIQA, TReS, MUSIQ, HyperIQA, Meta-IQA) 중 구현 및 성능 확인 후 MANIQA, MUSIQ 선택
- NR-IQA은 FIQA에 적합하지 않다는 결론
- FIQA 모델(MagFace, SDD-FIQA, SER-FIQ) 중 구현 가능성 및 앙상블 가능성을 고려하여 SDD-FIQA 선택
- SDD-FIQA의 Quality Network를 MANIQA로 변경 후 MS-Celeb-1M를 이용하여 학습

## 4. 학습 및 분석

## 5. 결론

***

---
# No-Reference Image Qaulity Assessment(NR-IQA) model을 활용한 Face  Image Assessment(FIQA) model 만들기

### Abstract

## 1. Introduction
기존의 NR-IQA는 이미지 전체의 품질을 판단하기 때문에 사람의 얼굴만의 품질을 판단하기에는 적합하지 않다. 또한, 기존의 FIQA는 대부분 Full Refence 기반으로 만들어지기 때문에 Refence가 없는 경우 model을 train하는 것이 불가능하다. 따라서 이번 프로젝트에서는 NR-IQA를 이용하여 NR-FIQA model을 만들어 보고자 한다.
사용한 모델은 NR-IQA model 2가지(MANIQA, MUSIQ), FIQA model 2가지(SDD-FIQA, MagFace)이며 사용한 dataset은 KonIQ-10k, Tid2013, 한국인 안면 데이터(ai hub), FFHQ이다. 먼저 NR-IQA와 FIQA model의 code를 분석하여 각 model의 적용 원리를 이해하고 NR-IQA model 중 하나, FIQA model 중 하나를 선택하여 두 mdoel을 접목시키도록 한다.

## 2. Related Work
### 2-1. Multi-dimension Attention Network for No-Reference Image Quality Assessment(MANIQA)
![maniqa](https://user-images.githubusercontent.com/103994779/193990724-5bd1cdc8-17b5-400f-a3e8-d2fe74ec2f1e.png)
MANIQA model의 가장 큰 특징은 Vision Transformer를 이용한다는 점과 Position Embedding을 통해 local interaction을 찾는다는 점이다. 기존의 NR-IQA model과 달리 이미지의 local interaction을 ViT에 input함으로써 이미지를 patch로 잘랐을 때 patch 간 interaction을 model이 학습하게 함으로써 더 정확한 score를 예측하도록 한다.

### 2-2. Multi-scale Image Quality Transformer(MUSIQ)
<img width="977" alt="musiq" src="https://user-images.githubusercontent.com/103994779/193990542-2e5f387d-5804-4564-b546-4ccd5cf0be2e.png">
MUSIQ model의 가장 큰 특징은 Conv layer를 통과하는 과정에서 이미지의 비율을 그대로 유지한다는 점이다. 기존의 IQA 방식은 conv layer를 통과하며 이미지의 크기가 작아지고 비율이 달라지기 때문에 기존의 이미지와 다른 이미지를 학습하는 것과 비슷한 영향을 주게 된다. MUSIQ의 경우 이미지를 resizing하지만 patch로 자르고 resizing하는 과정에서 각 patch마다의 이미지 비율을 유지하기 때문에 conv layer를 통과한 이후에도 원본 이미지와 같은 비율을 유지하며 resizing된 patch의 feature도 patch encodong module을 통해 Transformer에 전달하기 때문에 원본에 가까운 이미지 feature로 학습을 할 수 있게 된다.

### 2-3.  Unsupervised Face Image Quality Assessment with
Similarity Distribution Distance(SDD-FIQA)
![sdd](https://user-images.githubusercontent.com/103994779/193990574-1c3b39b4-5262-4ba9-a35e-bca8df42a073.png)
SDD-FIQA model의 특징은 intra-class와 inter-class 사이의 Wasserstein distance를 계산하여 이미지를 class 별로 나누어 학습하는 것이다. 기존의 FIQA의 경우 input된 이미지를 각각으로 나누어 feature를 찾기 때문에 유사한 이미지 사이의 상관관계 또는 유사하지 않은 이미지 사이의 상관관계에 대해 큰 의미를 두지 않았다. 하지만, SDD-FIQA model의 경우 이미지를 class 별로 나누어 input하기 때문에 model이 class에 따른 feature 차이를 학습할 수 있고, class내의 이미지에 대해 공통적인 feature를 학습함으로써 face에 대한 feature를 더 자세히 학습할 수 있다. 또한 단순한 거리를 구하는 Euclidean Distance를 쓰는 것이 아니라 calss 간 거리를 구할 수 있는 Wasserstein distance를 사용하기 때문에 

### 2-4. MagFace: A Universal Representation for Face Recognition and Quality Assessment

![magface](https://user-images.githubusercontent.com/103994779/193990509-a587cb33-3c1d-41bd-9e94-34ed279d1fc1.png)
MagFace model은  ArcFace model을 기반으로 cos $\theta$값을 이용해 이미지 간의 feature 차이를 학습한다. 하지만 ArcFace의 경우 단순히 cos $\theta$만을 이용하기 때문에 이미지 quality 차이에 따른 가중치를 줄 수 없는 문제가 있었다. MagFace는 cos $\theta$에 g와 m 이라는 가중치를 새로 부여함으로써 학습 시 이미지 quality에 따라 같은 class 내의 이미지라도 다른 feature 값을 갖게 되기 때문에 이미지 quality를 더 잘 예측할 수 있다.
## 3. The Proposed Model

## 4. Experiments
## 5. Conculsion

## Refen



