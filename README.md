# WORKSHOP
# Data-Cleaning-and-Data-Analysis

# AIM
To read the given perform data cleaning and data analysis.

# Algorithm
1. Perform Data cleaning process wherever necessary

2. Implement Boxplot method to detect outliers

3. Implement IQR method to Remove Outliers 

4. Implement Count plot method for univariate analysis

5.Implement DistPlot method for multivariate analysis

# Coding and Output

Data cleaning process 
~~~
import pandas as pd
data = pd.read_csv('supermarket.csv')

print("Missing values in each column:")
print(data.isnull().sum())

duplicate_rows = data.duplicated().sum()
print(f"\nNumber of duplicate rows: {duplicate_rows}")

if duplicate_rows > 0:
    data = data.drop_duplicates()
if data['Date'].dtype == 'object':
    data['Date'] = pd.to_datetime(data['Date'], format='%m/%d/%Y')

data = data.drop(columns=['Invoice ID'], axis=1)
print("\nData types after cleaning:")
print(data.dtypes)

print("\nCleaned data preview:")
print(data.head())
~~~
![Screenshot 2024-11-05 155342](https://github.com/user-attachments/assets/f92a982c-12b0-4953-ae2a-48aada423ecb)

Boxplot
~~~
import seaborn as sns
import matplotlib.pyplot as plt

# Plotting boxplots
plt.figure(figsize=(14, 6))

plt.subplot(1, 3, 1)
sns.boxplot(y=data['Unit price'])
plt.title('Boxplot of Unit Price')

plt.subplot(1, 3, 2)
sns.boxplot(y=data['Total'])
plt.title('Boxplot of Total')

plt.subplot(1, 3, 3)
sns.boxplot(y=data['Rating'])
plt.title('Boxplot of Rating')

plt.tight_layout()
plt.show()
~~~

![Screenshot 2024-11-05 153754](https://github.com/user-attachments/assets/5a795da6-1a9f-40db-9a3c-5bcc972e51e3)

IQR method

~~~
import pandas as pd

# Load your dataset
data = pd.read_csv('supermarket.csv')

# Function to remove outliers using IQR
def remove_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower_bound = Q1 - 1.5 * IQR
    upper_bound = Q3 + 1.5 * IQR
    return df[(df[column] >= lower_bound) & (df[column] <= upper_bound)]

# Removing outliers for 'Unit price', 'Total', and 'Rating'
for col in ['Unit price', 'Total', 'Rating']:
    data = remove_outliers_iqr(data, col)

# Display cleaned data shape
print(data.shape)

~~~
![Screenshot 2024-11-05 153921](https://github.com/user-attachments/assets/8aea8342-9cf2-4da3-aafb-2702f6552f61)

Count plot method

~~~
plt.figure(figsize=(8, 6))
sns.countplot(data=data, x='Product line')
plt.title('Count of Product Line')
plt.xticks(rotation=45)
plt.show()
~~~

![Screenshot 2024-11-05 153828](https://github.com/user-attachments/assets/17f6d784-085b-4901-8a12-32631d220057)

DistPlot method

~~~
sns.jointplot(x=data['Total'], y=data['Rating'], kind='scatter')
plt.title('Total vs Rating')
plt.show()

~~~
![Screenshot 2024-11-05 153843](https://github.com/user-attachments/assets/e2294d12-a720-4a7a-a933-0ac018bbe136)


# Result
 Thus we have cleaned the data and removed the outliers by  Data cleaning process.
