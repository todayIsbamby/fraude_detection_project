# fraude_detection_project

A machine learning project focused on fraud detection using production-style transactional data, highlighting real-world challenges such as class imbalance and evaluation trade-offs.

---

## 1. Dataset Overview

This project focuses on building a machine learning model for **fraud detection in transaction data**.

The dataset was extracted from a production-like transactional system using **SQL Server stored procedures**, ensuring consistency and reproducibility of labels.

Each row represents a single transaction, enriched with **transactional, temporal, and operational attributes** that are available prior to fraud confirmation.

**Key focus:**  
Understanding data distribution, evaluation pitfalls, and trade-offs in fraud detection.

---

## 2. Target Variable (Label)

### `fraud_result`

Binary target variable:

- **0** = Non-fraud  
- **1** = Fraud  

The label is **pre-generated at the database level** using a stored procedure based on predefined business rules and historical fraud logic.

In the notebook, `.astype(int)` is used solely for **type conversion** and does not alter the label definition.

> **Important note:**  
> The model does not infer fraud labels heuristically during training; instead, it learns patterns from an already curated and governed fraud label.

---

## 3. Feature Description and Availability

### Key Features Used

- **amount** – Transaction amount  
- **confirm_date_hour** – Hour at which the transaction was confirmed  
- **create_date_of_merchant** – Merchant creation timestamp  
- **transaction_count** – Historical transaction frequency  
- **channel** – Transaction channel  
- **status** – Transaction execution status  

All features are available **prior to fraud confirmation**, ensuring temporal consistency.

---

## 4. Class Imbalance Challenge

A key characteristic—and limitation—of this dataset is **severe class imbalance**.

- Fraudulent transactions represent only a **small fraction** of total observations  
- This mirrors real-world financial systems, where fraud is rare by nature  

### Impact on Model Performance

As a result:

- Overall accuracy appears high  
- Precision for fraud cases is high  
- Recall for fraud cases is low  

This indicates that the model is **conservative** and tends to favor non-fraud predictions, a common issue in imbalanced classification problems.

---

## 5. Evaluation Interpretation

Accuracy alone is **not sufficient** for evaluating fraud detection performance.

### Key Observations

- High True Negative rate  
- Low False Positive rate  
- High False Negative rate for fraud cases  

This behavior is expected given:

- Imbalanced data distribution  
- Optimization toward overall accuracy rather than fraud recall  

---

## 6. Limitations and Considerations

- The model primarily learns patterns aligned with **existing rule-based fraud logic**  
- Performance may degrade if business rules or fraud patterns change  
- Class imbalance limits the model’s ability to detect rare fraud events without additional techniques  

---

## 7. Future Improvements

Potential enhancements include:

- Applying resampling techniques (e.g. SMOTE, undersampling)  
- Using class-weighted loss functions  
- Optimizing for **Recall, F1-score, or PR-AUC** instead of Accuracy  
- Training alternative models that exclude rule-dependent features to improve generalization  

---

## 8. Summary

This project demonstrates a realistic fraud detection workflow using **production-style data with governed labels**.

While the dataset is highly imbalanced, it accurately reflects real-world constraints and highlights the challenges of detecting **rare fraudulent behavior** using supervised learning.
