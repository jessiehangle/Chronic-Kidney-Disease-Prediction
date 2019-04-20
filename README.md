# Chronic Kidney Disease Prediction
## Tools: 
R, Data Manipulating (Package MICE), Logistic Regression, Decision Tree, Data Visualization (Excel, ggplot2)

## Objective: 
In this study, we are to detect at-risk patients from a previous obtained clinical dataset, to define a series of factors that could indicate the presence of CKD, and to develop our credible and easy-to-use screening tool to measure an overall risk for random individual. The dataset contains various information-including demographic (age, gender, and race group) as well as physical record (whether an individual has a certain kind of disease in the past or not) of 8,819 individuals.

### Data Exploration: 

![Screen Shot 0031-04-20 at 19 46 05](https://user-images.githubusercontent.com/49817101/56463592-5185fd00-63a5-11e9-9c7d-7aea85972c05.png)

#### Handling Missing Values
For our case study dataset, we chose multiple imputation method. The aim of the imputation step is to fill in missing values multiple times using the information contained in the original data sample. It replaces each missing item with a more acceptable value from a set of plausible values, representing a distribution of possibilities. We selected a package from R to do the multiple imputation. The package is MICE (Multivariate Imputation by Chained Equations). By default, linear regression is used to predict continuous missing values. Once this cycle is complete, multiple datasets are generated. These datasets differ only in imputed missing values. 
