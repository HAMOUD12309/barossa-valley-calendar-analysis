# barossa-valley-calendar-analysis
A Python project that uses the calendar module to analyze a Barossa Valley dataset, focusing on monthly and seasonal trends.
## For the following analysis we downlaod the real air bnb data from:
https://data.insideairbnb.com/australia/sa/barossa-valley/2024-09-25/data/calendar.csv.gz

# 1 Reading our Data
```diff
import pandas as pd
df = pd.read_csv('calendar.csv')
df
```
<img width="820" alt="image" src="https://github.com/user-attachments/assets/7d99d426-3fbe-491c-9632-ff7e1b0f70c4" />

# 2 Knowing the Number of Available and Unavailable Rooms
``` diff
df.available.value_counts()
```
<img width="820" alt="image" src="https://github.com/user-attachments/assets/8e414d6f-3471-4b76-9a08-86d34379e4a3" />


# 3 Calculating the Percentage of Available (t) and unavailable (f) rooms.
``` diff
availability_percentage = df['available'].value_counts(normalize=True) * 100
availability_percentage
```
<img width="820" alt="image" src="https://github.com/user-attachments/assets/4adad9ca-b863-4c50-8d2c-95244bc59ad2" />


# 4 Counting the Busiest Dates.
``` diff
busiest = df[df['available']=='f']['date'].value_counts()
print(f'Busiest Dates: {busiest.head()}')
```
<img width="820" alt="image" src="https://github.com/user-attachments/assets/6cd493a1-425d-450c-99cc-d85d8ddfeaa7" />


# 5 Plot a Bar Graph to Show Availablitiy Percentage
``` diff
import matplotlib.pyplot as plt
availability_percentage.plot(kind='bar', color=['green', 'red'])
plt.title('Availability Percentages')
plt.ylabel('Percentage')
plt.xlabel('Available (t/f)')
plt.show()
```
<img width="820" alt="image" src="https://github.com/user-attachments/assets/d33dfe57-a4d9-4e80-839b-dd265c2c7176" />


# 6 Plotting the Busiest Days
``` diff
busiest_dates.head(10).plot(kind='bar', color='orange')
plt.title('Top 10 Busiest Dates')
plt.ylabel('Number of Listings Unavailable')
plt.xlabel('Date')
plt.show()
```
<img width="820" alt="image" src="https://github.com/user-attachments/assets/416c8a73-871d-453f-abe8-9db59e95bebc" />


# 7 Download and Read the Listings for Barossa Valley
``` diff
import pandas as pd
listings = pd.read_csv('listings.csv')
listings
```
<img width="1142" alt="image" src="https://github.com/user-attachments/assets/3f2bd0ed-8d47-4c45-82dc-96dda7950190" />


# 8 Listing Columns
``` diff
listings.columns
```
<img width="1142" alt="image" src="https://github.com/user-attachments/assets/65266640-e014-4440-884a-6451b8aeaf20" />


# 9 Room Prices Based on Their Type
``` diff
import matplotlib.pyplot as plt
price_by_room = listings.groupby('room_type')['price'].mean()
print(price_by_room)

# Plot price by room type
price_by_room.plot(kind='bar', color='cyan')
plt.title('Average Price by Room Type')
plt.ylabel('Average Price')
plt.xlabel('Room Type')

plt.show()
```
<img width="1142" alt="image" src="https://github.com/user-attachments/assets/b174d886-da5e-426e-9b83-7d2cc6286458" />


# 10 Top 10 Most Neighbohoods with the most listings
``` diff
neighborhood_counts = listings['neighbourhood'].value_counts().head(10)
print("Top 10 Neighborhoods by Listings:")
print(neighborhood_counts)

# Plot neighborhoods with most listings
neighborhood_counts.plot(kind='bar', color='lightcoral')
plt.title('Top 10 Neighborhoods by Listings')
plt.ylabel('Number of Listings')
plt.xlabel('Neighborhood')
plt.xticks(rotation=90)
plt.show()
```
<img width="1142" alt="image" src="https://github.com/user-attachments/assets/c98e3634-2678-4db4-ab2e-28c76e5517f9" />


# 11 Geographical Distribution of Listings (Price Colored)
``` diff
import matplotlib.pyplot as plt
import seaborn as sns
plt.figure(figsize=(10, 6))
sns.scatterplot(data=listings, x='longitude', y='latitude', hue='price', palette='viridis', size='price', sizes=(10, 200))
plt.title('Geographical Distribution of Listings (Price Colored)')
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.show()
```
<img width="1142" alt="image" src="https://github.com/user-attachments/assets/3694e0c8-1f0f-4ecb-8472-b54053be4c60" />


# 12 Seeing Listings on a Real Map
``` diff
import folium
from folium.plugins import HeatMap
import pandas as pd


barossa_valley = listings[['latitude', 'longitude', 'price']]  # Example, you may add more columns

# Create a base map centered around Barossa Valley
m = folium.Map(location=[-34.53142195913586, 138.94965644529995], zoom_start=10)

# Prepare the data for the heatmap
heat_data = [[row['latitude'], row['longitude']] for index, row in barossa_valley.iterrows()]

# Add the heatmap to the map
HeatMap(heat_data).add_to(m)

# Save the map as an HTML file to view in a browser
m.save('barossa_valley_heatmap.html')

# If you're using Jupyter Notebook, you can display the map directly in the notebook:
m
```
<img width="1142" alt="image" src="https://github.com/user-attachments/assets/968c47e4-5e67-4ae3-8b6b-e03c73eb4f67" />

