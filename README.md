# barossa-valley-calendar-analysis
A Python project that uses the calendar module to analyze a Barossa Valley dataset, focusing on monthly and seasonal trends.
## For the following analysis we downlaod the real air bnb data from:
https://data.insideairbnb.com/australia/sa/barossa-valley/2024-09-25/data/calendar.csv.gz
```diff
import pandas as pd
df = pd.read_csv('calendar.csv')
```
## 2
```diff
df['available'].value_counts(normalize=True)
```
<img width="1084" alt="Screenshot 1446-07-22 at 11 49 37" src="https://github.com/user-attachments/assets/9345c6d5-b5fd-41fc-ada8-d56414b7801f" />

## 3
```diff
busiest = df[df['available']=='f']['date'].value_counts()
print(f'Busiest Dates: {busiest.head()}')
```
