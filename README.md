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

![Screen Shot 0031-04-21 at 21 17 45](https://user-images.githubusercontent.com/49817101/56478147-f4f51180-647a-11e9-946c-1f1aba26fdef.png)
## PREDICTION
Our goal for this analysis is to maximize profit to correctly identify more people with CKD while maintaining reasonable accuracy for the screening tool. To make decision on which thresholds level to apply for our classification, we try to plot accuracy and profit with
different thresholds level. As we can see from the chart, we get the most accurate classification at threshold level 0.5. Our model could predict accurate probability of having CKD for 93% observations in the train data set. However, the cost associated with prediction model will go down drastically due to the fewest number of true positive the model can predict. In contrast, at threshold level 0.3, the cost we can get from prediction model will increase dramatically due to the huge increase in the number of total predicted true positive. However, at this threshold, the model get the lowest level of accuracy, just around 91%, which is still an acceptable accuracy level. Because our goal in this analysis is maximizing the profit, we apply threshold level at 0.3 to classify probability of having CKD among 2819 patients.

![Screen Shot 0031-04-21 at 21 19 53](https://user-images.githubusercontent.com/49817101/56478191-430a1500-647b-11e9-9f73-ad4c0097d66f.png)

### Confusion Matrix
Confusion matrix reflects changes in classification probability from logistic regression result. In Model 3, two confusion matrix were obtained to reflect accuracy level according to change in thresholds. When we decrease threshold to 0.3, there is an increase in both true positive and false positive while there is an huge decrease in number of true negative and false negative. Similarly the number of total true positive and false positive in model 4 also go up according change in thresholds level. We can see from these results below, model 4 only contains 8 variables but this model can predict good results compared to model 3 with 14 variables. This confirms the importance of all 8 variables in model 4 and based on these variables we built our screening tool.

![Screen Shot 0031-04-21 at 21 22 17](https://user-images.githubusercontent.com/49817101/56478223-9b411700-647b-11e9-9156-12dcd3bd6a6d.png)

Simplicity: The main objective for this screening tool is to be easy to use. Questions that are being asked in our
screening tool do not require any extra medical knowledge or exams except one’s demographic information and selfhealth
record. 
Accuracy: An accuracy check has been implemented on the training dataset. As a result, 88% of the population were correctly classified based on the points generated from our screening tool. The simple screening tool presented less accurate level compared to Model 3. This is because of shortages in some important variable such as HDL and PVD but it's quite impractical to ask in our survey. Appendix 4 shows the difference in prediction between screening tool and our full model.

![Screen Shot 0031-04-21 at 21 23 52](https://user-images.githubusercontent.com/49817101/56478246-d3e0f080-647b-11e9-98b5-92a1b2c9b96c.png)

## LIMITATIONS
Imputation approach was used to replace the missing value for generating a completed dataset for the model prediction. However, the imputing process might potentially weaken the validity of the result and lead us to bias interpretation on it. The significant factors we defined after replacing the missing values might differ from ones where the missing values are present. On the other hand, the dataset obtained also limit our ability to detect a perfect set of significant risk factors that put people at high risk of having CKD. For example, family history of kidney disease should be considered but this variable was not included in the dataset. To overcome the limitations mentioned above, a wider range of data needs to be included. In addition, certain considerable method to obtain data, such as developing clearer and straightforward questions for interviews, should be implemented to minimize the amount of missing values.


