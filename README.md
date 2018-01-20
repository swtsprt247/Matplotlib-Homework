# Matplotlib-Homework

Analysis:
1. Urban cities had the most riders.  
2. As a driver, you can potentially make more fares a rural setting and not have to drive as much
3. Urban cities have a high density of drivers, while surban cities aren't as dense.  Therefore surban 
fares are more expensive then urban.  



```python
 # Import Dependencies
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import os
```


```python
 # Import our data into pandas from CSV
file_name1 = os.path.join("raw_data","city_data.csv" )
file_name2 = os.path.join("raw_data","ride_data.csv" )

city_data_df = pd.read_csv(file_name1)
ride_data_df = pd.read_csv(file_name2)
```


```python
city_data_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nguyenbury</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>East Douglas</td>
      <td>12</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>West Dawnfurt</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rodriguezburgh</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
ride_data_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wiseborough</td>
      <td>2016-01-21 17:35:29</td>
      <td>44.18</td>
      <td>3645042422587</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spencertown</td>
      <td>2016-07-31 14:53:22</td>
      <td>6.87</td>
      <td>2242596575892</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nguyenbury</td>
      <td>2016-07-09 04:42:44</td>
      <td>6.28</td>
      <td>1543057793673</td>
    </tr>
  </tbody>
</table>
</div>




```python
#merge 2 dataframes together
combined_data = pd.merge(city_data_df, ride_data_df, how="inner", on="city")
combined_data.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-08-19 04:27:52</td>
      <td>5.51</td>
      <td>6246006544795</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-04-17 06:59:50</td>
      <td>5.54</td>
      <td>7466473222333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-05-04 15:06:07</td>
      <td>30.54</td>
      <td>2140501382736</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-01-25 20:44:56</td>
      <td>12.08</td>
      <td>1896987891309</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-08-09 18:19:47</td>
      <td>17.91</td>
      <td>8784212854829</td>
    </tr>
  </tbody>
</table>
</div>




```python
#citycity_df = combined_data.set_index("city")
#citycity_df.head()
```


```python
#average fair per city
city_fare = combined_data.groupby(['city']).fare.mean()
city_fare.head()
```




    city
    Alvarezhaven    23.928710
    Alyssaberg      20.609615
    Anitamouth      37.315556
    Antoniomouth    23.625000
    Aprilchester    21.981579
    Name: fare, dtype: float64




```python
#number of rides per city

city_rides = combined_data.groupby('city').date.count()
city_rides.head()


```




    city
    Alvarezhaven    31
    Alyssaberg      26
    Anitamouth       9
    Antoniomouth    22
    Aprilchester    19
    Name: date, dtype: int64




```python
#Drivers per city
city_drivers = combined_data.groupby('city').driver_count.mean()
city_drivers.head()

```




    city
    Alvarezhaven    21
    Alyssaberg      67
    Anitamouth      16
    Antoniomouth    21
    Aprilchester    49
    Name: driver_count, dtype: int64




```python
#Make a new table
Scatter_Table = pd.DataFrame({"Average fair per city": city_fare,
              "Rides per City": city_rides,
              "Drivers per City": city_drivers, 
             })
Scatter_Table.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average fair per city</th>
      <th>Drivers per City</th>
      <th>Rides per City</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <td>23.928710</td>
      <td>21</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>20.609615</td>
      <td>67</td>
      <td>26</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>37.315556</td>
      <td>16</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>23.625000</td>
      <td>21</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>21.981579</td>
      <td>49</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
Scatter_Table.to_csv("Scatter_Table.csv")
```


```python
file_name3 = os.path.join("Scatter_Table.csv" )

Scatter_Table_df = pd.read_csv(file_name3)
```


```python
Scatter_Table_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>Average fair per city</th>
      <th>Drivers per City</th>
      <th>Rides per City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alvarezhaven</td>
      <td>23.928710</td>
      <td>21</td>
      <td>31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alyssaberg</td>
      <td>20.609615</td>
      <td>67</td>
      <td>26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anitamouth</td>
      <td>37.315556</td>
      <td>16</td>
      <td>9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Antoniomouth</td>
      <td>23.625000</td>
      <td>21</td>
      <td>22</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aprilchester</td>
      <td>21.981579</td>
      <td>49</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
Big_Table = pd.merge(Scatter_Table_df, city_data_df, on="city")
Big_Table.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>Average fair per city</th>
      <th>Drivers per City</th>
      <th>Rides per City</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alvarezhaven</td>
      <td>23.928710</td>
      <td>21</td>
      <td>31</td>
      <td>21</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alyssaberg</td>
      <td>20.609615</td>
      <td>67</td>
      <td>26</td>
      <td>67</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anitamouth</td>
      <td>37.315556</td>
      <td>16</td>
      <td>9</td>
      <td>16</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Antoniomouth</td>
      <td>23.625000</td>
      <td>21</td>
      <td>22</td>
      <td>21</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aprilchester</td>
      <td>21.981579</td>
      <td>49</td>
      <td>19</td>
      <td>49</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
Urban = Big_Table[Big_Table["type"] == "Urban"]
x = Urban['Rides per City']
y = Urban["Average fair per city"]
s = Urban["Drivers per City"]
plt.scatter(x,y,s, c='g', label= 'Urban')

Suburban = Big_Table[Big_Table["type"] == "Suburban"]
x2 = Suburban['Rides per City']
y2 = Suburban["Average fair per city"]
s = Suburban["Drivers per City"]
plt.scatter(x2,y2,s, c='y', label= 'Suburban')

Rural = Big_Table[Big_Table["type"] == "Rural"]
x3 = Rural['Rides per City']
y3 = Rural["Average fair per city"]
s = Rural["Drivers per City"]
plt.scatter(x3,y3,s, c='b', label= 'Rural')

plt.title("Pyber Ride Sharing Data (2016)")
plt.ylabel("Average Fare ($)")
plt.xlabel("Total Number of Rides (Per City)")
plt.legend()
plt.style.use('ggplot')
plt.grid(True)
plt.xlim(0, 40)
plt.ylim(15, 45)
plt.rcParams['lines.linewidth']
plt.rcParams["figure.figsize"]


plt.savefig('Pyber Ride Sharing Data')
plt.show()
```


![png](output_14_0.png)



```python
#% of Total FAre by City Type
Total_sum = combined_data['fare'].sum()

Total_Type = combined_data.groupby(['type']).fare.sum()

TFCT = (Total_Type/Total_sum)*100
TFCT
```




    type
    Rural        6.579786
    Suburban    31.445750
    Urban       61.974463
    Name: fare, dtype: float64




```python
 # Dataset Total Fare by City type
types = ["Rural", "Suburban", "Urban",]
fare = [6.6, 31.4, 62.0]
colors = ["yellowgreen", "red", "lightskyblue"]
explode = (0, 0, 0.05)
```


```python
plt.title("% of Total Fares by City Type")
plt.pie(fare, explode=explode, labels=types, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=90)
plt.axis("equal")

plt.savefig('% of Total Fares by City Type')
plt.show()
```


![png](output_17_0.png)



```python
#% of Total Rides by City Type
Total_Rides = combined_data['date'].count()

Total_RidesType = combined_data.groupby(['type']).date.count()

Rides = (Total_RidesType/Total_Rides)*100
Rides
```




    type
    Rural        5.193187
    Suburban    27.295388
    Urban       67.511425
    Name: date, dtype: float64




```python
 # Dataset Total Rides by City type
types = ["Rural", "Suburban", "Urban",]
rides = [5.2, 27.3, 67.5]
colors = ["yellowgreen", "red", "lightskyblue"]
explode = (0, 0, 0.05)
```


```python
plt.title("% of Total Rides by City Type")
plt.pie(rides, explode=explode, labels=types, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=90)
plt.axis("equal")

plt.savefig('% of Total Rides by City Type')
plt.show()
```


![png](output_20_0.png)



```python
#% of Total Drivers by City Type
Total_Drivers = city_data_df['driver_count'].sum()

Total_DriversType = city_data_df.groupby(['type']).driver_count.sum()

Drives = (Total_DriversType/Total_Drivers)*100
Drives
```




    type
    Rural        3.105405
    Suburban    19.050463
    Urban       77.844133
    Name: driver_count, dtype: float64




```python
 # Dataset Total Drivers by City type
types = ["Rural", "Suburban", "Urban",]
drivers = [3.1, 19.0, 77.8]
colors = ["yellowgreen", "red", "lightskyblue"]
explode = (0, 0, 0.05)
```


```python
plt.title("% of Total Drivers by City Type")
plt.pie(drivers, explode=explode, labels=types, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=90)
plt.axis("equal")

plt.savefig('% of Total Drivers by City Type')
plt.show()
```


![png](output_23_0.png)





