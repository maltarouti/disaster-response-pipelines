# Disaster Response Pipelines

## Table of Content:
* [Project Overview](#project_overview)
* [Project Outline](#project_outline)
  * [Extract, Transform, and Load Pipeline](#etl_pipline)
  * [Machine Learning Pipleline](#machine_learning_pipeline)
  * [Flask Web app](#flask_app)
* [Training Dataset](#dataset)
* [Machine Learning Model](#model)
* [Files Structure](#files)
* [Requirments](#requirments)
* [Running Process](#running)
  * [Process Data](#process_data)
  * [Train Classifier](#train_classifier)
  * [Run the flask web app](#run_flask_app)
* [Conclusion](#conclusion)
* [Acknowledgements](#acknowledgements)

***
<a id='project_overview'></a>
## 1. Project Overview
Disaster response reduces possible losses from disasters and provide appropriate help to disaster victims. It is a continuous process in which governments, corporations, and civil society prepare for and mitigate the effects of catastrophes. An appropiate action at all disaster stages results in higher readiness, better warnings, and decreased susceptibility.

Social media applications are one of the best sources to get a quick overview of what is going on around the world, but it is difficult to go through everything on the internet. This project aims to help governments to filter millions of social media messages into categories by using a supervised machine learning model. The model is trained on [Figure Eight](https://appen.com/) dataset to categorize the messages into their right categories, so that the governments can respond to disasters quickly.

<a id='project_outline'></a>
## 2. Project Outline
This section explains all three parts of this project from cleaning the data to deploying the model on the flask app. 

<a id='etl_pipline'></a>
### 2.1 Extract, Transform, and Load Pipeline 
The Extract, Transform and Load (ETL) pipeline is responsible for preparing the dataset for the machine learning pipeline and wors as following:
* Extract the messages and their categories from the CSV files
* Clean and merge the messages and categories in one data frame
* Saves the data frame inside an SQLite database

<a id='machine_learning_pipeline'></a>
### 2.2 Machine Learning Pipleline 
The Machine Learning (ML) pipeline is responsible for creating the machine learning model pipeline and works as following:
* Load the dataset from the SQLite database 
* Create a machine learning pipeline that tokenizes and trains the SVM model on the training dataset 
* Evaluate the model on the testing dataset 
* Save the model as a pickle file 

<a id='flask_app'></a>
### 2.3 Flask Web App
Flask Web App is responsible for deploying the machine learning model on a website and allowing the user to use the trained model to do predictions.

![image](https://github.com/Murtada-Altarouti/Disaster-Response-Pipelines/blob/main/readme_images/website_example.png)

<a id='dataset'></a>
## 3. Training Dataset
The cleaned training dataset contains more than 26K labeled messages and has 36 different classes such as related, offer, food, water, and electricity. The following photo shows how many class the dataset has: ![image](https://github.com/Murtada-Altarouti/Disaster-Response-Pipelines/blob/main/readme_images/dataset.png)

<a id='model'></a>
## 4. The machine learning model
The macinhe learning model was built using [SVClinear](https://scikit-learn.org/stable/modules/generated/sklearn.svm.LinearSVC.html) from [scikit-learn](https://scikit-learn.org/) library. The model accruacy was calculated using [Numpy mean](https://github.com/Murtada-Altarouti/Disaster-Response-Pipelines/blob/1bd315ee829e9cda890a88b25fcce356198a1aa5/models/train_classifier.py#L101) which was equal to 95%. 

<a id='files'></a>
## 5. Files Structure
```
├── app #Website folder
│   ├── run.py #Responsible of running the website
│   └── templates
│       ├── go.html #Responsible of showing the results
│       └── master.html #The main page
|
├── data
│   ├── disaster_categories.csv #Categories dataset
│   ├── disaster_messages.csv #Messages dataset
│   ├── DisasterResponse.db #The cleaned dataset in SQLite database
│   └── process_data.py #Responsible for preparing the dataset 
|
├── models
│   ├── classifier.pkl #The SVM model
│   └── train_classifier.py #Responsible for creating the machine learning model
|
├── readme_images #This folder contains all images for the readme file
│   ├── dataset.png
│   └── website_example.png
└── README.md #Readme file 
```

<a id='requirments'></a>
## 6. Requirments
In order to to run this project, you must have [Python3](https://www.python.org/) installed on your machine. You also must have all listed libraries inside the `requirments.txt` so run the following command to install them: 
```
pip3 install -r requirments.txt
```

<a id='running'></a>
## 7. Running Process
This secions explains how to run each part of this project using command prompt or terminal

<a id='process_data'></a>
### 7.1 Process Data
You must be inside the `data` directory in order to run this command: 
```shell
python3 process_data.py disaster_messages.csv disaster_categories.csv <database_name>.db
```

<a id='train_classifier'></a>
### 7.2 Train Classifier 
You must be inside the `models` directory in order to run this command: 
```shell
python3 train_classifier.py ../data/<database_name>.db <model_name>.pkl
```

<a id='run_flask_app'></a>
### 7.3 Run the flask web app
You must be inside the `app` directory in order to run this command: 
```shell
python3 run.py
```
The link of the website will be `0.0.0.0:3001`

<a id='conclusion'></a>
## 8. Conclusion
In the conclusion, catastrophes are horrible if we are not properly prepared to deal with them, thus having a system that consistently delivers correct warnings is helpful to get an early notice of a potential disaster and decrease potential losses. The system was built using scikit-learn and achieved 95% accuracy, but that does not mean it is the best model. Testing different solutions such as [Reccurrent neural network](https://en.wikipedia.org/wiki/Recurrent_neural_network) may give a better result so, feel free to fork this repository and test different solutions.

<a id='acknowledgements'></a>
## 9. Acknowledgements
I would like to express my appreciation to Misk Academy and Udacity for the amazing work on the data science course and the support they give us to build this project
