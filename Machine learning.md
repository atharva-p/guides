# Unit 1 

# What is machine learning? 

Designing mathematical models that allows computers to learn from data and perform tasks without being explicitly programmed. 

Basic developmental steps of a machine learning model 
1. Data collection 
2. Data preprocessing - label the data, clean the data, etc 
3. Train the model 
4. Test the model's performance (also called as validation) 

# Why machine learning? 

_to be written_ 

# Types of machine learning methods 

1. Supervised learning - model gets to train on data that is labelled. Data labelling adds meaningful information or context to the data so that the machine learning model can learn from it. Other definitions of labelled data: input data that is accompanied by the desired output data. Used for classification or regression. 
2. Unsupervised learning - model gets unlabeled data to train on. In this, the model tries to figure out patterns in data without explicit guidance. Used for clustering
3. Semi supervised learning - model trains on both labelled and unlabeled data.
4. Reinforcement learning - model trains in an environment where it receives feedback in the form of rewards or punishments. 

# Noise in data 

Noise refers to irrelevant or random variation in data that doesn't represent any meaningful pattern

# [Bias and Variance](https://youtu.be/EuBBz3bI-aA) 

## Bias 

Bias is how well the mathematical prediction function of our ML model fits the actual function of the relationship. 

For example, if we have a straight line as our ML model and the actual relationship is a curve, our bias will be high as the ML function does not fit with the actual function of the relationship

Another ML model may have a squiggly line (_lines that bend and curve in an irregular way_) that hugs our training data. In our words the ML model function fits well with the function of the actual relationship. This model has a low bias 

## Variance 

Variance is how much an ML model varies in accuracy with different data sets. 

Using the same example, the linear straight line (which has high bias) will have low variance because the ML function will not strictly follow only the training data points, and hence will be able to perform on the testing data set too. We say that this model has a low variance. 

On the other hand, the squiggly line, even though fits the actual function very well, does so by hugging itself to only the data points from the training dataset. The ML function won't be able to perform on testing data as it's bound heavily to the training data points. Hence, this model will have a high variance. 

# Overfitting and underfitting 

## Overfitting

Because the squiggly line performs for the training data but not for the testing data, we say that the model is overfit. 

An overfit model has **low bias** (because it can fit close with the actual relationship function) and **high variance** (because it performs poorly when you change the data set). 

## Underfitting 

The straight line can perform on both the training and testing data sets with similar accuracy (low variance) but does not fit well to the actual relationship, meaning the predictions are not close to ideal (high bias). A model which has **high bias and low variance** is an underfit model  

## Ideal model 

The ideal model is somewhere in the middle of underfitting and overfitting. 

An ideal ML model can accurately model the true relationship, which means it has low bias. It also has low variability (or low variance), by producing consistent predictions across different data sets. 



