### caffeine-meeting

#### 프로젝트 아이디어
내 상황에 맞는 카페 추천해주는 시스템

#### 네이버 지도 크롤링
카페 이름, 방문자 리뷰, 쿼리, 주소(ex)서교동, 망원동, 동교동

#### 프로젝트 주제 선정 이유

- 고민되는 이유 : 네이버 지도에서 방문자 리뷰 데이터를 가져와서 봤을때  기존 text data에 비해 unstructed하고 diverse됐기 때문에

- 우리가 클로링한 데이터양이 딥러닝이 필요한 수준이 아닐 수 있어서 고민 중이다.

 ⇒ 리뷰 데이터를 사용한 논문[JOINT TRAINING OF RATINGS AND REVIEWS WITH
RECURRENT RECOMMENDER NETWORKS](https://openreview.net/pdf?id=Bkv9FyHYx)을 통해서 내용 학습이 필요할 것 같다.[요약문](https://github.com/edenLee94/caffeine-meeting/blob/main/review_rating/Readme.md)

User는 문장(내가 원하는 카페에서 얻을 이득)을 넣으면,
카페의 기존에 작성된 네이버 방문자 리뷰를 통해서 유사도를 비교해서 Top5를 추천해주는 형식으로 진행한다. 

그리고 기존에 있던 ‘합정역 카페’라고 검색을 하면, 망원, 상수, 홍대, 합정 결과가 모두 애매하게 나온다. -> 우리의 방향성을 그래서 ‘– –동(서교,합정,동교동)＇좀 더 명확하게 나눠서 진행할 예정이다. 
