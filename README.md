# Predicting Bike Sharing Patterns With Our First Neural Network Architecture

Udacity Deep Learning Nanodegree Project #1.

* This repo is about how to make predictions about Bike Sharing Patterns with our first built Neural Network.
* You can refer to Original Udacity repo [here](https://github.com/udacity/deep-learning-v2-pytorch); in project-bikesharing folder.

# Dataset Background

Bike sharing systems are new generation of traditional bike rentals where whole process from membership, rental and return back has become automatic. Through these systems,user is able to easily rent a bike from a particular position and return back at another position. Currently, there are about over 500 bike-sharing programs around the world which is composed of over 500 thousands bicycles. Today, there exists great interest in these systems due to their important role in traffic, environmental and health issues.

Apart from interesting real world applications of bike sharing systems, the characteristics of data being generated by these systems make them attractive for the research. Opposed to other transport services such as bus or subway, the duration of travel,departure and arrival position is explicitly recorded in these systems. This feature turns bike sharing system into a virtual sensor network that can be used for sensing mobility in the city. Hence, it is expected that most of important events in the city could be detected via monitoring these data.

# Project Overview

In this project, using the Bike-sharing provided dataset along with Neural Network Algorithms, I built a Neural Network and used it to predict daily bike rental ridership. The Neural Network was built from "scratch", using only NumPy to assist.

# Project Objective

The objective of this project is to build and train neural networks from scratch to predict the number of bikeshare users on a given day.

# Table Of Contents

* Introduction
* About The Dataset
* Dataset Description 
* Data Pre-Processing And Cleaning
* Creating Dummy Variables
* Standardizing The Continuous Variables
* Splitting The Data Into Train, Validation And Test Datasets
* Build The Neural Network
* Training The Neural Network
* Trained Network Results
* Prediction Results
* Installation
* Usage

1.   Introduction
     
     In this project, you'll get to build a neural network from scratch to carry out a prediction problem on a real dataset! By building a neural network from the ground up,          you'll have a much better understanding of gradient descent, backpropagation, and other concepts that are important to know.
     
     The data comes from the [UCI Machine Learning Database](https://archive.ics.uci.edu/ml/datasets/Bike+Sharing+Dataset)
     
2.   About The Dataset

     Bike-sharing rental process is highly correlated to the environmental and seasonal settings. For instance, weather conditions, precipitation, day of week, season, hour of        the day, etc. can affect the rental behaviors. The core data set is related to the two-year historical log corresponding to years 2011 and 2012 from Capital Bikeshare            system, Washington D.C., USA which is publicly available in http://capitalbikeshare.com/system-data. We aggregated the data on two hourly and daily basis and then extracted      and added the corresponding weather and seasonal information. Weather information are extracted from http://www.freemeteo.com.
     
3.   Dataset Description

     * hour.csv : bike sharing counts aggregated on hourly basis. Records: 17379 hours
     * day.csv : bike sharing counts aggregated on daily basis. Records: 731 days
     
     Both hour.csv and day.csv have the following fields, except hr which is not available in day.csv
	
	- instant: record index
	- dteday : date
	- season : season (1:springer, 2:summer, 3:fall, 4:winter)
	- yr : year (0: 2011, 1:2012)
	- mnth : month ( 1 to 12)
	- hr : hour (0 to 23)
	- holiday : weather day is holiday or not (extracted from http://dchr.dc.gov/page/holiday-schedule)
	- weekday : day of the week
	- workingday : if day is neither weekend nor holiday is 1, otherwise is 0.
	+ weathersit : 
		- 1: Clear, Few clouds, Partly cloudy, Partly cloudy
		- 2: Mist + Cloudy, Mist + Broken clouds, Mist + Few clouds, Mist
		- 3: Light Snow, Light Rain + Thunderstorm + Scattered clouds, Light Rain + Scattered clouds
		- 4: Heavy Rain + Ice Pallets + Thunderstorm + Mist, Snow + Fog
	- temp : Normalized temperature in Celsius. The values are divided to 41 (max)
	- atemp: Normalized feeling temperature in Celsius. The values are divided to 50 (max)
	- hum: Normalized humidity. The values are divided to 100 (max)
	- windspeed: Normalized wind speed. The values are divided to 67 (max)
	- casual: count of casual users
	- registered: count of registered users
	- cnt: count of total rental bikes including both casual and registered   

4.  Data Pre-Processing And Cleaning

    The Bike-Sharing Dataset consists of 17379 records and 17 columns with no duplicate or null values. And the unnecessary columns such as 'instant', 'dteday', 'season',           'weathersit', 'weekday', 'atemp', 'mnth', 'workingday', 'hr' are dropped. 
    
5.  Creating Dummy Variables

    The categorical columns such as 'season', 'weathersit', 'mnth', 'hr', 'weekday' are converted into dummies as they will be used in model building.

6.  Standarzing The Continuous Variables   

    To make training the network easier, I've standardized 'casual', 'registered', 'cnt', 'temp', 'hum', 'windspeed', each of the continuous variables. That is, I've shifted and     scale the variables such that they have zero mean and a standard deviation of 1.
     
7.  Splitting The Data Into Train, Validation And Test Datasets

    I've saved the data for the last approximately 21 days to use as a test set after I've trained the network. I've used this set to make predictions and compared them with         the actual number of riders.
     
    I've splitted the data into two sets, one for training and one for validating as the network is being trained. Since this is time series data, I've trained on historical         data, then tried to predict on future data (the validation set).
  
8.  Build The Neural Network

    Finally I built the Neural Network in addition to implementing both the forward pass and backwards pass through the network. I also set the hyperparameters: the learning         rate, the number of hidden units, and the number of training passes.

    ![](./assets/neural_network.png)
    
    The network has two layers, a hidden layer and an output layer. The hidden layer will use the sigmoid function for activations. The output layer has only one node and is         used for the regression or classification, the output of the node is the same as the input of the node. That is, the activation function is  𝑓(𝑥)=𝑥 . A function that takes       the input signal and generates an output signal, but takes into account the threshold, is called an activation function. We work through each layer of our network               calculating the outputs for each neuron. All of the outputs from one layer become inputs to the neurons on the next layer. This process is called forward propagation.

    I used the weights to propagate signals forward from the input to the output layers in a neural network. I used the weights to also propagate error backwards from the output     back into the network to update our weights. This is called backpropagation.
    
    
    
    Neural networks are extremely powerful in finding complex patterns in datasets. The feedforward neural network consists of a number of fully connected layers:

    * The input layer consists of the variables used for the prediction task.
    * An optional number of "hidden" layers, each of which analyzes the patterns of the data from the previous layer.
    * An output layer that combines the results of the last hidden layer and produces the prediction (classification or regression).
    The layers in the neural network being fully connected means that every node in every hidden layer processes information from all nodes from the previous layer. In the first     hidden layer, this means processing the input data; in subsequent hidden layers, this means processing, combining data from previous hidden layers. Then when this is all         done, the network checks its accuracy against known samples and backpropagates prediction error, gradually changing the weights between nodes in the network until ample         accuracy is achieved. This is how a neural network can identify complex relationships in datasets.

    In this particular case, the dataset presented a quite complex time series with several, and also partially cyclical fluctuations. I utilized only 1 hidden layer and 10         nodes to capture the variability of demand. In the end, as can be seen in the notebook, the prediction is quite accurate for most of the time periods, with a slight dimness     around the Festive Season. This is due to the fact that the training data didn't include much information of previous Festive Seasons and as such, couldn't train properly       for this scenario.
    
    Finally I built the Neural Network in addition to implementing both the forward pass and backwards pass through the network. I also set the hyperparameters: the learning         rate, the number of hidden units, and the number of training passes.
    
 9. Training The Neural Network

    Before Training the network, we need to run a unit test to ensure the correctness of the network implementation. I have set the hyperparmeters by choosing the number of         iterations,the learning rate and the number of hidden nodes.
    * The number of epochs(=2000) is chosen such that the network is trained well enough to accurately make predictions but is not overfitting on the training data.
    * The number of hidden units(=10) is chosen such that the network is able to accurately predict the number of bike riders, is able to generalize, and is not overfitting.
    * The learning rate(=1.0) is chosen such that the network successfully converges, but is still time efficient.
    * The number of output nodes(=1) is properly selected to solve the desired problem.
    
10. Trained Network Results
    
    Lastly, the Neural Network is initialized and trained. Its performance for training and validation loss can be seen in the image below.
    
    ```bash
    Progress: 100.0% ... Training loss: 0.068 ... Validation loss: 0.142
    ```
    ![Center Image](./Neuralnetwork_Output_Images/result_training.png)
    
11. Prediction Results
     
    Finally, the Neural Network is run against unseen test data and predictions can be seen in the image below.

    ![](./Neuralnetwork_Output_Images/result_prediction.png)
    
12. Installation

    For best experience with managing dependency I advise you to install [Anaconda](https://docs.anaconda.com/anaconda/install/) or [miniconda](https://docs.conda.io/projects/continuumio-conda/en/latest/user-guide/install/download.html)
    
    Create A Virtual Environment With Conda
    
    ```bash
    conda create --name deep-learning python=3
    ```
    
    Activate Environment
    
    ```
    conda activate deep-learning
    ```
    
    Install Dependencies
    
    ```
    pip install -r requirements.txt
    ```
    
    Download Or Clone This Project_Predicting_Bike_Sharing_Patterns Repository. Launch The App With Jupyter-Notebook.
    
    ```
    jupyter-notebook Your_first_neural_network.py
    ```
    
 13. Usage

     Run all code cells in the notebook. Optionally have a glance at the file `my_answers.py`.
     
 # Conclusion
 
   The predictions given by the model are quite accurate. However, the model overestimates bike ridership in December because it hasn't had sufficient holiday season training      examples.
    


    
     

      
