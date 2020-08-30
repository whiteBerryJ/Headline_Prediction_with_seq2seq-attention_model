# Headline_Prediction_with_seq2seq-attention_model
## 전체 code폴더 설명
구글 colab에서 작업한 news_headline.ipynb 파일이 있으며 해당 코드는
seq2seq + attention 모델을 사용하여 뉴스기사의 헤드라인을 예측한다.
뉴스 기사 내용 데이터와 headline에 대한 데이터가 존재한다.
예측하는데 필요한 encoder_model.h5, decoder_model.h5 파일이 존재한다.
코드를 실행시키는데 필요한 input파일들이 존재한다.


## 전처리
- 영어 대 소문자 제거
- 문자와 숫자를 제외한 특수문자 제거
- label인 headline에서 중복 행 제거
- suffle을 통해 test데이터가 한 종류의 기사로 편향되는 것을 막음.
- 데이터 시각화를 통해 문장의 max_len을 임의로 설정하여 과하게 padding되는 것을 막음.

한글의 특수성으로 스플릿으로만 구분하게 되면 정확도가 매우 낮게 훈련됨.
-koNLpy모듈로 형태소를 추출하여 훈련한 정확도 비교하였음.

## 토큰화
- koLNpy의 kkma 모듈을 사용하여 형태소 추출
- koNLpy의 모듈인 Komoran, Kkma, mecab, Hannanum, Okt를 비교하였고, 그 중 시간은 오래걸리지만
가장 성능이 좋았던 kkma 토크나이저를 채택하였다.

## 모델 구조:
3중 LSTM Layers를 사용했으며 각 레이어마다 dropout을 적용시켜 과적합을 방지하였다.
AttentionLayer을 사용하여 attention을 적용하였다.


## 개선할 점.
데이터량을 늘리되 여러 토픽의 기사들을 같은 비율로 학습시켜야 할 것 같다. 
프로젝트에서는 '스포츠동아'의 연예, 스포츠, 토픽 란의 데이터를 주로 사용하였고(18000여 개), 네이버의 속보 기사 또한 약 4000여개를 사용하였다.


