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


```
from google.colab import files
import pandas as pd
uploaded = files.upload()
df = pd.read_csv('Data_set.csv')
df.head()
```

![image](https://github.com/user-attachments/assets/b9398c0e-dfc6-4219-ae5b-6e73d208e33f)


```
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from scipy import stats

exp=pd.read_csv("Data_set.csv")
exp.head()
```

![image](https://github.com/user-attachments/assets/b7be6eaf-ffd0-4e39-99af-283df369de0e)

```
df.info()
print()
df.describe()
```

![image](https://github.com/user-attachments/assets/b3505afb-b008-4268-8f9b-dc023f700bfd)

```
df.isnull().sum()
```

![image](https://github.com/user-attachments/assets/6dbef214-2d5e-4eef-a9f8-522ef67e8c06)

```
df.isnull().sum(axis=1)
```

![image](https://github.com/user-attachments/assets/5b1bbc93-c34b-41ac-9df4-fccea842d279)

```
df_dropna = df.dropna()
df_dropna
```

![image](https://github.com/user-attachments/assets/07906ab0-3354-446f-b323-ecb6787e4530)

```
df_filled_const = df.fillna("O")
df_filled_const
```

![image](https://github.com/user-attachments/assets/374b9543-14d7-4d2b-a95c-0fff26ffaec5)

```
df_ffill = df.ffill()
df_bfill = df.bfill()
(df_ffill)
(df_bfill)
```

![image](https://github.com/user-attachments/assets/994fbb27-894a-4626-940f-86dc02c869fb)

```
column_name = "your_column" 
if column_name in df.columns and df[column_name].dtype in ['int64', 'float64']:
    df[column_name].fillna(df[column_name].mean(), inplace=True)
df
```

![image](https://github.com/user-attachments/assets/785399d1-6e90-4e78-acb1-76ddfef9e3c7)

```
age = [1, 3, 28, 27, 25, 92, 30, 39, 40, 50, 26, 24, 29, 94]
af = pd.DataFrame(age, columns=['Age'])
af
```



![image](https://github.com/user-attachments/assets/b17e63e9-407a-4e43-907e-bbd5a0a2dd41)


```
plt.figure(figsize=(5, 4))
sns.boxplot(y=af["Age"])
plt.title("Boxplot Before Removing Outliers")
plt.show()
```

![image](https://github.com/user-attachments/assets/f2115d65-16b4-45be-9cd7-3ede261d57e2)

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

```
af_no_outliers = af[(af["Age"] >= lower_bound) & (af["Age"] <= upper_bound)]
af_no_outliers
```

![image](https://github.com/user-attachments/assets/acabee34-9c50-4d3e-806c-99aeff8ee04a)







      
            >
# Result

Hence the data was cleaned , outliers were detected and removed.
