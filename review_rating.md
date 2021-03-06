#### JOINT TRAINING OF RATINGS AND REVIEWS WITH RECURRENT RECOMMENDER NETWORKS

IMDB 데이터셋을 활용하여 모델 성능에 대한 실험 진행!

## 논문의 ABSTRACT

Accurate modeling of ratings and text reviews is at the core of successful recommender systems.

combines ratings, reviews, and temporal patterns(시계열 데이터) to learn highly accurate recommendations.
We co-train for prediction on both numerical ratings and natural language reviews!

> 평점과 리뷰 데이터(text)를 모두 활용하여 추천시스템을 만들며, Recurrent 모델 구조를 활용하여 uesr, item의 다양한 component를 얻으려고 한다.
> 

## 논문의 Introduction

모델 예측 정확도는 실제 평점을 예측하는 것보다 주로 데이터셋을 나누고 테스트셋에 대한 평가가 이루어진다.

RRN은 RNN구조로 user, item 변화 등을 파악할 수 있으나, 리뷰의 시간적 변화 등을 제대로 포착할 수 없었다.

추천시스템에서 리뷰 데이터를 많이 사용하기 어려운 이유는 기존 텍스트 데이터에 비해 unstructed하고 diverse됐기 때문이다.

![A23BDB4C-7677-465C-A51E-BE86A6CB814F_4_5005_c.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ee307f87-91a9-4202-92ff-13086ce51751/A23BDB4C-7677-465C-A51E-BE86A6CB814F_4_5005_c.jpeg)

- joint generative model : 리뷰 데이터와 평점을 결합한 joint 모델 구조를 제안한다.
- nonlinear nonparametric review model : uesr와 movie의 state dynamics를 학습하면서 시간 변화에 따른 리뷰의 변화를 파악할 수 있다.
- 실험 : 시간 흐름과 함께 평점과 리뷰 데이터를 함께 모델링해서 IMDB 데이터셋에 대해 좋은 성능을 얻었다.

## 논문에서 제시한 Model

- ‘Recurrent Recommender Networks’ 논문에서 제시한 모델에 대한 설명
    
    ![4C6F7F7D-8E26-433D-A182-5141741F7AF9.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e73accfb-c525-4cdf-9de2-c88fb4478d5b/4C6F7F7D-8E26-433D-A182-5141741F7AF9.jpeg)
    
    [](https://dl.acm.org/doi/pdf/10.1145/3018661.3018689)
    
    user에 대한 state evolution은 user가 이전에 평점을 준 영화와 관련 있다.
    
    movie의 파라미터는 이전 시간에서 평가한 사용화의 인기에 따라 다르다.
    

위의 논문을 통해서 이 논문에서 모델을 어떻게 진행할까요?

![48CE2CA2-7461-48D7-9C9F-8945B8DC597F.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3c60e832-8825-4b9e-9f3f-6eda3aae7147/48CE2CA2-7461-48D7-9C9F-8945B8DC597F.jpeg)

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

## 학습 및 예측

![549B42B0-F2F4-4C74-BF92-2E59FA403737_4_5005_c.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/877af2b3-f6be-4177-b558-3a90e03adaf0/549B42B0-F2F4-4C74-BF92-2E59FA403737_4_5005_c.jpeg)

<학습>

Accurate ratings 와 accurate review를 예측하는 것이 목적이다.

D는 (i,j)쌍의 학습 데이터

<예측>

예측된 미래 상태에 따라 평점을 예측

최근 평점을 input으로 사용하여 상태를 업데이트하고 새롭게 예측된 상태를 통해 평점을 예측

## Experiments

![51EBEC86-566E-41F9-AAB3-19BAAE74D7B9_4_5005_c.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/aa498a5a-f639-4a82-8d3f-4f7c427e9db2/51EBEC86-566E-41F9-AAB3-19BAAE74D7B9_4_5005_c.jpeg)

K-core of IMDB dataset에 대해 평가를 진행한 결과이다.

RRN이 다른 4개의 baseline 모델(PMF,Time-SVD++,U-AutoRec,I-AutoRec)보다 더 좋은 성능을 나타내고, RRN(rating+text)이 성능을 더욱 향상시킴
