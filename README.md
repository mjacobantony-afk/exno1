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
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv("D:\\Data Science\\CSV files\\heights.csv")

print("Missing values:\n", df.isnull().sum())

df_cleaned = df.dropna(subset=['height'])

df_cleaned['height'] = pd.to_numeric(df_cleaned['height'], errors='coerce')

Q1 = df_cleaned['height'].quantile(0.25)
Q3 = df_cleaned['height'].quantile(0.75)
IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

df_no_outliers = df_cleaned[(df_cleaned['height'] >= lower_bound) & (df_cleaned['height'] <= upper_bound)]

plt.figure(figsize=(10, 5))
sns.boxplot(data=df_cleaned, x='height')
plt.title('Height Distribution with Outliers')
plt.show()

plt.figure(figsize=(10, 5))
sns.boxplot(data=df_no_outliers, x='height')
plt.title('Height Distribution after Removing Outliers')
plt.show()

print("Cleaned dataset:\n", df_no_outliers)

<img width="1121" height="672" alt="DS Unit 1 Project output-1" src="https://github.com/user-attachments/assets/00b38890-f2af-4169-90c4-ba14890b3392" />
<img width="1043" height="792" alt="DS Unit 1 Project output-2" src="https://github.com/user-attachments/assets/42982d48-c4d0-4446-84aa-0ecdcd39c893" />


# Result
The above code and output performs data cleaning and outlier detection and removal process on heights csv file. 
