# Final-project-submission
# Credit-risk-modelling-of-leading-European-P2P-lending-platform-Bondora....
The main purposes of this analysis are to summarize the characteristics of variables that can affect the loan status and to get some ideas about the relationships among variables.

Contents  & Preprocessing


# Table of Contents
•Understanding the Dataset
•Preprocessing
•Exploratory Data Analysis
•Feature Engineering
•Feature Scaling
•Data Splitting
•Model Building
•Deployment


# Abstract
• In this project we will be doing credit risk modeling of peer-to-peer lending Bondora systems, Peer-to-peer lending has attracted considerable attention in recent years, largely because it offers a novel way of connecting borrowers and lenders. But as with other innovative approaches to doing business, there is more to it than that. Some might wonder, for example, what makes peer-to-peer lending so different-or, perhaps, so much better- than working with a bank, or why has it become popular in many parts of the world.

• Certainly, the industry has witnessed strong growth in recent years. According to Business Insider, transaction volumes in the U.S. and Europe, the world's leading P2P markets, have expanded at double and, in some cases, triple-digit percentage rates, bolstered by widespread acceptance of doing business online and a supportive regulatory environment. 

• For investors, "peer-2-peer lending," or "P2P offers an attractive way to diversify portfolios and enhance long- term performance. When they invest through a peer-to-peer platform, they can profit from an asset class that has proven itself. Equally important, , especially at a time when many experts believe that traditional favorites such as stocks and bonds are riskier than ever.

• Default risk has long been a significant risk factor to test borrowers' behavior in Peer-to-Peer (P2P) lending. In P2P lending, loans are typically uncollateralized and lenders seek higher returns as compensation for the financial risk they take. In addition, they need to make decisions under information asymmetry that works in favor of the borrowers. In order to make rational decisions, lenders want to minimize the risk of default on each lending decision and realize the return that compensates for the risk

• As in the financial research domain, there are very few datasets available that can be utilized for building and   presenting credit risk models. This dataset will help the research community in building and performing research in the credit risk domain.

# Understanding the Dataset
The retrieved data is a pool of both defaulted and non-defaulted loans from the time period between 1st March 2009 and 27th January 2020. 
The data comprises of demographic and financial information of borrowers, and loan transactions

⚫ The news dataset contains the customer data from the time period between 2009 to 2020.

⚫ The dataset contains 112 features and 134529 records. 

⚫The Target label of the dataset is whether the client is Defaulted (labeled as 1) for Not Defaulted (labeled as 0) in this period. 

# Preprocessing
⚫ Percentage of Missing Values

Removing all the features which have more than 40% missing values.

⚫ Removal of Redundant Features

   •Removal features such as "Loan ID", "Loan number", "UserName", and "DateOfBirth" (because age is already present), since they are assigned to each loan      (or borrower) mainly for data storage and identification purposes and are meaningless for default prediction.

   • As IncomeTotal is present, Removal of "Income FromPrincipalEmployer", "IncomeFromPension", "IncomeFromFamily Allowance", "IncomeFromSocial                    Welfare","Income From LeavePay", "IncomeFromChildSupport", and "IncomeOther" Features. 

   • Removal unnecessary date features as we don't work on a time series study.

   • Removal of other features that have no effects on our analysis.

⚫ Creating of Target Variable ie Loan Status

Target Variable is created using 'Status' feature provided in the  dataset. The reason for not making status as Target Variable is that it has three unique values 'Current', 'Late' and 'Repaid'. There is no default feature but there is a feature 'DefaultDate' which tells us when the borrower has defaulted means on which date the borrower defaulted. So, combining 'Status' and 'DefaultDate' features for creating Target Variable.

# EDA 
EDA (Exploratory Data Analysis)
Dataset consist of different categorical and numerical distribution features Exploratory Data Analysis Process for this Projects involves plottingof the following.

Categorical Features :
• Percentage of Defaulted loans in the dataset.
• Residency of the Defaulters. 
• Gender distribution of Defaulters.  
• Check if the most Defaulters are New Credit Customers or not.  
• Language Code Distribution of the Defaulters.  
• Education wise distribution of Defaulters.  
• Employment Status distribution of the Defaulters.  
• Marital Status distribution of the Defaulters.  
• Distribution of Loan purpose the Defaulters.  
• Distribution of Employment Duration of the Defaulters.  
• Distribution of Occupation Area of the Defaulters
• Distribution of Home Ownership Type of the Defaulters. 
• Distribution of Ratings of the Defaulters. 
• Distribution of Credit Score EsMicroL of the Defaulters. 

Numerical Features :

⚫ Age distribution of the Defaulters :

   • Mean Age = Median Age which is about 40 years.

   • The data is almost Symmetric.


⚫ Monthly Payment distribution of the Defaulters :

   • Mean value is 130, it's smaller and this means that the monthly payments of the Defaulters are smaller.

   • There are a large number of Outliers above the upper limit.

⚫ AppliedAmount & Amount distribution of the Defaulters 

⚫ Previous Repayments Before Loan distribution of the Defaulters :
   • Mean value of the repaid money by the defaulters before the loan is 861.

   • Data is very much skewed to the right and this means that the defaulters repaid small amount of money with a mean value about 861.138

   • There are a lot of Outliers.


Correlation Plot of Numerical Variables
After Identifying outlying features, Heatmap is used to check the correlation of the features with the Target variable.

• There are features that are positively correlated to each other.

• There are features that are negatively correlated to each other. 

• Mostly, features are not correlated to each others.

# Handling Outliers

⚫ Data point that falls outside of 1.5 times of an interquartile range above the 3rd quartile and below the 1st quartile. 

⚫ Data point that falls outside of 3 standard deviations. We can use a Z-score, and if the Z-score falls outside of 2 standard deviation. 
   In EDA process outlier were already identified. There are different methods of dealing with outliers. 
   
⚫  Using Scatter plots

⚫ Using Box plots

⚫  Using Z-score

⚫  Using the Inter Quartile Range (IQR)

• A Loop for replacing outliers above upper bound with the upper bound value:

for column in df.select_dtypes ([float, int]).columns:

col_IQR = df[column].quantile(.75) - df[column].quantile(.25)

col_Max= df[column].quantile (.75) + (1.5 * col_IQR)

df[column][df[column] > col Max] = col_Max

• A Loop for replacing outliers under lower bound with the lower bound value:

for column in df.select_dtypes([Float, int)).columns:

col_IQR = df[column].quantile(.75) - df[column].quantile(.25) 

col_Min= df[column].quantile(25) - (1.5 * col_IQR)

df[column][df[column] < col_Min] = col Min

# Feature Scaling & Dimensionality Reduction (PCA)

Feature Scaling

We used StandardScalar to scale our data: StandardScaler is used to resize the distribution of the values inside each features. 

⚫So that the mean of the observed values is 0 and the Standard Deviation is 1.

⚫The values will between -1 and 1.

From sklearn.preprocessing import StandardScaler( ) 

scaler =  StandardScaler( ).fit(X_train)

rescaled = scaler.transform(X_train)

ValidationX=scaler.transform(X_valid)

• fit_transform( ) is used on the training data so that we can scale the training data and also learn the scaling parameters of that data Here, the model       built by us will learn the mean and variance of the features of the training set.

 These learned parameters are then used to scale our test data.

• transform( ) uses the same mean and variance as it is calculated from our training data to transform our test data. 

  Thus, the parameters learned by our model using the training data will help us to transform our test data.

  As we do not want to be biased with our model, but we want our test data to be a completely new and a surprise set for our model.

# Feature Extraction and Dimensionality-reduction using (PCA)

Principal component analysis, for PCA is a dimensionality-reduction method that is often used to reduce the dimensionality of large data sets, by transforming a large set of variables into a smaller one that still contains most of the information.

The idea of PCA is simple — reduce the number of variables of a data set, while preserving as much information as possible.

Due to the nature of Dataset, it was observed that performing PCA negatively affected the accuracy of our models.

So that is why we opt to leave this dimentionality reduction method.

# Splitting Data & Model Deployment
Spiliting Data into training and testing sets

80% of the dataset is consider as the training data while the remaining is used as testing data for our machine learning models.

from sklearn.nodel selection import train test split X_train, X_test, y_train, y_test train_test_split(x, y, random_state=42, test_size =0.2)


# Model Building

**Algorithms used:**

• **Support Vector Classifier** (Support Vector Machine)

• Regularization (to remove the underfitting  and overfitting):

  L1 (**Lasso** Regressor) & L2 (**Ridge** Regressor)


Metrics considered for Model Evaluation

Accuracy, Precision, Recall and F1 Score

• Accuracy: What proportion of actual positives and negatives is correctly classified?

• Precision: What proportion of predicted positives are truly positive ?

• Recall: What proportion of actual positives is correctly classified?

• F1 Score: Harmonic mean of Precision and RecallChoosing the features

After choosing LDA model based on confusion matrix here where choose the features taking in consideration the deployment phase.

Following Features were chosen for the deployment phase as they were observed to be highly correlated to the target varibal in the above steps.

1. Bids portfolio Manager
2. Refinance Liabilities
3. Country
4. Bids Api
5. Debt To Income
6. Use Of Loan
7. Bids Manual
8. Free Cas
9. Education
10. New Credit Customer
11. Restructured
12. Marital Status
13. Age
14. Principle Payment Made
15. Employment Status
16. Applied Amount
17. Interest And Penalty Payments Made
18. Employment Duration Current Employere
19.Interest
20.Previous Early Repayments Before Loan
21. Occupation Area
22. Monthly Payment
23. Verification Type
24. Home Ownership Type
25. Income Total
26. Language Code
27. Rating
28. Existing Liabilities
29. Gender
30. Credit Score EsMicrol


# Deployment
 
**Streamlit**

• It is a tool that lets you creating applications for your machine learning model by using simple python code.

• We write a python code for our app using Streamlit; the app asks the user to enter the data. 
The app runs on local host.

**Render**

• To deploy our Streamlit web application for free on Render. 

After this, our web application will be live on the internet and we could share it for any user input from the outside world.
