# Ex-03EDA

## AIM
To perform EDA on the given data set. 

# Explanation
The primary aim with exploratory analysis is to examine the data for distribution, outliers and 
anomalies to direct specific testing of your hypothesis.
 
# ALGORITHM
### STEP 1
Import the required packages(pandas,numpy,seaborn).

### STEP 2
Read and Load the Dataset.

### STEP 3
Remove the null values from the data and remove the outliers.

### STEP 4
Remove the non-numerical data columns using drop() method.

### STEP 5
Return object containing counts of unique values using (value_counts()).

### STEP 6
Plot the counts in the form of Histogram or Bar Graph.

### STEP 7
Find the pairwise correlation of all columns in the dataframe(.corr()).

### STEP 8
Save the final data set into the file.

# CODE
~~~
Program 
Developed by: Dhivya Shri.B
Register no:212221230009
~~~
```
import pandas as pd
import numpy as np
import seaborn as sns
df=pd.read_csv("titanic_dataset.csv")
df

#removing data containing too many null values
df.isnull().sum()
df.drop('Cabin',axis=1,inplace=True)

#analysing dataframe contents
df.info()
df.isnull().sum()

#cleaning data
df['Age']=df['Age'].fillna(df['Age'].median())
df['Embarked']=df['Embarked'].fillna(df['Embarked'].mode()[0])
df.isnull().sum()

#data is cleaned, checking for outliers
df.boxplot()
#removing outliers
cols = ['Age', 'Fare','SibSp','Parch','Fare']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
df
df.boxplot()

#maximum outliers removed
### Performing data analysis
#statistical analysis for single data group
df['Survived'].value_counts()
df['Pclass'].value_counts()
df['SibSp'].value_counts()
df['Embarked'].value_counts()
df['Sex'].value_counts()

#statistical analysis for two data groups
pd.crosstab(df["Pclass"],df["Survived"])
pd.crosstab(df["Sex"],df["Survived"])
pd.crosstab(df["Embarked"],df["Survived"])
pd.crosstab(df["SibSp"],df["Survived"])

#graphical analysis of categorical data--univariate
sns.countplot(x="Survived",data=df)
sns.countplot(x="Pclass",data=df)
sns.countplot(x="SibSp",data=df)
sns.countplot(x="Embarked",data=df)
sns.countplot(x="Sex",data=df)

#graphical analysis of non-categorical data or data with multiple categories--univariate
sns.displot(df["Fare"])
sns.displot(df["Age"])

#graphical analysis of categorical data--bivariate
sns.countplot(x="Sex",hue="Survived",data=df)
sns.countplot(x='Pclass',hue='Survived',data=df)
sns.countplot(x='Embarked',hue='Survived',data=df)

#graphical analysis of non-categorical data or data with multiple categories--bivariate
sns.displot(df[df["Survived"]==0]["Age"])
sns.displot(df[df["Survived"]==1]["Age"])

#Graphical representation of data--multivariate 
df.drop('Parch',axis=1,inplace=True)
sns.heatmap(df.corr(),annot=True)

#analysing pairwise correlation of columns in dataset
df.corr()
```

# OUPUT
# Original Data
![image](https://user-images.githubusercontent.com/94505585/162871480-43e41017-0058-4b24-85ac-b7bc93a94d87.png)
# Data after removing values with multiple null entries
![image](https://user-images.githubusercontent.com/94505585/162871568-39a8c87a-2ba4-4ffc-bee5-b6fbc3e9d76b.png)
![image](https://user-images.githubusercontent.com/94505585/162871586-34fc60b4-c4f8-4d98-af69-454a3efdea13.png)
![image](https://user-images.githubusercontent.com/94505585/162871606-c2e1f550-a8fd-42a4-9ec6-76ef5cab0a82.png)
# Data Cleaning Process
![image](https://user-images.githubusercontent.com/94505585/162871641-91574421-e0f4-458f-b9a5-da8bab73f5d6.png)
# Removing Outliers Process
![image](https://user-images.githubusercontent.com/94505585/162871688-5c43392c-b2bf-462c-8bbd-240dbcce08eb.png)
![image](https://user-images.githubusercontent.com/94505585/162871710-0c0805a5-94af-41d3-ba91-7d9b3513aeb2.png)
![image](https://user-images.githubusercontent.com/94505585/162871736-753eba44-f415-4815-9cc0-a3b41c4bde22.png)
# Performing data analysis:
# Statistical analysis for single data group
![image](https://user-images.githubusercontent.com/94505585/162871822-139cf033-da54-46ef-a6de-0c97a2d26b38.png)
![image](https://user-images.githubusercontent.com/94505585/162871878-121f640a-29ce-45ca-9c7b-a8a2661328ed.png) ![image](https://user-images.githubusercontent.com/94505585/162871901-a9b7e732-dd61-4ad2-be32-87a305256b92.png)
![image](https://user-images.githubusercontent.com/94505585/162871935-6f0f030d-d571-4cf0-bc41-7a3265d3d76a.png) ![image](https://user-images.githubusercontent.com/94505585/162871967-cf6c8c58-dfca-4c7c-91fa-635acbd51a80.png)
# Statistical analysis for two data groups
![image](https://user-images.githubusercontent.com/94505585/162872158-02ea51d3-cdf0-4963-9ab9-9b706f5eb55d.png) ![image](https://user-images.githubusercontent.com/94505585/162872188-a8d2e410-58e9-412e-8927-fa5dc76e2c60.png) ![image](https://user-images.githubusercontent.com/94505585/162872212-fcce629d-4326-4009-be28-0d396d5ec967.png) ![image](https://user-images.githubusercontent.com/94505585/162872231-7896967f-570a-4c0d-be54-5acd37ef71a5.png)
# Graphical analysis of categorical data-univariate
![image](https://user-images.githubusercontent.com/94505585/162872303-501dce27-de66-4758-a5e9-e9f3a6154034.png)
![image](https://user-images.githubusercontent.com/94505585/162872324-b566fd8d-151d-4b42-afe0-2c67338a022c.png)
![image](https://user-images.githubusercontent.com/94505585/162872343-08c0d6ef-57b5-4776-8f06-0c03e52f35ef.png)
![image](https://user-images.githubusercontent.com/94505585/162872365-e385d7e3-6c63-4571-83c6-4a4909da2692.png)
![image](https://user-images.githubusercontent.com/94505585/162872390-8e3ca41e-01bf-4023-a7e5-dbf4b88e2603.png)
# Graphical analysis of non-categorical data or data with multiple categories-univariate
![image](https://user-images.githubusercontent.com/94505585/162872507-7f425fd5-7ec4-4f6c-ab5a-6adf8b08a173.png)
![image](https://user-images.githubusercontent.com/94505585/162872541-ed7c889b-1c5b-42c1-a54e-9a8895d9af03.png)
# Graphical analysis of categorical data-bivariate
![image](https://user-images.githubusercontent.com/94505585/162872617-5509e72b-c7de-442b-87f8-df6d0725f3a4.png)
![image](https://user-images.githubusercontent.com/94505585/162872629-927e6273-26eb-4061-995a-8039bd93947d.png)
![image](https://user-images.githubusercontent.com/94505585/162872645-67a2b8d8-736f-4cc7-a76d-dd1893755520.png)
# Graphical analysis of non-categorical data or data with multiple categories-bivariate
![image](https://user-images.githubusercontent.com/94505585/162872733-981a1156-7962-4608-ae1e-b52ec110b551.png)
![image](https://user-images.githubusercontent.com/94505585/162872752-92c29d29-63c1-43a8-987d-1cf1f272b1f3.png)
# Graphical representation of data-multivariate
![image](https://user-images.githubusercontent.com/94505585/162872816-c9a09fed-91eb-4196-8d1c-9c0df859ec65.png)
# Pairwise correlation of columns in dataset
![image](https://user-images.githubusercontent.com/94505585/162872874-e6e080fe-4971-4f62-9679-156b1a07e6f2.png)

# RESULT
The data has been cleaned, outlier has been removed and the EDA on the given data has been performed.










