# Career Outcomes Engagement Analysis

This repository presents a comprehensive product analytics case study designed to explore the causal impact of student engagement—particularly project-based learning—on early career outcomes in the EdTech landscape.

It integrates a real-world inspired dataset with a synthetic learner engagement dataset to simulate challenges often tackled by data and product analysts working in education-focused organizations. The analysis is grounded in a rigorous causal inference framework using DoWhy and DAG modeling to identify and validate key hypotheses.

---

## Problem Statement

We're investigating whether **the number of projects a student completes during their education has a causal effect on the number of job offers** they receive post-graduation. This question explores whether project-based learning (a key pedagogical strategy in EdTech) translates into better career opportunities.

Our goal is to understand whether there is a **causal relationship (not just correlation)** between `Projects_Completed` and `Job_Offers`, using causal inference methods to simulate intervention-like reasoning without A/B testing.

### Why This Matters
- **For students**: Understand the value of project work in boosting employability.
- **For product teams**: Prioritize features that promote deeper engagement with practical projects.
- **For career services teams**: Advocate for more robust project mentorship or showcase tools.
- **For EdTech platforms**: Justify product strategy focused on portfolio development.

---

## Project Overview

In education technology, understanding which factors contribute to learner success—both academically and in their early careers—is vital for product development, curriculum design, and student support systems.

This project simulates the kinds of analysis used to evaluate:

- The **causal impact of learner activity on job outcomes**
- Whether projects completed by students serve as a valid intervention variable
- How **behavioral metrics** mediate or confound **career success**

It brings together foundational product analytics, causal inference, and statistical modeling into one pipeline.

---

## Core Questions

1. **Does completing more projects during an EdTech program causally influence the number of job offers a student receives?**
2. **Which factors confound or mediate this relationship—e.g., networking, internships, soft skills?**
3. **Can we validate this using DAGs and statistical refuters without needing randomized experiments?**

---

## Methodology

### 1. **Causal Graph Design (DAG Modeling)**
We constructed a Directed Acyclic Graph (DAG) to define our causal assumptions:
- Treatment: `Projects_Completed`
- Outcome: `Job_Offers`
- Confounders: `Networking_Score`, `Internships_Completed`, `Soft_Skills_Score`

This structure was formalized using `DoWhy`'s `CausalModel` class and validated for identifiability.

<img width="1042" height="753" alt="image" src="https://github.com/user-attachments/assets/c8c672c6-b9d5-4c80-ac7e-69159d70e47b" />

### 2. **Backdoor Criterion & Identified Estimand**
We applied the backdoor criterion to adjust for confounders and identify the average treatment effect (ATE) of `Projects_Completed` on `Job_Offers`.

### 3. **Regression Estimation**
We estimated the causal effect using linear regression, controlling for all identified confounders. The estimated effect was:
- **0.2257** (p < 0.001), indicating a significant positive causal impact.

### 4. **Robustness Checks (Refuters)**
To validate the strength of our causal estimate, we applied multiple refuters:
- Placebo Test: No effect found using fake treatment
- Subset Validation: Estimate remained stable across samples
- Random Common Cause: Estimate unchanged with noise
- Unobserved Confounder Simulation: Estimate varied within expected bounds

### 5. **Model Validation with Conditional Independence Tests**
Graph vs Data tests using partial correlation confirmed that our DAG was statistically plausible under different levels of conditioning (k = 0 to 4).

---

## Datasets

### `career_success.csv` 
- **Demographics**: Age, Gender  
- **Academic Performance**: High School GPA, SAT Scores, University GPA, Field of Study  
- **Skills & Activities**: Internships, Projects, Certifications, Soft Skills, Networking  
- **Career Outcomes**: Job Offers, Starting Salary, Career Satisfaction, Promotion Timeline, Job Level, Work-Life Balance, Entrepreneurship

### `student_metrics.csv` 
- Sprint Completions  
- Coaching Sessions  
- Workshop Attendance  
- Learning Time per Day  
- Time to First Login  
- Time to Graduation  
- Student NPS  
- Free → Paid Conversion  
- Program Type

---

## Goals
- Use DAGs to formally map causal assumptions
- Estimate ATE using backdoor-adjusted regression
- Validate model robustness using multiple refutation strategies
- Lay the groundwork for future experimentation using Bayesian or DiD frameworks

---

## Tools & Tech

- **Python**: Pandas, NumPy, Seaborn, Scikit-learn, DoWhy, NetworkX  
- **SQL**: Microsoft SQL Server  
- **Jupyter Notebooks**  
- **Visualization**: Matplotlib, Plotly, Graphviz

---

## Project Structure

```
edtech-career-analytics/
│
├── data/
│   ├── career_success.csv
│   ├── student_metrics.csv
│   ├── merged_dataset.csv
│
├── notebooks/
│   ├── 01_eda_career_success.ipynb
│   ├── 02_sql_exploration_edtech.ipynb
│   ├── 03_causal_dag_modeling.ipynb
│   ├── 04_estimation_and_refutation.ipynb
│
├── visuals/
│   ├── causal_dags/
│   ├── plots/
│
├── README.md
```
<img width="628" height="259" alt="image" src="https://github.com/user-attachments/assets/5080eb47-ebbc-4035-a639-e17204212810" />
---

Controlling for internships, networking score, and soft skills score, we estimate that completing one additional project **increases the expected number of job offers by approximately 23%,** with high statistical significance and a 95% confidence interval between 17%-28%.

--- 

## Model Limitations and Causal Trade-offs

While our causal model passed key robustness checks; including placebo and random confounder tests, it **may still be sensitive to unmeasured confounding variables.** This means that the estimated effect, though promising, **should not be treated as definitive.** Instead, it **should inform broader strategy decisions,** ideally alongside further validation methods like randomized trials or instrumental variable approaches.

--- 

## Final Takeaways

This project demonstrates how causal inference techniques can be applied in product analytics to simulate experimental thinking. The study set out to answer a central question in education-to-employment analytics: **"Do projects completed during education causally influence the number of job offers students receive?"** Using a causal inference and robust validation techniques, the analysis reveals that: **There is a positive causal effect of project completion on job offers.** Students who complete more projects are significantly more likely to receive additional job offers, even after accounting for potential confounders.

**Recommendations**

**1. Invest in Project-Based Learning Infrastructure:** Given the strong causal link between project completion and job offers, the platform should prioritize features that encourage students to complete more real-world projects during their learning journey.

**2. Enable Portfolio-Focused Support Tools:** Introduce tools like automated project feedback, peer showcases, and project-to-career alignment to help students better demonstrate their skills to potential employers.

This insight has strong implications for **EdTech product design**, **curriculum development**, and **student guidance systems**. It emphasizes the importance of **hands-on project work** not just as a learning tool, but as a **tangible career accelerator**. This is a strong example of how product analysts can move beyond correlation and begin shaping strategy through rigorous causal frameworks.
