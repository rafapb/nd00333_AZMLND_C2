# Operationalizing Machine Learning

This project is part of the Udacity Azure ML Nanodegree. In this project, I used Microsoft Azure to configure a cloud based ML model, deploy it, and consume it. I also created, published, and consumed a pipeline.

## Architectural Diagram

The main steps of the project are:

1. [Authentication](#step-1-authentication)
2. [Automated ML Experiment](#step-2-automated-ml-experiment)
3. [Deploy the best model](#step-3-deploy-the-best-model)
4. [Enable logging](#step-4-enable-logging)
5. [Swagger documentation](#step-5-swagger-documentation)
6. [Consume model endpoints](#step-6-consume-model-endpoints)
7. [Create and publish a pipeline](#step-7-create-and-publish-a-pipeline)

![Steps](/img/0-Steps.png)

## Key Steps

### Step 1 Authentication

Since I used the Udacity lab environment, this step was not necessary.

### Step 2 Automated ML Experiment

In this step, we run an AutoML experiment to find the best model. Azure [AutoML](https://docs.microsoft.com/en-us/azure/machine-learning/concept-automated-ml) is a service that runs experiments to find the best model in a very efficient way.

First, the dataset needs to be uploaded.

![Dataset](/img/2.1-Dataset.png)

This dataset contains data about direct marketing campaings (phone calls) of a Portuguese banking institution.  
The dataset used can be downloaded [here](https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv).

A detailed description of the data features can be found [here](https://archive.ics.uci.edu/ml/datasets/bank+marketing#).

Then, the AutoML experiment is run on a compute cluster.

![AutoML](/img/2.2-AutoML.png)

We can see that the best model is a Voting Ensemble with an AUC of 0.94773, which consists of an ensemble of LighGBM and XGBoost classifiers.

![BestMpdel](/img/2.3-BestModel.png)

### Step 3 Deploy the best model

The, we deploy the best model using [Azure Container Instances](https://docs.microsoft.com/en-us/azure/container-instances/container-instances-overview). By using the Azure Container Instance, we can pack all the dependencies and deploy the model, ensuring that it will work on any machine.

Deploying the model delivers it into production. It allows us to interact with the model via an HTTP endpoint by sending data over POST requests.

![Deployment](/img/3.1-Deployment.png)

![DeploymentSuccess](/img/3.2-DeploymentSuccess.png)

### Step 4 Enable logging

In this step, we enable Applications Insights to retrieve logs. 

We deployed the model in production but we did not enable logging since we wanted to do so after deployment using Python SDK.

We [enable app insights](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-enable-app-insights) by running the code in the logs.py file. Enabling apps insights allows us to collect data from the endpoint (output data, responses, requests rates, response times, failure rates, depenency rates, reponse times, failure rates, and exceptions).

![Logs](/img/4.1-Logs.png)

![Logs2](/img/4.2-Logs2.png)

![EnabledAppInsights](/img/4.3-EnabledAppInsights.png)

![AppInsights](/img/4.4-AppInsights.png)

### Step 5 Swagger documentation

In this step, we consumed the consume the deployed model using [Swagger](https://swagger.io/). The Swagger documentation describes the REST API using JSON.

After downloading the swagger.json file from Azure, we ran swagger.sh and serve.py to generate the swagger documentation.

![Swagger](/img/5.1-Swagger.png)
![Serve](/img/5.2-Serve.png)

Then, we can access the Swagger documentation in the specified port of our computer.

![SwaggerDoc1](/img/5.3-SwaggerDoc1.png)
![SwaggerDoc2](/img/5.4-SwaggerDoc2.png)

### Step 6 Consume model endpoints

In this step, we interact with the trained model via an [endpoint](https://docs.microsoft.com/en-us/azure/machine-learning/concept-endpoints). An endpoint allows us to send data and receive the prediction output of the deployed model.

We modify the endpoint.py script to match the scoring_uri and key of the deployed model.

![Endpoint1](/img/6.1-Endpoint1.png)

The script contains test data and the endpoint returns the prediction and a data.json file.

![Endpoint2](/img/6.2-Endpoint2.png)
![Endpoint3](/img/6.3-Endpoint3.png)

The Test section of the endpoint also allows us to test our endpoint and see the returned values.

![Endpoint4](/img/6.3-Endpoint4.png)
![Endpoint5](/img/6.4-Endpoint5.png)

### Step 7 Create and publish a pipeline

In this step, we create, publish, and consume a pipeline using a Jupyter Notebook. The Jupyer Notebook was provided by Udacity and the code was updated to match the environment we were working in. Also, the config.json file was uploaded in the same working directory as the notebook.

![PublishPipeline1](/img/7.1-PublishPipeline1.png)
![PublishPipeline2](/img/7.2-PublishPipeline2.png)
![PublishPipeline3](/img/7.3-PublishPipeline3.png)
![PublishPipeline4](/img/7.4-PublishPipeline4.png)
![PublishPipeline5](/img/7.4-PublishPipeline5.png)
![PublishPipeline6](/img/7.4-PublishPipeline6.png)

## Screen Recording

The screencast of this project can be found [here](https://drive.google.com/file/d/1GwUTYVcTUuWFUOn4WuH_HbF-_FMkAjXG/view?usp=sharing).

## Future Work

* Perform an exploratory data analysis of the dataset.
* Perform feature engineering on the dataset.
* Export the model to support [ONNX](https://docs.microsoft.com/en-us/azure/machine-learning/concept-onnx).
* Retrain the model periodically with more recent data and [monitor data drift](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-monitor-datasets?tabs=python).
