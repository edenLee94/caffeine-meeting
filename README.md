## caffeine-meeting
![initial](https://user-images.githubusercontent.com/47210353/175638330-1f12e620-77fd-4382-a82b-efd8062d672f.png)
### 프로젝트 아이디어
내 상황에 맞는 카페 추천해주는 시스템

### 네이버 지도 크롤링
카페 이름, 방문자 리뷰, 쿼리, 주소(ex)서교동, 망원동, 동교동

---
### 프로젝트 주제 선정 이유

검색을 통해서 커피를 마시러 가는 시대에 살고 있습니다. 

우리는  분명하게 자신이 가고자하는 카페가 있지만, 찾는 것은 비교적 쉽지않은 과정입니다. 

네이버 지도에 있는 저장 기능을 통해서 ‘다음에 가봐야지..’라는 생각으로 저장해두지만, 그 지역을 가야하는 날에는 모든 선택지가 애매합니다. 이러한 고민을 해보신 분들을 위해서 이 프로젝트를 설계했습니다. 

- 고민되는 이유 : 네이버 지도에서 방문자 리뷰 데이터를 가져와서 봤을때  기존 text data에 비해 unstructed하고 diverse됐기 때문에
    ⇒ 리뷰 데이터를 사용한 논문을 통해서 내용 학습이 필요할 것 같다. 
     ⇒ (IMDB dataset)리뷰 데이터, 평점을 사용한 논문[JOINT TRAINING OF RATINGS AND REVIEWS WITH
RECURRENT RECOMMENDER NETWORKS](https://openreview.net/pdf?id=Bkv9FyHYx)을 통해서 내용 학습이 필요할 것 같다.[요약문](https://github.com/edenLee94/caffeine-meeting/blob/main/review_rating/Readme.md)

-> 단순하게 문장 유사도를 이용하기 때문에 이 논문 사용이 적합하지않다.
    
`서비스 이용 방법`

원하는 분위기, 오늘 카페에 가서 무엇을 하고싶은지 구글폼을 통해서 적어주시면 분석 후 답변해드립니다.

설문지(구글폼) 이용 : [Find your favorite cafe 설문지](https://docs.google.com/forms/d/1NpMqjm_irWul-KTW8gLywuWKiSaeBKBMwZFVgc_Ikec/edit?hl=ko)


### [발표 자료](https://github.com/edenLee94/caffeine-meeting/blob/main/recom_forpdf.pdf)
User는 문장(내가 원하는 카페에서 얻을 이득)을 넣으면, 카페의 기존에 작성된 네이버 방문자 리뷰를 통해서 유사도를 비교해서 Top5를 추천해주는 형식으로 진행한다. 

그리고 기존에 있던 ‘합정역 카페’라고 검색을 하면, 망원, 상수, 홍대, 합정 결과가 모두 애매하게 나온다. -> 우리의 방향성을 그래서 ‘– –동(서교,합정,동교동)＇좀 더 명확하게 나눠서 진행할 예정이다. 

---
### TF-IDF을 이용한 카페 리뷰 유사도 분석을 통한 카페 추천 시스템 구현[code](https://github.com/edenLee94/caffeine-meeting/blob/main/cafe_sentence_similarity.ipynb)

#### CBF,content-based filtering(내용 기반 필터링)

어떤 아이템의 내용('리뷰')에 기반하여 유사한 콘텐츠를 추천해주는 것이다.
- 군집화
- 딥러닝 기반 이미지 유사도 비교
- TF-IDF

다음 3개의 방법 중에서 키워드, 장르, 텍스트 등의 유사성 기반인 TF-IDF의 방법을 이용해서 텍스트(리뷰)에 대해서 진행할 예정이다. 그리고 자카드 유사도, 코사인 유사도, 유클리디안 유사도 중에서 코사인 유사도방법을 채택할 것입니다.

---
### BERT를 이용한 카페 리뷰 유사도 분석을 통한 카페 추천 시스템 구현[code](https://github.com/edenLee94/caffeine-meeting/blob/main/cafedafe_Bert_base.ipynb)
