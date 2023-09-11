#### R-KrBIRD
  해당 모델은 R-BERT 모델로부터 영감을 얻어 KoBIGBIRD 모델의 Architecture를 수정한 모델이다.
  ![image](https://github.com/pej0918/Custom_Model/assets/79118751/75cbf66b-dc5c-4579-83f9-5aa9bd4d7a3e)


  
- R-BERT 모델로부터 아이디어를 얻어 KoBIGBIRD 모델의 아키텍쳐를 수정
- Relation Extraction Task에서 R-BERT 모델은 CLS 토큰 뿐만 아니라 entity1과 entity2 임베딩 벡터를 같이 활용함으로써 그 성능을 높이고자함
- 전체 대화 데이터와 형태소 및 키워드만을 추출한 데이터, 각각의 임베딩 벡터를 학습에 사용해보자는 관점에서 Customize된 모델
- 또한, KrBERT와 KoBIGBIRD의 CLS 토큰을 합침으로써 두 모델의 다양한 특징을 융합하여 각 모델의 장점을 활용하고 서로의 부족한 부분을 보완하고자 함. 이러한 과정은 전체 대화 데이터를 통해 대화의 문맥을 이해하고, 형태소 및 키워드를 통해 대화에서 중요한 부분을 학습하고자 설계된 과정이라고 볼 수 있음
- KrBERT의 언어 이해 능력과 KoBIGBIRD의 장문 처리 능력을 결합함으로써 입력 텍스트의 다양한 특징을 포함시키고, 긴 대화 데이터를 다루는 데 있어 KoBIGBIRD의 장점을, 문장 내의 미묘한 의미나 표현을 이해하는 데 Kr-BERT의 장점을 활용할 것으로 기대됨.


##### Process
      1. KrBERT와 kobigbird 모델을 사용하여 입력 토큰의 임베딩을 얻음.
      2. out과 out_bird에서 각각 첫 번째 토큰인 [CLS]의 임베딩을 가져옴 (cls_krbert 와 cls_kobigbird)
      3. 두 문장을 구분해주는, 즉 문장의 끝을 나타내는 인덱스(KoBIGBIRD는 3, KrBERT는 2)를 사용하여 comment_vector와 pos_key_vector를 추출 ->평균을 계산하여 벡터의 차원을 줄임.
      4. FCLayer를 사용하여 각 벡터를 적절하게 변환하여 각각의 결과를 cls_embedding, comment_embedding, pos_embedding으로 저장
      5. 4번의 과정을 통해 변환한 임베딩들을 연결(concat_embedding)하여 모델의 입력으로 사용
      6. label_classifier를 통해 최종 분류 결과를 얻음.
