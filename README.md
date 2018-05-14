### Written description of three observable trends based on the data:

1.	The most rides appear to be in urban areas, with rural being the least amount, though the rural areas seem to have the highest average fares per ride. Suburban average fares are somewhat mid-range between urban and rural areas.
2.	The amount of drivers is the least in rural areas, which likely explains as to why the fare percentages are higher – higher demand when supply is lower. Though urban city type still leads when it comes to number of drivers and amount of rides given. 
3.	Though the amount of rides and the drivers differ greatly between rural, urban and suburban, interestingly, the average price remains around the same number for all three city types.

```python
# dependencies, including seaborn
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```


```python
# import csv
city_import = "../Lesson-Plans/city_data.csv"
ride_import = "../Lesson-Plans/ride_data.csv"
```


```python
# read city csv file
city_import_df = pd.read_csv(city_import)
city_import_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tammyburgh</td>
      <td>11</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Melissaborough</td>
      <td>15</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Port Brianborough</td>
      <td>62</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>New Katherine</td>
      <td>68</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Lake Charlesside</td>
      <td>65</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
# read ride csv file
ride_import_df = pd.read_csv(ride_import)
ride_import_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Karenfurt</td>
      <td>2017-01-01 19:03:03</td>
      <td>32.90</td>
      <td>3383346995405</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Melissaborough</td>
      <td>2017-01-01 08:55:58</td>
      <td>19.59</td>
      <td>2791839504576</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Port Sandraport</td>
      <td>2017-01-01 16:21:54</td>
      <td>31.04</td>
      <td>3341437383289</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Curtismouth</td>
      <td>2017-01-03 06:36:53</td>
      <td>15.12</td>
      <td>6557246300691</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Port Michael</td>
      <td>2017-01-03 09:56:52</td>
      <td>19.65</td>
      <td>9887635746234</td>
    </tr>
  </tbody>
</table>
</div>




```python
# merge city and ride csvs
merge_csv = pd.merge(city_import_df, ride_import_df, on="city")
merge_csv.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tammyburgh</td>
      <td>11</td>
      <td>Urban</td>
      <td>2017-01-02 10:56:28</td>
      <td>12.40</td>
      <td>7963408790849</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Tammyburgh</td>
      <td>11</td>
      <td>Urban</td>
      <td>2017-01-02 04:28:03</td>
      <td>18.78</td>
      <td>2315208159060</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tammyburgh</td>
      <td>11</td>
      <td>Urban</td>
      <td>2017-01-03 03:00:08</td>
      <td>30.10</td>
      <td>558639764959</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Tammyburgh</td>
      <td>11</td>
      <td>Urban</td>
      <td>2017-01-01 00:10:21</td>
      <td>7.76</td>
      <td>9113511454178</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Tammyburgh</td>
      <td>11</td>
      <td>Urban</td>
      <td>2017-01-02 05:22:44</td>
      <td>22.00</td>
      <td>4171010688543</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Tammyburgh</td>
      <td>11</td>
      <td>Urban</td>
      <td>2017-01-02 21:29:38</td>
      <td>5.37</td>
      <td>5531485446571</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Tammyburgh</td>
      <td>11</td>
      <td>Urban</td>
      <td>2017-01-02 23:58:17</td>
      <td>11.68</td>
      <td>1012442651497</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Tammyburgh</td>
      <td>11</td>
      <td>Urban</td>
      <td>2017-01-02 21:10:16</td>
      <td>31.16</td>
      <td>7261786411548</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Tammyburgh</td>
      <td>11</td>
      <td>Urban</td>
      <td>2017-01-02 00:43:50</td>
      <td>10.64</td>
      <td>9221421228793</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Tammyburgh</td>
      <td>11</td>
      <td>Urban</td>
      <td>2017-01-01 12:39:10</td>
      <td>9.88</td>
      <td>6250336876297</td>
    </tr>
  </tbody>
</table>
</div>




```python
#remove duplicates in cities between csv files
city_import_df = city_import_df.drop_duplicates("city")
city_import_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tammyburgh</td>
      <td>11</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Melissaborough</td>
      <td>15</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Port Brianborough</td>
      <td>62</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>New Katherine</td>
      <td>68</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Lake Charlesside</td>
      <td>65</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
# average fare a city
avg_fare = merge_csv.groupby("city")["fare"].mean()
avg_fare.head(10).round(2)
```




    city
    Adamschester     29.59
    Alexisfort       27.37
    Amberberg        28.62
    Anthonyfurt      29.49
    Boyleberg        32.40
    Brianfurt        24.51
    Campbellmouth    34.18
    Catherinebury    27.31
    Curtismouth      25.05
    Davidbury        30.83
    Name: fare, dtype: float64




```python
# total rides a city
rides_total = merge_csv.groupby("city")["ride_id"].count()
rides_total.head(10)
```




    city
    Adamschester      9
    Alexisfort       33
    Amberberg        16
    Anthonyfurt      17
    Boyleberg         5
    Brianfurt        22
    Campbellmouth     8
    Catherinebury    29
    Curtismouth      31
    Davidbury        20
    Name: ride_id, dtype: int64




```python
# total number of drivers a city
drivers_total = merge_csv.groupby("city")["driver_count"].sum()
drivers_total.head()
```




    city
    Adamschester    243
    Alexisfort      792
    Amberberg       208
    Anthonyfurt     289
    Boyleberg        65
    Name: driver_count, dtype: int64




```python
# city type 
city_type = city_import_df.set_index("city")["type"]
city_type.head(10)
```




    city
    Tammyburgh           Urban
    Melissaborough       Urban
    Port Brianborough    Urban
    New Katherine        Urban
    Lake Charlesside     Urban
    New Catherine        Urban
    North Rachaelberg    Urban
    North Sandra         Urban
    Whitneyfurt          Urban
    West Nathanville     Urban
    Name: type, dtype: object




```python
# need dataframe for series
cities = pd.DataFrame({"Average Fare": avg_fare, "Total Rides": rides_total, "Total Drivers": drivers_total, "City Type": city_type})
cities.head(10).round(2)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Fare</th>
      <th>City Type</th>
      <th>Total Drivers</th>
      <th>Total Rides</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adamschester</th>
      <td>29.59</td>
      <td>Suburban</td>
      <td>243</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Alexisfort</th>
      <td>27.37</td>
      <td>Urban</td>
      <td>792</td>
      <td>33</td>
    </tr>
    <tr>
      <th>Amberberg</th>
      <td>28.62</td>
      <td>Suburban</td>
      <td>208</td>
      <td>16</td>
    </tr>
    <tr>
      <th>Anthonyfurt</th>
      <td>29.49</td>
      <td>Suburban</td>
      <td>289</td>
      <td>17</td>
    </tr>
    <tr>
      <th>Boyleberg</th>
      <td>32.40</td>
      <td>Suburban</td>
      <td>65</td>
      <td>5</td>
    </tr>
    <tr>
      <th>Brianfurt</th>
      <td>24.51</td>
      <td>Urban</td>
      <td>88</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Campbellmouth</th>
      <td>34.18</td>
      <td>Rural</td>
      <td>16</td>
      <td>8</td>
    </tr>
    <tr>
      <th>Catherinebury</th>
      <td>27.31</td>
      <td>Urban</td>
      <td>203</td>
      <td>29</td>
    </tr>
    <tr>
      <th>Curtismouth</th>
      <td>25.05</td>
      <td>Urban</td>
      <td>1240</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Davidbury</th>
      <td>30.83</td>
      <td>Suburban</td>
      <td>260</td>
      <td>20</td>
    </tr>
  </tbody>
</table>
</div>




```python
# scatter plots for urban, suburban, rural
urban_plot = plt.scatter(urban["Total Rides"],urban["Average Fare"], facecolors = "lightskyblue", edgecolors = "black", s = urban["Total Drivers"]*0.1,label= "Urban", alpha = 0.35, linewidth = 1.3)
suburban_plot = plt.scatter(suburban["Total Rides"], suburban["Average Fare"], facecolors = "gold", edgecolors = "black", s = urban["Total Drivers"]*0.07, label = "Suburban", alpha = 0.48, linewidth = 1.4)
rural_plot = plt.scatter(rural["Total Rides"], rural["Average Fare"], facecolors = "lightcoral",edgecolors = "black", s = rural["Total Drivers"]*2, label = "Rural", alpha = 0.60, linewidth = 1.7)

plt.xlim(1,40)
plt.ylim(20,50)

# add title and axis labels
plt.title("Pyber Rider and Fare Relationship")
plt.xlabel("Total Rides")
plt.ylabel("Average Fare")

# add legend
plt.legend(handles = [urban_plot, suburban_plot, rural_plot], loc = "upper right")

# show plot
plt.savefig("pyber.png")
plt.show()
```


![png](output_11_0.png)



```python
# city fare pie chart info
fare_info = merge_csv.groupby(["type"])["fare"].sum()
fare_info
```




    type
    Rural        4271.69
    Suburban    18779.26
    Urban       40093.25
    Name: fare, dtype: float64




```python
# pie chart specifics
pie_labels = fare_info.index
colors = ["lightcoral", "gold", "lightskyblue"]
explode = (0, 0, 0.13)
# plot
pie_chart = plt.pie(fare_info, labels= pie_labels, colors=colors, explode=explode, autopct="%1.1f%%", shadow=True, startangle =130)
plt.title("Total Fares Percentage by City Type")
plt.axis("equal")
plt.show()
```


![png](output_13_0.png)



```python
# city ride pie chart info
ride_info = merge_csv.groupby(["type"])["ride_id"].count()
ride_info
```




    type
    Rural        125
    Suburban     625
    Urban       1625
    Name: ride_id, dtype: int64




```python
# pie chart specifics
pie_labels2 = ride_info.index
colors = ["lightcoral", "gold", "lightskyblue"]
explode = (0, 0.17, 0)
# plot
pie_chart = plt.pie(ride_info, labels= pie_labels2, colors=colors, explode=explode, autopct="%1.1f%%", shadow=False, startangle =85)
plt.title("Total Rides Percentage by City Type")
plt.axis("equal")
plt.show()
```


![png](output_15_0.png)



```python
# city drivers pie chart info
driver_info = merge_csv.groupby(["type"])["driver_count"].sum()
driver_info.round(2)
```




    type
    Rural         662
    Suburban     8774
    Urban       60935
    Name: driver_count, dtype: int64




```python
# pie chart specifics
pie_labels3 = driver_info.index
colors = ["lightcoral", "gold", "lightskyblue"]
explode = (0.1, 0.17, 0.12)
# plot
pie_chart = plt.pie(driver_info, labels= pie_labels3, colors=colors, explode=explode, autopct="%1.1f%%", shadow=True, startangle =67)
plt.title("Total Driver Percentage by City Type")
plt.axis("equal")
plt.show()
```


![png](output_17_0.png)

