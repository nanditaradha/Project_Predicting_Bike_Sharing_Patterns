# Predicting Bike Sharing Patterns With Our First Neural Network Architecture

Udacity Deep Learning Nanodegree Project #1.

* This repo is about how to make predictions about Bike Sharing Patterns with our first built Neural Network.
* You can refer to Original Udacity repo[here](https://github.com/udacity/deep-learning-v2-pytorch);in project-bikesharing folder.

# Dataset Background

Bike sharing systems are new generation of traditional bike rentals where whole process from membership,rental and return back has become automatic.Through these systems, user is able to easily rent a bike from a particular position and return back at another position.Currently,there are about over 500 bike-sharing programs around the world which is composed of over 500 thousands bicycles.Today,there exists great interest in these systems due to their important role in traffic,environmental and health issues.

Apart from interesting real world applications of bike sharing systems,the characteristics of data being generated by these systems make them attractive for the research.Opposed to other transport services such as bus or subway,the duration of travel,departure and arrival position is explicitly recorded in these systems.This feature turns bike sharing system into a virtual sensor network that can be used for sensing mobility in the city.Hence,it is expected that most of important events in the city could be detected via monitoring these data.

# Project Overview

In this project,using the Bike-sharing provided dataset along with Neural Network Algorithms,i built a Neural Network and used it to predict daily bike rental ridership.The Neural Network was built from "scratch",using only NumPy to assist.

# Project Objective

The objective of this project is to build and train neural networks from scratch to predict the number of bikeshare users on a given day.

# Table Of Contents

* Introduction
* Dataset
* Dataset Description 
* Data Pre-Processing And Cleaning
* Creating Dummy Variables
* Standardizing The Continuous Variables
* Splitting The Data Into Train,Validation And Test Datasets
* Build The Neural Network
* Training The Neural Network
* Mpdel Evaluation
* Model Results

## 1.Introduction
     
     In this project,you'll get to build a neural network from scratch to carry out a prediction problem on a real dataset! By building a neural network from the ground up,          you'll have a much better understanding of gradient descent,backpropagation,and other concepts that are important to know.
     
## 2.Dataset

     Bike-sharing rental process is highly correlated to the environmental and seasonal settings.For instance,weather conditions,precipitation,day of week,season,hour of              the day,etc. can affect the rental behaviors.The core data set is related to the two-year historical log corresponding to years 2011 and 2012 from Capital Bikeshare system,      Washington D.C., USA which is publicly available in http://capitalbikeshare.com/system-data.We aggregated the data on two hourly and daily basis and then extracted and          added the corresponding weather and seasonal information.Weather information are extracted from http://www.freemeteo.com.
     
## 3.Dataset Description

     * hour.csv : bike sharing counts aggregated on hourly basis.Records: 17379 hours
     * day.csv : bike sharing counts aggregated on daily basis.Records: 731 days
     
	   Both hour.csv and day.csv have the following fields, except hr which is not available in day.csv

     instant: record index
     dteday : date
     season : season (1:springer, 2:summer, 3:fall, 4:winter)
     yr : year (0: 2011, 1:2012)
     mnth : month ( 1 to 12)
     hr : hour (0 to 23)
     holiday : weather day is holiday or not (extracted from http://dchr.dc.gov/page/holiday-schedule)
     weekday : day of the week
     workingday : if day is neither weekend nor holiday is 1, otherwise is 0.
     weathersit :
      - 1: Clear, Few clouds, Partly cloudy, Partly cloudy
      - 2: Mist + Cloudy, Mist + Broken clouds, Mist + Few clouds, Mist
      - 3: Light Snow, Light Rain + Thunderstorm + Scattered clouds, Light Rain + Scattered clouds
      - 4: Heavy Rain + Ice Pallets + Thunderstorm + Mist, Snow + Fog
     temp : Normalized temperature in Celsius. The values are divided to 41 (max)
     atemp: Normalized feeling temperature in Celsius. The values are divided to 50 (max)
     hum: Normalized humidity. The values are divided to 100 (max)
     windspeed: Normalized wind speed. The values are divided to 67 (max)
     casual: count of casual users
     registered: count of registered users
     cnt: count of total rental bikes including both casual and registered

## 4.Data Pre-Processing And Cleaning

     The Bike-Sharing Dataset consists of 17379 records and 17 columns with no duplicate or null values.And the unnecessary columns such as 'instant', 'dteday', 'season',            'weathersit', 'weekday', 'atemp', 'mnth', 'workingday', 'hr' are dropped. 
     
## 5.Creating Dummy Variables

     The categorical columns such as 'season', 'weathersit', 'mnth', 'hr', 'weekday' are converted into dummies as they will be used in model building.

## 6.Standarzing The Continuous Variables   

     To make training the network easier,I'll standardize 'casual', 'registered', 'cnt', 'temp', 'hum', 'windspeed', each of the continuous variables.That is,we'll shift and        scale the variables such that they have zero mean and a standard deviation of 1.
     
## 7.Splitting The Data Into Train,Validation And Test Datasets

     I'll save the data for the last approximately 21 days to use as a test set after I've trained the network.I'll use this set to make predictions and compare them with            the actual number of riders.
     
     I've splitted the data into two sets,one for training and one for validating as the network is being trained. Since this is time series data,I'll train on historical            data,then try to predict on future data (the validation set).
  
## 8.Build The Neural Network

     ![](assets/neural_network.png)
 
