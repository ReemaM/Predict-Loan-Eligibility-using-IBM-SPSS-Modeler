# Predict Loan Eligibility using Jupyter Notebook & IBM SPSS Modeler
Loans are the core business part of lending companies. The main profit came directly from the loan's interest. The lending companies grant loan after an intensive process of verification and validation. However, they still do not have an assurance if the applicant is able to repay the loan with no difficulties.

## Problem
Finance company deals in all home loans, they have a presence across all urban, semi-urban and rural areas. They want to automate the loan eligibility process based on the customer information provided from filling the online application form.
Thus, They target those applicants who are eligible for loan amount first.

## Learning Objectives
After completing this tutorial, you will understand how to;
- [Prepare data with Jupyter Notebook](#Preparing-your-data-with-Jupyter-Notebook)
- [Export Data from Jupyter Notebook](#Export-CSV-File-from-Jupyter-Notebook)
- [Build a Machine Learning Model using SPSS Modelr](#Build-a-Machine-Learning-Model-using-SPSS-Modelr)

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
+ **Gender**              Male/ Female
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
![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/1.gif)


## Upload the dataset to IBM Watson Studio
Open `Find and add data`  right-side panel, drag and drop the dataset (.csv file) from your computer to that area.
![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/2.gif)


## Preparing your data with Jupyter Notebook
### Create a new Notebook:
1. Go to the Notebooks section in the Asset dashboard of IBM Watson Studio. 
2. Click on `New Notebook`
3. Write a name for the notebook.
4. Click `Create Notebook`

### Insert the data as Panda Dataframe into the notebbok
![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/3.gif)
Change Dataframe name from **df_data_1** to **trainData**.

### Steps to Clean Null values from your Data:
1. Check the data types of the variables using `dtypes`.
![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/4.PNG)

2. Check the sum of Null Values.
![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/5.PNG)

3. Fill-in the null values of `Gender` by the most frequent value.
![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/6.PNG)

4. Fill-in the null values of `Married` and `Credit_History` by the most frequent value, and `LoanAmount` with the average value.
![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/7.PNG)

5. Fill-in the null values of `Loan_Amount_Term` with the average value, and `Self_Employed` by the most frequent value. For `Dependents` Fill-in the null values with 0. 
![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/8.PNG)

7. Now, let's check again the sum of Null values.
![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/9.PNG)
we have no null values, and we can proceed of building our model.

But first we have to export the cleaned dataframe to a CSV file, and import it to SPSS Modeler later.

### Export CSV File from Jupyter Notebook
1. Write dataframe to CSV file

```
trainData.to_csv('csvtrain.csv',index=False)
```

2. Upload the file to your Object Storage, and download it from there. 
```
[Enter Client Name].upload_file('csvtrain.csv', ['Enter Bucket Name'], 'csvtrain.csv')
```
Download the file from your Object Storage Service, and upload it to your Data Asset in the project as we did before.
## Build a Machine Learning Model using SPSS Modelr
### Create SPSS Modeler Flow
1. On the same Assets page, scroll down to the Modeler flows.
2. Click the `(+) New flow` icon.
3. Under the 'New' tab, name your modeler 'Loan Eligibility Predictive model'.
4. Click `Create`.

### Add and Prepare Data
1. Add data to the canvas using `Data Asset` node.
2. Double click the node and click `Change Data Asset` to open the Asset Browser. Select csvtrain.csv then click `OK` and `Save`.
![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/10.gif)

3. Drag and Drop `Type ` node to configure variables type, from Field Operations palette.
4. Double click the node or right click to open it. 
- Choose Configure Types to read the metadata.
- Change the Role from the drop down menu of [Loan_Status] from input to `output`. 
- Change the Role drop down menu of [LoanID] from none to `Record ID`.
- Click `Save`.
![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/11.gif)
![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/12.gif)

### Build Model
The model predicts the loan eligibility of two classes (Either Y:Yes or N:No). Thus, the choice of algorithms fell into Bayesian networks since it is known to give good results for predicting classification problem.
1. Splite Data into training and testing sets using `Partition` node, from Field Operations palette. It will be 
- Double click Partition node to customize the partition size into 80:20, change the ratio in the `Training Partition` to 80% and `Testing Partition` to 20%.
{image}

2. Drag and drop the `Bayes Net` node, from the Modeling Palette.
3. Double click the node to change settings. Check use custom field roles to assign PREDICTION_transformed as the target, and all the remaining attributes except Partition as input. When you finish, click `Save`.






 






