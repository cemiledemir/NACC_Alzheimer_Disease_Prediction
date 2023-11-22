# NACC_Alzheimer_Disease_Prediction

Alzheimer's disease is a progressive neurologic disorder. Alzheimer's disease is the most common cause of dementia — a continuous decline in thinking, behavioral and social skills that affects a person's ability to function independently. In this project we are aiming to develop a model to predict different progressive levels of Alzheimer's Disease (AD) by using the real dataset provided by **National Alzheimer's Coordinating Center (NACC)**. The dataset contains 4 different progressive levels of AD which is 0.0: no impairment, 0.25: questionable impairment, 0.5:Mild impairment and 1.0: Moderate & Severe impairment. In this challenge, we will try to use the tensorflow library to develop a basic Sequential model.
In multi-class classification, we have one basic assumption that our data can belong to only one label out of all the labels we have. Since the disease level classes are mutually exclusive, this is a multi-class classification problem.


**The first thing we do is to analyze data.**

The dataset consists of 9180 individuals. There are 38 columns in the dataset. There are no missing values. When we look at the distribution of disease levels: 

![Screenshot 2023-11-22 164807](https://github.com/cemiledemir/NACC_Alzheimer_Disease_Prediction/assets/52001813/bfd35cfe-938f-4cbd-bc1f-a5e93b3a133c)
