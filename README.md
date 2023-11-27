## NLP 알고리즘을 활용한 A.I 보이스 피싱 탐지 모델
- 본 프로젝트에서는 KoBIGBIRD 모델과 R-BERT, 그리고 KRBERT 모델을 Concat 및 Customize하여 최종 모델로 채택함.


### 📜 About Model 📜
* Relation Extraction Task에서 R-BERT 모델은 CLS 토큰 뿐만 아니라 entity1과 entity2 임베딩 벡터를 같이 활용함으로써 그 성능을 높이고자 하였다.
* 이에 해당 모델은 CLS 토큰 뿐만 아니라 전체 대화 데이터와 형태소 및 키워드만을 추출한 데이터, 각각의 임베딩 벡터를 학습에 사용해보자는 관점에서 Custom이 된 모델이라고 할 수 있다.
  
### ⚙️ How Customized? ⚙️
* 해당 모델은 R-BERT 모델로부터 영감을 얻어 KoBIGBIRD 모델의 Architecture를 수정한 모델

1. Kr-BERT의 CLS 토큰과 KoBIGBIRD의 CLS 토큰의 임베딩 값을 결합
2. 전체 대화 데이터와 키워드 및 형태소만을 추출한 데이터를 벡터로 분리. 이 과정에서 문장의 끝을 나타내는 인덱스를 사용. 이는 전체 대화 데이터를 통해 대화의 문맥을 이해하고, 형태소 및 키워드를 통해 대화에서 중요한 부분을 학습하고자 설계된 부분이다

### ❓ Why Customized? ❓
* KOBIGBIRD는 한국어에 특화되었으며, BERT의 8배인 최대 4096개의 TOKEN을 다룬 모델
--> 보통 보이스피싱은 전화 통화를 통해 발생하기 때문에 짧은 문장 보다는 긴 문장이 대다수
* R-Bert는 Bert기반의 모델로, 문맥을 고려한 entity 관계 추론에 특화된 모델로, 보이스피싱 문장에서 단어간의 관계성 및 문맥 관계성을 파악하는데 사용할 것이라 기대
* Custom 과정을 걸쳐 Kr-BERT의 언어 이해 능력과 KoBIGBIRD의 장문 처리 능력을 결합함으로써 입력 텍스트의  다양한 특징을 포함
* Kr-BERT와 KoBIGBIRD의 CLS 토큰을 합침으로써 두 모델의  다양한 특징을 융합하여 각 모델의 장점을 활용하고 서로의 부족한 부분을 보완


### 🦾 About Algorithms 🦾

![image](https://github.com/Voice-Phishing-Prevention-Project/NLP_CustomModel/assets/79118751/ec04554c-5ddc-42a8-a99c-096a7bcef2f9)

![image](https://github.com/Voice-Phishing-Prevention-Project/NLP_CustomModel/assets/79118751/8416654d-96b0-44ba-9625-2935a7528bb0)

![image](https://github.com/pej0918/2022_Hanium_Project/assets/79118751/461cd96a-0420-49ba-80e7-3ca785bf631a)

