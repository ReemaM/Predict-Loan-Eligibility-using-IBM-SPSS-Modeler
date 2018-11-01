# Predict Loan Eligibility using Watson Studio
Loans are the core business of loan companies. The main profit comes directly from the loan's interest. The loan companies grant loan after an intensive process of verification and validation. However, they still do not have an assurance if the applicant is able to repay the loan with no difficulties.

## Problem
Mortgage loan companies have a presence across all urban, semi-urban and rural areas. They want to automate the loan eligibility process based on customer data provided from filling the online application form.
Thus, they first target those applicants who are eligible to make a loan.

## Learning Objectives
After completing this tutorial, you will understand how to;
- [Add and Prepare your data](#Add-and-Prepare-Data)
- [Build a Machine Learning Model](#Build-a-Machine-Learning-Model)
- [Save the Model](#Save-the-Model)

## Prerequisites
In order to complete this tutorial, you will need the following:
- [IBM Cloud](https://www.ibm.com/cloud/) account.
- [Object Storage](https://console.bluemix.net/catalog/services/cloud-object-storage) Service.
- [Watson Studio](https://console.bluemix.net/catalog/services/watson-studio) Service.
- [Machine Learning](https://console.bluemix.net/catalog/services/machine-learning) Service.

## Estimated time
The overall time of reading and follwing this tutorial is 1 hour approx.

## Dataset
The dataset is from [Analytics Vidhya](https://datahack.analyticsvidhya.com/contest/practice-problem-loan-prediction-iii/#data_dictionary)


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

## Create a Project in Watson Studio 
From Watson Studio main page, click on `New project`. Choose `Complete` to get the full functionalities. Once you enter your project name, click on `Create`.


![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/1_1.gif)



## Upload the dataset to IBM Watson Studio
Open `Find and add data` on the right-side panel, drag and drop the dataset (.csv file) from your computer to that area.


![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/2.gif)

## Create SPSS Modeler Flow
1. On the same Assets page, scroll down to Modeler flows.
2. Click the `(+) New flow` icon.
3. Under the 'New' tab, name your modeler 'Loan Eligibility Predictive model'.
4. Click `Create`.

## Add and Prepare Data
1. Add data to the canvas using the `Data Asset` node.
2. Double click on the node and click `Change Data Asset` to open the Asset Browser. Select train.csv then click `OK` and `Save`.


![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/10_1.gif)

Let’s look into the summary statistics of our data using the `Data Audit` node. 

3. Drag and drop the `Data Audit` node, and connect it with the Data Asset node. After running the node you can see your audit report on right side panel. 


![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/10_2.gif)

We can see that some columns have missing values. Let’s remove the rows that has null values using the `Select` node. 


4. Drag and drop the `Select` node, connect it with the Data Asset node and right click on it and open the node.


5. Select discard mode and provide the below condition to remove rows with null values.


```
(@NULL(Gender) or @NULL(Married) or @NULL(Dependents) or @NULL(Self_Employed) or @NULL(LoanAmount) or @NULL(Loan_Amount_Term) or @NULL(Credit_History))

```

![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/10_3.gif)


Now our data is clean, and we can proceed with building the model.

### Configure Variables Type

1. Drag and Drop the `Type` node to configure variables type, from Field Operations palette.
2. Double click the node or right click to open it. 
- Choose Configure Types to read the metadata.
- Change the Role from the drop down menu of [Loan_Status] from input to `output`. 
- Change the Role drop down menu of [LoanID] from none to `Record ID`.
- Click `Save`.

![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/11_1.gif)


## Build a Machine Learning Model

### Build Model
The model predicts the loan eligibility of two classes (Either Y:Yes or N:No). Thus, the choice of algorithms fell into Bayesian Networks since it is known to give good results for predicting classification problems.


1. Splite Data into training and testing sets using the `Partition` node, from Field Operations palette.
- Double click the Partition node to customize the partition size into 80:20, change the ratio in the `Training Partition` to 80 and `Testing Partition` to 20.


![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/13_1.gif)



2. Drag and drop the `Bayes Net` node, from the Modeling Palette.
3. Double click the node to change the settings. Check `Use custom field roles` to assign Loan_Status as the target, and all the remaining attributes as input except Partition and Loan_ID. When you finish, click `Save`.


![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/14_1.gif)



4. `Run` your Bayesian Network node, then you will see your model in an orange colored node.


![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/15_1.gif)


### View the Model
- Right click on the orange colored node, then Click on `View` .
- Now you can see the Network Graph and other model information here.


![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/16_1.gif)

### Evaluate the Performance of the Model
1. Drag and drop the `Analysis` node from the Output section, and connect it with the model. 
2. After running the node you can see your analysis report on the right side panel. 

![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/17.gif)

The analysis report shows we have achieved 82.3% accuracy on our test data set with this model.
At the end, you can build more models within the same canvas until you get the result you want.
 
## Save the Model
1. Right-click on the Bayes Net node and select `Save branch` as a model.
2. Enter a name for the model. A machine learning service should be added automatically if you already created a one. 
3. Click on `Save`. 

![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/18.gif)

In the Asset page under `Watson Machine Learning models` you can access your saved model, where you can deploy it later.

![Alt Text](https://github.com/Hisaah/Predict-Loan-Eligibility-using-IBM-SPSS-Modeler/blob/master/images/19.gif)
 

## Summary
In this tutorial, you learned how to create a complete predictive model, from importing the data, preparing the data, to training the model and saving it. You learned how to use SPSS Modeler and export the model to Watson Machine Learning models.
