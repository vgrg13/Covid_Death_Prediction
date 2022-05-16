# Table of Contents
1. [Covid Death Predictor Model Objective](#Covid-Death-Predictor-Model-Objective)
2. [Approach](#Approach)
3. [Data Sources](#Data-Sources)
4. [Model Predictors](#Model-Predictors)
5. [Model Performance and Validation Results](#Model-Performance-and-Validation-Results)
6. [Final Report](#Final-Report)

# Covid Death Predictor Model Objective
Given certain characteristics about an individual, can the machine predict if the patient will die due to COVID-19? 

The purpose of the model is to help hospitals predict patients in critical conditions to better allocate resources to those in need. Since there is no variable that represents serious hospitilization, we used death as the dependent variable.

***

# Approach

**Followed a 6-step approach**

- Data Identification & Collection: Researched for databases containing patient information related to Covid Cases in the United States. Found an extensive dataset on the CDC website after looking into other wesbites like Kaggle. 

- Data Quality Assessment & Preparation: Filter out columns containing irrelevant variables. Then eliminated all rows that do not have complete information. Kept the columns on age-group, sex, race, ethnicity, state fips code, symptom, if they were hosptialized or not, if they were admitted into the ICU or not, and if they died or not. 

- EDA (Exploratory Data Analysis): Plotted probability of dying against every variable

- Feature Engineering: We first used one hot encoding to transform all binary categorical variables into 0 and 1s. Next, we transformed the variable of race into multiple separate binary variables (ex. race_white y/n)

- Model Development: Used Random Forest Classifier since we were working with predominantly categorical variables. Performed grid search to optimize the model and adjusted threshold of the model to account for the imbalance in the data set.

- Model Validation: Assessed model performance on test dataset using various methods

***

# Data Source

The data is sourced from the CDC website and includes over 27 million covid cases from the United States dating from January 2021 along with specific details about each case. The variables include: case month/year, state of residence, state FIPS code, county of residence, county FIPS code, age group, sex, race, ethnicity, survived or not, exposure, symptoms, and more.

Public Data Source -- https://data.cdc.gov/Case-Surveillance/COVID-19-Case-Surveillance-Public-Use-Data-with-Ge/n8mc-b4w4/data

***

# Model Predictors

The below image shows a computer generated feature importance plot. The longer the bar, the more importance the computer gives to that certain categorical variable. For example, in the case of this model, the machine gives the most importance to whether or not the patient was hospitalized and the age group the patient fell in. This tells us that status of hospitlization and age matter the most in predicting whether or not a patient will die. 

**Feature Importance**

![Screen Shot 2022-05-15 at 9 37 59 PM](https://user-images.githubusercontent.com/88556975/168505567-202f281d-e767-403a-84e9-40a10f2f5157.png)

***

# Model Performance and Validation Results

The below image shows an AUC (area under the curve) graph. The high value of the AUC curve (0.96) shows that the model does very well in distinguishing between the positive and negative classes (in this case dying or not). 

**AUC Curve**

![Screen Shot 2022-05-15 at 9 35 46 PM 2](https://user-images.githubusercontent.com/88556975/168505471-83a3a19d-7453-4b40-a4f0-23d0dab6f0f2.png)

The below table presents values for precision and recall. Recall is the same as the true positive rate (the machine correctly predicting a death) and should be optimized to prevent the most deaths. The table shows that for the value of 1 (representing deaths), the recall in 0.96 and the precision is 0.13. The high recall is exactly what we want which has a side effect of having a low precision.

**Performance Stats**

                  precision  recall  f1-score   support

           0       1.00      0.86      0.92     14684
           1       0.13      0.96      0.23       316

         accuracy                      0.86     15000


The final image is a confusion matrix of the test data. Most importantly, it shows that the machine correctly predicted 304/316 deaths. 

**Confusion Matrix**

![image](https://user-images.githubusercontent.com/88556975/168504832-88cf0106-0648-4bcf-af3f-934338487d7b.png)

<>
***

# Final Report

Final Report -- https://github.com/vgrg13/Covid_Death_Prediction/blob/main/final%20project%20end-to-end%20summary.docx

***

