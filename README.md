# Prediction of Default Payments of Credit Card Clients

In this report is presented some details of data exploration, and the prediction of defaulting person with machine learning programs in the classification problem.

## 1.0 Introduction

The dataset used in this report consist in an open database with default payments of clients in Taiwan. This dataset is available for download in [UCI – Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/default+of+credit+card+clients). The dataset can be used for a binary classification in order to predict whether the client will pay the bill amount or to estimate the real probability of default payment. 
This report shares some details of data exploration and machine learning models training for a binary classification. After getting the scores of recall and accuracy for every model which was trained in Python language, I decided to make the analysis statistic of results in R language. For each model trained with Decision Tree, Random Forest and KNeighbors algorithms were made ten versions summarising thirty models.   
Finally, I apply the model in real financial problem for the two best models trained and I show how much money can be saved.


## 2.0 Data Exploration

According the site, the data belongs the business area, it has 30,000 instances (real and integer) and 24 columns. The source also gave information about the data of each column.
1. **Limit_bal**: Amount of the given credit (NT dollar): it includes both the individual consumer credit and his/her family (supplementary) credit.
2. **Sex**: gender of people
3. **Age**: years
4. From **Pay_0** to **Pay_6**: History of past payment. We tracked the past monthly payment records (from April to September, 2005) as follows:
  - **Pay_0**: the repayment status in September, 2005; 
  - **Pay_1**: the repayment status in August, 2005...
  - **Pay_6**: the repayment status in April, 2005. 
The measurement scale for the repayment status is: -1 = pay duly; 1 = payment delay for one month; 2 = payment delay for two months; . . .; 8 = payment delay for eight months; 9 = payment delay for nine months and above.
5. From **Bill_amt1** to **Bill_amt6**: Amount of bill statement (NT dollar). 
- **Bill_amt1**: amount of bill statement in September, 2005; 
- **Bill_amt2**: amount of bill statement in August, 2005; ...; 
- **Bill_amt6**: amount of bill statement in April, 2005.
6. From **Pay_amt1** to **Pay_amt6**: Amount of previous payment (NT dollar). PAY_AMT1 = amount paid in September, 2005; 
- **Pay_amt2**: amount paid in August, 2005; ...;
- **Pay_amt6**: amount paid in April, 2005.

### 2.1 Manipulation of Data

There aren’t missing values in dataset. First of all, the dataset was storage in df to begin with the manipulation. The figure below depicts the type of data, which contradicts the information gave on site about the data instances. 

![Figure 1: Types of data](https://user-images.githubusercontent.com/45640708/146437534-5ce460ed-981c-4c21-b307-c5744f2a0ec7.png)

The first column was dropped and the last one was renamed to **defaulting person**. The data of some columns were converted to string because the number represents a categorical attribute. 

![image](https://user-images.githubusercontent.com/45640708/146438555-3bcb8549-5142-4a72-8e3c-c96ebafed2ff.png)


The dataset had inconsistent values in **education** and **marital status** columns. There were values that weren’t mentioned in the attribute information, for instance, values from zero to six in education values, but the site talked about from one to four. The **one** value means graduated school, **two** – university, **three** – high school and **four** – others. The values **five**, **six** and **zero** were assigned values four. Furthermore, the marital status should have only values from one to three, but the zero values that had in the column were classified like **others** (value 3). 
The dataset is a case of imbalanced data due to the class 1 for defaulting person column corresponds only for 22.1% of total. We made the data balancing with two techniques: synthetic minority over-sampling technique (smote) and under sampling the majority class.

![image](https://user-images.githubusercontent.com/45640708/146439213-c1243c74-3a33-4f05-8931-3f6f7e68024e.png)

The dataset after the cleaning process and treatment, the over sampled data and under sampled data were saved in different files.

