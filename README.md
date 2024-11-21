# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
           from google.colab import drive
drive.mount('/content/drive')

ls drive/MyDrive/'Colab Notebooks'/DATA/

# **DATA CLEANING**




import pandas as pd
import numpy as np

df=pd.read_csv('drive/MyDrive/Data Science/Data_set.csv')

# CHECK OUT NULL VALUES IN DATA SET USING FUNCTION
df_null=df.isnull()
print(df_null)

# DISPLAY THE SUM ON NULL VALUES IN EACH ROWS
df_sum=df.isnull().sum()
print(df_sum)

# DROP NULL VALUES
df_drop=df.isnull().dropna()
print(df_drop)

# FILL NULL VALUES WITH CONSTANT VALUE "O"
df_null_0=df.fillna(0)
print(df_null_0)

# FILL NULL VALUES WITH ffill METHOD
df_null_ffill=df.ffill()
print(df_null_ffill)

# FILL NULL VALUES WITH bfill METHOD
df_bfill=df.bfill()
print(df_bfill)

 #CALCULATE MEAN VALUE OF A COLUMN AND FILL IT WITH NULL VALUES
 df_mean1=df['num_episodes'].fillna(df['num_episodes'].mean())
print(df_mean1)

df_mean2=df['rating'].fillna(df['rating'].mean())
print(df_mean2)

df_mean3=df['current_overall_rank'].fillna(df['current_overall_rank'].mean())
print(df_mean3)

df_mean4=df['lifetime_popularity_rank'].fillna(df['lifetime_popularity_rank'].mean())
print(df_mean4)

df_mean5=df['watchers'].fillna(df['watchers'].mean())
print(df_mean5)

# DROP NULL VALUES
df_dropna=df.dropna()
print(df_dropna)

# **Outlier Detection and Removal - IQR**


import seaborn as sns

age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
print(af)

# USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
sns.boxplot(af)

sns.scatterplot(af)

q1=af.quantile(0.25)
q2=af.quantile(0.5)
q3=af.quantile(0.75)

iqr=q3-q1
print(iqr)

Q1=np.percentile(af,25)
Q2=np.percentile(af,50)
Q3=np.percentile(af,75)

IQR=Q3-Q1

lower_bound=Q1-1.5*IQR
upper_bound=Q3+1.5*IQR

outliers = [x for x in age if x < lower_bound or x > upper_bound]

print('Q1:',Q1)
print('Q3:',Q3)
print('IQR:',IQR)
print('Lower bound:',lower_bound)
print('Upper bound:',upper_bound)
print('Outliers:',outliers)

af=af[((af>=lower_bound)&(af<=upper_bound))]
print(af)

af.dropna()

sns.boxplot(af)

sns.scatterplot(af)

# **Z Score**

from scipy import stats

data=[1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,72,75,78,81,84,87,90,93]
df=pd.DataFrame(data)

sns.boxplot(df)

mean=np.mean(data)
print(mean)

std=np.std(data)
print(std)

z=np.abs(stats.zscore(df))
print(z)

threshold=3
outliers = df[abs(df) > 3]
print("Outliers:")
print(outliers)

df_cleaned = df[(z <= threshold)]
print(df_cleaned)

sns.boxplot(df_cleaned)

sns.scatterplot(df_cleaned)

![Screenshot 2024-11-21 141456](https://github.com/user-attachments/assets/b7e4abea-7afc-4ee1-a59b-cbed9d902093)
![Screenshot 2024-11-21 141517](https://github.com/user-attachments/assets/56b54c9d-b220-4086-855f-d57b360727af)
![Screenshot 2024-11-21 141526](https://github.com/user-attachments/assets/b421f443-bd83-47da-8383-3b986b322c19)
![Screenshot 2024-11-21 141550](https://github.com/user-attachments/assets/04af1e9d-ca00-488b-bcdb-24d00f98d733)
![Screenshot 2024-11-21 141602](https://github.com/user-attachments/assets/20d842e0-d92a-45e5-86b8-5a8792e91312)
![Screenshot 2024-11-21 141614](https://github.com/user-attachments/assets/5b979a72-af0e-4f50-acc5-5b076567a010)
![Screenshot 2024-11-21 141626](https://github.com/user-attachments/assets/7c84f788-2d80-45c6-a8cc-f97d5af31017)
![Screenshot 2024-11-21 141640](https://github.com/user-attachments/assets/6b6e5669-e4a0-4810-a03a-8a8322a48d60)
![Screenshot 2024-11-21 141724](https://github.com/user-attachments/assets/d8dd6103-9e23-4545-9c79-189e77c6b601)
![Screenshot 2024-11-21 141734](https://github.com/user-attachments/assets/e8a3546e-9eff-445a-8bf9-921748bcf623)
![Screenshot 2024-11-21 141743](https://github.com/user-attachments/assets/17bbf2b3-a53a-4318-a88a-5ef40efd2ebf)
![Screenshot 2024-11-21 141748](https://github.com/user-attachments/assets/31c55dc3-0c53-49b2-a431-41948e03f39d)
![Screenshot 2024-11-21 141754](https://github.com/user-attachments/assets/b164f230-e32c-44c2-8685-827be6c12776)
![Screenshot 2024-11-21 142001](https://github.com/user-attachments/assets/e7217d9c-78bb-43c0-9569-f5a26c24c13c)
![Screenshot 2024-11-21 142008](https://github.com/user-attachments/assets/02b99618-1817-4d63-a9f3-707a94640bee)
![Screenshot 2024-11-21 142014](https://github.com/user-attachments/assets/0f13327c-301c-485e-aa3f-3f1388633847)
![Screenshot 2024-11-21 142020](https://github.com/user-attachments/assets/56dbc72e-cb24-4e39-8aae-b1577256efac)
![Screenshot 2024-11-21 142148](https://github.com/user-attachments/assets/ef844ff9-9e4b-4149-b9d9-b2ec0a85e970)
![Screenshot 2024-11-21 142159](https://github.com/user-attachments/assets/6bc6c968-84ec-4fbb-b130-936fe11965c3)
![Screenshot 2024-11-21 142206](https://github.com/user-attachments/assets/0ad1b3be-a22e-46a2-9e50-50bdccb983f0)
![Screenshot 2024-11-21 142213](https://github.com/user-attachments/assets/6c6d38a3-f46b-459f-af49-f166e1835879)
![Screenshot 2024-11-21 142219](https://github.com/user-attachments/assets/b3b972a2-fede-46bb-9416-90d72cbca046)
![Screenshot 2024-11-21 142225](https://github.com/user-attachments/assets/e56b2702-bd99-4f0a-8305-e283a20f5e5a)
![Screenshot 2024-11-21 142230](https://github.com/user-attachments/assets/1bfd65bc-0d67-4731-a66c-213693e3d037)


# Result
          <<include your Result here>>
