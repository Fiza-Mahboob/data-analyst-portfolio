
# SaaS Subscription Metrics Dashboard (Power BI)

## Overview
A multi-page Power BI report modeling the core metrics of a subscription 
business: MRR, churn, cohort retention, and region-based access control.

## Questions This Dashboard Answers
- What is current MRR, and how has it changed month over month?
- What is the churn rate, and which segments drive it?
- How well are customers retained over time (cohort analysis)?
- Which contract type, region, or segment is most at risk?
- What is the estimated customer lifetime value (LTV)?

## Data Source
IBM Telco Customer Churn dataset (Kaggle). The original data contains 
tenure in months but no real dates or regions, so SignupDate, ChurnDate, 
and Region were derived/assigned for modeling purposes. Findings about 
region in particular reflect this assignment, not a real business pattern.

## Tools & Techniques
- Power Query: custom columns, data shaping, date table via M code
- Data modeling: dual date relationships (active SignupDate, inactive 
  ChurnDate activated with USERELATIONSHIP)
- DAX: MRR, churn rate, ARPU, LTV, cohort retention (ALLEXCEPT), MRR movement
- Row-level security: 4 regional manager roles
- Custom theming and multi-page report design

## Dashboard Pages
![Revenue & Customer Health](images/RevenueHealth.png)
![Cohort Retention](screenshots/02_cohort_retention.png)
![Churn & Customer Risk](images/churn_risk.png)
![MRR Movement](screenshots/04_mrr_movement.png)

## Row-Level Security
Same report, different views depending on the assigned role.
![North Manager](screenshots/rls_north.png)
![South Manager](screenshots/rls_south.png)

## Key Insights
- Contract type is the strongest churn driver: month-to-month customers 
  churn at 42.71% vs 2.83% for two-year contracts
- Overall churn is 26.54%, high for a subscription business
- Average cohort retention is 74.3% across 93 signup cohorts; very small 
  early cohorts show extreme values due to sample size
- Churned MRR only appears from mid-2024 onward because churn dates were 
  modeled within the last 24 months

## Limitations & Next Steps
- Derived dates and regions (see Data Source)
- RLS roles are assigned manually; a production version would map users to 
  regions dynamically with USERPRINCIPALNAME()
