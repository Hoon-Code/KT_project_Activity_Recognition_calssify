![image](https://github.com/user-attachments/assets/af600b16-052f-4d3c-a401-51331a9abc96)# 스마트폰 센서 데이터 기반 행동 인식 분류
---
## 프로젝트 개요 
- 주제 : 스마트폰 센서 데이터를 활용한 행동 인식
- 학습과목 : 데이터전처리, 머신/딥러닝
- 데이터 출처 : <https://archive.ics.uci.edu/dataset/240/human+activity+recognition+using+smartphones>
- 중점사항 : 561개 feature값에 대한 데이터 탐색, 6개 class 관계를 고려한 모델링
- 프로젝트 목표 : 스마트폰 기반의 센서 데이터 활용해 동작 분류 하는 모델 완성 
---

## 도메인 이해 
![image](https://github.com/user-attachments/assets/08f84762-c1a0-4aff-9035-a9ed11de8957)
![image](https://github.com/user-attachments/assets/9b067e53-16b3-44ae-8b99-7b0dd66e67af)
---

## 데이터 소개
![image](https://github.com/user-attachments/assets/328bf7b6-d608-49d5-87fd-c886e28fe6c9)

### 데이터 수집방식

![image](https://github.com/user-attachments/assets/ce6617cf-c865-4f77-9bb9-4dbcbeeac4eb)
![image](https://github.com/user-attachments/assets/e65e9a51-53d2-4b3e-92a4-621d0b7d6207)
![image](https://github.com/user-attachments/assets/66365e08-5061-47c3-b2f8-6b6401a88b0e)
![image](https://github.com/user-attachments/assets/615b7213-e086-438b-a870-87c60102f68e)
![image](https://github.com/user-attachments/assets/6bf60ca8-47b4-4732-b36b-995cf3214aa7)
![image](https://github.com/user-attachments/assets/6dd928e6-9d66-4d0b-af6c-2ee689c6c783)
---

## 핵심사항
![image](https://github.com/user-attachments/assets/f0dd7fb3-a034-4a08-87cf-25293f0e3900)
![image](https://github.com/user-attachments/assets/c67622fc-dcdb-41d3-8a7f-486384f55e15)
![image](https://github.com/user-attachments/assets/a8f625cb-1273-41b0-a8d7-3c72d994ed3f)
---

## 데이터 전처리/EDA

1) **RandomForest이용해 feature_importance구해서 내림차순 정렬 후 데이터프레임 형성/EDA** 
![image](https://github.com/user-attachments/assets/dde3140a-1775-45ca-a5f3-c5f6831b97ae)

2) **정적/동적 행동으로 나누기 위해 변수 만든후 해당 변수를 구분하는데 중요한 변수를 RandomForest의 feature_importance통해 내림차순 정렬후 데이터프레임 형성/EDA**
![image](https://github.com/user-attachments/assets/c9c762d1-3b39-46a1-b7d2-d1f45081630d)

3) **개별 동작별 중요도를 구하기 위해 RandomForest의 feature_importance통해 내림차순 정렬후 각각 데이터 프레임 형성/EDA**

4) **각각의 관점별 중요도를 구한 데이터프레임 하나로 합친후 저장/EDA**
- 관점1 : 6개 행동 전체중 변수 중요도
- 관점2 : 동적,정적 행동별 변수 중요도
- 관점3~관점8 : 각각 행동별 변수 중요도
![image](https://github.com/user-attachments/assets/14cb2fbf-588f-4469-b3bd-3b8dd08f6708)

## 단계별 모델링
단계 1) 정적, 동적 행동 분류 모델 생성 
단계 2) 세부 동작에 대한 분류 모델 생성 
  - 단계1 모델에서 0으로 예측 -> 정적 행동 3가지 분류 모델링
  - 단계1 모델에서 1로 예측 -> 동적 행동 3가지 분류 모델링

![image](https://github.com/user-attachments/assets/441f2bac-c3e7-49d7-815c-5590b751742d)

-> 이진분류에 쓰일 target과 세부동작에 대한 분류에 쓰일 target 나눠서 train_test_split진행
- 단계 1)에서 이진분류시 모델로 RandomForest 사용

![image](https://github.com/user-attachments/assets/263b9dc4-94aa-4b06-bfac-761df7c5880c)

- 정적,동적 각각 행동 세부동작에 대한 모델로는 LogisticRegression모델 사용

**정적**

![image](https://github.com/user-attachments/assets/f8754e54-3a1a-4e65-9574-7a41a5a1d137)

**동적**

![image](https://github.com/user-attachments/assets/28d8263d-20aa-49f6-8722-b0fcb499b181)



## 분류 모델 합치기 
- **두단계 모델 통합, test데이터에 대해 최종 예측결과와 성능평가 나오도록 함수로 만들기(데이터파이프라인 구축)**

![image](https://github.com/user-attachments/assets/7fb86477-9c73-4e48-8040-68f1741ac7ec)

![image](https://github.com/user-attachments/assets/cfb6970e-317a-429b-b28d-1a40d20e40fd)

- test셋으로 예측, 평가

![image](https://github.com/user-attachments/assets/cd9f72f6-4f60-4fb6-9b9e-b8d4dbba0e83)

