# Analyzing Credit Risk with Cloud Pak for Data

Welcome to our workshop! In this workshop we'll be using the [Cloud Pak for Data](https://dataplatform.cloud.ibm.com/docs/content/wsj/getting-started/overview-cpdaas.html?context=analytics) platform to Collect Data, Organize Data, Analyze Data, and Infuse AI into our applications.

## About this workshop

In this workshop we will be using a credit risk / lending scenario. In this scenario, lenders respond to an increased pressure to expand lending to larger and more diverse audiences, by using different approaches to risk modeling. This means going beyond traditional credit data sources to alternative credit sources (i.e. mobile phone plan payment histories, education, etc), which may introduce risk of bias or other unexpected correlations.

The credit risk model that we are exploring in this workshop uses a training data set that contains 20 attributes about each loan applicant. The scenario and model use synthetic data based on the [UCI German Credit dataset](https://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)). The data is split into three CSV files and are located in the [data]({{ site.baseurl}}/data/split) directory of the GitHub repository.

## Agenda

| Topic | Description | Type |
| :--- | :--- | :--- |
| Introduction | Course/Workshop Introduction | Lecture |
| Platform Overview | Cloud Pak for Data overview | Lecture |
| Environment Setup | Environment provisioning and setup | Hands-on lab |
| Data Wrangling | Data wrangling overview | Lecture |
| Data Wrangling using Data Refinery  | Data aggregation, processing and wrangling | Hands-on lab |
| Machine Learning  | Machine Learning overview | Lecture |
| Automated ML with AutoAI | Build and save predictive models using AutoAI | Hands-on lab |
| Model Deployment  | Model Deployment overview | Lecture |
| Online Deployment & Testing | Deploy a model for real time predictions | Hands-on lab |
| Batch Deployment & Testing | Deploy a model for batch procesing | Hands-on lab |
| Model Integration to Python Application | Invoke model endpoint from an application | Hands-on lab |
| Trusted AI | Trusted AI Overview | Lecture |
| Trust and Transparency | Using the AIF360 and AIX360 toolkits | Hands-on lab |
| Model Versioning | Updating Models Overview | Lecture |
| Versioning Models and Deployments | Update ML models | Hands-on lab |
| Prescriptive Models | Decision Optimization (DO) Overview | Lecture |
| Building and Deploying a DO Model | Use CPLEX to build a model and deploy to WML | Hands-on lab |
| Conclusion | Wrap up discussion | Lecture |

## Compatability

This workshop has been tested on the following platforms:

* **macOS**: Mojave (10.14), Catalina (10.15)
  * Google Chrome version 81
