Overview

This project demonstrates an end-to-end Banking Customer Lifetime Value (CLV) analytics solution built on the Databricks Lakehouse Platform using the Medallion Architecture (Bronze, Silver, Gold).

The solution ingests a single Excel dataset (banking.xlsx), transforms raw banking transaction data into curated analytical datasets, trains a machine learning model using Gradient Boosted Trees (GBTRegressor), registers the model with MLflow, and serves insights through Databricks AI/BI Dashboards.

Business Problem

Banks need to identify their most valuable customers and predict future customer value to:

Improve customer retention
Increase cross-sell opportunities
Reduce churn
Prioritize relationship management efforts
Optimize marketing and loyalty campaigns

This project predicts Customer Lifetime Value (CLV) using transaction activity, balances, tenure, and customer satisfaction scores.

                    banking.xlsx
                           |
                           v

                Databricks Volume
      /Volumes/banking/clv/raw_files/

                           |
                           v

   ==================================================
                    BRONZE LAYER
   ==================================================

                bronze_banking (Raw)

                           |
                           v

   ==================================================
                    SILVER LAYER
   ==================================================

      silver_customers
      silver_accounts
      silver_transactions

                           |
                           v

   ==================================================
                     GOLD LAYER
   ==================================================

      gold_customer_revenue
      gold_customer_clv
      customer_360
      clv_features

                           |
                           v

                  Feature Engineering

                           |
                           v

                   VectorAssembler

                           |
                           v

                    Train/Test Split
                        80% / 20%

                           |
                           v

                     GBTRegressor

                           |
                           v

                      Predictions

                           |
                           v

                   Model Evaluation
                      RMSE / R²

                           
                           v

                    MLflow Registry

                           |
                           v

                  Model Serving API

                           |
                           v

               Databricks AI/BI Dashboard



Technology Stack
Data Engineering
Databricks
Unity Catalog
Delta Lake
Delta Live Tables
Auto Loader
Databricks Volumes
Machine Learning
Apache Spark MLlib
VectorAssembler
GBTRegressor
MLflow
Visualization
Databricks AI/BI Dashboard
Data Storage
Delta Tables


age (numeric)
job : type of job (categorical:admin.','bluecollar','entrepreneur','housemaid','management','retired','selfemployed','services','student','technician','unemployed','unknown')
marital : marital status (categorical:'divorced','married','single','unknown'; note: 'divorced' means divorced or widowed)
education (categorical: 'basic.4y','basic.6y','basic.9y','high.school','illiterate','professional.course','university.degree','unknown')
default: has credit in default? (categorical: 'no','yes','unknown')
balance: average yearly balance, in euros (numeric)
housing: has housing loan? (categorical: 'no','yes','unknown')
loan: has personal loan? (categorical: 'no','yes','unknown')
contact: contact communication type (categorical:'cellular','telephone')
day: last contact day of the month (numeric 1 -31)
month: last contact month of year (categorical: 'jan', 'feb','mar', …, 'nov', 'dec')
duration: last contact duration, in seconds (numeric).
Important note: this attribute highly affects the output target (e.g., ifduration=0 then y='no'). Yet, the duration is not known before a call is performed. Also, after the end of the call y is obviously known.Thus, this input should only be included for benchmark purposes and should be discarded if the intention is to have a realistic
predictive model.
campaign: number of contacts performed during this campaign and for this client (numeric, includes last contact)
pdays: number of days that passed by after the client was last contacted from a previous campaign (numeric; 999 means client was not previously contacted)
previous: number of contacts performed before this campaign and for this client (numeric)
poutcome: outcome of the previous marketing campaign(categorical: 'failure','nonexistent','success')
target: has the client subscribed a term deposit? (binary:"yes","no")

            
