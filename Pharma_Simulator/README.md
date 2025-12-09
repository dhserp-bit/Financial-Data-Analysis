# 💊 약가 제도 개편에 따른 제약사 손익 민감도 분석

## 📌 Project Overview
정부의 **'약가 제도 개선안(복제약 가격 인하)'**이 국내 주요 제약사의 재무 건전성에 미치는 영향을 정량적으로 분석한 스트레스 테스트(Stress Test) 모델입니다.

단순한 과거 데이터 조회가 아닌, **DART Open API**를 활용하여 **2025년 3분기 최신 누적 실적**을 실시간으로 수집하고, 재무제표 주석(Footnote)을 심층 분석하여 기업별 리스크 노출도(Risk Exposure)를 정교하게 산출했습니다.

## 🎯 Key Objectives
1.  **Automated Data Collection:** DART API를 활용해 2025년 3분기 누적(Cumulative) 재무 데이터 자동 추출.
2.  **Hybrid Analysis:** API로 확인 어려운 '제품/상품 매출 비중' 및 '내수 비중'은 사업보고서 주석을 교차 검증(Cross-check)하여 반영.
3.  **Financial Stress Test:** 약가 15% 일괄 인하 시나리오 적용 시, **영업이익 증발(Profit Erosion)** 및 **적자 전환(Turn to Red)** 가능성 진단.

## 🛠 Tech Stack
-   **Language:** Python 3.x
-   **Data Collection:** `dart-fss` (Open DART API Wrapper)
-   **Data Analysis:** `pandas` (Dataframe manipulation)
-   **Visualization:** `matplotlib`, `seaborn` (Impact Simulation Charting)

## 📊 Analysis Logic (Methodology)
본 프로젝트는 **'내수 시장'**에서 판매되는 **'자체 생산 제품(제네릭 포함)'**만이 약가 인하의 직접적 타깃이 된다는 점에 착안하여 아래와 같은 로직을 수립했습니다.

### 1. Data Pipeline
* **Quantitative Data (API):** 매출액, 영업이익 (2025 3Q Cumulative)
* **Qualitative Data (Manual):**
    * 제품(Product) vs 상품(Merchandise) 비중
    * 내수(Domestic) vs 수출(Export) 비중
    * R&D 비용 규모

### 2. Stress Test Formula
$$\text{Revenue Loss} = \text{Total Revenue} \times \text{Product Ratio} \times \text{Domestic Ratio} \times \text{Price Cut Rate (15\%)}$$

$$\text{New Operating Profit} = \text{Current OP} - \text{Revenue Loss}$$

## 📉 Key Findings (Based on 2025 3Q Data)

### 🚨 1. 유한양행 (Yuhan Corp.) : Risk of "Turn to Red"
* **Data Fact:** 통념과 달리 2025년 3분기 기준 **제품 매출 비중(48.5%)**이 상품 매출을 상회함을 주석 분석을 통해 발견.
* **Simulation Result:** 기술료 수익 감소로 영업이익률(OPM)이 4.8%로 낮아진 상황에서 약가 인하 충격(-947억 원) 발생 시, **영업이익 적자 전환(-164억 원)** 위험이 포착됨.

### 📉 2. 한미약품 (Hanmi Pharm.) : Extreme Profit Erosion
* **Data Fact:** 자체 제품 비중이 **97.8%**에 달해 규제 민감도가 극도로 높음.
* **Simulation Result:** 약가 인하 시 매출 감소분이 **기존 영업이익의 약 90%를 잠식**하며, 이에 따라 **R&D 비용 부담률이 15.2% → 17.6%로 급증**하여 미래 성장 동력 저하 우려.

## 📈 Visualizations
*(GitHub 렌더링 이슈 발생 시 [NBViewer](https://nbviewer.org/)를 통해 확인해주세요.)*

![Profit Impact Chart](results/profit_impact_chart.png)
*Figure 1. 약가 인하 시나리오별 영업이익 변화 (유한양행 적자전환 위험)*

![RnD Burden Chart](results/rnd_burden_chart.png)
*Figure 2. 매출 감소에 따른 R&D 비용 부담률 증가*

## 🚀 How to Run

### Prerequisites
* Python 3.8+
* DART API Key ([Get Key Here](https://opendart.fss.or.kr/))

### Installation
```bash
pip install dart-fss pandas matplotlib seaborn
