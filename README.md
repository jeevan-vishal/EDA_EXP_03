**EXP 3 - Delhi Air Quality Analysis**
### Name:Jeevan Vishal.G.D.
### Date:06.02.26
**Aim**


To compare air quality parameters in Delhi across different stations and analyze the relationship between pollutants (e.g., PM2.5 and NO₂) using scatter plots and correlation analysis.


**Procedure / Algorithm**

1)Load the dataset using pandas.

2)Preprocess the data:

3)Convert the date column (period.datetimeFrom.utc) to datetime format.

4)Drop missing or invalid values.

5)Pivot the dataset so each pollutant (parameter) becomes a separate column.

6)Plot scatter plot between PM2.5 and NO₂ to study their relationship.

7)Plot correlation heatmap between all pollutants to identify relationships.

8)Interpret the results — identify which pollutants are correlated and which stations are most polluted.


**Program**

**Name : NIRANJAN S**

**Reg No:212224040221**

```
import pandas as pd
print("Dataset shape:", df.shape)
print("\nHead of dataset:")
print(df.head())

print("\nData types:")
print(df.dtypes)

print("\nNull counts:")
print(df.isnull().sum())
```
```
df['datetime'] = pd.to_datetime(df['period.datetimeFrom.utc'], errors='coerce')
df['pm25'] = pd.to_numeric(df['value'], errors='coerce')

df = df.dropna(subset=['datetime', 'pm25']).reset_index(drop=True)
```
```
df['date'] = df['datetime'].dt.strftime('%Y-%m-%d')
df['month'] = df['datetime'].dt.month
df['hour'] = df['datetime'].dt.hour
df.head(10)
```
```
import matplotlib.pyplot as plt
import seaborn as sns
plt.figure(figsize=(10, 6))
sns.boxplot(x='month', y='pm25', data=df)
plt.xlabel('Month')
plt.ylabel('PM2.5')
plt.show()
```
```
monthly_avg = df.groupby('month')['pm25'].mean().reset_index()
plt.figure(figsize=(8, 5))
plt.plot(monthly_avg['month'], monthly_avg['pm25'], marker='o')
plt.xlabel('Month')
plt.ylabel('Average PM2.5')
plt.grid(True)
plt.show()
```
```
daily_avg = df.groupby('date')['pm25'].mean().reset_index()
exceed_days = daily_avg[daily_avg['pm25'] > 25]
total_days = daily_avg['date'].nunique()
exceed_count = exceed_days.shape[0]
exceed_percent = (exceed_count / total_days) * 100

print(f"Days exceeding WHO limit: {exceed_count} days")
print(f"Percentage of days exceeding WHO limit: {exceed_percent:.2f}%")
```
```
daily_avg = df.groupby('date')['pm25'].mean().reset_index()
exceed_days = daily_avg[daily_avg['pm25'] > 25]
total_days = daily_avg['date'].nunique()
exceed_count = exceed_days.shape[0]
exceed_percent = (exceed_count / total_days) * 100

print(f"Days exceeding WHO limit: {exceed_count} days")
print(f"Percentage of days exceeding WHO limit: {exceed_percent:.2f}%")
```
```
top5_days = daily_avg.sort_values(by='pm25', ascending=False).head(5)
print("Top 5 worst-polluted days (date and PM2.5):")
print(top5_days)
```
**Output**

<img width="821" height="580" alt="image" src="https://github.com/user-attachments/assets/ca75e1dc-8cf0-4daf-bbe6-3920c2114b53" />
<img width="872" height="41" alt="image" src="https://github.com/user-attachments/assets/845eef97-a2f4-48d2-ad87-d50fdd305859" />
<img width="1157" height="421" alt="image" src="https://github.com/user-attachments/assets/f3c61d38-c71c-4e88-8b40-928ebbc4fae5" />
<img width="998" height="582" alt="image" src="https://github.com/user-attachments/assets/d77eab24-eaf5-4c2e-86b9-c07d92121b8f" />
<img width="780" height="492" alt="image" src="https://github.com/user-attachments/assets/d24cf9a2-74f4-42ca-bfbd-de378695c5ba" />
<img width="1107" height="55" alt="image" src="https://github.com/user-attachments/assets/f0c84261-5092-4385-8017-55b20d1410e2" />
<img width="795" height="497" alt="image" src="https://github.com/user-attachments/assets/c545bdf3-9eef-4d67-b5fd-99e1a988c480" />
<img width="417" height="150" alt="image" src="https://github.com/user-attachments/assets/9e7e989f-1e50-4c87-85e6-c6a080bd639c" />












**Interpretation**

1)PM2.5 and NO₂ show a strong positive correlation, suggesting that both pollutants increase together, likely due to vehicle and industrial emissions.

2)  # write other insights

**Result**

The dataset was successfully loaded and processed to extract pollutant-wise and station-wise air quality data for Delhi.


