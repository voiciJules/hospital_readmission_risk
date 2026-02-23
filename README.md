# 30-Day Hospital Readmission Risk Stratification
#### End-to-End Modeling & Operational Simulation (EDA → ML → Risk Strategy)

## Project Objective
To develop a machine learning–based risk stratification framework for predicting 30-day hospital readmissions and evaluate its operational value for targeted post-discharge interventions.

Rather than focusing solely on binary classification, this project emphasizes risk ranking and resource optimization under realistic healthcare constraints.

## 1. Exploratory Data Analysis (EDA)
### Key Findings
🔹 Class Imbalance
- 30-day readmissions represent a minority of cases (~11%).
- Accuracy alone is misleading.
- Recall-sensitive evaluation and threshold optimization are required.
  
🔹 Age Distribution
- The 20–30 age group shows the highest proportional readmission rate (14.2%), but with smaller sample size.
- Older age groups (70–90) demonstrate consistently high readmission rates with substantially larger populations.
- Operationally, older patients contribute more to total readmission burden.
  
🔹 Length of Stay
- Readmitted patients had slightly longer average stays (4.77 vs 4.35 days).
- Statistically significant (p < 0.001), but small effect size (Cohen’s d = 0.14).
- Indicates limited standalone predictive strength.
  
🔹 Clinical Complexity Indicators
- Higher number of medications and lab procedures observed among readmitted patients.
- Distributions overlap considerably.
- Suggests weak but consistent association with clinical complexity.
- Reinforces need for multivariate modeling.

#### EDA Conclusion
- Individual variables demonstrate modest effects.  
- This supports the use of nonlinear, multivariate machine learning models to capture interactions and complex relationships.

## 2. Modeling Approach
### Models Evaluated
| Model               | ROC-AUC | PR-AUC |
| ------------------- | ------- | ------ |
| Logistic Regression | 0.642   | 0.203  |
| Random Forest       | 0.662   | 0.216  |

#### Conclusion :
- Random Forest demonstrated improved discrimination and better handling of class imbalance.

## 3. Threshold Trade-off Analysis
Default threshold (0.5):
- Recall ≈ 0.6%
- Nearly all high-risk patients missed.
  
Lowering threshold improves recall:  
| Threshold | Recall | Precision |
| --------- | ------ | --------- |
| 0.30      | 4.0%   | 52.3%     |
| 0.25      | 7.5%   | 37.6%     |
| 0.20      | 16.1%  | 28.4%     |
| 0.15      | 35.2%  | 21.2%     |
  
#### Conclusion: 
- The model should not be used as a strict binary classifier.  
- Threshold selection must align with operational capacity.  

## 4. Risk Stratification Performance (Top-K Evaluation)
Rather than threshold-based classification, we evaluated ranking-based performance.  
| Intervention Capacity | Recall |
| --------------------- | ------ |
| Top 5%                | 12.95% |
| Top 10%               | 22.72% |
| Top 15%               | 30.69% |
| Top 20%               | 37.21% |

#### Interpretation 
- Targeting the top 10% highest-risk patients captures ~23% of all readmissions.  
- Random selection would capture only 10%.  
- Model improves targeting efficiency by more than 2×.  

## 5. Operational & Financial Simulation

**Assumptions (conservative scenario):**
- Readmission cost: $15,000
- Intervention cost: $200 per patient
- Intervention success rate: 20%
  
**Results (Top 10% strategy):**
- Patients targeted: 2,035
- Readmissions captured: 516
- Expected prevented readmissions: 103
- Intervention cost: $407,000
- Estimated savings: $1,548,000
- Net projected savings: $1,141,000

## 6. Why This Matters for Hospitals
- Even with moderate predictive accuracy (AUC ≈ 0.66), risk-based prioritization yields meaningful operational value.
  
**Key implications:**
- Improved allocation of transitional care resources
- Reduction in avoidable bed occupancy
- Enhanced quality-of-care performance metrics
- Financial sustainability through targeted intervention
  
The model functions best as a risk stratification tool, not a binary decision engine.

## 7. Key Takeaways
- Individual clinical variables have limited standalone impact.
- Multivariate modeling improves risk discrimination.
- Threshold selection dramatically affects recall.
- Ranking-based deployment maximizes operational value.
- Moderate models can deliver strong strategic benefit when properly deployed.

## 8. Technologies Used
- Python (Pandas, Scikit-learn)
- Random Forest, Logistic Regression
- Statistical Testing (Welch’s t-test, Cohen’s d)
- Risk Segmentation
- Operational Simulation

## 9. Analytical Contributions
This project integrates:  
- Clinical pattern exploration through structured EDA  
- Statistical validation beyond p-values (effect size analysis)  
- Machine learning modeling under class imbalance constraints  
- Threshold-aware decision strategy  
- Risk ranking–based operational prioritization  
- Financial impact simulation under conservative assumptions  