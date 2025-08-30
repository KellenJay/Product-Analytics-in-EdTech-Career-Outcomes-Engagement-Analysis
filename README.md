# Product-Analytics-in-EdTech-Career-Outcomes-Engagement-Analysis
This repository presents a comprehensive product analytics case study designed to explore the relationships between student engagement, educational experiences, and early-career outcomes in the EdTech landscape.

It integrates a real-world inspired dataset (from Kaggle) with a synthetic learner engagement dataset to simulate challenges often tackled by data and product analysts working in education-focused organizations.

---

## Project Overview

In education technology, understanding which factors contribute to learner success—both academically and in their early careers—is vital for product development, curriculum design, and student support systems.

This project simulates the kinds of analysis used to evaluate:

- The impact of learner engagement on job outcomes
- The causal effect of interventions like coaching or sprint completions
- How behavioral metrics can predict career success

It brings together foundational product analytics, causal inference, and statistical modeling into one pipeline.

---

## Core Questions

This project attempts to answer three central product analytics questions:

1. **How does early student engagement (e.g., coaching sessions, sprint completions, learning time) influence job offer outcomes or starting salary?**
2. **What is the estimated causal effect of coaching or support features on employment and promotion timelines, using observational data?**
3. **Can Bayesian models surface meaningful uplift or risk signals in learner segments for targeted intervention strategies?**

These questions will guide data exploration, feature engineering, and experiment simulation.

---

## Datasets

### `career_success.csv` (Kaggle Dataset)
This dataset contains 400 anonymized student records covering:

- **Demographics**: Age, Gender  
- **Academic Performance**: High School GPA, SAT Scores, University GPA, Field of Study  
- **Skills & Activities**: Internships, Projects, Certifications, Soft Skills, Networking  
- **Career Outcomes**: Job Offers, Starting Salary, Career Satisfaction, Promotion Timeline, Job Level, Work-Life Balance, Entrepreneurship

### `student_metrics.csv` (Synthetic Dataset)
This custom dataset simulates learning engagement metrics common in EdTech platforms:

- Sprint Completions  
- Coaching Sessions  
- Workshop Attendance  
- Learning Time per Day  
- Time to First Login  
- Time to Graduation  
- Student NPS  
- Free → Paid Conversion  
- Program Type  

The two datasets will be merged to conduct multi-faceted analysis from both an education and product engagement lens.

---

## Goals

- Identify engagement patterns that correlate with job success  
- Use causal inference to estimate non-random effects of support interventions  
- Apply Bayesian approaches for uplift modeling across learner cohorts  
- Prototype business-facing dashboards to surface actionable insights

---

## Tools & Tech

- **Python**: Pandas, NumPy, Seaborn, Scikit-learn, PyMC  
- **SQL**: Microsoft SQL Server  
- **Jupyter Notebooks**  
- **Visualization**: Plotly, Matplotlib, Streamlit (for optional dashboard UI)  
- **EDA + Experiment Planning**  

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
│   ├── 03_causal_inference_simulation.ipynb
│   ├── 04_bayesian_modeling_uplift.ipynb
│
├── visuals/
│   ├── charts/
│   ├── dashboard_mockups/
│
├── README.md
```

---

## Highlights

- ✅ Combines public and synthetic data for realism  
- ✅ Demonstrates causal inference without A/B tests  
- ✅ Focused on product-centric EdTech metrics  
- ✅ Developed with modular, business-first analytics flow  
