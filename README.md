# End-to-End Supervised Credit Card Fraud Detection

This repository contains a comprehensive, production-ready machine learning solution for detecting fraudulent credit card transactions. The project demonstrates the complete data science lifecycle: from rigorous data cleaning and advanced feature engineering to model selection, final evaluation on out-of-time data, and a detailed financial impact analysis to guide business strategy.

The final **CatBoost** model developed in this project successfully identifies **60% of fraudulent transactions** by reviewing only the top 3% of riskiest transactions, translating to an estimated **$53 million in annual fraud savings**.

-----

## Project Workflow & Key Stages

This project was executed in a structured, multi-stage process to ensure the final model is not only statistically robust but also operationally viable and financially beneficial.

-----

### **1. Data Cleaning & Preparation**

The initial dataset of nearly 100,000 transactions required extensive cleaning to prepare it for modeling. This critical first step involved:

  * **Outlier & Irrelevance Filtering**: Removed non-purchase transactions and unrealistic outliers (e.g., amounts \> $3M) to focus the analysis on relevant purchase data.
  * **Intelligent Imputation**: Systematically handled missing merchant information (`Merchnum`, `state`, `zip`) by creating mappings from related fields (e.g., inferring a merchant's state from its ZIP code) and assigning logical placeholders like 'unknown' or 'foreign' where appropriate. This approach preserved valuable data records that would otherwise be discarded.

-----

### **2. Advanced Feature Engineering**

Over **2,000 candidate features** were engineered to transform raw transactional data into powerful predictive signals. The goal was to capture complex behavioral and temporal patterns that distinguish fraudulent activity from legitimate spending.

  * ]**Velocity & Aggregation Features**: Created extensive features capturing transaction counts and amount statistics (average, max, total) over multiple rolling time windows (1, 3, 7, 14, 30, and 60 days). These were computed for various entities and their interactions, such as:
      * Card-level history (`Cardnum`)
      * Merchant-level history (`Merchnum`)
      * Card-Merchant interaction history
      * Geographic patterns (Card-State, Card-ZIP)
  * **Target Encoding**: Converted high-cardinality categorical variables (e.g., `Merch state`, `Merch zip`) into numerical risk indicators using a smoothed, out-of-fold target encoding strategy to prevent data leakage.
  * **Specialized Features**: Incorporated forensic and anomaly-based features, including **Benford's Law** deviations, distance-based metrics between sequential transactions, and unsupervised anomaly scores.

-----

### **3. Rigorous Feature Selection**

To combat the curse of dimensionality and prevent overfitting, a systematic feature selection process was employed.

  * **Hybrid Approach**: A combination of filter methods (using information value) and wrapper methods was used.
  * **Backward Elimination**: Multiple trials were conducted with models like LightGBM and CatBoost. The most effective strategy was a **backward elimination** process starting with 200 features, which identified a robust and diverse final set of approximately **20 features** that maximized performance while ensuring model parsimony.

-----

### **4. Model Exploration & Selection**

A wide array of algorithms was evaluated to identify the optimal modeling technique for this specific problem. The candidate models included:

  * **Baselines**: Logistic Regression, Decision Tree, and k-Nearest Neighbors.
  * **Advanced Ensembles**: **LightGBM**, **XGBoost**, and **CatBoost**.
  * **Neural Networks**: A multi-layer perceptron.

The gradient boosting models significantly outperformed the baselines. **CatBoost** emerged as the top-performing model, demonstrating a slight edge in performance on the crucial **out-of-time (OOT) validation set**, likely due to its sophisticated handling of categorical features.

-----

### **5. Financial Analysis & Business Recommendation**

A model's statistical performance is only valuable if it translates to a positive business impact. A thorough financial analysis was conducted to determine the optimal operational strategy.

  * **Cost-Benefit Analysis**: A model was built to quantify **fraud savings** (prevented losses) against **review costs** (operational expense of investigating flagged transactions).
  * **Optimal Cutoff Recommendation**: The analysis revealed that while net savings are maximized at a 10-12% review rate, this is operationally infeasible. A final recommendation was made to set the score cutoff to flag approximately **5% of transactions** for review.
  * **Projected Impact**: This recommended threshold creates a strategic balance between maximizing fraud capture and respecting operational constraints, delivering an estimated **$53 million in net annual savings**.

-----

## Key Skills & Technical Competencies

This project provides a comprehensive demonstration of skills in machine learning, data engineering, and business analytics.

  * **End-to-End Machine Learning**: Complete lifecycle management from data ingestion and cleaning to model deployment and financial reporting.
  * **Advanced Feature Engineering**: Expertise in creating high-quality, predictive features, including velocity checks, behavioral aggregations, and target encoding.
  * **Model Selection & Tuning**: Proficient in evaluating, selecting, and tuning a wide range of machine learning models, with deep experience in gradient boosting frameworks (**CatBoost**, **XGBoost**, **LightGBM**).
  * **Robust Model Validation**: Strong understanding of the importance of **out-of-time validation** to ensure model generalization and stability in a real-world, dynamic environment.
  * **Financial & Business Acumen**: Ability to translate model performance into tangible business metrics (cost, savings, ROI) and provide data-driven strategic recommendations.
  * **Python Data Science Stack**: Mastery of **Pandas**, **NumPy**, **Scikit-learn**, and visualization libraries like **Matplotlib** and **Seaborn**.
