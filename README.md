# Operationalizing Machine Learning

This project is part of the Udacity Azure ML Nanodegree. In this project, I used Microsoft Azure to configure a cloud based ML model, deploy it, and consume it. I also created, published, and consumed a pipeline.

## Architectural Diagram

The main steps of the project are:

1. [Authentication](#authentication)
2. [Automated ML Experiment](#automated-ml-experiment)
3. [Deploy the best model](#deploy-the-best-model)
4. [Enable logging](#enable-logging)
5. [Swagger Documentation](#swagger-documentation)
6. [Consume model endpoints](#6.-consume-model-endpoints)
7. [Create and publish a pipeline](#create-and-publish-a-pipeline)

![Steps](/img/0-Steps.png)


## Key Steps

# [1. Authentication](#authentication)

Since I used the Udacity lab environment, this step was not necessary.

2. [Automated ML Experiment](#automated-ml-experiment)

In this step, we run an AutoML experiment to find the best model.

First, the dataset needs to be uploaded.

![Dataset](/img/2.1-Dataset.png)

This dataset contains data about direct marketing campaings (phone calls) of a Portuguese banking institution.  
The dataset used can be downloaded [here](https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv).

A detailed description of the data features can be found [here](https://archive.ics.uci.edu/ml/datasets/bank+marketing#).

Then, the AutoML experiment is ran on a compute cluster.

![AutoML](/img/2.2-AutoML.png)

We can see that the best model is a Voting Ensemble with an AUC of 0.94773, which consists of an ensemble of LighGBM and XGBoost classifiers.

![BestMpdel](/img/2.3-BestModel.png)

3. [Deploy the best model](#deploy-the-best-model)

The best model can then be deployed using an Azure Container Instance.

Deploying the best model allows us to interact with the HTTP API service and to interact with the model by sending data over POST requests.

![Deployment](/img/3.1-Deployment.png)

![DeploymentSuccess](/img/3.2-DeploymentSuccess.png)

4. [Enable logging](#enable-logging)

In this step, we enable Applications Insights and retrieve logs.

![Logs](/img/4.1-Logs.png)

![EnabledAppInsights](/img/4.2-EnabledAppInsights.png)

![AppInsights](/img/4.3-AppInsights.png)


5. [Swagger Documentation](#swagger-documentation)

In this step, we consumed the consume the deployed model using Swagger.

After downloading the swagger.json file from Azure, we run swagger.sh and serve.py to generate the swagger documentation.

![Swagger](/img/5.1-Swagger.png)
![Serve](/img/5.2-Serve.png)

Then, we can access the Swagger documentation in the specified port of our computer.

![SwaggerDoc1](/img/5.3-SwaggerDoc1.png)
![SwaggerDoc2](/img/5.4-SwaggerDoc2.png)

# 6. Consume model endpoints

In this step, we interact with the trained model.

We modify the endpoint.py script to match the scoring_uri and key of the deployed model.

![Endpoint1](/img/6.1-Endpoint1.png)

The script contains test data and the endpoint returns the prediction and a data.json file.

7. [Create and publish a pipeline](#create-and-publish-a-pipeline)

In this step, we create, publish, and consume a pipeline using a Jupyter Notebook.

![PublishPipeline1](/img/7.1-PublishPipeline1.png)
![PublishPipeline2](/img/7.2-PublishPipeline2.png)
![PublishPipeline3](/img/7.3-PublishPipeline3.png)
![PublishPipeline4](/img/7.4-PublishPipeline4.png)


## Screen Recording

The screencast of this project can be found [here](https://drive.google.com/file/d/12YTh9X4dAiOMzdL5zE4RwyQP5XfGk2LW/view?usp=sharing).

## Future Work

* Perform an exploratory data analysis of the dataset.
* Perform feature engineering on the dataset.
* Export the model to support [ONNX](https://docs.microsoft.com/en-us/azure/machine-learning/concept-onnx).
