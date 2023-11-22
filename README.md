# NACC_Alzheimer_Disease_Prediction

Alzheimer's disease is a progressive neurologic disorder. Alzheimer's disease is the most common cause of dementia — a continuous decline in thinking, behavioral and social skills that affects a person's ability to function independently. In this project we are aiming to develop a model to predict different progressive levels of Alzheimer's Disease (AD) by using the real dataset provided by **National Alzheimer's Coordinating Center (NACC)**. The dataset contains 4 different progressive levels of AD which is 0.0: no impairment, 0.25: questionable impairment, 0.5:Mild impairment and 1.0: Moderate & Severe impairment. In this challenge, we will try to use the tensorflow library to develop a basic Sequential model.
In multi-class classification, we have one basic assumption that our data can belong to only one label out of all the labels we have. Since the disease level classes are mutually exclusive, this is a multi-class classification problem.


**The first thing we do is to analyze data.**

The dataset consists of 9180 individuals. There are 38 columns in the dataset. There are no missing values. When we look at the distribution of disease levels: 

![Screenshot 2023-11-22 164807](https://github.com/cemiledemir/NACC_Alzheimer_Disease_Prediction/assets/52001813/bfd35cfe-938f-4cbd-bc1f-a5e93b3a133c)

Of the participants, %48.6 had no impairment, while %32 had questionable impairment, %12.3 had Mild impairment and %7.09 had Moderate & Severe impairment.

As we can see, the disease level classes are not equally represented in the dataset, which means the dataset we deal with is **unbalanced.** This can make the classifier biased toward the one or two classes with lots of samples.

When we look at the relationship between age - disease level :

![Screenshot 2023-11-22 165533](https://github.com/cemiledemir/NACC_Alzheimer_Disease_Prediction/assets/52001813/a958537a-9b02-4257-b608-33db0c75808e)

Interestingly, there is a higher concentration of 80-90 years old patients in the Moderate & Severe impairment group than those in the Normal impairment group. Intuitively, we would expect Alzheimer's patients would live less.

## Multicollinearity:
We have checked if there are high correlations between two or more independent variables. The presence of correlated predictors does not provide any unique or new information to our analysis. In fact, it may cause our analysis to be less reliable by making our coefficients unstable. The highly correlated variables are as below:

* INDEPEND_1 - NACCMOCA - Positive
* INDEPEND_1 - INDEPEND_2 - Negative
* RESİDENC_1 - RESİDENC_2 - Negative

## Correlation Matrix:

![Picture1](https://github.com/cemiledemir/NACC_Alzheimer_Disease_Prediction/assets/52001813/332d909f-7da3-4c4d-b6a1-850f6c61c728)

That’s why I dropped out “INDEPEND_1” and “RESİDENC_2” columns.

## Methods & Results
Before constructing the model, train train dataset size was determined as 70%, validation dataset size as 15% and the test size 15%. Also, we need 4 outputs so, we converted y to dummy y.

Sequential models allow for the creation of models layer-by-layer. Each layer has exactly one input tensor and one output tensor. For the project, we have no multiple inputs or outputs for both the model and layers. That is why we built a sequential model. 

In this model, We found that if we use a shallow network (with a single hidden layer of 100 nodes) performs very poorly. İnstead, If we use a deep feedforward neural network (with 3 hidden layers of less nodes) we get better results. In order to avoid overfitting problems, one of the regularization techniques, Dropout, is used. Activation functions for the hidden layer are determined as “reLu” and for the output layer as “softmax”. 

For the optimization algorithm, Adam optimizer was selected because it generally has faster computation time, and requires fewer parameters for tuning. Also, categorical cross entropy loss function is used since  it is used for multi-class classification models where there are two or more output labels. 
According to the parameters of  0.005 learning rate, 100 epochs, 128 batch size, we get:

loss: 0.6467  
accuracy: 0.8562  
precision: 0.7248
recall: 0.6848

![Picture2](https://github.com/cemiledemir/NACC_Alzheimer_Disease_Prediction/assets/52001813/66eeda11-0c0d-4ec1-a037-ee0c400ec3fe)

**Evaluating the model against the test set**

 Micro average, macro average, and weighted average of F1-scores is given in the table below.

![Screenshot 2023-11-22 170608](https://github.com/cemiledemir/NACC_Alzheimer_Disease_Prediction/assets/52001813/800201e8-c67a-401b-98f9-d4fc50234627)

**Let's look at the confusion matrix.**
We see the numbers gather in the middle in the matrix which means the model does not predict the label at the extremes. (e.g. when the actual value is 0 but the model predicts 2 or 3). According to the results, while it should have predicted 1, but highly overestimated as 0. 

![Picture3](https://github.com/cemiledemir/NACC_Alzheimer_Disease_Prediction/assets/52001813/18cdadcf-abac-47c2-9c16-e9eb03a6e50a)

Also the **precision,recall and F1-Score** metrics for each label confirms the table above. Our most successful prediction was the 0.00 class which means non-alzheimer's. This is not surprising at all. As we mentioned before this is an unbalanced data and the model is biased to predict the dominant class. 

![Screenshot 2023-11-22 170816](https://github.com/cemiledemir/NACC_Alzheimer_Disease_Prediction/assets/52001813/53587c2f-7168-42c2-9255-ef953114e089)

We should use oversampling methods to evaluate the model. 
