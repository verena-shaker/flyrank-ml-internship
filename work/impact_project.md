 # General AI Fluency - Impact Project

## 1. Portfolio Case Study: ICU Patient Survival Prediction

### Problem
In Intensive Care Units (ICUs), doctors face critical time-sensitive decisions. Identifying high-risk patients early helps prioritize medical attention and optimize resource allocation to save lives.

### What I Did
- **Data Preprocessing & EDA:** Handled missing values systematically (median imputation for numerical features, mode for categorical variables).
- **Feature Selection:** Selected the most relevant features correlated with patient mortality using Mutual Information (MI) and Recursive Feature Elimination (RFE).
- **Handling Class Imbalance:** Evaluated SMOTE (which didn't perform well on this dataset) and successfully addressed severe class imbalance using `scale_pos_weight`.
- **Model Evaluation:** Experimented with multiple machine learning algorithms; **XGBoost** delivered the best predictive performance for survival outcomes.

### What Came of It
Built a reliable risk-stratification ML pipeline that evaluates ICU patient data to provide actionable decision support for medical staff, ensuring critical cases receive immediate focus.

---

## 2. Next Case Study & Reminder Setup
- **Next Project Name:** Google Search Ranking & Discoverability Capstone (FlyRank)
- **Reminder Setup:** Set a Google Calendar nudge to review, summarize, and publish the FlyRank ML project findings into the portfolio using this exact 3-beat framework.
- **Evidence:** `work/reminder.png` (Screenshot of the calendar event attached in repo).

## 3. Preserved AI Context
My AI workspace is pre-configured with my tech stack (Python, Scikit-Learn, XGBoost, Pandas) and structure, enabling seamless generation of future case studies without repeating environment context.
