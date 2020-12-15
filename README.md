# CHURN PREDICTION PROJECT

This project contains the solution for this business case: https://sejaumdatascientist.com/predicao-de-churn/

The business case uses dataset from this kaggle webpage: https://www.kaggle.com/mervetorkan/churndataset

**Disclaimer: The following context is completely fictitious**

# The Business Challenge
## TopBank Company business model
* The company sells banking services to its customers through physical branches and an online portal.
* Offers financial products such as bank account, investments and insurance.
* Main Product: bank account without costs, valid for 12 months. After this period, the account must be renovated.
* Bank return per client:
 * 15% if client's income is lower than the average;
 * 20% if client's income is higher than the average;
 
## Problem
* In the last few months the rate of customers canceling their accounts and leaving the bank had a significant increase;

## Goal
* Reduce customer evasion, aka **churn rate**;
*  Distribute financial incentives among clients in order to maximize ROI (Return on Investment).
*  The sum of incentives for each client cannot exceed R$10,000.00;

## Deliverables
* Answer following questions:
 * What is TopBank's current Churn rate? 
 * How does it vary monthly?
 * What is the model's performance in classifying customers as churns?
 * What is the expected return, in terms of revenue, if the company uses its model to avoid churn from customers?
* Maximize ROI;
* Deployed model that receives a customers database through API and returns the probability if client churning;

## Data

* RowNumber: corresponds to the record (row) number and has no effect on the output.
* CustomerId: contains random values and has no effect on customer leaving the bank.
* Surname: the surname of a customer has no impact on their decision to leave the bank.
* CreditScore: can have an effect on customer churn, since a customer with a higher credit score is less likely to leave the bank.
* Geography: a customer’s location can affect their decision to leave the bank.
* Gender: it’s interesting to explore whether gender plays a role in a customer leaving the bank.
* Age: this is certainly relevant, since older customers are less likely to leave their bank than younger ones.
* Tenure: refers to the number of years that the customer has been a client of the bank. Normally, older clients are more loyal and less likely to leave a bank.
* Balance: also a very good indicator of customer churn, as people with a higher balance in their accounts are less likely to leave the bank compared to those with lower balances.
* NumOfProducts: refers to the number of products that a customer has purchased through the bank.
* HasCrCard: denotes whether or not a customer has a credit card. This column is also relevant, since people with a credit card are less likely to leave the bank.
* IsActiveMember: active customers are less likely to leave the bank.
* EstimatedSalary: as with balance, people with lower salaries are more likely to leave the bank compared to those with higher salaries.
* Exited: whether or not the customer left the bank. (0=No,1=Yes)

# Solution
## Main insights:
A ratio of medians from positive response to negative response show that clients that have left the bank:
* Have balance 20% higher;
* 25% older in age;
* Bought only 1 product;
* Does not have lower salary, tenure or credit score;

| ![](https://github.com/marcellohro-hub/Churn_prediction/blob/master/imgs/medians.png) | 
|:--:| 

Probability higher of exiting bank than expected value for:
* German;
* Female;
* Not being an active member;

| ![](https://github.com/marcellohro-hub/Churn_prediction/blob/master/imgs/cat.png) | 
|:--:| 

## Final model accuracy:

After testing various methods, neural networks with a smoteTOMEK oversampling was chosen;

Final parameters after fine-tuning: 
* optimizer: Adam
* hidden layer 1: 32 neurons
* hidden layer 2: 4 neurons
* dropout_rate: 0.0
* batch_size : 16

| ![](https://github.com/marcellohro-hub/Churn_prediction/blob/master/imgs/download.png) | 
|:--:| 

Final Score:
* Recall: 0.72
* Ballanced Accuracy: 0.77
* F1 Score: 0.60
* Kappa Score: 0.48


## Business solution -  maximizing ROI

To avoid churning the following conditions were proposed:

**For clients with probability of churning greater than 50%:**
* Invest 10% * return * (probability of churning), with a ceiling of 10,000

**For clients with probability of churning lower than 50%:**
* Invest value equals the return of client with a ceiling of 500

Results using conditions:
* ROI considering 100% sucess with the incentives: 23 dolars for each dolar invested

**For more details please read notebook**
