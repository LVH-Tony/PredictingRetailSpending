![Featuretools Image](https://cdn.analyticsvidhya.com/wp-content/uploads/2018/02/featuretools.png)


# 🏪 **Predicting Retail Spending with Automated Feature Engineering in Featuretools**

In this notebook, we will implement an automated feature engineering solution with [Featuretools](https://docs.featuretools.com/#minute-quick-start) for a set of online retail purchases. The dataset (available from the [UCI machine learning repository](https://archive.ics.uci.edu/ml/datasets/online+retail#)) is a series of time-stamped purchases and does not come with any labels, so we'll have to make our own prediction problem. After defining the problem, we can use automated feature engineering to build a set of features that are used for training a predictive model.

This set of retail spending data is great practice both for defining our own prediction problem (known as [prediction engineering](http://ieeexplore.ieee.org/document/7796929/)), and for using some of the time-based capabilities of Featuretools, notably cutoff times. Whenever we have time-series data, we need to be extra careful to not "leak labels" or use information from the future to predict a past event. Usually, when we're doing manual feature engineering, this can be an issue and often, a system will work well in development but utterly fail when deployed because it was trained on invalid data. Fortunately, Featuretools will take care of the time issue for us, creating a rich set of features that obey the time restrictions.

## 🛣 **Roadmap**

*Following is an outline for this notebook:*

1. **Read in data, inspect, and clean**

2. **Develop a prediction problem**
    * Create a dataframe of labels - what we want to predict, and cutoff times - the point that all data must come before for predicting a label

3. **Create an entityset and add entities**
    * Normalize the original table to develop new tables 
    * These new tables can be used for making features

4. **Run deep feature sythesis on the entityset to make features**
    * Use the cutoff times to make features using valid data for each label

5. **Use the features to train a machine learning model**
    * Measure performance of the model relative to an informed baseline

6. **Tune deep feature synthesis**
    * Specify custom primitives
    * Adjust maximum depth of features
    * Re-evaluate model

This problem is a great display of both the time and feature-creation capabilities of Featuretools. Also, we'll be able to use custom primitives to expand on our domain knowledge. Doing this problem by hand and ensuring we use only valid data for each label is a daunting task (as can be seen in the Manual Retail Spending notebook)! 
