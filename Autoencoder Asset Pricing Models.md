- 샤프 지수 = (펀드 수익률 - 무위험 수익률) / 위험 \
(위험은 표준편차를 이용해 측정, 샤프 지수는 높은 것이 좋은 것)

# Autoencoder Asset Pricing Models
논문 링크 : https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3335536

### 선행연구 KPS

- latent factor(잠재 변수)를 찾고 동적인 선형모형으로 factor loading(요인 분석) \
수익률 패턴은 risk factor(위험 변수)에 의해 동적으로 영향! \
→ 잠재 위험 변수는 수익률에 영향! 

-  r i,t ​ =β(z i,t−1 ​ ) ′ f t ​ +u i,t ​ \
 r(N×1) = 수익률, ft(K×1) = 잠재 위험 변수(latent rist factor)

- factor loading \
 : β(z i,t−1 ​ ) ′ =z i,t−1 ′ ​ Γ \
 z(P×1) = 종목특성 \
 잠재 변수의 계수가 종목 특성값이 변함에 따라 동적으로 변함
 
- [수익률이외의 외부 정보] \
 IPCA(Instrumental PCA) \
 instrumental variable(도구 변수)에 기반한 조건부 factor 가중치 계산 방법
 
 ## 오토인코더 Chicago Booth
 
- [수익률 이외의 외부 정보] \
 Conditional Autoencoder \
 차원감축 기법 PCA 대신 오토인코더를 사용해 선형성을 일반화 \
 비선형 함수를 여러 층 쌓아 정보 압축
 <img src="https://user-images.githubusercontent.com/58911440/83472444-364f5180-a4c2-11ea-8a36-1027108851f3.png">
 
 ### Beta (왼쪽)
 
 - input : N x P 행렬 (N:종목, P:종목 특성값) \
ouput : N x K 행렬 (K:잠재변수의 개수)
 
 ### Factor (오른쪽)
 
 -  case 1. \
 input : N x 1 행렬 (개별 주식의 수익률) \
      output : K x 1 행렬 (종목이 선형 조합된 포트폴리오)    
*  case 2. \
input : P x 1 행렬 (각 특성에 따라 구성된 포트폴리오의 수익률) \
      output : K x 1 행렬 (종목의 수익률)
      
### 실험

 - 1957년 3월 ~ 2016년 12월, 총 60년치 데이터 사용
 - 총 3만여개의 종목, 94개의 종목 특성 사용
 - PCA, IPCA, Conditional Autoencoder 모델 4개, benchmark 포트폴리오
      
### 훈련 
 
 손실 : L2 Loss(실제 값과 예측치 사이의 오차값의 제곱 합) \
 정규화 : L1 Norm(벡터 p, q의 각 원소들의 차이의 절대값 합), Early Stopping, Ensemble \
 최적화 : minibatch SGD(확률적 경사 하강법), batch-norm

- L1 Norm은 여러가지 path를 가지지만 L2 Norm(벡터 p, q의 유클리디안 거리)은 Unique shortest path를 가진다.
 - L1 Loss : 실제 값과 예측치 사이의 오차값의 절대값들의 합, L1 Loss가 L2 Loss에 비해 Outlier(극단치)에 대하여 덜 민감하다.
 
 ### 견고성
 
 <img src="https://user-images.githubusercontent.com/58911440/83485632-673f7e80-a4e2-11ea-86ae-60ca1d4b6a85.PNG">
 각각 Beta와 Factor에 대한 모델 기여도 측면에서 94개의 주식 특성 중요도의 순위을 나타낸다.
 
 ### 결론
 
 - 오토인코더를 사용한 자산 가격 책정을 위한 잠재 요인 모델링에 대한 새로운 접근법
 - 차익 거래의 경제적 제한을 포함하는 비선형 조건부 자산 가격 책정 모델

