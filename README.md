# FixMatch

 FixMatch: Simplifying Semi-Supervised Learning with Consistency and Confidence

## A Combination of Approaches

![Diagram of FixMatch](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b37f6306-68cb-4de9-8ac3-434580a23c9c/Untitled.png)

Diagram of FixMatch

- **Consistency Regularization**기반 **준지도학습(Semi-supervised learning)** 방법론
    - label이 존재하지 않는 data에 noise를 주입한 뒤 모델이 noise가 없는 원본 데이터와 noise가 주입된 데이터를 동일한 class 분포로 예측하도록 학습

그 중에서도,

- **FixMatch**
    - 한 이미지를 서로 다른 방식으로 변형하여 대조하는 방식
    - **Pseudo Labeling과 Consistency Regularization을 결합**
        - Weak augmentation과 strong augmentation(RandAugment, CTAugment)에 pseudo labeling 방법을 함께 도입해 높은 성능 향상
        

### **Pseudo Labeling**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eb84762e-bf38-485c-9621-2346d3262010/Untitled.png)

1. Labeled data로 모델 학습
2. Labeled data로 학습된 모델을 가지고 unlabeled data 추론
3. 추론값들 중 가장 확시한 것을 pseudo label로 만듦
4. Labeled data에 pseudo label을 가진 data 포함
5. 반복

이러한 반복 과정을 통해 labeled data는 조금씩 늘어가고, unlabeled data는 조금씩 줄어갑니다. 

### **Consistency Regularization**

"데이터에 가해진 작은 변형은 라벨을 변형시키지 않는다”

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0596be33-9cf2-4130-9f14-f8d231bc5ef7/Untitled.png)

- 왼쪽 사진의 예측 확률 분포와 오른쪽 사진의 예측 확률 분포를 동일하게 만들도록 학습
- 두 확률 분포의 차이가 손실이 됨

![Formula of Consistency Regularization](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ca82d57b-7b04-41bf-8590-b1c9ee32135d/Untitled.png)

Formula of Consistency Regularization

### **Entropy Minimization**

"좀 더 확실하게 만들기”

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/849f6649-7f9a-4be8-be0d-70a5d83da6d8/Untitled.png)



## The Architecture of FixMatch

- Weakly augmented 된 이미지를 사용하여 모델 추론함으로써 pseudo label을 만듦 → Pseudo Labeling
- Threshold에 따라 추론 결과는 하나의 label을 가지게 되므로, One-hot vector로 바뀜 → Entropy Minimization
- Strongly augmented 된 이미지를 사용하여 모델 추론한 확률 분포와 차이가 줄어들도록 학습 → Consistency Regularization

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/924136e1-2755-4842-827d-c80e9717dfa0/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9f050d3d-916e-4eaa-81f8-7c42c8c4d1aa/Untitled.png)

---

Reference
[](https://arxiv.org/ftp/arxiv/papers/2001/2001.07685.pdf)

[[Paper Review] ReMixMatch & FixMatch : Consistency-based Semi-supervised Learning Methods](http://dsba.korea.ac.kr/seminar/?mod=document&uid=248)

[FixMatch 논문 w/ Naver Shopping Classification Project](https://ainote.tistory.com/6)
