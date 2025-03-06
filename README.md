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

![image](https://github.com/user-attachments/assets/05543660-1640-43cd-ac0a-dadf8128ee5d)

# IMPORT CSV FILE HERE
```
from google.colab import files
import pandas as pd
uploaded = files.upload()
df = pd.read_csv('Data_set.csv')
df.head()
```

![image](https://github.com/user-attachments/assets/b9398c0e-dfc6-4219-ae5b-6e73d208e33f)

# READ CSV FILE HERE
```
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from scipy import stats

exp=pd.read_csv("Data_set.csv")
exp.head()
```

![image](https://github.com/user-attachments/assets/b7be6eaf-ffd0-4e39-99af-283df369de0e)

# DISPLAY THE INFORMATION ABOUT CSV AND RUN THE BASIC DATA ANALYSIS FUNCTIONS
```
df.info()
print()
df.describe()
```

![image](https://github.com/user-attachments/assets/b3505afb-b008-4268-8f9b-dc023f700bfd)


# CHECK OUT NULL VALUES IN DATA SET USING FUNCTION
```
df.isnull().sum()
```

![image](https://github.com/user-attachments/assets/6dbef214-2d5e-4eef-a9f8-522ef67e8c06)

# DISPLAY THE SUM ON NULL VALUES IN EACH ROWS
```
df.isnull().sum(axis=1)
```

![image](https://github.com/user-attachments/assets/5b1bbc93-c34b-41ac-9df4-fccea842d279)


# DROP NULL VALUES
```
df_dropna = df.dropna()
df_dropna
```

![image](https://github.com/user-attachments/assets/07906ab0-3354-446f-b323-ecb6787e4530)

# FILL NULL VALUES WITH CONSTANT VALUE "O"
```
df_filled_const = df.fillna("O")
df_filled_const
```

![image](https://github.com/user-attachments/assets/374b9543-14d7-4d2b-a95c-0fff26ffaec5)

# FILL NULL VALUES WITH ffill or bfill METHOD 
```
df_ffill = df.ffill()
df_bfill = df.bfill()
(df_ffill)
(df_bfill)
```

![image](https://github.com/user-attachments/assets/994fbb27-894a-4626-940f-86dc02c869fb)

# CALCULATE MEAN VALUE OF A COLUMN AND FILL IT WITH NULL VALUES
```
column_name = "your_column" 
if column_name in df.columns and df[column_name].dtype in ['int64', 'float64']:
    df[column_name].fillna(df[column_name].mean(), inplace=True)
df
```

![image](https://github.com/user-attachments/assets/785399d1-6e90-4e78-acb1-76ddfef9e3c7)


# OUTLIER DETECTION USING BOXPLOT (AGE DATA)
```
age = [1, 3, 28, 27, 25, 92, 30, 39, 40, 50, 26, 24, 29, 94]
af = pd.DataFrame(age, columns=['Age'])
af
```

![image](https://github.com/user-attachments/assets/b17e63e9-407a-4e43-907e-bbd5a0a2dd41)

# USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER

```
plt.figure(figsize=(5, 4))
sns.boxplot(y=af["Age"])
plt.title("Boxplot Before Removing Outliers")
plt.show()
```

![image](https://github.com/user-attachments/assets/85330115-4d15-4a4a-8214-5b110f496e3b)



# PERFORM IQR METHOD AND DETECT OUTLIER VALUES
```
Q1 = af["Age"].quantile(0.25)
Q3 = af["Age"].quantile(0.75)
IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

outliers = af[(af["Age"] < lower_bound) | (af["Age"] > upper_bound)]
outliers
```

![image](https://github.com/user-attachments/assets/3cc3d6a2-03f1-4991-9820-44c8612910cc)


# REMOVE OUTLIERS
     
```
af_no_outliers = af[(af["Age"] >= lower_bound) & (af["Age"] <= upper_bound)]
af_no_outliers
```

![image](https://github.com/user-attachments/assets/acabee34-9c50-4d3e-806c-99aeff8ee04a)

# BOXPLOT AFTER OUTLIER REMOVAL

```
plt.figure(figsize=(5, 4))
sns.boxplot(y=af_no_outliers["Age"])
plt.title("Boxplot After Removing Outliers")
plt.show()
```

![image](https://github.com/user-attachments/assets/4e9f275c-c264-4a74-9743-a59815ef998e)

# OUTLIER DETECTION USING Z-SCORE METHOD

```
data = [1, 12, 15, 18, 21, 24, 27, 30, 33, 36, 39, 42, 45, 48, 51, 54, 57, 60,
        63, 66, 69, 72, 75, 78, 81, 84, 87, 90, 93, 96, 99, 158]
df = pd.DataFrame(data, columns=["Values"])
df
```

![image](https://github.com/user-attachments/assets/d4394422-7b8a-410c-895c-0bf017fe8287)


# BOXPLOT BEFORE Z-SCORE OUTLIER REMOVAL

```
plt.figure(figsize=(5, 4))
sns.boxplot(y=df["Values"])
plt.title("Boxplot Before Removing Z-Score Outliers")
plt.show()
```

![image](https://github.com/user-attachments/assets/2d26cb30-e644-4159-9af1-84bdebd09f59)


# CALCULATE Z-SCORES

```
from scipy import stats 
df["Z_Score"] = stats.zscore(df["Values"])
```

![image](https://github.com/user-attachments/assets/5fd82c9b-4b95-47d1-b5b8-1e24372cd59e)

# SET THRESHOLD TO DETECT OUTLIERS (|Z| > 3)

```
outliers_z = df[abs(df["Z_Score"]) > 3]
outliers_z
```
![image](https://github.com/user-attachments/assets/e56af5c3-c5a0-407d-805f-34f43635deb0)


# REMOVE OUTLIERS BASED ON Z-SCORE
```
df_no_outliers = df[abs(df["Z_Score"]) <= 3].drop(columns=["Z_Score"])
df_no_outliers
```
![image](https://github.com/user-attachments/assets/5422ed7b-e60e-4285-b4e1-afc682cd97be)

# BOXPLOT AFTER Z-SCORE OUTLIER REMOVAL

```
plt.figure(figsize=(5, 4))
sns.boxplot(y=df_no_outliers["Values"])
plt.title("Boxplot After Removing Z-Score Outliers")
plt.show()
```

![image](https://github.com/user-attachments/assets/9a1df7c6-6ef9-4e3d-b3cb-0286338f6ced)

            
# Result

Hence the data was cleaned , outliers were detected and removed.
