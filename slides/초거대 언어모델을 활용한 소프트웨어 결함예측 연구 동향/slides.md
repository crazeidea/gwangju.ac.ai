---
marp: true
theme: default
paginate: true
---

# 대규모 언어 모델을 이용한 소프트웨어 결함 예측

## 류덕산 | 전북대학교

### 최강훈

---

# 소프트웨어 결함 예측 (Software Defect Prediction, SDP)

- 소프트웨어 품질과 관련된 정량적 데이터를 분석하여, 결함이 발생할 가능성이 높은 소프트웨어 개체를 식별, 품질 보증 활동 (코드리뷰, 테스팅 등)이 집중되도록 가이드

---

# 소프트웨어 결함 예측의 정량적 데이터

- Code Metrics
  - 함수 내 분기문의 개수
  - 함수 내 조건문의 최대 중첩 깊이
  - 함수의 매개번수의 개수
- 결함 보고서
- 테스트 결과
- 개발자 간의 수신/발신 메시지
- Commit 내역

---

1. 소프트웨어 산출물 (소스코드)로부터 소프트웨어 척도와 결함/비결함 라벨 또는 결함의 개수를 추출
2. 데이터 정규화, 특징 선택, 노이즈 제거
3. 분류 모델은 결함/비결함을 예측, 회귀 모델은 결함의 수를 예측
   ![bg right width:100% ](image.png)

---

# SDP 기술의 진화

1. 전통적인 기계 학습
   - 로지스틱 회귀, SVM, 랜덤 포레스트
2. 딥 러닝
   - CNN, DNN, DBN, LSTM
3. 대규모 언어 모델(LLM)
   - CodeBERT, GraphCodeBERT, UniXCoder, CodeT5+

---

![bg width:95%](image-1.png)

---

# 소프트웨어 공학에서의 LLM

- 코드 생성
- 테스트 케이스 생성
- 코드 요약
- 취약점 수정

---

![bg width: 95%](image-2.png)

---

# 소프트웨어 결함 예측과 LLM
## 소프트웨어 결함 예측에 LLM의 적용 가능성 <sup>[1]</sup>

- 소프트웨어 결함 예측의 데이터는 정형화된 데이터
- BERT, GPT-2 등의 LLM을 활용한 이상탐지를 진행한 결과 효과적인 결과를 보임

<!-- _footer: '[1] 이정화, 주은정, 류덕산 (2024). 소프트웨어 결함 예측
에서의 LLM 적용 가능성에 대한 고찰, 2024 한국컴퓨
터종합학술대회 (Korea Computer Congress 2024)' -->
---

## 매개변수 효율적 미세조정 <sup>[2]</sup>
- 전체 매개변수에 대하여 Fine-Tuning을 진행하는 것이 아닌, 일부 매개변수에 대하여 Fine-Tuning을 진행하는 방법
   -  적은 수의 매개변수를 학습하는것 만으로도 모델 전체를 Fine-Tuning 하는 것과 비슷한 성능을 보임
- 코드 변경 학습에서 매개변수 효율적 미세조정 <sub>(Parameter Efficient Fine-Tuning, PEFT)</sub>기법이 전체모델 미세조정 <sub>(Full-Model Fine Tuning, FMFT)</sub>보다 더 적은 계산 비용으로 더 나은 성능을 제공할 수 있음을 확인.

<!-- _footer: '[2] Wang, C., Yang, Y., Gao, C., Peng, Y., Zhang, H., & Lyu, 
M. R. (2023). Prompt tuning in code intelligence: An 
experimental evaluation. IEEE Transactions on Software 
Engineering.' -->

---

## 프롬프트 조정의 효과 <sup>[3]</sup>
- 모델의 미세 조정은 입력하는 데이터의 양에 크게 좌우되지만, 일반적으로 데이터는 항상 부족함
- 프롬프트 조정은 프롬프트에 작업별 지식을 제공하여 데이터 부족 문제를 완화 
- 프롬프트 조정이 미세조정보다 성능이 우수함을 보임

<!-- _footer: '[3] ng, C., Sun, Y., Li, K., Zhou, P., Lv, J., & Lu, A. (2024). 
Genetic  Auto-prompt  Learning  for  Pre-trained  Code 
Intelligence  Language  Models.  arXiv  preprint 
arXiv:2403.13588' -->

---

## 유전적 자동 프롬프트 (Genetic Auto-Prompt, GenAP) <sup>[4]</sup>
- 사용자의 입력에 따라 프롬프트를 생성하는 모델 <sub>(CodeBERT)</sub>이 생성한 프롬프트를, 결함 예측 모델의 입력으로 사용
- 수동으로 디자인한 프롬프트에 비해 우수한 성능을 보임

<!-- _footer: '[4] ng, C., Sun, Y., Li, K., Zhou, P., Lv, J., & Lu, A. (2024). 
Genetic  Auto-prompt  Learning  for  Pre-trained  Code 
Intelligence  Language  Models.  arXiv  preprint 
arXiv:2403.13588' -->

---

# 미래 연구 방향

- 결함 예측을 위한 프롬프트 엔지니어링
- 다양한 데이터 소스 활용
  - 코드 자체, 코드 척도, 주석, 내부 구조 정보등의 추가 데이터 활용
- 계산 비용 절감
- 새로운 LLM 출력 결과 적용
- 데이터 부족 문제 해결
  - 프롬프트 조정의 적극적 활용
- 정형데이터에 적합한 LLM 모델 개발 및 사용

---

# 결론

- LLM은 SDP에서 유망한 결과를 보여줌
   - 소프트웨어 품질 보증을 크게 향상시킬 잠재력 보유
- 효과성과 효율성 향상을 위한 지속적인 연구
