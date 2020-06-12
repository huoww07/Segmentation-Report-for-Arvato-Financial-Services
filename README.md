# Segmentation-Report-for-Arvato-Financial-Services

## Table of Contents
  1. Installation
  2. Project motivation
  3. File description
  4. Summary of results
  5. Licensing, Acknowledgements

## Installation
The code does not require specific installation. It runs in ipython notebook environment with Python version 3. Required libraries to run the code (installation via: pip install library_name) include: pandas, numpy, matplotlib, seaborn, sklearn.

## Project movivation
This is a collaborative project between Udacity and Arvato Finacial Solutions to identify customers from a mailout campaign. The project serves as the Capstone project for Udacity nanodegree. There is also a Kaggle competition with the associated datasets.

In this project, a mail-order company was interested in identifying segments of the general population to target with their product. Demographic information was provided for general population and a customer population. The unsupervised learning techniques were used to identify the population that mostly likely would respond to the campaign. Next, the mail-out customer data with order response was used to train an supervised model. The fine tuned model was used to make prediction on test dataset and submitted for Kaggle competition.

## File description
1. submit - Arvato Project Wrokbook.ipynb contains all codes that were used for this project. The results were shown as matplotlib figures in the notebook.

2. The source data can be found at:
https://www.kaggle.com/c/udacity-arvato-identify-customers/overview.



## Summary of results
The preprocessing of the data includes 1) finding and filling in missing values and 2) dealing with categorical data. For step 1, I found that there are a considerable amount of missing values in terms of features (columns) and customers (row). When looking at the attributes information excel sheet, I noticed that most features uses -1 or 0 for unknown value. So for missing value, I simply filled in with -1 indicating unknown, to be consistent with the data collection standard. When dealing with categorical data or columns with 'object' data type, I had to choose between one-hot encoding or multiple encoder. I ended up using multiple encoder since one-hot encoding expands the existing number of features. Another problem I ran into was one column seemed to be in time series format (yyyy-mo-date) from visual inspection. So I used datetime modual to change that into year, month and date column.

Since the data had many features, I firstly used PCA analysis to reduce the dimensionality. According to the cumulative sum of explained variance, I noticed that 1st component explained 60% variance and the first 4 components combined can explain >99% of the variance. So 1) I analyzed the feature coefficient for the 1st component in order to identify key contributing features and 2) I continued using PCA transformed data with the first 4 components for future analysis. When analyzing the 1st component, the "year of birth" seems to have a strong coefficient, indicating the variability of this feature in the dataset. The second most important feature seems to be the newly generated "year" column. I couldn't find any information about the original feature with datetime format, but I suspect that the "year" column correlates with "year of birth", however, I have to run the correlation analysis to confirm.

After dimensionality reduction, the first 4 components explained >99% of the variance, so I went ahead to use these 4 components for kmeans clustering. Different numbers of centroids were tested to find the "elbow" number in order to gain the most information with the least number of clusters. By using 5 clusters, I was able to visualize the difference in distribution of general population and customers population. It proved the validity of dimensionality reduction and kmeans clustering.

Finally, I chose to use Gradient Boosting Classifier as the model to predict the target population. The train data was first split into train and test dataset. The model was fine tuned one parameter at a time by manually evaluating the test accuracy scores. During this process, I was able to visualize overfitting (increased training accuracy but decreased test accuracy). The best model with the highest TEST accuracy was then used to predict the provided test dataset and the result was submitted to kaggle for competition. After a few tweaks, my submission ranked around 100.

Future improvement: 1) the treatment on missing value can be improved by imputing the mode or medium. 2) My inspection on correlation of "year" and "year of birth" needs to be investigated, this is to prevent the effect on highly correlated input features biasing the model. 3) The model selection can be flexible. The deep neutron network can be tested for improvement.

The reports were also on Medium:
https://medium.com/@huoww07/segmentation-report-for-arvato-financial-services-bb4b18e9b8b0


## Licensing, Acknowledgements
Licensing: Feel free to use the code here as you would like! Comments and suggestions are welcome!
Acknowledgement: Thanks to Kaggle competition for data availability and Udacity course instructors from Data Science nanodegree.  
