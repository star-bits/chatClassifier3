# chatClassifier3
- [chatClassifier](https://github.com/star-bits/chatClassifier)
- [chatClassifier2](https://github.com/star-bits/chatClassifier2)

문장만 보고 누가 쓴 건지 추측해보자

- 2022년의 데이터는 train set, 2023년 1월의 데이터는 test set으로 이용함 (각각 93만개, 5만개)
- 대화량 상위 62명의 데이터만 사용함 
- SentencePiece를 이용해 vocab size 10000으로 토큰화
- 정수변환 이후 최대 길이 25로 padding (99% 이상의 데이터가 길이 25 이하)
- gensim Word2Vec을 이용해 pretrained Word2Vec embedding vectors 생성

| Model                                                         | Validation Accuracy | Test Accuracy |
|---------------------------------------------------------------|---------------------|---------------|
| Multi-kernel 1D CNN with trainable embedding layer            | 0.246               | 0.288         |
| Multi-kernel 1D CNN with pretrained Word2Vec embedding vectors| 0.249               | 0.287         |
| LSTM with pretrained Word2Vec embedding vectors               | 0.276               | 0.302         |
| Transformer with trainable embedding layer                    | **0.294**           | **0.327**     |
| Transformer with pretrained Word2Vec embedding vectors        | 0.232               | 0.270         |

## Inference 예시 (Transformer with trainable embedding layer)
```
존예디컵 여름 풀파티 하기 딱이긴 하겠네요
1/1 [==============================] - 0s 28ms/step
1) 爱德华/잠실르엘판매중/25: 96.40%
2) 랄프: 0.43%
3) 정대만: 0.41%
4) Jinyoung. woo: 0.35%
5) 심언니: 0.27%
```
```
다 없어졌.
1/1 [==============================] - 0s 23ms/step
1) 권인호: 53.41%
2) 랄프: 19.20%
3) Edward Jeong: 7.54%
4) 박찬홍/ 주생아/엉아들 잘부탁해~: 3.45%
5) 라테라테: 3.11%
```
```
ㅎㅎ
1/1 [==============================] - 0s 30ms/step
1) 박찬홍/ 주생아/엉아들 잘부탁해~: 46.65%
2) 랄프: 12.19%
3) malarka: 6.11%
4) 김반포: 6.08%
5) 촉촉: 3.41%
```

## Word2Vec 유사 토큰 예시
```
gom22_word2vec.wv.most_similar('▁선착순', topn=10)
[('▁시작합니다', 0.5552059412002563),
 ('▁선물을', 0.5508813261985779),
 ('▁늦지', 0.542372465133667),
 ('▁기회는', 0.534000813961029),
 ('분간', 0.5311708450317383),
 ('▁종료됩니다', 0.5190539360046387),
 ('▁보냈습니다', 0.5137362480163574),
 ('▁않았어요', 0.5063295364379883),
 ('▁게임을', 0.49447911977767944),
 ('▁장오픈', 0.4536493122577667)]
```
```
gom22_word2vec.wv.most_similar('▁존예디컵', topn=10)
[('▁남친', 0.7010402679443359),
 ('▁동생', 0.6910679936408997),
 ('▁여친', 0.6905515789985657),
 ('▁가족', 0.6805916428565979),
 ('▁남편', 0.6728658676147461),
 ('▁부모님', 0.6604858636856079),
 ('▁여사친', 0.6370567679405212),
 ('▁여자', 0.6136230826377869),
 ('▁지인', 0.598432719707489),
 ('▁슈렁', 0.5925098657608032)]
```
