# 인디음악 가사 감성 분석 프로젝트 
더욱 상세한 내용은 [블로그](https://hajinnote.tistory.com/30)를 참조

### 주제 선정 
- 인디음악은 사람들이 잘 모르기 때문에 가사로 감성 분석을 해서 추천해주면 어떨까? 싶어서 도전하게된 프로젝트.

- 가설 1: word2vec으로 감성사전 구축 후 이를 이용해 bert같은 모델로 지도학습  

- 가설 2: 토픽 모델링으로 키워드를 뽑아내 이를 이용해 추천 


### 프로젝트 진행

**데이터수집**
- 가사 데이터 수집은 멜론을 이용했다. 인디음악에도 스타일별로 하위 장르가 나뉘는데 바이브나 벅스 등등 다른 곳은 하위 스타일을 나눠놓은 곳이 없어서 멜론으로 결정

**데이터 전처리**
- 특수문자 제거, 가사 없는 데이터 제거 

- 형태소 분석 & 불용어 제거 
  - mecab으로 품사 태깅 후 사용할 품사(명사, 동사, 형용사)만 남기고 제거 
  
  - 한글자 단위 단어는 의미 분석이 애매 하므로 제거 

  - 영어 가사도 많아서 영어 불용어 따로 제거 
  
*불용어 제거 전후 분포*
  ![img1 daumcdn](https://user-images.githubusercontent.com/83392231/176832939-151565ed-2c9f-4443-a333-9159d4e29ea9.png)


*고빈도 단어 워드클라우드 시각화*
![img1 daumcdn-1](https://user-images.githubusercontent.com/83392231/176833061-22fb7ca4-8e48-44f9-b377-550e1a4701c2.png)

**word2vec 학습**
- word2vec 학습 후 감성단어 별로 노래를 분류. 

  - 인디음악 특성 상 노래 분위기가 비슷하고 핵심단어가 너무 겹쳐 분류가 제대로 되지 않음 
  
  - 각 문장의 단어가 너무 적어서 이를 사용해 레이블링을 할 수 없다고 보여짐
  
**토픽 모델링**
- 문서 집합에서 숨겨진 주제를 찾아내 문서나 키워드별로 묶어주는 알고리즘. lda를 사용해 토픽 모델링

  - 위에서 말한 것처럼 인디음악 감성 분위기가 너무 비슷해서 비슷한 토픽만 계속 나오는 현상 발생 

![img1 daumcdn-2](https://user-images.githubusercontent.com/83392231/176834207-413c2d53-e73c-4b3f-a624-cbc491458dd8.png)


### 프로젝트 결과
- 인디음악 특성상 결이 비슷비슷해서 분류 할만한 기준점을 찾기 힘듦(노래의 특성이기도한데 사랑 관련 키워드가 압도적으로 많음)

- 불용어를 제거하고 나니 가사가 너무 짧아져서 문장으로 비교는 힘들고 문서 단위로 비교해야 어느정도 의미 있는 분류가 될 것 같다. 

- 단어 분포같은 방식이 아닌 tf-tdf 같이 문서 유사도 방식을 적용하면 훨씬 나은 결과를 얻을 수 있을 것 같다. 

