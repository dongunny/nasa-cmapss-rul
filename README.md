# 🚀 NASA C-MAPSS 터보팬 엔진 예지보전 (Predictive Maintenance) 프로젝트

**Phase 3: 시계열 센서 데이터 기반 잔존 수명(RUL) 예측 딥러닝 모델링**

## 1. 프로젝트 개요
* **프로젝트명:** 항공기 터보팬 엔진 시계열 센서 데이터를 활용한 RUL(Remaining Useful Life) 예측
* **목표:** 센서의 열화(Degradation) 패턴을 학습하여 엔진 고장 시점을 사전에 예측, 유지보수 비용 절감 및 안정성 확보
* **데이터셋:** NASA C-MAPSS (Turbofan Engine Degradation Simulation Data Set) FD001
* **핵심 기술:** Python, TensorFlow/Keras, LSTM (Long Short-Term Memory), Sliding Window

## 2. 문제 정의 및 특징
* **다변량 시계열 (Multivariate Time Series):** 21개의 복잡한 센서 데이터가 시간 흐름(Cycle)에 따라 동시다발적으로 변화.
* **열화 과정 시뮬레이션 (Run-to-Failure):** 정상 상태에서 시작하여 결함이 누적되고 최종적으로 고장(Failure)에 이르는 과정을 추적.
* **목표 변수 변환:** 고장 시점까지 남은 사이클 횟수인 **RUL**을 직접 예측하는 회귀(Regression) 문제.

## 3. 핵심 파이프라인
1. **Data Preprocessing:** 불필요한 고정 센서(분산 0) 제거, Min-Max 스케일링을 통한 다변량 센서 정규화.
2. **Sliding Window:** 2D 시계열 데이터를 딥러닝(LSTM)이 이해할 수 있도록 `(Samples, Time Steps, Features)`의 3차원 텐서로 변환.
3. **Modeling:** 과거 시간축의 맥락을 기억하는 순환 신경망(LSTM) 구조 설계 및 Dropout 적용으로 과적합 방지.
4. **Evaluation:** RMSE(Root Mean Squared Error) 지표를 통해 예측 오차 최소화 검증.

## 4. 최종 성능
* **모델:** 2-Layer LSTM Network
* **결과 (RMSE):** 단순 머신러닝 대비 월등한 시계열 맥락 이해를 바탕으로 최적의 예측 성능 달성. (RUL 수렴 그래프 확인 가능)

## 5. 실행 가이드
본 레포지토리의 `CMAPSS_LSTM_Colab.ipynb` 파일을 Google Colab 환경에 업로드하여 즉시 실행해 보실 수 있습니다.
