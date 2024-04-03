+++
image = "img/portfolio/PredictiveModelAlcohol.png"
showonlyimage = false
date = "2023-12-15T19:57:40+05:30"
title = "Predictive Modeling: Classifying Alcoholic Status"
draft = false
weight = 2
+++

Used random forest, gradient boosting, principal component analysis, logistic regression, and neural net models to select the best classification model to predict the Alcoholic Status of an individual based on their vital signs.

<!--more-->

---

> The code for this project can be found in [this GitHub repository](https://github.com/acwilb/Classification-Predictive-Modeling-Project). All data cleaning, analysis, and visualizations were done in R.

---

#### Introduction

Alcohol addiction and its associated health impacts are a significant public health concern in many countries around the world. Notably, over half of all American adults have a family history of problem drinking or alcohol addiction. Annually, the U.S. grapples with an alarming estimate of 88,000 deaths directly attributed to alcohol-related causes, a stark indicator of the negative impact of alcohol on public health and societal well-being.

The purpose of this project is to create the best classification model to predict an individual's alcoholic status based on their vital signs. This was done as a final project and part of a time-constrained data modeling competition.

#### The Data

The dataset used in this project comes from the National Health Insurance Service in Korea. The data consists of training and testing datasets, each containing 26 predictors corresponding to vital signs in the human body. The training dataset consists of 70,000 observations, while the testing dataset includes 30,000 observations.

By applying a combination of different imputations of missing values, feature selection, and modeling techniques, the goal is to develop a model that can accurately predict individuals’ alcoholic status.

#### Model Exploration: Best Models

##### Random Forest

Using R's [randomForest package](https://cran.r-project.org/web/packages/randomForest/index.html), we begin by imputing NA values using the na.roughfix() function -- replacing NA values for numerical predictors with the column medians and replacing NA values for categorical predictors with the column modes.

Creating a Random Forest classifier using the training dataset with NA values imputed in this way resulted in the highest testing data accuracy of the entire project. Using Alcoholic Status as the response variable, all predictor variables in the dataset, the parameters **importance = TRUE** and **ntree = 1000**, the model tried 5 variables at each split and obtained an OOB error rate of 27.4%.

This method was very computationally expensive, but did not require much fixing of the parameters to obtain the highest accuracy possible. When running this model on the testing data, we obtain an accuracy of 72.953%.

![Best mtry Plot](/img/alcpred/mtry.png)

Applying the tuneRF() function to the data in order to find the best mtry parameter for the Random Forest model confirmed that the mtry parameter value that would give the lowest OOB error is **mtry = 5**.

##### Gradient Boosting

Using R's [gmb package](https://cran.r-project.org/web/packages/gbm/gbm.pdf), we fit a generalized boosted regression model using Alcoholic Status as the response variable, all predictor variables in the dataset, and the parameters **distribution = "bernoulli"**, **n.trees = 2500**, and **interaction.depth = 6**.

![GBM Relative Influence Plot](/img/alcpred/gbm.png)

Based on the plot of relative influence and the summary of the GBM output, we see that the predictors Smoking Status, Age, Sex, and Gamma GTP levels are the top 4 most influential in predicting an individual's alcoholic status.

Based on the confusion matrix from the GBM model, the training data accuracy for this model was 81.65%, while the testing data accuracy was 72.27%, indicating overfitting of this particular model. It should also be noted that this model used the original data, including the NA values.

#### Model Exploration: Other Methods Tried

##### Numeric Feature Selection - Principal Component Analysis

Using R's princomp() function, scaling the numeric values of the training dataset, the first four principal components were shown to be the most significant since they explain almost 90% of the total variance.

![PCA Scree Plot](/img/alcpred/screeplot.png)

The scree plot of the PCA visualizes the importance of each principal component, and in this case tells us to retain the first four principal components in our analysis.

![PCA Cos2 Plot](/img/alcpred/PCAcos2.png)

The cos2 visualization shows use how much each predictor contributes to the four most significant principal components. We see that the predictors **triglyceride**, **gamma GTP**, **total cholesterol**, **LDL cholesterol**, **SGOT ALT**, and **SGOT AST** appear to be the most significant predictors in the data set.

##### Categorical Feature Selection - Random Forest

After fitting a Random Forest model to the training data, we examine the variable importance of this model's output to determine which categorical variables to retain for our analysis.

![RF Importance Plot](/img/alcpred/RFimportance.png)

Based on the variable importance plot using the Random Forest model, the most significant categorical variables are **Smoking Status**, **Sex**, and **Age**.

##### Logistic Regression using Selected Predictors

Using R's glm() function to fit a generalized linear model to the training data subsetted to the most important predictors, the training data accuracy is 69.59% and the testing data accuracy is 69.41%.

##### Random Forest using Selected Predictors

Once again using R's randomForest package, we fit the Random Forest model to the training data subsetted to the most important predictors to get a training data accuracy of 70.26% and a testing data accuracy of 72.81%.

#### Limitations

The purpose of this project was to gain experience in working with many different machine learning predictive models, and most of the emphasis was placed on the learning process rather than the final result of the models. In addition, this project was constrained by a given time limit for the Data Mining & Statistical Models course final project Kaggle competition. Therefore, some of the more computationally expensive models could not be explored to their fullest potential given the time constraints.

##### Multicollinearity

Given that the predictors in this dataset were measures of an individual's vital signs, many of these variables were naturally highly correlated.

![Correlation Plot](/img/alcpred/correlation.png)

Based on the corrlation plot for all predictors, we see that weight is highly correlated with height, waistline, and BMI, while total cholesterol is highly correlated with LDL cholesterol. Attempts to take these highly correlated variables out of the training dataset resulted in lower accuracy of the fitted models, leading to the decision to keep these correlated variables in the data.

##### Model Exploration

The models tried for this project included Logistic Regression, Linear Discriminant Analysis, Quadratic Discriminant Analysis, Decision Trees, KNN, Random Forest, Gradient Boosting, Ensemble Model, and Neural Net. The models that produced the most promising results were included in the project's analysis, while the results that were not promising were left out.

The models focused on for this project were very computationally expensive, so making adjustments to the models in order to improve accuracy took most of the time allotted for this competition.

##### Interpretability

Given that the final model that produced the highest accuracy is the Random Forest model, the results are harder to put into context since this model is notably non-interpretable. Achieving this accuracy came as a trade-off for interpretability of the results.
