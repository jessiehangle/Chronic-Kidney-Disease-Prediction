# Chronic Kidney Disease Prediction
## Tools: 
R, Data Manipulating (Package MICE), Logistic Regression, Decision Tree, Data Visualization (Excel, ggplot2)

## Objective: 
In this study, we are to detect at-risk patients from a previous obtained clinical dataset, to define a series of factors that could indicate the presence of CKD, and to develop our credible and easy-to-use screening tool to measure an overall risk for random individual. The dataset contains various information-including demographic (age, gender, and race group) as well as physical record (whether an individual has a certain kind of disease in the past or not) of 8,819 individuals.

## Data Exploration: 

![Screen Shot 0031-04-20 at 19 46 05](https://user-images.githubusercontent.com/49817101/56463592-5185fd00-63a5-11e9-9c7d-7aea85972c05.png)

### Handling Missing Values
For our case study dataset, we chose multiple imputation method. The aim of the imputation step is to fill in missing values multiple times using the information contained in the original data sample. It replaces each missing item with a more acceptable value from a set of plausible values, representing a distribution of possibilities. We selected a package from R to do the multiple imputation. The package is MICE (Multivariate Imputation by Chained Equations). By default, linear regression is used to predict continuous missing values. Once this cycle is complete, multiple datasets are generated. These datasets differ only in imputed missing values. 
![Screen Shot 0031-04-21 at 21 05 10](https://user-images.githubusercontent.com/49817101/56477993-692eb580-6479-11e9-93bf-81ef8da6b789.png)

## Model Fitting 
Once the imputation of the data is done, we split the data into training set and test set. Training set is used to fit our model which we will be testing over the testing set. Division of data is done such that 75% of given data is train data and 25% is test data.
Step 1: Working with the perfect set of data. We have created a logistic regression model using the perfect train data set (data without any missing value).

![Screen Shot 0031-04-21 at 21 12 28](https://user-images.githubusercontent.com/49817101/56478074-3a650f00-647a-11e9-8e05-70ebae7bd778.png)

Step 2: With the Imputed data: While imputing missing data, we have carefully maintained the density curve of each variable. Hence, we created the model with the imputed dataset which analyses the significant variable in model. Using Logistic Regression, we then created Model 2 with all 33 variables and applied backward elimination approach to identify variables which are most significant. These variables then were included in Model 3.

![Screen Shot 0031-04-21 at 21 14 10](https://user-images.githubusercontent.com/49817101/56478097-77310600-647a-11e9-922d-b5b123ca8820.png)


Step 3: Objective of our analysis is to create easy to use screening tool. Although Model 3 has all significant variables, some of these variables such as CHF, PVD, HDL or family history of hypertension can not be obtained by easy-to-use screening tool. Some people might not be aware of these parameters while filling up the data in screening tool. We have further tried to reduce number of variables in model 3 by building new model (Model 4) including 7 significant variables which are Age, Gender, Activity, Hypertension, Diabetes, CVD and Anemia. According to the case study, Race group also plays an important role in increasing risk of having CKD, so we consider Race Group in our reduced model.
![Screen Shot 0031-04-21 at 21 11 17](https://user-images.githubusercontent.com/49817101/56478117-a2b3f080-647a-11e9-9719-1e5bc5e4d2f9.png)

### Comparison between four models
As we can see from Table 4, there is a significant drop in AIC from Model2 to Model3 which means that our Model 3 is more significant compared to Model2. The difference between the null deviance and the residual deviance shows how our model is doing against the null model (a model with only the intercept). The wider this gap, the better. Analyzing the table, we can see the drop-in deviance in model 3. The accuracy of each model is above 90% which is quite a good result.

