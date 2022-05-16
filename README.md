# Table of Contents
1. [Covid Death Predictor Model Objective](#Covid-Death-Predictor-Model-Objective)
2. [Approach](#Approach)
3. [Data Sources](#Data-Sources)
4. [Model Predictors](#Model-Predictors)
5. [Model Performance and Validation Results](#Model-Performance-and-Validation-Results)
6. [Final Report](#Final-Report)

# Covid Death Predictor Model Objective
Given certain characteristics about an individual, can the machine predict if the patient will die due to COVID-19? 

The purpose of the model is to support medcial diagnosis through forecasting a Covid patient's condition using Machine Learning algorithms.

***

# Approach

**Followed a 6-step approach**

- Data Identification & Collection: Researched for databases containing patient information related to Covid Cases in the United States. Found an extensive dataset on the CDC website after looking into other wesbites like Kaggle. 

- Data Quality Assessment & Preparation: Filtered out columns containing irrelevant variables such as ICU Y/N due to it mostly being missing. Kept the columns for age-group, sex, race, ethnicity, state FIPS (Federal Information Processing System) code, symptom, if they were hosptialized or not, and if they died or not. Then eliminated rows missing death information and age group. (done outside in excel)

- EDA (Exploratory Data Analysis): Plotted probability of dying against every variable

- Feature Engineering: We used one hot encoding approach to transform categorical variables into multiple separate binary variables (ex. race)

- Model Development: Used Random Forest Classifier since we were working with predominantly categorical variables. Performed grid search on depth and min_sample_leaf to optimize the model and adjusted threshold of the model to account for the imbalance (only 2% death rate) in the data set.

- Model Validation: Assessed model performance on test dataset using various methods

**Refer to end to end modeling code here:**
https://github.com/vgrg13/Covid_Death_Prediction/blob/main/Final_Project.ipynb

***

# Data Source

The data is sourced from the CDC website and has 27 million covid cases from the United States as of August 2021 along with specific details about each case. The variables include: case month/year, state of residence, state FIPS code, county of residence, county FIPS code, age group, sex, race, ethnicity, survived or not, exposure, symptoms, and more.

Public Data Source -- https://data.cdc.gov/Case-Surveillance/COVID-19-Case-Surveillance-Public-Use-Data-with-Ge/n8mc-b4w4/data

***

# Model Predictors

The below image shows a computer generated feature importance plot. The longer the bar, the more importance the computer gives to that certain categorical variable. For example, in the case of this model, the machine gives the most importance to whether or not the patient was hospitalized and the age group the patient fell in. This tells us that status of hospitlization and age matter the most in predicting whether or not a patient will die. 

**Feature Importance**

![Screen Shot 2022-05-15 at 9 37 59 PM](https://user-images.githubusercontent.com/88556975/168505567-202f281d-e767-403a-84e9-40a10f2f5157.png)

***

# Model Performance and Validation Results

**After train/test split, 15,000 cases were used to judge the performance of the model**

The below image shows an AUC (area under the curve) graph. The high value of the AUC curve (0.96) shows that the model does very well in distinguishing between the positive and negative classes (in this case dying or not). 

**AUC Curve**

![Screen Shot 2022-05-15 at 9 35 46 PM 2](https://user-images.githubusercontent.com/88556975/168505471-83a3a19d-7453-4b40-a4f0-23d0dab6f0f2.png)

The below table presents values for precision and recall. Recall is the same as the true positive rate (the machine correctly predicting a death) and should be optimized to prevent the most deaths. Precision also considers false positives along with true positives. The table shows that for the value of 1 (representing deaths), the recall in 0.96 and the precision is 0.13. In this scenario, recall is more important because of the emphasis on true positives instead of false positives. 


**Performance Stats**

                  precision  recall  f1-score   support

           0       1.00      0.86      0.92     14684
           1       0.13      0.96      0.23       316

         accuracy                      0.86     15000


The final image is a confusion matrix of the test data. Most importantly, it shows that the machine correctly predicted 304/316 deaths. 

**Confusion Matrix**

![image](https://user-images.githubusercontent.com/88556975/168504832-88cf0106-0648-4bcf-af3f-934338487d7b.png)

***

# Results Overview

- Given some simple demographic information about the patients, the model will predict around 16% or 2400 patients to have increased risk of dying (True Positives + False Positives). Out of these 2400 patients, around 12% or 300 patients will die (True Positives). Almost none of the people the model predicts as not dying will die (about 0.1%)

- The high rate of the model identifying a positive case (recall) comes with its drawbacks. Due to the nuances of establishing a threshold, the high recall causes a low precision rate. In this scenario, though, recall holds more significance than precision. 

- So, after applying the model, we can allocate resources properly to those in need, thus decreasing the covid death rate. We can group patients with high risks in one area where resources are largely concentrated.

***

