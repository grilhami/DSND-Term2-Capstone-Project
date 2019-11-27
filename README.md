# DSND-Term2-Capstone-Project
Udacity Data Science Nanodegree Term 2 Project: Capstone Project

## Installation
The project is supported by Python 3.x libraries and packages:

- Numpy
- Pandas
- Seaborn
- Matplotlib
- Sciki-tlearn
- Jupyter Notebook

## Project Overview

This data set contains simulated data that mimics customer behavior on the Starbucks rewards mobile app. Once every few days, Starbucks 
sends out an offer to users of the mobile app. An offer can be merely an advertisement for a drink or an actual offer such as a discount 
or 
BOGO (buy one get one free). Some users might not receive any offer during certain weeks.

Not all users receive the same offer, and that is the challenge to solve with this data set.

Your task is to combine transaction, demographic and offer data to determine which demographic groups respond best to which offer type. 
This data set is a simplified version of the real Starbucks app because the underlying simulator only has one product whereas Starbucks 
actually sells dozens of products.

Every offer has a validity period before the offer expires. As an example, a BOGO offer might be valid for only 5 days. You'll see in 
the 
data set that informational offers have a validity period even though these ads are merely providing information about a product; for 
example, if an informational offer has 7 days of validity, you can assume the customer is feeling the influence of the offer for 7 days 
after receiving the advertisement.

You'll be given transactional data showing user purchases made on the app including the timestamp of purchase and the amount of money spent 
on a purchase. This transactional data also has a record for each offer that a user receives as well as a record for when a user actually 
views the offer. There are also records for when a user completes an offer.

Keep in mind as well that someone using the app might make a purchase through the app without having received an offer or seen an offer.

## Data Sets

The data is contained in three files:

portfolio.json - containing offer ids and meta data about each offer (duration, type, etc.)
profile.json - demographic data for each customer
transcript.json - records for transactions, offers received, offers viewed, and offers completed
Here is the schema and explanation of each variable in the files:

portfolio.json

- id (string) - offer id
- offer_type (string) - type of offer ie BOGO, discount, informational
- difficulty (int) - minimum required spend to complete an offer
- reward (int) - reward given for completing an offer
- duration (int) - time for offer to be open, in days
- channels (list of strings)


profile.json

- age (int) - age of the customer
- became_member_on (int) - date when customer created an app account
- gender (str) - gender of the customer (note some entries contain 'O' for other rather than M or F)
- id (str) - customer id
- income (float) - customer's income


transcript.json

- event (str) - record description (ie transaction, offer received, offer viewed, etc.)
- person (str) - customer id
- time (int) - time in hours since start of test. The data begins at time t=0
- value - (dict of strings) - either an offer id or transaction amount depending on the record

## Results

Based on the chart above, we know have some understanding about which offers have high conversions.

First, just like a funnel on a website, we want to find the offer that moves from large number during the 'offer recieved' phase, to 
smaller numbers during the 'offer completed phase'. According to the graph, the offers that seems to mathc the criteria are offer 0, 1, 
5, 6, and 8.

Second, there are events where the offers were not actually attractive to the customers. Although used, they are not in the mind of the 
customer. These offers include offer 3, 4, and 9.

Finally, informational notice cannot be converted to purchases. This includes offer 2 and 7.

Now that we know which offer is effective and which are not, we can use this information to provide labels for the demographic data. 
Basically, we want to label if a certain individual will make a purchase if given the effective offers.

A combination fo cross-validation and grid search is used to get optimal parameters by using recall, precision, and f-1 score as the 
scoring metric. Logistic Regression and Random Fores method as the classifier of the offer effective.

**Logistic Regression**
```
             precision    recall  f1-score   support

          0       0.00      0.00      0.00       620
          1       0.72      1.00      0.84      1604

avg / total       0.52      0.72      0.60      2224
```

**Logistic Regression (Optimized)**
```
             precision    recall  f1-score   support

          0       0.00      0.00      0.00       620
          1       0.72      1.00      0.84      1604

avg / total       0.52      0.72      0.60      2224
```

**Random Forest**
```
             precision    recall  f1-score   support

          0       0.35      0.30      0.32       620
          1       0.74      0.78      0.76      1604

avg / total       0.63      0.65      0.64      2224
```

**Random Forest (Optimized)**
```
             precision    recall  f1-score   support

          0       1.00      0.00      0.01       620
          1       0.72      1.00      0.84      1604

avg / total       0.80      0.72      0.61      2224
```
