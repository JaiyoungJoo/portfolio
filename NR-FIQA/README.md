# 프로젝트 주제
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


