- https://github.com/JaiyoungJoo/portfolio/blob/main/NR-FIQA/hyper-IQA/HyperIQA_Joo.pdf
- https://github.com/JaiyoungJoo/portfolio/blob/main/NR-FIQA/hyper-IQA/HyperIQA_implementation_Joo.pdf

# HyperIQA Implementation
- 논문 저자들이 `demo.py`를 만들어 놓음.
- 실행할 경우 demo image의 predict score를 output함.
- 이번 프로젝트에서 사용하기 위해 `demo.ipynb` 생성
- koniq_pretrained.pkl 파일 필요([Google drive](https://drive.google.com/file/d/1OOUmnbvpGea0LIGpIWEbOyxfWx6UCiiE/view?usp=sharing) or [Baidu cloud](https://pan.baidu.com/s/1yY3O8DbfTTtUwXn14Mtr8Q) (password: 1ty8))
- pretrained 폴더 생성 후 `koniq_pretrained.pkl` 파일을 넣음.
- 1번 셀 실행 후 2번 셀에서 `torch.load` 경로 확인 후 실행
- filenames에 predict 하고자하는 이미지 폴더 경로를 넣음.
- 결과를 저장하기 위한 `dataframe`을 생성
- `im_path = f'./data/{filename}'` 에 이미지 폴더 경로를 넣음.
- `dataframe` 이름 확인 후 셀 실행 시 `dataframe`에 결과가 삽입.

# Dataset
### KonIq-10k
- http://database.mmsp-kn.de/koniq-10k-database.html

![koniqsample](https://user-images.githubusercontent.com/103994779/192446632-a500cfb9-c7dd-48bf-9d26-23388ef56d36.png)

- 총 10,073장의 이미지
- 512x384 px
- 우리가 자주 보는 사진 이미지와 유사

# Result
- 원본 이미지 489장을 test data로 Image_predic_score를 추출
- 얼굴을 자른 이미지 489장을 test data로 Face_predic_score를 추출

![Hyper_result](https://user-images.githubusercontent.com/103994779/192446910-c73a92b0-4892-4fee-8a65-90ab2a8f1b9d.png)

***
- 원본 이미지 MOS_zscore와 원본 이미지 predict_score 비교
  - predict_score가 MOS_zscore에 비해 조금 낮지만 큰 차이는 없다

![Hyper_predict_score](https://user-images.githubusercontent.com/103994779/192447397-2f58f208-ad94-4c5e-84ce-90e286f532c4.png)

***
- 원본 이미지 MOS_zscore와 얼굴 자른 이미지 face_predict_score 비교
  - face_predict_score가 대부분 20 ~ 40점 사이 값을 갖는다.
  - MOS_zscore가 높을 수록 차이가 심해진다.

![Hyper_face_predict_score](https://user-images.githubusercontent.com/103994779/192447492-3377d806-ec34-4535-806d-dbe6475a44dd.png)

***
- PLCC, SRCC, MSE 비교 

![Untitled](https://user-images.githubusercontent.com/103994779/192447558-7adc265e-14b8-427c-b0e2-1affebae4fbe.png)

***
![hyper-ffhq-high-image](https://user-images.githubusercontent.com/103994779/194014942-cf907cba-e90e-4162-a971-11c6506a1b57.jpg)
![hyper-ffhq-low-image](https://user-images.githubusercontent.com/103994779/194014945-0e371db6-d981-49cf-9857-ab90cad11921.jpg)




