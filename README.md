# Diwali-sales-Analysis
Performed data cleaning and manipulation Performed exploratory data analysis (EDA) using pandas, matplotlib and seaborn libraries 
"""Diwali Sales Analysis .ipynb

Original file is located at https://colab.research.google.com/drive/1W3UdToWglkiF6hyKJ4k8PrSo6QtZpsUa """

Data Cleaning
Drop Columns
python
Copy code
df.drop(['unnamed1','Status'],axis=1,inplace=True)
Check for Missing Values
python
Copy code
df.isnull().sum()
Drop Rows with Missing Values
python
Copy code
df.dropna(inplace=True)
Rename Columns
python
Copy code
df.rename(columns={'Marital_Status':'Marriage status'}, inplace=True)
Exploratory Data Analysis (EDA)
Gender Distribution
python
Copy code
ax = sns.countplot(x='Gender', data=df)
for bars in ax.containers:
    ax.bar_label(bars)
Sales by Gender
python
Copy code
sales_gen = df.groupby(['Gender'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)
sns.barplot(x='Gender', y='Amount', data=sales_gen)
Age Group Analysis
python
Copy code
sns.countplot(data=df, x='Age Group', hue='Gender')
Sales by Age Group
python
Copy code
sales_age = df.groupby(['Age Group'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)
sns.barplot(x='Age Group', y='Amount', data=sales_age)
Top 10 States by Orders
python
Copy code
sales_state = df.groupby(['State'], as_index=False)['Orders'].sum().sort_values(by='Orders', ascending=False).head(10)
sns.barplot(x='State', y='Orders', data=sales_state)
Marriage Status
python
Copy code
ax = sns.countplot(data=df, x='Marriage status')
for bars in ax.containers:
    ax.bar_label(bars)
Sales by Marriage Status and Gender
python
Copy code
sales_state = df.groupby(['Marriage status', 'Gender'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)
sns.barplot(data=sales_state, x='Marriage status', y='Amount', hue='Gender')
Occupation
python
Copy code
ax = sns.countplot(data=df, x='Occupation')
for bars in ax.containers:
    ax.bar_label(bars)
Sales by Occupation and Gender
python
Copy code
sv = df.groupby(['Occupation','Gender'])['Amount'].mean().reset_index()
sns.barplot(data=sv, x='Occupation', y='Amount', hue='Gender')
Product Category
python
Copy code
ax = sns.countplot(data=df, x='Product_Category')
for bars in ax.containers:
    ax.bar_label(bars)
Sales by Product Category
python
Copy code
sales_state = df.groupby(['Product_Category'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False).head(10)
sns.barplot(data=sales_state, x='Product_Category', y='Amount')
Top 10 Most Sold Products
python
Copy code
fig1, ax1 = plt.subplots(figsize=(12,7))
df.groupby('Product_ID')['Orders'].sum().nlargest(10).sort_values(ascending=False).plot(kind='bar')

sales_state = df.groupby(['Product_ID'], as_index=False)['Orders'].sum().sort_values(by='Orders', ascending=False).head(10)
sns.barplot(data=sales_state, x='Product_ID', y='Orders')




