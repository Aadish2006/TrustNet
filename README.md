# 🚀 TrustNet – Twitter/X Bot Detection  

## 📌 Problem Statement  
Social platforms like Twitter (now X) play a crucial role in news, discussions, and civic coordination. However, malicious automated accounts (“bots”) distort reach, spread misinformation, and manipulate public sentiment.  

The challenge: **distinguish bot accounts from genuine human users using openly available metadata** while minimizing false positives (wrongly flagging real users).  

---

## 🔍 Approach  

**Dataset:** Used a Cresci-style benchmark dataset containing labeled bot and genuine accounts.  

**Preprocessing & Cleaning:**  
- Dropped identifiers (usernames, IDs) to prevent leakage.  
- Converted timestamps into `account_age_days`.  
- Normalized language codes & categorical variables.  
- Handled skewed features via `log1p` transform.  

**Feature Engineering:**  
- Ratios like `followers/friends`.  
- Activity velocity (`statuses_per_day`, `favourites_per_day`).  
- Boolean flags for verification, protection, etc.  

**Train/Test Strategy:** Stratified split (80/20) to preserve class balance.  

**Modeling:** Benchmarked classical ML models → Logistic Regression, KNN, Decision Tree, Random Forest, and CatBoost.  

**Evaluation:** Focused on **precision** (avoid false positives) and **recall** (catch most bots).  

---

## 🧠 Algorithms & Models Used  
- **Logistic Regression** → baseline linear model  
- **K-Nearest Neighbors (KNN)** → distance-based local patterns  
- **Decision Tree** → interpretable but prone to overfitting  
- **Random Forest ✅** → best performance with high precision & recall  
- **CatBoost** → robust ensemble, strong candidate for categorical-heavy features  

---

## 📊 Results  
- **Random Forest** achieved **extremely high precision (zero false positives)** and **strong recall**, making it the most reliable model for deployment.  
- Logistic Regression performed surprisingly well given engineered ratios.  
- CatBoost validated ensemble robustness but had limited gain with numeric-dominant features.  

---

## 📚 Key Learnings  
- Feature engineering (ratios, log transforms, derived features) matters more than raw data.  
- Metadata alone can yield strong performance, but it limits generalizability.  
- Handling **imbalanced data** with stratified splits prevents misleading results.  
- High precision is critical to preserve user trust — false positives must be minimized.  

---

## 🔮 Future Improvements  

**Feature Expansion:**  
- Use profile text and tweet embeddings (e.g., miniLM, fastText).  
- Graph/network features (clustering coefficient, reciprocity).  
- Temporal posting patterns & entropy measures.  

**Model Enhancements:**  
- Ensemble stacking (Random Forest + CatBoost + Logistic Regression).  
- LightGBM / XGBoost for additional benchmarking.  

**Deployment:**  
- Build monitoring for concept drift (bot tactics evolve).  
- Add explainability & fairness checks.  

---

## 🛠️ How to Use (Google Colab)  

### 1. Clone Repository  
```bash
!git clone https://github.com/Aadish2006/TrustNet.git
cd TrustNet-Bot-Detection
