# Hybrid Nanofluid PV/T System – Machine Learning Performance Prediction

[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![CatBoost](https://img.shields.io/badge/CatBoost-optimized-green)](https://catboost.ai/)
[![XGBoost](https://img.shields.io/badge/XGBoost-optimized-orange)](https://xgboost.readthedocs.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 📌 Overview

This repository contains machine learning models for predicting the **thermal and electrical performance** of photovoltaic thermal (PV/T) solar modules cooled by **hybrid nanofluids**:

- Al₂O₃-Cu
- TiO₂-SiO₂
- Al₂O₃-SiO₂
- Graphene-Al₂O₃

We use **CatBoost** and **XGBoost** with **Particle Swarm Optimization (PSO)** for hyperparameter tuning, achieving **R² > 0.9999** on physics-based synthetic data.

---

## 🔬 Key Features

- ✅ **Synthetic data generation** using heat transfer & fluid dynamics equations (Brinkman, Maxwell, Gnielinski)
- ✅ **Multi-output regression** for 7 performance metrics
- ✅ **PSO hyperparameter optimization** for CatBoost & XGBoost
- ✅ **Model saving & deployment** ready (`.cbm` files)
- ✅ **Comprehensive evaluation** (R², MAE, RMSE, feature importance plots)

---

## 📊 Performance Metrics Predicted

| Target | Description | Unit | Range |
|--------|-------------|------|-------|
| `u_avg` | Average fluid velocity | m/s | 0.15 – 0.90 |
| `pressure_drop` | Pressure drop across channel | Pa | 50 – 500 |
| `T_out` | Outlet temperature | K | 300 – 340 |
| `T_cell` | PV cell temperature | K | 298 – 350 |
| `Nu` | Nusselt number | – | 10 – 200 |
| `eta_th` | Thermal efficiency | % | 10 – 95 |
| `eta_el` | Electrical efficiency | % | 8 – 22 |

---

## 🚀 Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/Samuel-33-sys/hybrid-nanofluid-pvt-ml.git
cd hybrid-nanofluid-pvt-ml
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Generate Synthetic Dataset
```bash
python src/data_generation.py --dataset Al2O3_Cu --samples 5000
```

### 4. Train CatBoost with PSO
```bash
python src/catboost_trainer.py --data data/pvt_nanofluid_AL203_CU_data.csv
```

### 5. Train XGBoost with PSO
```bash
python src/xgboost_trainer.py --data data/pvt_nanofluid_AL203_CU_data.csv
```

### 6. Evaluate Models
```bash
python src/evaluate_models.py --models_dir models/catboost_models/
```

---

## 🧠 Model Performance (Test Set)

| Target | R² (CatBoost) | MAE | RMSE |
|--------|--------------|-----|------|
| `u_avg` | 0.99998 | 1.2×10⁻⁴ | 1.6×10⁻⁴ |
| `pressure_drop` | 0.999997 | 1.2 Pa | 1.6 Pa |
| `T_out` | 0.99996 | 0.08 K | 0.10 K |
| `T_cell` | 0.99997 | 0.09 K | 0.11 K |
| `Nu` | 0.99996 | 0.03 | 0.05 |
| `eta_th` | 0.99997 | 0.04% | 0.06% |
| `eta_el` | 0.99997 | 0.01% | 0.02% |

---

## 📈 Example Usage (Python)

```python
from catboost import CatBoostRegressor
import numpy as np

# Load pre-trained model
model = CatBoostRegressor()
model.load_model('models/catboost_eta_th.cbm')

# Predict thermal efficiency for φ_total=1.5%, x_Al2O3=0.6
# Input: [phi_total, x_Al2O3]
X_new = np.array([[0.015, 0.6]])
prediction = model.predict(X_new)[0]
print(f"Predicted Thermal Efficiency: {prediction:.2f}%")
```

---

## 📁 Repository Structure

```
hybrid-nanofluid-pvt-ml/
│
├── data/                          # Dataset CSV files
│   ├── pvt_nanofluid_AL203_CU_data.csv
│   ├── pvt_nanofluid_TiO2_SiO2_data.csv
│   ├── pvt_nanofluid_AL203_SiO2_data.csv
│   └── pvt_nanofluid_Graphene_Al2O3_data.csv
│
├── notebooks/                     # Jupyter notebooks
│   ├── 01_data_generation.ipynb
│   ├── 02_eda_visualization.ipynb
│   └── 03_model_training_evaluation.ipynb
│
├── src/                           # Python source code
│   ├── data_generation.py         # Physics-based synthetic data
│   ├── catboost_trainer.py        # CatBoost + PSO training
│   ├── xgboost_trainer.py         # XGBoost + PSO training
│   ├── evaluate_models.py         # Metrics & visualizations
│   └── utils.py                   # Shared helper functions
│
├── models/                        # Trained model files (.cbm)
├── results/                       # Outputs
│   ├── metrics/                   # CSV metric summaries
│   └── plots/                     # Feature importance, parity plots
│
├── docs/                          # Documentation
│   ├── methodology.md
│   └── project_report.md
│
├── requirements.txt
├── .gitignore
├── LICENSE
└── README.md
```

---

## 📚 Physical Models Used

| Property | Correlation |
|----------|------------|
| Dynamic viscosity | Brinkman model |
| Thermal conductivity | Maxwell model |
| Heat transfer coefficient | Gnielinski correlation |
| Nusselt number | Dittus-Boelter equation |
| Electrical efficiency | Linear temperature model |

---

## 📄 License

This project is licensed under the **MIT License** – see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- Physical models based on Brinkman, Maxwell, and Gnielinski correlations
- [CatBoost](https://catboost.ai/) and [XGBoost](https://xgboost.readthedocs.io/) libraries
- Inspired by experimental PV/T solar collector research

---

## 📧 Contact  
**Project Link:** https://github.com/Samuel-33-sys/hybrid-nanofluid-pvt-ml
