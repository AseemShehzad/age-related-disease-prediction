# Prediction of Age-Related Diseases

The dataset contains 54 unnamed health characteristics and the goal is predict whether a patient has age-related disease based on these features. So, this is essentianly a binary classification problem.

## Getting Our Hands Dirty With The Data
First off, I needed to handle missing values. I used a mix of median and mode to keep things simple. Columns with more than 5% missing data were dropped. Why 5%? Well, if too much data is missing from a column, it's like trying to fill in a book when half the pages are missing. It's better to drop it and move on! The columns with less with 5% missing data were filled using median/mode.

Then, I split the data into numerical and categorical features. I standardized numerical features (using the ever-dependable StandardScaler) and one-hot encoded categorical features to make it easier for our models to digest.

## Hunting For Outliers
Data is rarely perfect, and outliers are one of its most notorious imperfections, and this project had a lot of outliers! These are the data points that sit far away from others, skewing our model's perception. But how do we spot them?

Use the Isolation Forest. This method is perfect for high-dimensional data, like ours. It works by isolating observations by randomly selecting a feature and then randomly selecting a split value between the maximum and minimum values of that selected feature. The logic argument goes: isolating anomaly observations is easier because only a few conditions are needed to separate those cases from the normal observations. Using the contamination parameter, we removed about 5% of the data as outliers.

Winsorizing was also considered but not used, because of superior performace with dropping the outliers using Isolation Forest.

## Machine Learning Models
Now comes the fun part! Training the models!

I started with decision trees - specifically, the RandomForestClassifier. Decision trees are great for interpretability and can handle both categorical and numerical data. The RandomForestClassifier gave us an accuracy of about 87%! Other decision trees were also tried, but randomforest outperformed the ADAboost and GradientBoosting here!

But, being a deep learning enthusiast, I decided to throw a neural network at the data and see what sticks.

The neural network was a Multi-layer Perceptron (MLP), a type of Feed-Forward Neural network. With several Dense layers and some Dropout to prevent overfitting, this algorithm gave us an validation accuracy of 95%!

I used the Adam optimizer with gradient clipping and added an EarlyStopping callback to prevent the model from overfitting. The model still overfitted but it performed well on the test data, since test data was very close in ditribution to the training data!

In the end, it was the neural network that came out on top beating RandomForests.

## Final Thoughts
It was fascinating to see how different methods performed on the same dataset. We started with some traditional ML (Random Forests) and then moved on to something a bit more complex (Neural Networks), and the results were certainly interesting.

This project was a fantastic journey of exploring, cleaning, and modeling data. It offered a chance to apply some ML techniques and showed how important it is to understand your data before feeding it to any model.

Note: This dataset is a part of a Kaggle competition.