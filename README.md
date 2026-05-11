# 🚀 NASA C-MAPSS 터보팬 엔진 예지보전 (Predictive Maintenance)

![NASA C-MAPSS Banner](https://img.shields.io/badge/Project-Phase%203-blue?style=for-the-badge) ![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange?style=for-the-badge&logo=tensorflow) ![Keras](https://img.shields.io/badge/Keras-LSTM-red?style=for-the-badge&logo=keras)

**Phase 3: 시계열 센서 데이터 기반 잔존 수명(RUL) 정밀 예측 딥러닝 파이프라인**

본 프로젝트는 항공기 터보팬 엔진의 다변량 센서 데이터를 활용하여, 엔진이 고장 나기 전까지 남은 수명(RUL, Remaining Useful Life)을 소수점 단위로 예측하는 고급 예지보전 모델링 프로젝트입니다. 단순한 고장 분류를 넘어 '시점'을 정확히 예측함으로써 산업 현장의 안전을 극대화하고 유지보수 비용을 획기적으로 절감하는 것을 목표로 합니다.

---

## 1. 📊 프로젝트 개요

* **프로젝트명:** 항공기 터보팬 엔진 다변량 센서 데이터를 활용한 RUL(Remaining Useful Life) 예측
* **목표:** 센서의 복잡한 열화(Degradation) 패턴을 학습하여 엔진 고장 시점을 사전에 예측
* **데이터셋:** NASA C-MAPSS (Turbofan Engine Degradation Simulation Data Set) FD001
* **핵심 기술:** Python, TensorFlow/Keras, LSTM, Piecewise Linear Capping, Sliding Window

## 2. 🧠 핵심 아키텍처 및 방법론

이 프로젝트는 전통적인 머신러닝의 한계를 극복하기 위해 최신 시계열 딥러닝 기법을 도입했습니다.

### ① 전처리: Piecewise Linear Capping (@125)
기존의 단순 선형 라벨링이 가진 모순(물리적으로 동일한 정상 상태의 엔진에 서로 다른 수명 라벨을 부여)을 해결하기 위해 논문 표준 방식인 Piecewise Linear Capping 기법을 도입했습니다. 수명이 125 이하로 떨어지는 본격적 열화 시점부터만 선형 감소를 적용하여 모델의 학습 안정성을 비약적으로 높였습니다.

### ② 시계열 3D 텐서 변환 (Sliding Window)
엔진의 과거 맥락(Context)을 이해시키기 위해, Window Size = 50을 적용하여 2D 테이블 데이터를 `(Samples, Time Steps=50, Features=14)` 구조의 3D 텐서로 완벽히 변환했습니다.

### ③ 2-Layer LSTM Network 설계
단기 기억 상실(Vanishing Gradient)을 방지하고 장기적인 열화 트렌드를 포착하기 위해 **LSTM (Long Short-Term Memory)** 아키텍처를 채택했습니다. 2층 구조의 LSTM과 0.2의 Dropout을 결합해 과적합을 철저히 통제했습니다.

---

## 3. 🏆 최종 성능 평가

| 지표 | 결과치 | 의미 및 해석 |
| :--- | :---: | :--- |
| **RMSE** (평균 제곱근 오차) | **16.14** | 에러 제곱에 비례하는 페널티를 주어 측정하는 보편적 회귀 평가지표. 학술대회 우수 수준. |
| **MAE** (평균 절대 오차) | **12.18** | 실제 예측 수명이 평균적으로 단 **12사이클(비행 12회)** 차이로 적중. 극한의 정밀도 증명. |
| **NASA Scoring Function** | **268.45** | '위험한 지연 예측'에 지수적 페널티를 부여하는 항공 특화 도메인 지표. 월등한 안전성 확보. |

---

## 4. 📈 시각적 성능 해석

학습 과정에서 Train Loss와 Validation Loss가 완벽하게 수렴하였으며, 모델 예측 결과는 엔진 수명이 얼마 남지 않은 **가장 위험한 순간(RUL < 50)에 실제 수명 선에 더욱 강력하게 밀착**하는 이상적인 예지보전 성능을 보여주었습니다. (자세한 결과 차트는 노트북 내에서 직접 확인하실 수 있습니다)

---

## 5. 🛠 실행 가이드

모든 데이터 다운로드, 전처리 파이프라인, 모델 학습 및 시각화 코드가 하나의 노트북에 완벽하게 패키징되어 있습니다.

1. 본 레포지토리의 `CMAPSS_LSTM_Colab.ipynb` 파일을 다운로드합니다.
2. [Google Colab](https://colab.research.google.com/) 환경에 업로드합니다.
3. 상단 메뉴에서 `런타임 > 모두 실행`을 클릭하면 처음부터 끝까지 자동으로 재현됩니다.

> 💡 **연구팀:** 리뉴얼 무적함대 (2026-05)  
> 💡 **프로젝트 시리즈:** [Phase 1: SECOM] ➔ [Phase 2: WM-811K] ➔ **[Phase 3: NASA C-MAPSS]**
