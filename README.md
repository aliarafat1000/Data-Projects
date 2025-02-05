# Maximizing Revenue for Taxi Cab Drivers through Payment Type Analysis (EDA)

## Problem Statement 🚖📊

Maximizing revenue is essential for taxi drivers in a competitive industry. This project explores how **payment methods** impact **fare prices** through data analysis. By leveraging **EDA, hypothesis testing, and data visualization**, we aim to provide actionable insights that help drivers optimize earnings.

## Objective 🎯

We conduct an **A/B test** to analyze the relationship between **total fare amount** and **payment type (cash vs. card)**. Using **Python, NumPy, Pandas, Matplotlib, Seaborn, and Scipy**, we investigate whether digital payments generate higher revenue and how this can benefit drivers.

## Research Question ❓

**Does the total fare amount vary based on the payment method? Can we encourage customers to use payment methods that generate higher revenue for drivers, without negatively impacting their experience?**

---

## **Methodology**

To address this research question, we conducted Exploratory Data Analysis (EDA), visualized data distributions, and applied hypothesis testing techniques to draw meaningful conclusions.

### **Step 1: Importing Libraries**

The following Python libraries were used:

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import scipy.stats as st
import warnings
from PIL import Image
from IPython.display import display
import statsmodels.api as sm
warnings.filterwarnings('ignore')
```

### **Step 2: Loading Dataset**

We imported the dataset from a local directory:

```python
data = pd.read_csv(r'D:\Data Analyst\stats\tech classes\archive\yellow_tripdata_2020-01.csv')
print(data.head(3))
```

To understand column definitions, we displayed the metadata:

```python
img = Image.open(r"D:\Data Analyst\stats\tech classes\archive\data_description.png")
display(img)
```

---

## **Exploratory Data Analysis (EDA)**

### **Step 3: Data Cleaning**

#### **Feature Extraction**

- Converted `tpep_pickup_datetime` and `tpep_dropoff_datetime` to datetime format.
- Derived `duration` by calculating the difference between drop-off and pickup times.

```python
data['tpep_pickup_datetime'] = pd.to_datetime(data['tpep_pickup_datetime'])
data['tpep_dropoff_datetime'] = pd.to_datetime(data['tpep_dropoff_datetime'])
data['duration'] = (data['tpep_dropoff_datetime'] - data['tpep_pickup_datetime']).dt.total_seconds()/60
```

#### **Dropping Unnecessary Columns**

```python
df = data[['passenger_count', 'payment_type', 'fare_amount', 'trip_distance', 'duration']]
```

#### **Handling Missing Values**

We checked for missing values and found only 1% of missing data, which we dropped:

```python
print(df.isnull().sum())
df.dropna(inplace=True)
```

#### **Handling Duplicates**

We removed duplicate entries:

```python
df.drop_duplicates(inplace=True)
```

#### **Handling Outliers**

Box plots before and after removing outliers:

```python
plt.boxplot(df['fare_amount'])
plt.show()
```

We used the Interquartile Range (IQR) method to remove outliers:

```python
for col in ['fare_amount', 'trip_distance', 'duration']:
    q1 = df[col].quantile(0.25)
    q3 = df[col].quantile(0.75)
    IQR = q3 - q1
    lower_fence = q1 - 1.5*IQR
    upper_fence = q3 + 1.5*IQR
    df = df[(df[col] >= lower_fence) & (df[col] <= upper_fence)]
plt.boxplot(df['fare_amount'])
plt.show()
```

---

## **Data Visualization**

### **Payment Type Distribution**

```python
plt.title('What do customers prefer as payment method?')
plt.pie(df['payment_type'].value_counts(normalize=True), labels=df['payment_type'].value_counts().index, startangle=90, shadow=True, autopct='%1.1f%%', colors=['#FA643F', '#FFBCAB'])
plt.show()
```

### **Effect of Distance and Fare on Payment Method**

```python
plt.figure(figsize=(12,5))
plt.subplot(1,2,1)
plt.title('Distribution of Fare amount')
plt.hist(df[df['payment_type'] == 'Card']['fare_amount'], bins=20, edgecolor='k', color='#FA643F', label='Card')
plt.hist(df[df['payment_type'] == 'Cash']['fare_amount'], bins=20, edgecolor='k', color='#FFBCAB', label='Cash')
plt.legend()
plt.subplot(1,2,2)
plt.title('Distribution of Trip Distance')
plt.hist(df[df['payment_type'] == 'Card']['trip_distance'], bins=20, edgecolor='k', color='#FA643F', label='Card')
plt.hist(df[df['payment_type'] == 'Cash']['trip_distance'], bins=20, edgecolor='k', color='#FFBCAB', label='Cash')
plt.legend()
plt.show()
```

## **Hypothesis Testing**

### **Step 4: T-Test for Fare Amount and Payment Type**

**Null Hypothesis (H0):** There is no difference in the average fare between cash and card payments.\
**Alternative Hypothesis (H1):** There is a difference in the average fare between cash and card payments.

Since the data was not normally distributed (confirmed via a QQ plot), we performed an independent T-test:

```python
card_sample = df[df['payment_type'] == 'Card']['fare_amount']
cash_sample = df[df['payment_type'] == 'Cash']['fare_amount']
t_stats, p_value = st.ttest_ind(card_sample, cash_sample, equal_var=False)
print('T Statistics:', t_stats, 'P-Value:', p_value)
```

### **Results and Conclusion**

- The p-value was less than 0.05, indicating a statistically significant difference.
- **Customers who pay by card tend to have higher fare amounts than those who pay in cash.**
- Encouraging card payments could lead to increased revenue for taxi drivers.

---

## **Key Insights and Recommendations**

- **Higher Fares with Card Payments:** Data suggests that card users tend to have longer trips with higher fares.
- **Encouraging Digital Payments:** Taxi companies could offer incentives (discounts, loyalty points) for card payments.
- **Optimizing Payment Preferences:** Educating drivers about customer preferences can help them strategize ride acceptance.

This markdown file is structured for **GitHub documentation**, with step-by-step code explanations and supporting images placed at relevant sections.

