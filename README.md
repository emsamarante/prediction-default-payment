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

## 3.0 Methodology

Although I could have chosen more than three algorithms - or even others-, I have selected only three: KNN, Decision Tree and Random Forest. In order to get the results, each of them was trained in ten model versions, which were made in different files.
As some versions required the cross validation, it was necessary to apply the statistical analysis in order to check whether there was any difference.
As shown in the figure below, the difference of complexity between them is in the layer of knowledge, the main distinction between versions 7 and 9 and between 8 and 10 being the technique used to selecting features.

![image](https://user-images.githubusercontent.com/45640708/146440580-81ddb0c4-0187-4ad4-9162-8bd589bc6bbd.png)

## 4.0 Statistical Analysis

The two models with the lowest variation coeficient were Random Forest of Version 7 to recall score and Decision Tree of Version 9 to accuracy score.
The Shapiro test was applied in the results in order to check if the data to recall and accuracy score have normal distribution. To both sets of data, only one version per set has non normal distribution, for instance: 
- Recall Score: Random Forest of Version 8
- Accuracy Score = Random Forest of Version 10

The Tukey's multicomparison analysis method was applied to test the largest pair-wise difference among the results to both data sets. As a result, the two best models to each metric score were:
- **Recall Score**: KNN of Version 5 - 93.62%
- **Accuracy Score**: Random Forest of Version 5 - 87.47%

![image](https://user-images.githubusercontent.com/45640708/146586619-e5867ff1-3b1f-4cc5-ae76-eed6b1d2f425.png)
![image](https://user-images.githubusercontent.com/45640708/146586692-6e37018e-ad50-4244-a408-01616d1a0b9d.png)

## 5.0 Business Application

I've simulated the models in business application for two scenarios: one per each model. In both, the company granted a financial credit of 2 millions dollars for their clients, and the model predict how much money was payed for them. Then, the Figure below shows how much money was saved in comparison of two models which have only 6.15% of difference in performance.

**The losses company was reduced in a -50.84%!!!**

![image](https://user-images.githubusercontent.com/45640708/146597239-0e1e8c22-0d87-46c1-a4dd-7c8145635f17.png)
