# Pandas Foundations

## Chapter 4 : Case Study - Sunlight in Austin

### Reading in a data file

```python
# Import pandas
import pandas as pd

# Read in the data file: df
df = pd.read_csv(data_file)

# Print the output of df.head()
print(df.head())

# Read in the data file with header=None: df_headers
df_headers = pd.read_csv(data_file, header=None)

# Print the output of df_headers.head()
print(df_headers.head())
```
13904  20110101  0053  12  OVC045  ...  .21  .22  .23 29.95.1  .24
0  13904  20110101   153  12  OVC049  ...                  30.02     
1  13904  20110101   253  12  OVC060  ...                  30.02     
2  13904  20110101   353  12  OVC065  ...                  30.04     
3  13904  20110101   453  12  BKN070  ...                  30.04     
4  13904  20110101   553  12  BKN065  ...                  30.06     

[5 rows x 44 columns]
   0         1    2   3       4   ... 39 40 41     42 43
0  13904  20110101   53  12  OVC045  ...           29.95   
1  13904  20110101  153  12  OVC049  ...           30.02   
2  13904  20110101  253  12  OVC060  ...           30.02   
3  13904  20110101  353  12  OVC065  ...           30.04   
4  13904  20110101  453  12  BKN070  ...           30.04   

[5 rows x 44 columns]
    
    
### Re-assigning column names

```python
# Split on the comma to create a list: column_labels_list
column_labels_list = column_labels.split(",")

# Assign the new column labels to the DataFrame: df.columns
df.columns = column_labels_list

# Remove the appropriate columns: df_dropped
df_dropped = df.drop(list_to_drop, axis='columns')

# Print the output of df_dropped.head()
print(df_dropped.head())
```
 Wban      date  Time  StationType sky_condition  ... relative_humidity wind_speed wind_direction station_pressure sea_level_pressure
0  13904  20110101    53           12        OVC045  ...                24         15            360            29.42              29.95
1  13904  20110101   153           12        OVC049  ...                23         10            340            29.49              30.01
2  13904  20110101   253           12        OVC060  ...                22         15            010            29.49              30.01
3  13904  20110101   353           12        OVC065  ...                27          7            350            29.51              30.03
4  13904  20110101   453           12        BKN070  ...                25         11            020            29.51              30.04
    
[5 rows x 17 columns]

### Cleaning and tidying datetime data
```python
# Convert the date column to string: df_dropped['date']
df_dropped['date'] = df_dropped['date'].astype(str)

# Pad leading zeros to the Time column: df_dropped['Time']
df_dropped['Time'] = df_dropped['Time'].apply(lambda x:'{:0>4}'.format(x))

# Concatenate the new date and Time columns: date_string
date_string = df_dropped['date'] + df_dropped['Time']

# Convert the date_string Series to datetime: date_times
date_times = pd.to_datetime(date_string, format='%Y%m%d%H%M')

# Set the index to be the new date_times container: df_clean
df_clean = df_dropped.set_index(date_times)

# Print the output of df_clean.head()
print(df_clean.head())
```
                   Wban      date  Time  StationType sky_condition  ... relative_humidity wind_speed wind_direction station_pressure sea_level_pressure
2011-01-01 00:53:00  13904  20110101  0053           12        OVC045  ...                24         15            360            29.42              29.95
2011-01-01 01:53:00  13904  20110101  0153           12        OVC049  ...                23         10            340            29.49              30.01
2011-01-01 02:53:00  13904  20110101  0253           12        OVC060  ...                22         15            010            29.49              30.01
2011-01-01 03:53:00  13904  20110101  0353           12        OVC065  ...                27          7            350            29.51              30.03
2011-01-01 04:53:00  13904  20110101  0453           12        BKN070  ...                25         11            020            29.51              30.04
    
[5 rows x 17 columns]

### Cleaning the numeric columns
```python
# Print the dry_bulb_faren temperature between 8 AM and 9 AM on June 20, 2011
print(df_clean.loc['2011-6-20 8:00:00':'2011-6-20 9:00:00', 'dry_bulb_faren'])

# Convert the dry_bulb_faren column to numeric values: df_clean['dry_bulb_faren']
df_clean['dry_bulb_faren'] = pd.to_numeric(df_clean['dry_bulb_faren'], errors='coerce')

# Print the transformed dry_bulb_faren temperature between 8 AM and 9 AM on June 20, 2011
print(df_clean.loc['2011-6-20 8:00:00':'2011-6-20 9:00:00', 'dry_bulb_faren'])

# Convert the wind_speed and dew_point_faren columns to numeric values
df_clean['wind_speed'] = pd.to_numeric(df_clean['wind_speed'], errors='coerce')
df_clean['dew_point_faren'] = pd.to_numeric(df_clean['dew_point_faren'], errors='coerce')
```
2011-06-20 08:27:00     M
2011-06-20 08:28:00     M
2011-06-20 08:29:00     M
2011-06-20 08:30:00     M
2011-06-20 08:31:00     M
2011-06-20 08:32:00     M
2011-06-20 08:33:00     M
2011-06-20 08:34:00     M
2011-06-20 08:35:00     M
2011-06-20 08:53:00    83
Name: dry_bulb_faren, dtype: object
2011-06-20 08:27:00     NaN
2011-06-20 08:28:00     NaN
2011-06-20 08:29:00     NaN
2011-06-20 08:30:00     NaN
2011-06-20 08:31:00     NaN
2011-06-20 08:32:00     NaN
2011-06-20 08:33:00     NaN
2011-06-20 08:34:00     NaN
2011-06-20 08:35:00     NaN
2011-06-20 08:53:00    83.0
Name: dry_bulb_faren, dtype: float64

### Statistical exploratory data analysis

### Signal min, max, median
```python
# Print the median of the dry_bulb_faren column
print(df_clean['dry_bulb_faren'].median())

# Print the median of the dry_bulb_faren column for the time range '2011-Apr':'2011-Jun'
print(df_clean.loc['2011-Apr':'2011-Jun', 'dry_bulb_faren'].median())

# Print the median of the dry_bulb_faren column for the month of January
print(df_clean.loc['2011-Jan', 'dry_bulb_faren'].median())
```
72.0
78.0
48.0

### Signal variance
```python
# Downsample df_clean by day and aggregate by mean: daily_mean_2011
daily_mean_2011 = df_clean.resample('D').mean()

# Extract the dry_bulb_faren column from daily_mean_2011 using .values: daily_temp_2011
daily_temp_2011 = daily_mean_2011['dry_bulb_faren'].values

# Downsample df_climate by day and aggregate by mean: daily_climate
daily_climate = df_climate.resample('D').mean()

# Extract the Temperature column from daily_climate using .reset_index(): daily_temp_climate
daily_temp_climate = daily_climate.reset_index()['Temperature']

# Compute the difference between the two arrays and print the mean difference
difference = daily_temp_2011 - daily_temp_climate
print(difference.mean())
```
>>1.3301831870056477

### Sunny or cloudy
```python
# Using df_clean, when is sky_condition 'CLR'?
is_sky_clear = df_clean['sky_condition']=='CLR'

# Filter df_clean using is_sky_clear
sunny = df_clean.loc[is_sky_clear]

# Resample sunny by day then calculate the max
sunny_daily_max = sunny.resample('D').max()

# See the result
sunny_daily_max.head()
```
              Wban      date    Time  StationType sky_condition  ...  relative_humidity wind_speed wind_direction station_pressure  sea_level_pressure
2011-01-01  13904.0  20110101  235300         12.0           CLR  ...                 53       16.0            360            29.78               30.33
2011-01-02  13904.0  20110102  225300         12.0           CLR  ...                 76        8.0            360            29.82               30.38
2011-01-03  13904.0  20110103  045300         12.0           CLR  ...                 85        0.0            000            29.71               30.27
2011-01-04      NaN       NaN     NaN          NaN           NaN  ...                NaN        NaN            NaN              NaN                 NaN
2011-01-05  13904.0  20110105  235300         12.0           CLR  ...                 79        0.0            000            29.54               30.08

[5 rows x 16 columns]


```python
# Using df_clean, when does sky_condition contain 'OVC'?
is_sky_overcast = df_clean['sky_condition'].str.contains('OVC')

# Filter df_clean using is_sky_overcast
overcast = df_clean.loc[is_sky_overcast]

# Resample overcast by day then calculate the max
overcast_daily_max = overcast.resample('D').max()

# See the result
overcast_daily_max.head()
```
               Wban      date    Time  StationType  sky_condition  ...  relative_humidity wind_speed wind_direction station_pressure  sea_level_pressure
2011-01-01  13904.0  20110101  035300         12.0         OVC065  ...                 27       15.0            360            29.51               30.03
2011-01-02      NaN       NaN     NaN          NaN            NaN  ...                NaN        NaN            NaN              NaN                 NaN
2011-01-03  13904.0  20110103  235300         12.0  SCT042 OVC055  ...                 79       10.0            200            29.70                   M
2011-01-04  13904.0  20110104  235300         12.0  SCT010 OVC016  ...                100        8.0            VR             29.59                   M
2011-01-05  13904.0  20110105  065300         12.0  SCT006 OVC011  ...                 96        3.0            250            29.48                   M

[5 rows x 16 columns]

```python
# From previous steps
is_sky_clear = df_clean['sky_condition']=='CLR'
sunny = df_clean.loc[is_sky_clear]
sunny_daily_max = sunny.resample('D').max()
is_sky_overcast = df_clean['sky_condition'].str.contains('OVC')
overcast = df_clean.loc[is_sky_overcast]
overcast_daily_max = overcast.resample('D').max()

# Calculate the mean of sunny_daily_max
sunny_daily_max_mean = sunny_daily_max.mean()

# Calculate the mean of overcast_daily_max
overcast_daily_max_mean = overcast_daily_max.mean()

# Print the difference (sunny minus overcast)
print(sunny_daily_max_mean - overcast_daily_max_mean)
```
Wban               0.000000
StationType        0.000000
dry_bulb_faren     6.504304
dew_point_faren   -4.339286
wind_speed        -3.246062
dtype: float64

### Visual exploratory data analysis

### Weekly average temperature and visibility
```python
# Import matplotlib.pyplot as plt
import matplotlib.pyplot as plt

# Select the visibility and dry_bulb_faren columns and resample them: weekly_mean
weekly_mean = df_clean[['visibility','dry_bulb_faren']].resample('W').mean()

# Print the output of weekly_mean.corr()
print(weekly_mean.corr())

# Plot weekly_mean with subplots=True
weekly_mean.plot(subplots=True)
plt.show()
```
>>![](/img/Visual-EDA-pandas-foundations-case-study.png)


### Daily hours of clear sky
```python
# Using df_clean, when is sky_condition 'CLR'?
is_sky_clear = df_clean['sky_condition'] == 'CLR'

# Resample is_sky_clear by day
resampled = is_sky_clear.resample('D')

# See the result
resampled
```
>>DatetimeIndexResampler [freq=<Day>, axis=0, closed=left, label=left, convention=start, base=0]

```python
# From previous step
is_sky_clear = df_clean['sky_condition'] == 'CLR'
resampled = is_sky_clear.resample('D')

# Calculate the number of sunny hours per day
sunny_hours = resampled.sum()

# Calculate the number of measured hours per day
total_hours = resampled.count()

# Calculate the fraction of hours per day that were sunny
sunny_fraction = sunny_hours / total_hours
```

```python
# From previous steps
is_sky_clear = df_clean['sky_condition'] == 'CLR'
resampled = is_sky_clear.resample('D')
sunny_hours = resampled.sum()
total_hours = resampled.count()
sunny_fraction = sunny_hours / total_hours

# Make a box plot of sunny_fraction
sunny_fraction.plot(kind='box')
plt.show()
```
>>![](/img/Box-plot-pandas-foundations-case-study.png)

### Heat or humidity
```python
# Resample dew_point_faren and dry_bulb_faren by Month, aggregating the maximum values: monthly_max
monthly_max = df_clean[['dew_point_faren','dry_bulb_faren']].resample('M').max()

# Generate a histogram with bins=8, alpha=0.5, subplots=True
monthly_max.plot(kind='hist', bins=8, alpha=0.5, subplots=True)

# Show the plot
plt.show()
```
>>![](/img/histogram-pandas-foundations-case-study.png)

### Probability of high temperatures
```python
# Extract the maximum temperature in August 2010 from df_climate: august_max
august_max = df_climate.loc['2010-Aug','Temperature'].max()
print(august_max)

# Resample August 2011 temps in df_clean by day & aggregate the max value: august_2011
august_2011 = df_clean.loc['2011-Aug','dry_bulb_faren'].resample('D').max()

# Filter for days in august_2011 where the value exceeds august_max: august_2011_high

august_2011_high = august_2011.loc[august_2011 > august_max]

# Construct a CDF of august_2011_high
august_2011_high.plot(kind='hist', normed=True, cumulative=True, bins=25)

# Display the plot
plt.show()
```
>>![](/img/histogram-cdf--pandas-foundations-case-study.png)
