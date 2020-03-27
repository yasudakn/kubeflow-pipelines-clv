# Predicting Customer Lifetime Value with Kubeflow Pipelines

## Overview

This repository maintains code samples accompanying the **Predicting Customer Lifetime Value with Kubeflow Pipelines** reference guide.

The **Predicting Customer Lifetime Value** reference guide  discusses operationalization of Customer Lifetime Value (CLV) modeling techniques described in the [Predicting Customer Lifetime Value with AI Platform](https://cloud.google.com/solutions/machine-learning/clv-prediction-with-offline-training-intro) series of articles.

The primary goal of the guide is to demonstrate how to orchestrate two Machine Learning workflows:
- The training and deployment of the Customer Lifetime Value predictive model.
- Batch inference using the deployed Customer Lifetime Value predictive model.

The below diagram depicts the high level architecture:

![KFP Runtime](./images/arch-final.png)


## Deploying Kubeflow Pipelines

The guide has been developed and tested on [AI Platform Pipelines](https://cloud.google.com/ai-platform/pipelines/docs). 

You can run also run the pipelines on a full [Kubeflow](https://www.kubeflow.org/) installation  or on a [standalone deployment of Kubeflow Pipelines](https://www.kubeflow.org/docs/pipelines/installation/standalone-deployment/)

Refer to [README](./install/README.md) in the `/install` folder of this repo for the instructions on how to deploy and configure **AI Platform Pipelines**.

## Building and deploying 

The building and deploying of the solution components has been automated using **Cloud Build**. 

Refer to [README](./deploy/README.md) in the `/deploy` folder of this repo for the detailed deployment instructions.

## Running the pipelines

There are two ways to run the solution's pipelines:
- Using Kubeflow Pipelines UI
- Using KFP SDK

Refer to [README](./run/README.md) in the `/run` folder of this repo for detailed instructions on how to trigger runs.

## Repository structure

`/pipelines`
The source code for two template KFP Pipelines:
- The pipeline that automates CLV model training and deployment
- The pipeline that automates batch inference 


`/components`

The source code for the KFP components that wrap selected **AutoML Tables** APIs.

`/install`

Kubeflow Pipelines  installation script

`/deploy`

Cloud Build configuration for automated building and deployment.

`/run`

Sample code demonstrating how to use the `kfp.Client()` programmatic interface to KFP services.



## Acknowledgements

The sample dataset used in the samples is based on the publicly available [Online Retail Data Set](http://archive.ics.uci.edu/ml/datasets/Online+Retail) from the UCI Machine Learning Repository. 

The original dataset was preprocessed to conform to the the schema used by the solution's pipelines and uploaded to a public GCP bucket as `gs://clv-datasets/transactions/`. 



