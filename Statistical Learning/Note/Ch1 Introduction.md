## Introduction

###  Supervised Learning 

- Outcome measurement Y (also called dependent variable,response, target).    
- Vector of p predictor measurements X (also called inputs,regressors, covariates, features, independent variables).    
- In the regression problem, Y is quantitative (e.g price,blood pressure).    
- In the classification problem, Y takes values in a finite,unordered set (survived/died, digit 0-9, cancer class of tissue sample).    
- We have training data (x 1 ,y 1 ),...,(x N ,y N ). These are observations (examples, instances) of these measurements.    

### Unsupervised Learning 

- No outcome variable, just a set of predictors (features) measured on a set of samples.    
- objective is more fuzzy — find groups of samples that behave similarly, find features that behave similarly, find linear combinations of features with the most variation.    
- difficult to know how well your are doing. 
- different from supervised learning, but can be useful as a pre-processing step for supervised learning. 

### Statistical Learning versus Machine Learning

There is much overlap — both fields focus on supervised and unsupervised problems:     
Machine learning has a greater emphasis on large scale applications and prediction accuracy.
Statistical learning emphasizes models and their interpretability, and precision and uncertainty.