---
title: "1 Neural Networks and Deep Learning"
collection: talks
type: "Deep Learning"
permalink: /dl/2023-05-08-course-1
venue: "Algo"
date: 2023-05-01
location: "Kowloon Tung, Hong Kong"
---
Process 50%

- [Introduction](#introduction)
- [Section One](#section-one)
  - [Subsection One A](#subsection-one-a)
  - [Subsection One A](#subsection-one-b)



## Introduction
### Section One
#### Subsection One A
#### Subsection One B
## Week 1: Introduction to Deep Learning 2nd
First week is easy intros.

## Week 2: Netural Networks Basics 2nd
Second week is very important fundations for both ML & DL.
### 2.1 Binary Classification

forward & back propogation 

## Introduction2
## Introduction3
## Introduction4
## Introduction5
## Introduction6


'''cpp
import csv
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from ta.momentum import RSIIndicator
from ta.trend import MACD

from sklearn.feature_selection import SelectKBest, mutual_info_classif, SelectFromModel, RFE, f_classif
from sklearn.model_selection import train_test_split
from sklearn.svm import SVC
from sklearn.linear_model import LogisticRegression
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score, roc_auc_score, classification_report, confusion_matrix


from sklearn.preprocessing import StandardScaler

from sklearn.pipeline import Pipeline

# Load Excel data into a pandas DataFrame
df = pd.read_csv('^HSCE.csv')
df

import matplotlib.dates as mdates
# Create the plot
fig, ax = plt.subplots()
ax1 = ax.twinx()
ax.plot(df['Date'], df['Adj Close'],label='Close Price',color='red')
ax1.plot(df['Date'], df['Volume'],label='Volume',color='blue')

# Set the date format for the X-axis tick labels
date_format = mdates.DateFormatter('%Y-%m-%d')
ax.xaxis.set_major_formatter(date_format)

# Set the plot title and axis labels
ax.set_title('Price and Volume Over Time')
ax.set_xlabel('Date')
ax.set_ylabel('Close Price')
ax1.set_ylabel(' Volume')

# Show the plot
plt.show()

data=df['Volume']
# Calculate median and interquartile range
median = data.median()
iqr = np.percentile(data, 85) - np.percentile(data, 25)

# Define threshold for outliers
threshold = 1.5

# Identify outliers
lower_bound = median - threshold * iqr
upper_bound = median + threshold * iqr
outliers = data[(data < lower_bound) | (data > upper_bound)]


df = df.drop(outliers.index)


df['Open_Close'] = df['Open'] - df['Adj Close']
df['High_Low'] = df['High'] - df['Low']

df['log_return'] = np.log(df['Adj Close']) - np.log(df['Adj Close'].shift(1))
df['momentum'] = df['Adj Close'] - df['Adj Close'].shift(10)

df['past_return_1'] = df['log_return'].shift(1)
df['past_return_2'] = df['log_return'].shift(2)
df['past_return_3'] = df['log_return'].shift(3)
df['past_return_4'] = df['log_return'].shift(4)
df['past_return_5'] = df['log_return'].shift(5)
df['past_return_6'] = df['log_return'].shift(6)
df['past_return_7'] = df['log_return'].shift(7)
df['past_return_10'] = df['log_return'].shift(10)
df['past_return_15'] = df['log_return'].shift(15)

df['MA_5'] = df['Adj Close'].rolling(window=5).mean()
df['MA_10'] = df['Adj Close'].rolling(window=10).mean()
df['MA_15'] = df['Adj Close'].rolling(window=15).mean()

df['EMA_5'] = df['Adj Close'].ewm(span=5, adjust=False).mean()
df['EMA_10'] = df['Adj Close'].ewm(span=10, adjust=False).mean()
df['EMA_15'] = df['Adj Close'].ewm(span=15, adjust=False).mean()

# Calculate RSI and MACD
rsi = RSIIndicator(df['Adj Close']).rsi()
macd = MACD(df['Adj Close']).macd()

# Add RSI and MACD as features
df['RSI'] = rsi
df['MACD'] = macd

df.dropna(inplace=True)

# features as input x  
# label return > 0.25% as 1, others as 0
X = df[['RSI','MACD','Open_Close','High_Low','Volume','past_return_1','past_return_2','past_return_3','past_return_4','past_return_6', 'past_return_5','past_return_7', 'past_return_10', 'past_return_15', 'momentum', 'MA_5', 'MA_10', 'MA_15', 'EMA_5', 'EMA_10', 'EMA_15']]
y = np.where(df['log_return'] > 0.0025, 1, 0)


# Split data into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Feature selection using RFE
rfc = RandomForestClassifier(n_estimators=100, random_state=42)
rfe = RFE(estimator=rfc, n_features_to_select=10, step=1)
rfe.fit(X_train, y_train)
selected_features = X_train.columns[rfe.support_]

# Train Random Forest Classifier on selected features
rfc.fit(X_train[selected_features], y_train)
y_pred = rfc.predict(X_test[selected_features])

# Print classification report and confusion matrix
accuracy = accuracy_score(y_test, y_pred)
print('Accuracy:', accuracy)
print(classification_report(y_test, y_pred))
print(confusion_matrix(y_test, y_pred))



# Rank feature importance
importance = pd.DataFrame({'Feature': selected_features, 'Importance': rfc.feature_importances_})
importance = importance.sort_values(by='Importance', ascending=False)
sns.barplot(x='Importance', y='Feature', data=importance)
plt.title('Feature Importance')
# Add importance values to the bar chart
for i, v in enumerate(importance['Importance']):
    plt.text(v + 0.01, i + 0.1, str(round(v, 3)), color='black')
plt.show()
# Plot confusion matrix
cm = confusion_matrix(y_test, y_pred)
sns.heatmap(cm, annot=True, cmap='Blues', fmt='g')
plt.xlabel('Predicted')
plt.ylabel('True')
plt.title('Confusion Matrix')
plt.show()


# Plot classification report
report = classification_report(y_test, y_pred, output_dict=True)
sns.heatmap(pd.DataFrame(report).iloc[:-1, :].T, annot=True, cmap='Blues', fmt='.2f')
plt.title('Classification Report')
plt.show()
'''

remind: Treasury trading now

[Coursera - Neural Networks and Deep Learning](https://www.coursera.org/learn/neural-networks-deep-learning)
