# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary
This dataset contains data about a [bank marketing dataset ](https://archive.ics.uci.edu/ml/datasets/Bank+Marketing) and we seek to predict whether a bank customer would for a term deposit or not, on the basis of available data. 

The best performing model turned out to be VotingEnsemble with the best metric of 0.9485. 

## Scikit-learn Pipeline

Pipeline Architecture primarily includes:
1. Data cleaning of the given dataset: before fitting the model.
2. Hyperparameter tuning: The hyperparameters were fine-tuned by using AzureML HyperDrive, and the primary metric goal was to maximize the metric output.
3. Classification Algorithm: Logistic Regression

The random sampler: RandomParameterSampling chooses values from a diversified uniform parameter space, to conduct a non-biased experiment. 

The early stopping policy: BanditPolicy, with a slack factor of 0.1  helps in saving the compute power, by pre-empting the model runs, which do not indicate the best model.

## AutoML

Some of the pipelines generated by AutoML: MaxAbsScaler LightGBM, MaxAbsScaler XGBoostClassifier
The best model: VotingEnsemble used optimized hyperpameters(generated from custom config and sampler) to come out with the best possible metric in the experiment.

We did not consider the hyperparameter space in the logistic regression model and it's constrained to a pre-defined logic, whereas AutoML, on the contrary considers the hyperparameter space and various models before choosing the best model. To improve the Logistic regression performance, the hyperparameter space needs to be tweaked uniformly for better results. This will enable the models to spend more time in finding models that can truly turn out to be the best models. To improve the AutoML performance, the early stopping policy can be optimised in a way to stop the execution of models which take excesively more time than the statistical mean of all the runs, at any moment of time. This will enable the models to spend more time in finding models that can truly turn out to be the best models.

## Pipeline comparison

Logistic regression model's accuracy: 0.9
AutoML best model's accuracy of 0.9485.  
AutoML model has a better accuracy by almost 5% 
As I mentioned earlier, we did not consider the hyperparameter space in the logistic regression model and it's constrained to a pre-defined logic, whereas AutoML, on the contrary considers the hyperparameter space and various models before choosing the best model.


## Future work
As I mentioned earlier, The early stopping policy: BanditPolicy, can be optimised in a way to stop the execution of models which take excesively more time than the statistical mean of all the runs, at any moment of time. This will enable the models to spend more time in finding models that can truly turn out to be the best models.
