---
layout: post
title: Predicting the Default of Credit Crad Clients
subtitle: Analysis of prediction Models Used and the Predictive Accuracy of Probability of Default Clients.
cover-img: /assets/img/banking.jpg

gh-badge: [star, fork, follow]
tags: [test]
comments: true
---

## Abstract
In recent years, financial institutions invested a lot on risk prediction than crisis management. The reason for that is to use financial information, such as business financial statement,customer transaction and repayment records, etc., to predict business performance or individual customers’ credit risk and to reduce the damage and uncertainty.  
In this article, I’ll explain the method, models, and demonstrate the building of a Credit Card Prediction system using machine learning algorithms to help credit card issuers to reduce their risk.

## Dataset
The data collected in this dataset represents the case of customers’ default payments in Taiwan. 
Here is the link to the Dataset: [DATASET](https://archive.ics.uci.edu/ml/datasets/default+of+credit+card+clients#)

### Introduction
From the perspective of risk control, estimating the probability of default will be more meaningful than classifying customers into the binary results. 
To do so, first we need to look at how the data is distributed;
After exploring the datset, splitting the dataset into train and test dataset, I have creaeted I have determined the majority class as follwos:

let's first extract the correct values from the value and salary coulmns:

![]( /assets/img/majority.JPG)

Tha majority class occurs with 78%, so this is considered to ba a case of implanaced classes.
Because the target feature is impalanced, the "Accoracy Score" is not going to be the best model evaluation metric. Also, as I would rather have some extra false positives over saving some extra false negatives; it is crusial to identify true positives. Thus, I am using the Sinsitivity/Recall scoring and ROC to evaluate my models.

## Models
For this project I have used Logistic Refression, Random Forest Classifier, and XGBoost to develop models of risk predictions.

### 1-Logistic Regression:
The first statistical model I used was the Logistic Regression. Logistic regression is a classification algorithm used to assign observations to a discrete set of classes. In order to train my logistic regression model I used the “LogisticRegression” class from the “sklearn.linear_model” module. the validation accuracy of the model was 81%, which is the highest among all models. The ROC score was 71%.
![]( /assets/img/LRROC.JPG)
However, the recall/sensitivity was 24% which is the lowest among all models.
![]( /assets/img/LRcon.JPG)

### 2-Random Forest Classifier:
The Random Forest Classifier is a statistical model that fits a number of decision trees on varioues sub-samples of the dataset. One of the advantages of Random Forest over Decision Trees is that it is less sensitive to hyperparameteres and fits better.
In order to train my Random Forest model I used the "RandomForestClassifier" class from the “sklearn.linear_model” module with tuning the hyperbarameters to increase the bias and to put into consideration the weight of classes.
![]( /assets/img/ran1.JPG)
The ROC score for this model was 77.7% and the recall scpre was 58.7%
Then I generated the permutation importances of the model and remoced all of the features that are have a negative impact on the model
![]( /assets/img/perm.JPG)
The final ROC sore remained teh same with a slight improvement in the recall score to become 58.9%.
![]( /assets/img/ranconf.JPG)
![]( /assets/img/ranroc.JPG)

### 3-XGBoost:
The last statistical model I used was the XGBoost. XGBoost uses ensembles trees like the Random Forest Classifier, but utilizes a tecnique different than the bagging technique used by the random forest classifier. The tecniques that XGBoost utlizes called boosting. Boosting works in a similar way as bagging, except that the trees are grown sequentially.
In order to train my XGBoost model I used the "XGBClassifier" class from the “XGBoost” module with tuning the hyperbarameters to increase the bias and to put into consideration the weight of classes.
The ROC score for this model was 77.8% and the recall score has increased to 61%%

![]( /assets/img/xgbcon.JPG)
![]( /assets/img/xgbroc.JPG)
### Summary
The main goal is to predict more True Positives which indicate high risk customers to minimize the risk to the credit card issuer.
Thus, the best model to be used n this case the XGBoost

### Source Code
The Code used to generate the formentioned models is:
[Notebook](https://colab.research.google.com/drive/1qg6x_1ZSFqchT7EmMvKMmFPBDa_B4D-1?usp=sharing)

