# Airbnb Listings Analysis

## Overview

This repository contains the analysis of **Airbnb listings 2019** based on various attributes such as **room type**, **price**, **neighborhood group**, **reviews**, and more. The goal of the analysis is to explore and visualize key patterns in the dataset, providing insights into pricing strategies, customer engagement, and listing performance across different locations and room types.

## Data Source

The dataset used in this analysis comes from **Airbnb** and contains information about various listings across New York City, including attributes such as:

- **Price**: Price per night for the listing.
- **Room Type**: Type of room available (e.g., Entire home/apt, Private room).
- **Neighbourhood Group**: The borough in which the listing is located (e.g., Brooklyn, Manhattan).
- **Number of Reviews**: The number of reviews a listing has received.
- **Availability 365**: The number of days the listing is available throughout the year.

## Files

- **`airbnb_data.csv`**: The raw data file containing Airbnb listings information.
- **`airbnb_analysis.ipynb`**: Jupyter Notebook containing the code for data cleaning, exploration, and visualization.

The required libraries include:
- `pandas`
- `matplotlib`
- `seaborn`
- `numpy`

## Analysis Overview

### 1. **Room Type Distribution**
We start by exploring the distribution of room types across the dataset. This analysis helps us understand the proportion of listings available as **entire homes**, **private rooms**, **shared rooms**, and other categories.

- **Visualization**: Countplot of room types.

```python
plt.figure(figsize=(8,4))
sns.countplot(data=df, x='room_type', palette='cool')
plt.title('Room Type Distribution')
plt.show()
```

### 2. **Price Distribution Across Room Types**
Next, we analyze how the **price** varies across different room types. This helps understand the pricing trends for different types of accommodation.

- **Visualization**: Barplot showing average price by room type.

```python
plt.figure(figsize=(12,6))
sns.barplot(x=avg_price_by_room.index, y=avg_price_by_room.values, palette='Set2')
plt.title('Average Price by Room Type')
plt.ylabel('Average Price')
plt.xlabel('Room Type')
plt.show()
```

### 3. **Price Variation Across Neighborhood Groups**
We examine how the **price** varies by **neighborhood group** (borough) to see which locations tend to have higher or lower prices.

- **Visualization**: Boxplot of price variation across neighborhoods.

```python
plt.figure(figsize=(12,6))
sns.boxplot(data=df, x='neighbourhood_group', y='price', palette='Set2')
plt.ylim(0, 500)
plt.title('Price Variation Across Neighborhood Groups')
plt.show()
```

### 4. **Correlation Between Price and Reviews**
To see if there is any correlation between the **price** of a listing and the **number of reviews**, we perform a scatterplot analysis.

- **Visualization**: Scatterplot showing price vs. number of reviews.

```python
sns.scatterplot(data=airbnb, x='price', y='number_of_reviews', alpha=0.6)
plt.title('Price vs. Number of Reviews')
plt.xlabel('Price')
plt.ylabel('Number of Reviews')
plt.show()
```

### 5. **Density of Listings by Longitude and Latitude**
We also explore the geographic distribution of listings. A **Kernel Density Estimate (KDE)** plot is used to visualize the density of listings by **longitude** and **latitude**.

- **Visualization**: KDE plot of listings by geographic location.

```python
sns.kdeplot(x=sub_6['longitude'], y=sub_6['latitude'], cmap="jet", fill=True, thresh=0.05)
plt.title('Density of Listings')
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.show()
```

### 6. **Top 5 Hosts with Most Listings**
A breakdown of the top hosts with the **most listings** is provided to understand whether hosts are managing multiple properties.

```python
listings_per_host = df.groupby('host_id').size().sort_values(ascending=False).head(5)
```

### 7. **Key Performance Indicators (KPIs)**
- **Average Price**: The average price per night for the listings.
- **Occupancy Rate**: The average occupancy rate calculated as the ratio of availability to 365 days.
- **Reviews per Listing**: The average number of reviews per listing.
- **Cancellation Rate**: A metric to evaluate trustworthiness based on cancellations (if data is available).

These KPIs provide valuable insights into the performance of listings, helping hosts and stakeholders understand pricing strategies, engagement levels, and booking trends.

## Conclusion

This analysis provides insights into how various factors such as **room type**, **neighborhood**, **price**, and **reviews** impact Airbnb listings. By leveraging these insights, Airbnb hosts can optimize their pricing strategies and better understand customer preferences. The visualizations presented also help in identifying areas of improvement for both pricing and listing management.
