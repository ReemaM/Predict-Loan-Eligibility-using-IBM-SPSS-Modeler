# Predict-Loan-Eligibility-using-Jupyter-Notebook-&-IBM-SPSS-Modeler
Loans are the core business part of lending companies. The main profit came directly from the loan's interest. The lending companies grant loan after an intensive process of verification and validation. However, they still do not have an assurance if the applicant is able to repay the loan with no difficulties.

## Problem
Finance company deals in all home loans, they have a presence across all urban, semi-urban and rural areas. They want to automate the loan eligibility process based on the customer information provided from filling the online application form.
Thus, They target those applicants who are eligible for loan amount first.

## Learning Objectives
After completing this tutorial, you will understand how to;
- [Prepare data with Jupyter Notebook](#Preparing-your-data-with-Jupyter-Notebook)
- [Export Data from Jupyter Notebook](#)
- [Build a Machine Learning Model using SPSS Modelr](#)

## Prerequisites
In order to complete this tutorial, you will need the following prerequisites:
- [IBM Cloud](https://www.ibm.com/cloud/) account.
- [Object Storage](https://console.bluemix.net/catalog/services/cloud-object-storage) Service.
- [Watson Studio Service](https://console.bluemix.net/catalog/services/watson-studio) Service.

## Estimated time
The overall time of reading and follwing this tutorial is 1 hour approx.

## Dataset
The dataset is taking from [Analytics Vidhya](https://datahack.analyticsvidhya.com/contest/practice-problem-loan-prediction-iii/#data_dictionary)


**The formate of the data:**
+ **Variable**            Description
+ **Loan_ID**             Unique Loan ID
+**Gender**              Male/ Female
+ **Married**             Applicant married (Y/N)
+ **Dependents**          Number of dependents
+ **Education**           Applicant Education (Graduate/ Under Graduate)
+ **Self_Employed**       Self employed (Y/N)
+ **ApplicantIncome**     Applicant income
+ **CoapplicantIncome**   Coapplicant income
+ **LoanAmount**          Loan amount in thousands
+ **Loan_Amount_Term**    Term of loan in months
+ **Credit_History**      Credit history meets guidelines
+ **Property_Area**       Urban/ Semi Urban/ Rural
+ **Loan_Status**         Loan approved (Y/N)

## Create a project in Watson Studio 
From Watson Studio main page, click on `New project`. Choose `Complete` to get full functionalities. Once you enter your project name, click on `Create`.
![Alt Text](https://github.com/{user}/{repo}/raw/master/path/to/1.gif)


## Upload the dataset to IBM Watson Studio
Open `Find and add data`  right-side panel, drag and drop the dataset (.csv file) from your computer to that area.
![Alt Text](https://github.com/{user}/{repo}/raw/master/path/to/1.gif)


## Preparing your data with Jupyter Notebook
