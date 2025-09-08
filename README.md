## Causal Inference Analysis

Our goal was to estimate whether completing more projects **causally increases** the number of job offers students receive.  
We implemented multiple causal inference approaches, carefully diagnosing assumptions at each step.

---

### Step 1: DAG Modeling
- Constructed a Directed Acyclic Graph (DAG) with:  
  - **Treatment:** Projects_Completed  
  - **Outcome:** Job_Offers  
  - **Confounders:** Internships_Completed, Networking_Score, Soft_Skills_Score  
- Applied the backdoor criterion and confirmed identifiability of the treatment effect.  
- Initial regression suggested a positive causal effect, but we moved beyond regression to test robustness.  

<img width="1042" height="753" alt="image" src="https://github.com/user-attachments/assets/c8c672c6-b9d5-4c80-ac7e-69159d70e47b" />

---

### Step 2: Propensity Score Matching (Quartile Split) – *Failed*
- Attempted quartile split (≤5 projects vs ≥8 projects).  
- **Result:** Propensity score distributions had no overlap (controls ≤0.11, treated ≥0.92).  
- After trimming, **zero controls remained** → matching not defensible.  

<img width="898" height="717" alt="image" src="https://github.com/user-attachments/assets/603226d1-9cc2-46aa-aa01-def9ef91db84" />


**Takeaway:** Demonstrates the importance of overlap checks before reporting causal estimates.

---

### Step 3: Inverse Probability of Treatment Weighting (Median Split) – *Partial Success*
- Redefined treatment using a median split (≥6 projects vs <6).  
- Applied stabilized IPTW with trimming.  
- **Diagnostics:** Balance improved but remained poor (SMD ≈ 1.6–2.0 > 0.1).  
- **Result:** Estimated ATE ≈ **1.68 job offers** (p < 0.001, 95% CI [1.51, 1.85]).

**Caution:** Large effect likely overstated due to residual imbalance.

---

### Step 4: Overlap Weights (ATO) – *Final & Robust*
To address imbalance, we applied **Overlap Weights**, which target the region of common support.  
We compared three propensity models:

- **Logistic (baseline):** ATO = 0.180, poor balance (max|SMD|=0.55).  
- **Polynomial Logistic (deg 2):** ATO = 0.026, good balance (max|SMD|=0.08).  
- **Gradient Boosting:** ATO = 0.023, excellent balance (max|SMD|=0.02).  

<img width="1243" height="612" alt="image" src="https://github.com/user-attachments/assets/e98a0d26-f393-4a4f-868f-04328f734770" />

**Final takeaway:**  
- With flexible propensity models, balance was achieved and the effect shrank to near zero.
- IPTW reduced imbalance slightly but remained above the |SMD| < 0.10 threshold across covariates.
- Overlap weights achieved near-zero SMDs (especially with flexible PS), indicating excellent balance and a more credible estimate.
  
- **Conclusion:** Once confounding is properly addressed, there is **no statistically significant causal effect** of project completion on job offers in the overlap population.  

<img width="1572" height="688" alt="image" src="https://github.com/user-attachments/assets/8b248cea-a635-4397-8823-6e738d5ecad7" />

---

### Trade-offs and Limitations
- **PSM (Quartile Split):** intuitive but requires strong overlap — failed in our data.  
- **IPTW:** simple and interpretable but sensitive to extreme weights and poor balance.  
- **Overlap Weights:** more robust to limited overlap, but results apply only to the *overlap population* (students with moderate likelihood of treatment).  
- **Propensity Model Choice:** naive logistic overstated effects; flexible models (polynomial, gradient boosting) achieved balance but revealed null effects.   

---

### Why This Matters
- **Diagnostic rigor:** Showed when methods fail (PSM, IPTW) and why.  
- **Robust modeling:** Iterated through flexible PS models until balance was credible.  
- **Practical insight:** Naive models overstated effects, while robust overlap weighting revealed a null effect.  
