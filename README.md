# Optimizing an ML Pipeline in Azure

## Overview

In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run. Using the [Bank Marketing Dataset](https://archive.ics.uci.edu/ml/datasets/Bank+Marketing) and the Azure ML Studio, the following steps are followed:

1. Input the dataset into Registered Datasets;
2. Create a compute instance;
3. Using the Python SDK and a Scikit-learn model (Logistic Regression), it is developed an Azure ML pipeline;
4. An AutoML run inside Azure ML Studio is then created to perform a series of experiments.

At the end of this project, we want to create a solid understanding about the Azure ML Studio and some important standard practices of MLops inside Azure platform.

## Summary

The dataset is related with direct marketing campaigns of banking institution. Usually, marketing campaigns are based on phone calls. Often, more than one contact to the same client was required, in order to access if the product (bank term deposit) would be ('yes') or not ('no') subscribed.

In this context, the best model was developed by the AutoML. The Voting Ensemble model had an accuracy of *0.91* and an weighted accuracy of *0.95*.

The chosen classification algorithm was Logistic Regression as it is a sample problem and the output is binary. With that said, a binary classification is a good fit for Logistic Regression. The hyperparameters to explore was the **Inverse of regularization strength** represented by the letter *C* and the **Maximum number of iterations** represented by *max_iter*. These hyperparameters are important because the play an important role on the algorithm conversion and regularization.

Finally, the early stopping policy was also defined based on slack criteria, and a frequency and delay interval for evaluation. This part is important to prevent the model from overfitting and also extra computational resources that is no longer needed if an especific target is set. We use the bandit policy because this policy early terminates any runs where the primary metric is not within the specified slack factor/slack amount with respect to the best performing training run.


## Scikit-learn Pipeline

For the Scikit-learn Pipeline a python script named *train.py* was developed. It was responsible to load the data and transform the necessary features and return a prepared dataset. Insided the Azure Hyperdrive, the algorith is passed with the two hyperparameters mentioned before (**Inverse of regularization strength** and **Maximum number of iterations**). These parameters are important for regularization and also convergense.

## AutoML

AutoML is a powerful tool for all machine learning professionals and it is incredible its flexibility. In this project, we set the AutoML configuration with accuracy as primary metric and cross validation. The cross validation is important to avoid overfitting and let the model to generalize the data better. For computational resources reasons, an experiment timeout of 30 minutes was set. 

## Pipeline comparison

After the training and validation of both models, AutoML performs better since the space of the hyperparameters search is more flexible. While in Scikit-learn Pipeline we have a close scope of hyperparameters or a more *hands on* way to improve the space of search, in AutoML we can select not only the hyperparameters but also the algorithms in a simple way just passing as an argument. It allows the Machine Learning engineers to focus on results and improve the business understanding and let the operation and orquestration on the cloud.

Both results are good for the given dataset, but AutoML performed better with an accuracy of *0.91* while Scikit-learn Pipeline had an accuracy of *0.90*

The architecture of both pipelines are different, but the ideas are close: Load the data, instanciate the infrastructure to compute, set the parameters and call the compute method. The main difference is the that using AutoML we have infitine possibilities to increase the search for a better algorithm or a hyperparameter combination.

## Future work

For improvements and future experiments it is important to explore other algorithms and validate more metrics. Accuracy in this case is very important, but also using a confusion matrix or a weighted accuracy can be important. Moreover, we can modify the experiments with other hyperparameters and increase the cross validation to enhance models performance and generalization.

Explainability is crucial in some areas. With that said, explore more this azure feature is important and interesting.
**What are some areas of improvement for future experiments? Why might these improvements help the model?**
