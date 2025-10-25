## 🛒 이커머스 고객 이탈 예측 Project Portfolio (정민영)

🗓️ 기간: 2025.06.04 ~ 2025.06.05 (2일)
🙋 팀명: 원조1호 이커머스 컨설턴트

### ✨ 한 줄 요약
고객 행동 데이터를 기반으로 이탈 확률을 예측하고, RFM+KMeans로 고객 페르소나를 도출해 클러스터별 마케팅 전략을 자동 제안하는 Streamlit 대시보드.

### 🔗 시연영상: https://youtu.be/ykYhSbUtJSw?si=5VuTGHW617vJAUPm

### 🙋 역할(정민영)
- 머신러닝 모델 학습·평가 파이프라인 구축, 임계값/하이퍼파라미터 최적화로 최종 모델 선정
- Streamlit 대시보드 개발(모델 비교, 이탈 예측, 클러스터 분석 시각화)
- Gemini API 연동으로 클러스터별 마케팅 전략 자동 생성

### 🔍 핵심 성과
- 최종 선정 모델(GradientBoosting, threshold=0.1375): Accuracy 0.9938, Positive Recall 1.0000, Precision(1) 0.9645, F1(1) 0.9819
- RFM(Recency, Frequency, Monetary) 기반 KMeans k=6 세그먼트 도출 및 페르소나·전략 정의
- 대시보드에서 이탈 고위험 고객 추출/다운로드 및 클러스터별 전략 자동 제안 지원

---

## 1) 데이터와 핵심 EDA 인사이트(요약)
- 이탈률 약 17% 수준 → 집중 관리 대상 존재
- 만족도 낮을수록 이탈률 급등(t-test 유의) → CS/경험 개선이 핵심
- 불만 제기 고객 이탈률 2배 이상(카이제곱 유의) → 불만 고객 케어 우선
- 마지막 주문 이후 경과일↑일수록 이탈↑(t-test 유의) → 재방문 유도 필요

![graph1.PNG](img/graph1.PNG)

![graph2.PNG](img/graph2.PNG)

---

## 2) 모델링: 후보 비교와 최종 선정
- 후보 모델: XGBoost, GradientBoosting, RandomForest, HistGradientBoosting, Stacking, Voting, LGBM, KNN, SVC
- 공통 전처리/스케일링 후 Test셋 성능 비교(Accuracy/Recall/Precision/F1) + 임계값(threshold) 튜닝 병행

### 최종 모델: GradientBoosting(+threshold=0.1375)
- Positive Recall을 1.0000으로 확보하여 이탈 고객 미스 최소화, 동시에 Accuracy 0.9938 달성
- 요약 지표(클래스 1): Precision 0.9645, Recall 1.0000, F1 0.9819

![st6.PNG](img/st6.PNG)

---

## 3) 클러스터링 기반 고객 세분화: KMeans(k=6) + 페르소나/전략
- 특징: RFM(`DaySinceLastOrder`→recency, `OrderCount`→frequency, `CashbackAmount`→monetary) 표준화 후 KMeans
- 클러스터별 평균 R/F/M과 이탈 확률을 요약하고 페르소나·전략을 매핑

| 클러스터 | 페르소나(요약) | 예시 전략 |
|---|---|---|
| 0 | 최근 방문·저빈도·중하 지출, 이탈 고위험 | 즉시 리텐션 쿠폰/푸시, 후속 액션 자동화 |
| 1 | 장기 비활성, 저지출 | 리마인드/리타겟팅, 휴면 복귀 혜택 |
| 2 | 단발성 고지출 | VIP 첫구매 리텐션, 프리미엄 리마케팅 |
| 3 | 핵심 로열, 높은 빈도/지출 | 멤버십/독점 프로모션, 리뷰 요청 |
| 4 | 오래됐지만 고지출 | VIP 리턴 캠페인, 감사/혜택 리마인드 |
| 5 | 중간 활동/소비 | 이탈 방지형 개인화 프로모션 |

대시보드 캡처: ![Cluster](img/st8.PNG)

---

## 4) 전략 자동화(Gemini)와 대시보드
- 클러스터별 평균 특성(R/F/M, 이탈확률)을 입력해 Gemini가 바로 실행 가능한 마케팅 문구/전략을 자동 생성
- 고위험 고객 리스트를 클러스터별로 필터링·CSV 다운로드 지원 → 운영 즉시 활용 가능  
캡처: ![Gemini](img/st12.PNG)

---

## 5) 화면 스냅샷
![Home](img/st2.PNG) ![EDA](img/st5.PNG)  
![Model](img/st7.PNG) ![Cluster](img/st9.PNG)  
![Gemini](img/st13.PNG)



---

## 부록(데이터/ERD 캡처)
![Dataset](img/dataset.PNG) ![ERD](img/erd.PNG)

> 전체 깃허브 링크: https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN14-2nd-3Team