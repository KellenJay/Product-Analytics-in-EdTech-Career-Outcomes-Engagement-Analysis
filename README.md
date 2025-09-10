# Causal Inference Analysis: Do Projects Lead to More Job Offers?

This repository explores whether completing more projects causally increases students’ job offers.  
We apply multiple causal inference frameworks, diagnosing assumptions at each step, and finish with business-ready insights.


## Step 1: DAG Modeling

Constructed a Directed Acyclic Graph (DAG) to formalize assumptions.

- **Treatment (X):** `Projects_Completed`  
- **Outcome (Y):** `Job_Offers`  
- **Confounders (C):** `Internships_Completed`, `Networking_Score`, `Soft_Skills_Score`  

Applied the **backdoor criterion** to confirm identifiability.  
Initial regression suggested a positive effect — but regression alone cannot establish causality.  

→ Moved to design-based estimators.  

<img width="1042" height="753" alt="DAG" src="https://github.com/user-attachments/assets/45e2eed0-5fb9-46ab-bd38-864f358b80e8" />



## Step 2: Propensity Score Matching (Quartile Split) → Failed

- Treatment defined as **high projects (≥8)** vs **low projects (≤5)**.  
- **Result:** No overlap in propensity scores (controls ≤0.11 vs treated ≥0.92).  
- After trimming, zero controls remained.  

**Takeaway:** Matching not defensible; highlights why overlap checks are essential.  

<img width="897" height="705" alt="PSM histogram" src="https://github.com/user-attachments/assets/9de26c63-8700-4a26-9ae1-5c59e02863aa" />



## Step 3: Inverse Probability of Treatment Weighting (Median Split) → Partial Success

- Treatment redefined as **high projects (≥6)** vs **low projects (<6)**.  
- Applied stabilized IPTW with trimming.  
- **Diagnostics:** Balance improved but remained poor (SMD ≈ 1.6–2.0 >> 0.1).  
- **Estimate:** ATE ≈ +1.68 job offers (p < 0.001, 95% CI [1.51, 1.85]).  

**Caution:** Large effect likely inflated due to residual imbalance.  

<img width="907" height="712" alt="image" src="https://github.com/user-attachments/assets/f4e96289-f96e-4376-aef1-3eae882b7002" />



## Step 4: Overlap Weights (ATO) → Robust & Credible

To focus on the **region of common support**, we applied overlap weights.  

Compared three propensity models:  
- Logistic (baseline): ATO = 0.180, poor balance (max|SMD|=0.55).  
- Polynomial logistic (deg 2): ATO = 0.026, good balance (max|SMD|=0.08).  
- Gradient boosting: ATO = 0.023, excellent balance (max|SMD|=0.02).  

**Result:** Effect shrank to near zero once balance was achieved.  

<img width="898" height="696" alt="image" src="https://github.com/user-attachments/assets/ad1627f5-4ce3-4bcb-a145-864d32753a55" />



## Step 5: Bayesian Inference → Stability & Trade-offs

Fit a Bayesian Negative Binomial regression (with confounder adjustment).  
Reported **posterior rate ratios** instead of point estimates.  

**Findings:**  
- Naive (unadjusted) models overstated the effect (RR > 2.5).  
- Adjusted models centered near 1.0 with wide credible intervals → no clear causal effect.  
- Prior sensitivity (narrow, baseline, wide) produced nearly identical posteriors → results are **data-driven, not prior-driven**.  

<img width="1607" height="636" alt="Screenshot 2025-09-10 0051592" src="https://github.com/user-attachments/assets/ea1fa1db-e602-4971-9b8b-a960f92d168b" />



## Trade-offs and Lessons

- **PSM:** Simple and intuitive, but requires strong overlap. Failed in our data.  
- **IPTW:** Easy to interpret, but unstable under poor overlap (overstated effects).  
- **Overlap Weights:** Robust to limited overlap; revealed null effect but applies only to overlap population.  
- **Bayesian GLM:** Provided richer uncertainty quantification and showed robustness to prior choice.  



## Final Conclusion

Naive models suggested projects strongly increase job offers.  
But once confounders (internships, networking, soft skills) were properly addressed:

- **Overlap weights** and **Bayesian inference** converged on a **null effect** (RR ≈ 1.0, credible intervals crossing 1.0).  
- **Interpretation:** Project completion alone does **not** drive job offers; its apparent effect is confounded by internships and networking.  



## Recommendations for the Business

1. **Don’t over-invest in project count alone.** More projects are not sufficient to improve job outcomes.  
2. **Strengthen internships and networking opportunities.** These confounders explained most of the apparent project effect.  
3. **Promote holistic career readiness.** Balance project-based learning with soft skills and professional connections.  
4. **Use causal inference in product analytics.** Diagnosing overlap, balance, and robustness prevents overconfident conclusions from naive models.  

