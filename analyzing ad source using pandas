import pandas as pd

# Examine the first few rows of ad_clicks.
ad_clicks = pd.read_csv('ad_clicks.csv')
print(ad_clicks.head())

# How many views (i.e., rows of the table) came from each utm_source?
most_views = ad_clicks.groupby('utm_source').user_id.count().reset_index()
print(most_views)

# Create a new column called is_click, which is True if ad_click_timestamp is not null and False otherwise.
ad_clicks['is_click'] = ad_clicks.ad_click_timestamp.isnull()
print(ad_clicks.head())

# We want to know the percent of people who clicked on ads from each utm_source.
clicks_by_source = ad_clicks.groupby(['utm_source', 'is_click']).user_id.count().reset_index()
print(clicks_by_source)

# Now let’s pivot the data so that the columns are is_click (either True or False), the index is utm_source, and the values are user_id.
clicks_pivot = clicks_by_source.pivot(
  columns = 'is_click',
  index = 'utm_source',
  values = 'user_id'
).reset_index()
print(clicks_pivot)

# Create a new column in clicks_pivot called percent_clicked which is equal to the percent of users who clicked on the ad from each utm_source.
clicks_pivot['percent_clicked'] = clicks_pivot[True] / (clicks_pivot[True] + clicks_pivot[False])
print(clicks_pivot)

# We can group by experimental_group and count the number of users.
a_b = ad_clicks.groupby('experimental_group').user_id.count().reset_index()
print(a_b)

# Group by both experimental_group and is_click and count the number of user_id‘s.
percent_a_b = ad_clicks.groupby(['experimental_group','is_click']).user_id.count().reset_index()
print(percent_a_b)

# You might want to use a pivot table like we did for the utm_source exercises.
percent_a_b_pivot = percent_a_b.pivot(
  columns = 'is_click',
  index = 'experimental_group',
  values = 'user_id'
).reset_index()
print(percent_a_b_pivot)

# For each group (a_clicks and b_clicks), calculate the percent of users who clicked on the ad by day.
a_clicks = ad_clicks[ad_clicks.experimental_group == 'A']
b_clicks = ad_clicks[ad_clicks.experimental_group == 'B']
print(a_clicks.head())
print(b_clicks.head())

# Compare the results for A and B.
day_a = a_clicks.groupby(['is_click','day']).user_id.count().reset_index()
print(day_a)

day_a_pivot = day_a.pivot(
  columns = 'is_click',
  index = 'day',
  values = 'user_id'
).reset_index()
print(day_a_pivot)

day_a_pivot['percent_clicked'] = day_a_pivot[True] / (day_a_pivot[True]+day_a_pivot[False])
print(day_a_pivot)

day_b = b_clicks.groupby(['is_click','day']).user_id.count().reset_index()
print(day_b)

day_b_pivot = day_b.pivot(
  columns = 'is_click',
  index = 'day',
  values = 'user_id'
).reset_index()
print(day_b_pivot)

day_b_pivot['percent_clicked'] = day_b_pivot[True] / (day_b_pivot[True]+day_b_pivot[False])
print(day_b_pivot)
