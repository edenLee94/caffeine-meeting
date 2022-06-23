
논문에서 제시한 Model

- ‘Recurrent Recommender Networks’ 논문에서 제시한 모델에 대한 설명
    - user에 대한 state evolution은 user가 이전에 평점을 준 영화와 관련 있다.
    - movie의 파라미터는 이전 시간에서 평가한 사용화의 인기에 따라 다르다.
    
위의 논문을 통해서 이 논문에서 모델을 어떻게 진행할까요?

→ These states are directly used to predict ratings and within an LSTM to model review text.(review text는 LSTM을 이용해서 진행)

1. Dynamic user and movie state
    - uesr/item  평점 과거 데이터를 input으로 사용해서 state를 update
    - 영화 관람하고 좋아요/싫어요 등으로 인한 user 상태 변화를 모델링 가능
2. Rating emissions
    - 사용자의 장기적 신호 또는 영화 장르와 같은 시간에 따라 크게 변하지 않는 요소에 대한 내용 반영
3. Review text model
    - character단위 LSTM 네트워크 활용
    - 이 네트워크는 평점 모델과 동일한 user/item의 latent 상태를 반영
    - 병목(bottlenect) 층에서 정적인 정보와 동적인 상태 모두 합치게 된다.

#### 학습 및 예측

<학습>
Accurate ratings 와 accurate review를 예측하는 것이 목적이다.
D는 (i,j)쌍의 학습 데이터
<예측>
예측된 미래 상태에 따라 평점을 예측!
최근 평점을 input으로 사용하여 상태를 업데이트하고 새롭게 예측된 상태를 통해 평점을 예측

#### Experiments

K-core of IMDB dataset에 대해 평가를 진행한 결과이다.

RRN이 다른 4개의 baseline 모델(PMF,Time-SVD++,U-AutoRec,I-AutoRec)보다 더 좋은 성능을 나타내고, RRN(rating+text)이 성능을 더욱 향상시킴
