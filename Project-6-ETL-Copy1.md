

```python
# 1
# Import dependencies
import pandas as pd
import numpy as np
from sqlalchemy import create_engine
import datetime
from datetime import date
import calendar
import warnings
warnings.filterwarnings('ignore')
```

### Store csv data into DataFrames


```python
# 2
# 1 of 11 crimes
# Store CSV into DataFrame
crimes = "Resources/LA_Crime.csv"
# la_crimes_rate = pd.read_csv(crime)
crimes = pd.read_csv(crimes)
# crimes.head()
crimes.head(2)
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
      <th>DR Number</th>
      <th>Date Reported</th>
      <th>Date Occurred</th>
      <th>Time Occurred</th>
      <th>Area ID</th>
      <th>Area Name</th>
      <th>Reporting District</th>
      <th>Crime Code</th>
      <th>Crime Code Description</th>
      <th>MO Codes</th>
      <th>...</th>
      <th>Weapon Description</th>
      <th>Status Code</th>
      <th>Status Description</th>
      <th>Crime Code 1</th>
      <th>Crime Code 2</th>
      <th>Crime Code 3</th>
      <th>Crime Code 4</th>
      <th>Address</th>
      <th>Cross Street</th>
      <th>Location</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>191907890</td>
      <td>43549</td>
      <td>43102</td>
      <td>800</td>
      <td>19</td>
      <td>Mission</td>
      <td>1918</td>
      <td>946</td>
      <td>OTHER MISCELLANEOUS CRIME</td>
      <td>0913 0100</td>
      <td>...</td>
      <td>NaN</td>
      <td>IC</td>
      <td>Invest Cont</td>
      <td>946</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>12900    DRONFIELD                    AV</td>
      <td>NaN</td>
      <td>(34.3048, -118.4333)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>191604279</td>
      <td>43473</td>
      <td>43102</td>
      <td>1100</td>
      <td>16</td>
      <td>Foothill</td>
      <td>1656</td>
      <td>624</td>
      <td>BATTERY - SIMPLE ASSAULT</td>
      <td>1202 1701 0417 0562 0447 0416</td>
      <td>...</td>
      <td>ROCK/THROWN OBJECT</td>
      <td>AO</td>
      <td>Adult Other</td>
      <td>624</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>10400    PARR                         AV</td>
      <td>NaN</td>
      <td>(34.2579, -118.3131)</td>
    </tr>
  </tbody>
</table>
<p>2 rows × 26 columns</p>
</div>




```python
# 13
# 1 of 11 parking
# Store CSV into DataFrame
parking = "Resources/LA_Parking.csv"
parking = pd.read_csv(parking)
parking.head(2)
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
      <th>Ticket number</th>
      <th>Issue Date</th>
      <th>Issue time</th>
      <th>Meter Id</th>
      <th>Marked Time</th>
      <th>RP State Plate</th>
      <th>Plate Expiry Date</th>
      <th>VIN</th>
      <th>Make</th>
      <th>Body Style</th>
      <th>Color</th>
      <th>Location</th>
      <th>Route</th>
      <th>Agency</th>
      <th>Violation code</th>
      <th>Violation Description</th>
      <th>Fine amount</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1116198775</td>
      <td>43101</td>
      <td>1520</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CA</td>
      <td>201807.0</td>
      <td>NaN</td>
      <td>MITS</td>
      <td>SU</td>
      <td>BK</td>
      <td>8701 WINNETKA</td>
      <td>17EL1</td>
      <td>1</td>
      <td>4000A1</td>
      <td>NO EVIDENCE OF REG</td>
      <td>50</td>
      <td>99999.000</td>
      <td>99999.000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1116198764</td>
      <td>43101</td>
      <td>1515</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CA</td>
      <td>201812.0</td>
      <td>NaN</td>
      <td>GMC</td>
      <td>VN</td>
      <td>WH</td>
      <td>8401 WINNETKA</td>
      <td>17EL1</td>
      <td>1</td>
      <td>4000A1</td>
      <td>NO EVIDENCE OF REG</td>
      <td>50</td>
      <td>6389044.544</td>
      <td>1903724.333</td>
    </tr>
  </tbody>
</table>
</div>




```python
print(crimes.max(axis=0)) 
```

    DR Number                                      191907890
    Date Reported                                      43549
    Date Occurred                                      43102
    Time Occurred                                       2359
    Area ID                                               21
    Area Name                                       Wilshire
    Reporting District                                  2197
    Crime Code                                           956
    Crime Code Description    VIOLATION OF RESTRAINING ORDER
    Victim Age                                            99
    Premise Code                                         719
    Premise Description          YARD (RESIDENTIAL/BUSINESS)
    Weapon Used Code                                     512
    Status Code                                           JO
    Status Description                             Juv Other
    Crime Code 1                                         956
    Crime Code 2                                         998
    Crime Code 3                                         NaN
    Crime Code 4                                         NaN
    Address                                          WESTERN
    Location                            (34.3245, -118.4696)
    dtype: object
    


```python
print(parking.max(axis=0)) 
```

    Ticket number                     4324502420
    Issue Date                             43101
    Issue time                              2321
    Meter Id                                 NaN
    Marked Time                              NaN
    RP State Plate                            NY
    Plate Expiry Date                     201910
    VIN                                      NaN
    Make                                    VOLV
    Body Style                                VN
    Color                                     YE
    Location                 HURRICANE/ SPEEDWAY
    Agency                                    56
    Violation code                          8603
    Violation Description    WITHIN INTERSECTION
    Fine amount                              363
    Latitude                         6.50345e+06
    Longitude                         1.9046e+06
    dtype: object
    


```python
# 3
# 2 of 11 crimes
type (crimes)
```




    pandas.core.frame.DataFrame




```python
# 3
# 2 of 11 parking
type (parking)
```




    pandas.core.frame.DataFrame




```python
# 4
# 3 of 11 crimes
crimes.columns
```




    Index(['DR Number', 'Date Reported', 'Date Occurred', 'Time Occurred',
           'Area ID', 'Area Name', 'Reporting District', 'Crime Code',
           'Crime Code Description', 'MO Codes', 'Victim Age', 'Victim Sex',
           'Victim Descent', 'Premise Code', 'Premise Description',
           'Weapon Used Code', 'Weapon Description', 'Status Code',
           'Status Description', 'Crime Code 1', 'Crime Code 2', 'Crime Code 3',
           'Crime Code 4', 'Address', 'Cross Street', 'Location '],
          dtype='object')




```python
# 4
# 3 of 11 parking
parking.columns
```




    Index(['Ticket number', 'Issue Date', 'Issue time', 'Meter Id', 'Marked Time',
           'RP State Plate', 'Plate Expiry Date', 'VIN', 'Make', 'Body Style',
           'Color', 'Location', 'Route', 'Agency', 'Violation code',
           'Violation Description', 'Fine amount', 'Latitude', 'Longitude'],
          dtype='object')




```python
# https://erikrood.com/Python_References/extract_month_year_pandas_final.html

crimes['Date Reported'] = pd.DatetimeIndex(crimes['Date Reported']).year
crimes['month'] = pd.DatetimeIndex(crimes['Date Reported']).month
```


```python
# https://erikrood.com/Python_References/extract_month_year_pandas_final.html
parking['Issue Date'] = pd.DatetimeIndex(parking['Issue Date']).year
parking['month'] = pd.DatetimeIndex(parking['Issue Date']).month
```


```python
crimes.head(2)
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
      <th>DR Number</th>
      <th>Date Reported</th>
      <th>Date Occurred</th>
      <th>Time Occurred</th>
      <th>Area ID</th>
      <th>Area Name</th>
      <th>Reporting District</th>
      <th>Crime Code</th>
      <th>Crime Code Description</th>
      <th>MO Codes</th>
      <th>...</th>
      <th>Status Code</th>
      <th>Status Description</th>
      <th>Crime Code 1</th>
      <th>Crime Code 2</th>
      <th>Crime Code 3</th>
      <th>Crime Code 4</th>
      <th>Address</th>
      <th>Cross Street</th>
      <th>Location</th>
      <th>month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>191907890</td>
      <td>1970</td>
      <td>43102</td>
      <td>800</td>
      <td>19</td>
      <td>Mission</td>
      <td>1918</td>
      <td>946</td>
      <td>OTHER MISCELLANEOUS CRIME</td>
      <td>0913 0100</td>
      <td>...</td>
      <td>IC</td>
      <td>Invest Cont</td>
      <td>946</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>12900    DRONFIELD                    AV</td>
      <td>NaN</td>
      <td>(34.3048, -118.4333)</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>191604279</td>
      <td>1970</td>
      <td>43102</td>
      <td>1100</td>
      <td>16</td>
      <td>Foothill</td>
      <td>1656</td>
      <td>624</td>
      <td>BATTERY - SIMPLE ASSAULT</td>
      <td>1202 1701 0417 0562 0447 0416</td>
      <td>...</td>
      <td>AO</td>
      <td>Adult Other</td>
      <td>624</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>10400    PARR                         AV</td>
      <td>NaN</td>
      <td>(34.2579, -118.3131)</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>2 rows × 27 columns</p>
</div>




```python
parking.head(2)
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
      <th>Ticket number</th>
      <th>Issue Date</th>
      <th>Issue time</th>
      <th>Meter Id</th>
      <th>Marked Time</th>
      <th>RP State Plate</th>
      <th>Plate Expiry Date</th>
      <th>VIN</th>
      <th>Make</th>
      <th>Body Style</th>
      <th>Color</th>
      <th>Location</th>
      <th>Route</th>
      <th>Agency</th>
      <th>Violation code</th>
      <th>Violation Description</th>
      <th>Fine amount</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1116198775</td>
      <td>1970</td>
      <td>1520</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CA</td>
      <td>201807.0</td>
      <td>NaN</td>
      <td>MITS</td>
      <td>SU</td>
      <td>BK</td>
      <td>8701 WINNETKA</td>
      <td>17EL1</td>
      <td>1</td>
      <td>4000A1</td>
      <td>NO EVIDENCE OF REG</td>
      <td>50</td>
      <td>99999.000</td>
      <td>99999.000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1116198764</td>
      <td>1970</td>
      <td>1515</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CA</td>
      <td>201812.0</td>
      <td>NaN</td>
      <td>GMC</td>
      <td>VN</td>
      <td>WH</td>
      <td>8401 WINNETKA</td>
      <td>17EL1</td>
      <td>1</td>
      <td>4000A1</td>
      <td>NO EVIDENCE OF REG</td>
      <td>50</td>
      <td>6389044.544</td>
      <td>1903724.333</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
## https://chrisalbon.com/python/data_wrangling/pandas_split_lat_and_long_into_variables/
# Create two lists for the loop results to be placed
lat = []
lon = []

# For each row in a varible,
for row in crimes['Location ']:
    # Try to,
    try:
        # Split the row by comma and append
        # everything before the comma to lat
        lat.append(row.split(',')[0])
        # Split the row by comma and append
        # everything after the comma to lon
        lon.append(row.split(',')[1])
    # But if you get an error
    except:
        # append a missing value to lat
        lat.append(np.NaN)
        # append a missing value to lon
        lon.append(np.NaN)

# Create two new columns from lat and lon
crimes['latitude'] = lat
crimes['longitude'] = lon
```


```python
crimes.head(2)
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
      <th>DR Number</th>
      <th>Date Reported</th>
      <th>Date Occurred</th>
      <th>Time Occurred</th>
      <th>Area ID</th>
      <th>Area Name</th>
      <th>Reporting District</th>
      <th>Crime Code</th>
      <th>Crime Code Description</th>
      <th>MO Codes</th>
      <th>...</th>
      <th>Crime Code 1</th>
      <th>Crime Code 2</th>
      <th>Crime Code 3</th>
      <th>Crime Code 4</th>
      <th>Address</th>
      <th>Cross Street</th>
      <th>Location</th>
      <th>month</th>
      <th>latitude</th>
      <th>longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>191907890</td>
      <td>1970</td>
      <td>43102</td>
      <td>800</td>
      <td>19</td>
      <td>Mission</td>
      <td>1918</td>
      <td>946</td>
      <td>OTHER MISCELLANEOUS CRIME</td>
      <td>0913 0100</td>
      <td>...</td>
      <td>946</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>12900    DRONFIELD                    AV</td>
      <td>NaN</td>
      <td>(34.3048, -118.4333)</td>
      <td>1</td>
      <td>(34.3048</td>
      <td>-118.4333)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>191604279</td>
      <td>1970</td>
      <td>43102</td>
      <td>1100</td>
      <td>16</td>
      <td>Foothill</td>
      <td>1656</td>
      <td>624</td>
      <td>BATTERY - SIMPLE ASSAULT</td>
      <td>1202 1701 0417 0562 0447 0416</td>
      <td>...</td>
      <td>624</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>10400    PARR                         AV</td>
      <td>NaN</td>
      <td>(34.2579, -118.3131)</td>
      <td>1</td>
      <td>(34.2579</td>
      <td>-118.3131)</td>
    </tr>
  </tbody>
</table>
<p>2 rows × 29 columns</p>
</div>




```python
crimes.columns
```




    Index(['DR Number', 'Date Reported', 'Date Occurred', 'Time Occurred',
           'Area ID', 'Area Name', 'Reporting District', 'Crime Code',
           'Crime Code Description', 'MO Codes', 'Victim Age', 'Victim Sex',
           'Victim Descent', 'Premise Code', 'Premise Description',
           'Weapon Used Code', 'Weapon Description', 'Status Code',
           'Status Description', 'Crime Code 1', 'Crime Code 2', 'Crime Code 3',
           'Crime Code 4', 'Address', 'Cross Street', 'Location ', 'month',
           'latitude', 'longitude'],
          dtype='object')




```python
# 5 
# 4 of 11 crimes
# Create new data with select columns

la_crimes_new = crimes[['Date Reported', 'month', 'latitude', 'longitude','Crime Code 1', 'Address',]].copy()
la_crimes_new.head()
# rename columns
la_crimes_new.rename(columns={'Date Reported':'Year','month':'Month','latitude':'Lat','longitude':'Lon', 'Crime Code 1':'Violation code','Address':'Address'}, inplace=True)
la_crimes_new
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
      <th>Year</th>
      <th>Month</th>
      <th>Lat</th>
      <th>Lon</th>
      <th>Violation code</th>
      <th>Address</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.3048</td>
      <td>-118.4333)</td>
      <td>946</td>
      <td>12900    DRONFIELD                    AV</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.2579</td>
      <td>-118.3131)</td>
      <td>624</td>
      <td>10400    PARR                         AV</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.1758</td>
      <td>-118.379)</td>
      <td>420</td>
      <td>TUJUNGA</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.1095</td>
      <td>-118.1903)</td>
      <td>900</td>
      <td>5900    HAYES                        AV</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.034</td>
      <td>-118.4404)</td>
      <td>440</td>
      <td>2400    PURDUE                       AV</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.0431</td>
      <td>-118.3482)</td>
      <td>510</td>
      <td>400 S  CROCKER                      ST</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1970</td>
      <td>1</td>
      <td>(33.7242</td>
      <td>-118.2869)</td>
      <td>230</td>
      <td>2200    BARBOUR                      CT</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.0432</td>
      <td>-118.2085)</td>
      <td>331</td>
      <td>2500 E  1ST                          ST</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.0467</td>
      <td>-118.2411)</td>
      <td>330</td>
      <td>3RD                          ST</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.2083</td>
      <td>-118.5754)</td>
      <td>354</td>
      <td>20300    SATICOY                      ST</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.2198</td>
      <td>-118.5989)</td>
      <td>649</td>
      <td>21500    ROSCOE                       BL</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.232</td>
      <td>-118.608)</td>
      <td>649</td>
      <td>8900    NEVADA                       AV</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.1872</td>
      <td>-118.5691)</td>
      <td>440</td>
      <td>6400    PENFIELD                     AV</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.2276</td>
      <td>-118.6045)</td>
      <td>946</td>
      <td>8600    TOPANGA CANYON               BL</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.2011</td>
      <td>-118.5863)</td>
      <td>956</td>
      <td>7200    KELVIN                       AV</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.2029</td>
      <td>-118.5929)</td>
      <td>440</td>
      <td>7300    VARIEL                       AV</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.2183</td>
      <td>-118.5906)</td>
      <td>341</td>
      <td>20900    BURTON                       ST</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.1679</td>
      <td>-118.5804)</td>
      <td>956</td>
      <td>20600    VENTURA                      BL</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.1792</td>
      <td>-118.6408)</td>
      <td>740</td>
      <td>23600    OXNARD                       ST</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.1803</td>
      <td>-118.6094)</td>
      <td>510</td>
      <td>6000    MAGNOL                       LN</td>
    </tr>
    <tr>
      <th>20</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.152</td>
      <td>-118.5763)</td>
      <td>330</td>
      <td>20300    RUSTON                       RD</td>
    </tr>
    <tr>
      <th>21</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.1883</td>
      <td>-118.6536)</td>
      <td>341</td>
      <td>VALLEY CIRCLE</td>
    </tr>
    <tr>
      <th>22</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.1829</td>
      <td>-118.6102)</td>
      <td>420</td>
      <td>6200    RANDI                        AV</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.2083</td>
      <td>-118.5776)</td>
      <td>510</td>
      <td>20400    SATICOY                      ST</td>
    </tr>
    <tr>
      <th>24</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.2083</td>
      <td>-118.5991)</td>
      <td>331</td>
      <td>21500    SATICOY                      ST</td>
    </tr>
    <tr>
      <th>25</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.1565</td>
      <td>-118.626)</td>
      <td>341</td>
      <td>22900    GERSHWIN                     DR</td>
    </tr>
    <tr>
      <th>26</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.2104</td>
      <td>-118.6368)</td>
      <td>510</td>
      <td>7700    WOODHALL                     AV</td>
    </tr>
    <tr>
      <th>27</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.2103</td>
      <td>-118.6016)</td>
      <td>331</td>
      <td>7700    OWENSMOUTH                   AV</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.1905</td>
      <td>-118.6059)</td>
      <td>440</td>
      <td>6600    TOPANGA CANYON               BL</td>
    </tr>
    <tr>
      <th>29</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.2029</td>
      <td>-118.5906)</td>
      <td>740</td>
      <td>7300    INDEPENDENCE                 AV</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>169</th>
      <td>1970</td>
      <td>1</td>
      <td>(33.9727</td>
      <td>-118.285)</td>
      <td>510</td>
      <td>7500 S  BROADWAY</td>
    </tr>
    <tr>
      <th>170</th>
      <td>1970</td>
      <td>1</td>
      <td>(33.9689</td>
      <td>-118.2739)</td>
      <td>624</td>
      <td>100 W  78TH                         ST</td>
    </tr>
    <tr>
      <th>171</th>
      <td>1970</td>
      <td>1</td>
      <td>(33.9933</td>
      <td>-118.3138)</td>
      <td>627</td>
      <td>S  GRAMERCY                     PL</td>
    </tr>
    <tr>
      <th>172</th>
      <td>1970</td>
      <td>1</td>
      <td>(33.985</td>
      <td>-118.2937)</td>
      <td>510</td>
      <td>1100 W  60TH                         PL</td>
    </tr>
    <tr>
      <th>173</th>
      <td>1970</td>
      <td>1</td>
      <td>(33.9692</td>
      <td>-118.3003)</td>
      <td>236</td>
      <td>7800 S  NORMANDIE                    AV</td>
    </tr>
    <tr>
      <th>174</th>
      <td>1970</td>
      <td>1</td>
      <td>(33.9747</td>
      <td>-118.2695)</td>
      <td>210</td>
      <td>300 E  FLORENCE                     AV</td>
    </tr>
    <tr>
      <th>175</th>
      <td>1970</td>
      <td>1</td>
      <td>(33.96</td>
      <td>-118.309)</td>
      <td>210</td>
      <td>WESTERN</td>
    </tr>
    <tr>
      <th>176</th>
      <td>1970</td>
      <td>1</td>
      <td>(33.997</td>
      <td>-118.3101)</td>
      <td>210</td>
      <td>1500 W  51ST                         ST</td>
    </tr>
    <tr>
      <th>177</th>
      <td>1970</td>
      <td>1</td>
      <td>(33.9797</td>
      <td>-118.3309)</td>
      <td>230</td>
      <td>6600    CRENSHAW                     BL</td>
    </tr>
    <tr>
      <th>178</th>
      <td>1970</td>
      <td>1</td>
      <td>(33.9892</td>
      <td>-118.3062)</td>
      <td>624</td>
      <td>1700 W  SLAUSON                      AV</td>
    </tr>
    <tr>
      <th>179</th>
      <td>1970</td>
      <td>1</td>
      <td>(33.9691</td>
      <td>-118.3308)</td>
      <td>888</td>
      <td>7800    CRENSHAW                     BL</td>
    </tr>
    <tr>
      <th>180</th>
      <td>1970</td>
      <td>1</td>
      <td>(33.9656</td>
      <td>-118.2608)</td>
      <td>410</td>
      <td>8100    MCKINLEY                     AV</td>
    </tr>
    <tr>
      <th>181</th>
      <td>1970</td>
      <td>1</td>
      <td>(33.9908</td>
      <td>-118.3367)</td>
      <td>210</td>
      <td>57TH</td>
    </tr>
    <tr>
      <th>182</th>
      <td>1970</td>
      <td>1</td>
      <td>(33.9905</td>
      <td>-118.2915)</td>
      <td>210</td>
      <td>57TH                         ST</td>
    </tr>
    <tr>
      <th>183</th>
      <td>1970</td>
      <td>1</td>
      <td>(33.9746</td>
      <td>-118.3003)</td>
      <td>626</td>
      <td>FLORENCE                     AV</td>
    </tr>
    <tr>
      <th>184</th>
      <td>1970</td>
      <td>1</td>
      <td>(33.9892</td>
      <td>-118.3089)</td>
      <td>510</td>
      <td>1800 W  SLAUSON                      AV</td>
    </tr>
    <tr>
      <th>185</th>
      <td>1970</td>
      <td>1</td>
      <td>(33.988</td>
      <td>-118.3439)</td>
      <td>320</td>
      <td>4000 W  58TH                         PL</td>
    </tr>
    <tr>
      <th>186</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.0937</td>
      <td>-118.2781)</td>
      <td>740</td>
      <td>1700    GRIFFITH PARK                BL</td>
    </tr>
    <tr>
      <th>187</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.0917</td>
      <td>-118.234)</td>
      <td>434</td>
      <td>2400    RIVERDALE                    AV</td>
    </tr>
    <tr>
      <th>188</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.0912</td>
      <td>-118.245)</td>
      <td>420</td>
      <td>1400    CERRO GORDO                  ST</td>
    </tr>
    <tr>
      <th>189</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.0941</td>
      <td>-118.2236)</td>
      <td>354</td>
      <td>3400    MACEO                        ST</td>
    </tr>
    <tr>
      <th>190</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.1211</td>
      <td>-118.2414)</td>
      <td>310</td>
      <td>3400    DREW                         ST</td>
    </tr>
    <tr>
      <th>191</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.3216</td>
      <td>-118.4958)</td>
      <td>626</td>
      <td>16600    FOOTHILL                     BL</td>
    </tr>
    <tr>
      <th>192</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.2338</td>
      <td>-118.472)</td>
      <td>930</td>
      <td>9000    ORION                        AV</td>
    </tr>
    <tr>
      <th>193</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.3039</td>
      <td>-118.4358)</td>
      <td>420</td>
      <td>13900    AZTEC                        ST</td>
    </tr>
    <tr>
      <th>194</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.3245</td>
      <td>-118.4696)</td>
      <td>341</td>
      <td>13000    GLENOAKS                     BL</td>
    </tr>
    <tr>
      <th>195</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.261</td>
      <td>-118.4698)</td>
      <td>922</td>
      <td>10600 N  SEPULVEDA                    BL</td>
    </tr>
    <tr>
      <th>196</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.2528</td>
      <td>-118.4403)</td>
      <td>745</td>
      <td>14100    VAN NUYS                     BL</td>
    </tr>
    <tr>
      <th>197</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.2229</td>
      <td>-118.4198)</td>
      <td>330</td>
      <td>13000    SCHOENBORN                   ST</td>
    </tr>
    <tr>
      <th>198</th>
      <td>1970</td>
      <td>1</td>
      <td>(34.2389</td>
      <td>-118.4536)</td>
      <td>740</td>
      <td>9200    VAN NUYS                     BL</td>
    </tr>
  </tbody>
</table>
<p>199 rows × 6 columns</p>
</div>




```python
parking.columns
```




    Index(['Ticket number', 'Issue Date', 'Issue time', 'Meter Id', 'Marked Time',
           'RP State Plate', 'Plate Expiry Date', 'VIN', 'Make', 'Body Style',
           'Color', 'Location', 'Route', 'Agency', 'Violation code',
           'Violation Description', 'Fine amount', 'Latitude', 'Longitude',
           'month'],
          dtype='object')




```python
# 5 
# 4 of 11 crimes
# Create new data with select columns

la_parking_new = parking[['Issue Date', 'month', 'Latitude', 'Longitude','Violation code', 'Location',]].copy()
la_parking_new.head()
# rename columns
la_parking_new.rename(columns={'Issue Date':'Year','month':'Month','Latitude':'Lat','Longitude':'Lon', 'Location':'Address'}, inplace=True)
la_parking_new
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
      <th>Year</th>
      <th>Month</th>
      <th>Lat</th>
      <th>Lon</th>
      <th>Violation code</th>
      <th>Address</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1970</td>
      <td>1</td>
      <td>99999.000</td>
      <td>99999.000</td>
      <td>4000A1</td>
      <td>8701 WINNETKA</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1970</td>
      <td>1</td>
      <td>6389044.544</td>
      <td>1903724.333</td>
      <td>4000A1</td>
      <td>8401 WINNETKA</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1970</td>
      <td>1</td>
      <td>6481976.496</td>
      <td>1837862.766</td>
      <td>4000A1</td>
      <td>1100 S HOPE ST</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1970</td>
      <td>1</td>
      <td>99999.000</td>
      <td>99999.000</td>
      <td>4000A1</td>
      <td>BUNKER HILL/ALPINE</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1970</td>
      <td>1</td>
      <td>99999.000</td>
      <td>99999.000</td>
      <td>4000A1</td>
      <td>HOPE/N OF VENICE</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1970</td>
      <td>1</td>
      <td>6476114.662</td>
      <td>1872692.343</td>
      <td>4000A1</td>
      <td>4730 CRYSTAL SPRING</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1970</td>
      <td>1</td>
      <td>99999.000</td>
      <td>99999.000</td>
      <td>4000A1</td>
      <td>901 E GAGE</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1970</td>
      <td>1</td>
      <td>99999.000</td>
      <td>99999.000</td>
      <td>80560000</td>
      <td>1600 W 52ND ST</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1970</td>
      <td>1</td>
      <td>6424732.340</td>
      <td>1808177.629</td>
      <td>8603</td>
      <td>6615 PACIFIC AVE</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1970</td>
      <td>1</td>
      <td>6483814.008</td>
      <td>1824574.390</td>
      <td>80560000</td>
      <td>1048 E 43RD ST</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1970</td>
      <td>1</td>
      <td>6470119.909</td>
      <td>1831801.178</td>
      <td>24</td>
      <td>1566 W JEFFERSON AVE</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1970</td>
      <td>1</td>
      <td>6477830.985</td>
      <td>1806914.271</td>
      <td>22500E</td>
      <td>218 88TH ST W</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1970</td>
      <td>1</td>
      <td>6481213.440</td>
      <td>1795030.086</td>
      <td>22500E</td>
      <td>11913 AVALON BLVD S</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1970</td>
      <td>1</td>
      <td>6478226.081</td>
      <td>1810457.067</td>
      <td>5204A-</td>
      <td>159 80TH ST E</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1970</td>
      <td>1</td>
      <td>6478226.081</td>
      <td>1810457.067</td>
      <td>22500E</td>
      <td>159 80TH ST E</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1970</td>
      <td>1</td>
      <td>6475790.703</td>
      <td>1793371.856</td>
      <td>80.69A+</td>
      <td>12400 FIGUEROA ST S</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1970</td>
      <td>1</td>
      <td>6475790.703</td>
      <td>1793371.856</td>
      <td>80.69A+</td>
      <td>12400 FIGUEROA ST S</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1970</td>
      <td>1</td>
      <td>99999.000</td>
      <td>99999.000</td>
      <td>80.56E4+</td>
      <td>16320 FIGUEROA ST S</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1970</td>
      <td>1</td>
      <td>99999.000</td>
      <td>99999.000</td>
      <td>80.61</td>
      <td>16900 VERMONT AVE S</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1970</td>
      <td>1</td>
      <td>99999.000</td>
      <td>99999.000</td>
      <td>5204A-</td>
      <td>16900 VERMONT AVE S</td>
    </tr>
    <tr>
      <th>20</th>
      <td>1970</td>
      <td>1</td>
      <td>99999.000</td>
      <td>99999.000</td>
      <td>80.61</td>
      <td>16900 VERMONT AVE S</td>
    </tr>
    <tr>
      <th>21</th>
      <td>1970</td>
      <td>1</td>
      <td>99999.000</td>
      <td>99999.000</td>
      <td>80.61</td>
      <td>16900 VERMONT AVE S</td>
    </tr>
    <tr>
      <th>22</th>
      <td>1970</td>
      <td>1</td>
      <td>99999.000</td>
      <td>99999.000</td>
      <td>80.61</td>
      <td>16900 VERMONT AVE S</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1970</td>
      <td>1</td>
      <td>99999.000</td>
      <td>99999.000</td>
      <td>80.61</td>
      <td>16900 VERMONT AVE S</td>
    </tr>
    <tr>
      <th>24</th>
      <td>1970</td>
      <td>1</td>
      <td>6473892.990</td>
      <td>1780105.276</td>
      <td>5200</td>
      <td>800 163RD ST</td>
    </tr>
    <tr>
      <th>25</th>
      <td>1970</td>
      <td>1</td>
      <td>6473892.990</td>
      <td>1780105.276</td>
      <td>80.56E4+</td>
      <td>800 163RD ST</td>
    </tr>
    <tr>
      <th>26</th>
      <td>1970</td>
      <td>1</td>
      <td>6473892.990</td>
      <td>1780105.276</td>
      <td>80.56E4+</td>
      <td>800 163RD ST</td>
    </tr>
    <tr>
      <th>27</th>
      <td>1970</td>
      <td>1</td>
      <td>99999.000</td>
      <td>99999.000</td>
      <td>80.69B</td>
      <td>15100 FIGUEROA ST S</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1970</td>
      <td>1</td>
      <td>6479608.464</td>
      <td>1742898.812</td>
      <td>80.53</td>
      <td>921 BAY VIEW AVE</td>
    </tr>
    <tr>
      <th>29</th>
      <td>1970</td>
      <td>1</td>
      <td>6485330.281</td>
      <td>1862903.541</td>
      <td>5204A-</td>
      <td>2903 W GLENHURST AVE</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>169</th>
      <td>1970</td>
      <td>1</td>
      <td>6478013.661</td>
      <td>1822196.935</td>
      <td>22500H</td>
      <td>193 48TH ST E</td>
    </tr>
    <tr>
      <th>170</th>
      <td>1970</td>
      <td>1</td>
      <td>6478093.754</td>
      <td>1822197.024</td>
      <td>22500H</td>
      <td>181 48TH ST E</td>
    </tr>
    <tr>
      <th>171</th>
      <td>1970</td>
      <td>1</td>
      <td>6474802.201</td>
      <td>1812562.723</td>
      <td>80.56E4+</td>
      <td>759 74TH ST E</td>
    </tr>
    <tr>
      <th>172</th>
      <td>1970</td>
      <td>1</td>
      <td>6474802.201</td>
      <td>1812562.723</td>
      <td>80.56E4+</td>
      <td>758 74TH ST E</td>
    </tr>
    <tr>
      <th>173</th>
      <td>1970</td>
      <td>1</td>
      <td>6471271.383</td>
      <td>1820382.673</td>
      <td>22500E</td>
      <td>1309 53RD ST W</td>
    </tr>
    <tr>
      <th>174</th>
      <td>1970</td>
      <td>1</td>
      <td>6471095.518</td>
      <td>1816748.834</td>
      <td>22507.8A-</td>
      <td>1333 61ST ST W</td>
    </tr>
    <tr>
      <th>175</th>
      <td>1970</td>
      <td>1</td>
      <td>6474466.453</td>
      <td>1810394.340</td>
      <td>80.61</td>
      <td>822 80TH ST W</td>
    </tr>
    <tr>
      <th>176</th>
      <td>1970</td>
      <td>1</td>
      <td>6474466.453</td>
      <td>1810394.340</td>
      <td>80.61</td>
      <td>822 80TH ST W</td>
    </tr>
    <tr>
      <th>177</th>
      <td>1970</td>
      <td>1</td>
      <td>6456559.393</td>
      <td>1828067.866</td>
      <td>80.61</td>
      <td>3878 POTOMAC AVE</td>
    </tr>
    <tr>
      <th>178</th>
      <td>1970</td>
      <td>1</td>
      <td>6456559.393</td>
      <td>1828067.866</td>
      <td>80.61</td>
      <td>3878 POTOMAC AVE</td>
    </tr>
    <tr>
      <th>179</th>
      <td>1970</td>
      <td>1</td>
      <td>6468891.347</td>
      <td>1830487.384</td>
      <td>22500E</td>
      <td>1603 WEST 36TH PLACE</td>
    </tr>
    <tr>
      <th>180</th>
      <td>1970</td>
      <td>1</td>
      <td>6471992.730</td>
      <td>1827654.509</td>
      <td>22500E</td>
      <td>3919 SOUTH BUDLONG AVENUE</td>
    </tr>
    <tr>
      <th>181</th>
      <td>1970</td>
      <td>1</td>
      <td>6455226.192</td>
      <td>1827437.031</td>
      <td>80.61</td>
      <td>4040 NICOLET AVENUE</td>
    </tr>
    <tr>
      <th>182</th>
      <td>1970</td>
      <td>1</td>
      <td>6455226.192</td>
      <td>1827437.031</td>
      <td>80.61</td>
      <td>4040 NICOLET AVENUE</td>
    </tr>
    <tr>
      <th>183</th>
      <td>1970</td>
      <td>1</td>
      <td>6455575.025</td>
      <td>1827529.365</td>
      <td>80.61</td>
      <td>4025 COCO AVE</td>
    </tr>
    <tr>
      <th>184</th>
      <td>1970</td>
      <td>1</td>
      <td>6455194.531</td>
      <td>1827179.480</td>
      <td>80.61</td>
      <td>4061 NICOLET AVE</td>
    </tr>
    <tr>
      <th>185</th>
      <td>1970</td>
      <td>1</td>
      <td>6455461.577</td>
      <td>1827253.005</td>
      <td>80.61</td>
      <td>4065 COCO AVENUE</td>
    </tr>
    <tr>
      <th>186</th>
      <td>1970</td>
      <td>1</td>
      <td>6455325.121</td>
      <td>1828262.521</td>
      <td>5204A-</td>
      <td>3939 NICOLET AVENUE</td>
    </tr>
    <tr>
      <th>187</th>
      <td>1970</td>
      <td>1</td>
      <td>6455325.121</td>
      <td>1828262.521</td>
      <td>80.61</td>
      <td>3939 NICOLET AVENUE</td>
    </tr>
    <tr>
      <th>188</th>
      <td>1970</td>
      <td>1</td>
      <td>6455325.121</td>
      <td>1828262.521</td>
      <td>80.61</td>
      <td>3939 NICOLET AVENUE</td>
    </tr>
    <tr>
      <th>189</th>
      <td>1970</td>
      <td>1</td>
      <td>6454864.481</td>
      <td>1828351.704</td>
      <td>80.61</td>
      <td>3930 URSULA AVE</td>
    </tr>
    <tr>
      <th>190</th>
      <td>1970</td>
      <td>1</td>
      <td>6457067.087</td>
      <td>1829939.294</td>
      <td>80.71.3</td>
      <td>3640 CHESAPEAKE AVENUE</td>
    </tr>
    <tr>
      <th>191</th>
      <td>1970</td>
      <td>1</td>
      <td>6465731.433</td>
      <td>1831134.846</td>
      <td>5204A-</td>
      <td>2050 WEST 35TH PLACE</td>
    </tr>
    <tr>
      <th>192</th>
      <td>1970</td>
      <td>1</td>
      <td>6465731.433</td>
      <td>1831134.846</td>
      <td>22500E</td>
      <td>2050 WEST 35TH PLACE</td>
    </tr>
    <tr>
      <th>193</th>
      <td>1970</td>
      <td>1</td>
      <td>6471115.782</td>
      <td>1841031.581</td>
      <td>80.56E4+</td>
      <td>1101 SOUTH MARIPOSA AVENUE</td>
    </tr>
    <tr>
      <th>194</th>
      <td>1970</td>
      <td>1</td>
      <td>6471432.694</td>
      <td>1841084.871</td>
      <td>80.56E4+</td>
      <td>1091 FEDORA ST</td>
    </tr>
    <tr>
      <th>195</th>
      <td>1970</td>
      <td>1</td>
      <td>6468706.413</td>
      <td>1835745.541</td>
      <td>80.56E4+</td>
      <td>2025 WEST 22ND STREET</td>
    </tr>
    <tr>
      <th>196</th>
      <td>1970</td>
      <td>1</td>
      <td>6471989.947</td>
      <td>1826831.094</td>
      <td>22500E</td>
      <td>3980 SOUTH BUDLONG AVENUE</td>
    </tr>
    <tr>
      <th>197</th>
      <td>1970</td>
      <td>1</td>
      <td>6471989.947</td>
      <td>1826831.094</td>
      <td>22500E</td>
      <td>3980 BUDLONG AVENUE</td>
    </tr>
    <tr>
      <th>198</th>
      <td>1970</td>
      <td>1</td>
      <td>6440401.435</td>
      <td>1882622.935</td>
      <td>80.56E4+</td>
      <td>12300 MAGNOLIA AVE</td>
    </tr>
  </tbody>
</table>
<p>199 rows × 6 columns</p>
</div>



###  Connect to local database


```python
# 6
# 5 of 11 crimes
### Connect to local database
rds_connection_string = "root:modelobootcamp@127.0.0.1/ladata_db"
engine = create_engine(f'mysql://{rds_connection_string}')
connection = engine.connect()
```


```python
# 7
# 6 of 11 crimes
connection.execute('use ladata_db;')
```




    <sqlalchemy.engine.result.ResultProxy at 0x1aa52255828>




```python
# 8
# 7 of 11 crimes
engine.table_names()
```




    ['crime',
     'crimes_la',
     'crimes_la_new',
     'parking',
     'parking_crime',
     'parking_la',
     'parking_la_new',
     'parkings']




```python
# 9
# 8 of 11 crimes
la_crimes_new.to_sql(name='crimes_la_new', con=engine, if_exists='append', index=False)
```


```python
# 20
# 8 of 11 parking
la_parking_new.to_sql(name='parking_la_new', con=engine, if_exists='append', index=False)
```


```python
# 10
# 9 of 11 crimes
results = engine.execute('select * from crimes_la_new;')
```


```python
# 21
# 9 of 11 parking
results = engine.execute('select * from parking_la_new;')
```

### Confirm data has been added by querying the parking_la table


```python
connection.execute('use ladata_db;')
```




    <sqlalchemy.engine.result.ResultProxy at 0x1aa522039e8>




```python
for item in results:
    print(item)
```

    (1970, 1, 99999.0, 99999.0, '4000A1', '8701 WINNETKA')
    (1970, 1, 6389044.544, 1903724.333, '4000A1', '8401 WINNETKA')
    (1970, 1, 6481976.496, 1837862.7659999998, '4000A1', '1100 S HOPE ST')
    (1970, 1, 99999.0, 99999.0, '4000A1', 'BUNKER HILL/ALPINE')
    (1970, 1, 99999.0, 99999.0, '4000A1', 'HOPE/N OF VENICE')
    (1970, 1, 6476114.6620000005, 1872692.343, '4000A1', '4730 CRYSTAL SPRING')
    (1970, 1, 99999.0, 99999.0, '4000A1', '901 E GAGE')
    (1970, 1, 99999.0, 99999.0, '80560000', '1600 W 52ND ST')
    (1970, 1, 6424732.34, 1808177.629, '8603', '6615 PACIFIC AVE')
    (1970, 1, 6483814.007999999, 1824574.39, '80560000', '1048 E 43RD ST')
    (1970, 1, 6470119.909, 1831801.178, '24', '1566 W JEFFERSON AVE')
    (1970, 1, 6477830.985, 1806914.271, '22500E', '218 88TH ST W')
    (1970, 1, 6481213.44, 1795030.086, '22500E', '11913 AVALON BLVD S')
    (1970, 1, 6478226.081, 1810457.0669999998, '5204A-', '159 80TH ST E')
    (1970, 1, 6478226.081, 1810457.0669999998, '22500E', '159 80TH ST E')
    (1970, 1, 6475790.703, 1793371.856, '80.69A+', '12400 FIGUEROA ST S')
    (1970, 1, 6475790.703, 1793371.856, '80.69A+', '12400 FIGUEROA ST S')
    (1970, 1, 99999.0, 99999.0, '80.56E4+', '16320 FIGUEROA ST S')
    (1970, 1, 99999.0, 99999.0, '80.61', '16900 VERMONT AVE S')
    (1970, 1, 99999.0, 99999.0, '5204A-', '16900 VERMONT AVE S')
    (1970, 1, 99999.0, 99999.0, '80.61', '16900 VERMONT AVE S')
    (1970, 1, 99999.0, 99999.0, '80.61', '16900 VERMONT AVE S')
    (1970, 1, 99999.0, 99999.0, '80.61', '16900 VERMONT AVE S')
    (1970, 1, 99999.0, 99999.0, '80.61', '16900 VERMONT AVE S')
    (1970, 1, 6473892.99, 1780105.2759999998, '5200', '800 163RD ST')
    (1970, 1, 6473892.99, 1780105.2759999998, '80.56E4+', '800 163RD ST')
    (1970, 1, 6473892.99, 1780105.2759999998, '80.56E4+', '800 163RD ST')
    (1970, 1, 99999.0, 99999.0, '80.69B', '15100 FIGUEROA ST S')
    (1970, 1, 6479608.464, 1742898.812, '80.53', '921 BAY VIEW AVE')
    (1970, 1, 6485330.281, 1862903.541, '5204A-', '2903 W GLENHURST AVE')
    (1970, 1, 6484997.397000001, 1862632.9109999998, '80.71.3', '3014 W GLENHURST AVE')
    (1970, 1, 6485061.482000001, 1862656.6069999998, '5204A-', '3003 W GLENHURST AVE')
    (1970, 1, 6484997.397000001, 1862632.9109999998, '5204A-', '3014 W GLENHURST AVE')
    (1970, 1, 6484708.629, 1862668.216, '80.71.3', '3047 W GLENHURST AVE')
    (1970, 1, 6484201.28, 1862657.7969999998, '5204A-', '3118 W GLENHURST AVE')
    (1970, 1, 6483777.636, 1863097.9440000001, '5204A-', '3221 W GLENHURST AVE')
    (1970, 1, 6483752.716, 1863123.835, '5204A-', '3226 W GLENHURST AVE')
    (1970, 1, 6483744.409, 1863132.465, '5204A-', '3229 W GLENHURST AVE')
    (1970, 1, 6484051.759, 1862813.1430000002, '22500F', '3155 W GLENHURST AVE')
    (1970, 1, 6483744.409, 1863132.465, '5204A-', '3229 W GLENHURST AVE')
    (1970, 1, 6483719.489, 1863158.356, '5204A-', '3234 W GLENHURST AVE')
    (1970, 1, 6483702.875, 1863175.6169999999, '5204A-', '3238 W GLENHURST AVE')
    (1970, 1, 6483227.778, 1863669.2140000002, '5204A-', '3342 W GLENHURST AVE')
    (1970, 1, 6482820.717, 1864092.126, '5204A-', '3428 W GLENHURST AVE')
    (1970, 1, 6483183.738, 1857827.9419999998, '5204A-', '2300 GLENDALE BLVD N')
    (1970, 1, 6483362.177999999, 1855985.426, '80.69.2', '2030 GLENDALE BLVD N')
    (1970, 1, 6483565.9520000005, 1852889.6090000002, '5204A-', '1917 W DELTA ST')
    (1970, 1, 6483565.9520000005, 1852889.6090000002, '80.61', '1917 W DELTA ST')
    (1970, 1, 6484845.142000001, 1851894.18, '5204A-', '1571 N PARMER AVE')
    (1970, 1, 6484552.235, 1851429.824, '5204A-', '1524 W SCOTT AVE')
    (1970, 1, 6484780.765, 1852156.708, '5204A-', '1612 N MORTON AVE')
    (1970, 1, 6484818.243, 1852180.01, '5204A-', '1619 N MORTON AVE')
    (1970, 1, 6484761.873, 1851601.9119999998, '22500F', '1529 N PARMER AVE')
    (1970, 1, 6484733.757999999, 1851500.4519999998, '22500F', '1516 N PARMER AVE')
    (1970, 1, 6484733.757999999, 1851500.4519999998, '22500F', '1516 N PARMER AVE')
    (1970, 1, 6483828.449, 1850587.6919999998, '5204A-', '1320 ECHO PARK AVE N')
    (1970, 1, 6484295.433999999, 1850123.5369999998, '5204A-', '1509 SUNSET BLVD W')
    (1970, 1, 6485435.997, 1849524.841, '80.56E4+', '1300 N DOUGLAS ST')
    (1970, 1, 6485314.243, 1849157.2959999999, '22500H', '1370 W ALLISON AVE')
    (1970, 1, 6485198.757999999, 1849265.616, '22500H', '1210 N DOUGLAS ST')
    (1970, 1, 6486427.373, 1845930.844, '5204A-', '1000 SUNSET BLVD W')
    (1970, 1, 6483561.933999999, 1841237.084, '22500.1+', '550 FIGUEROA ST N')
    (1970, 1, 6488213.4860000005, 1845334.7480000001, '80.61', '760 N HILL PL')
    (1970, 1, 6489455.595, 1844485.1, '22500F', '741 N NEW HIGH ST')
    (1970, 1, 6483879.786, 1844535.332, '5204A-', '1238 1ST ST W')
    (1970, 1, 6483879.786, 1844535.332, '80.61', '1238 1ST ST W')
    (1970, 1, 6483879.786, 1844535.332, '80.61', '1238 1ST ST W')
    (1970, 1, 6483335.126, 1844653.6409999998, '80.56E4+', '200 TOLUCA ST S')
    (1970, 1, 6482703.015, 1845124.456, '80.61', '108 S WITMER ST')
    (1970, 1, 6482306.431, 1844379.9980000001, '80.56E4+', '231 S WITMER ST')
    (1970, 1, 6480518.771000001, 1841476.815, '80.69B', '715 S WITMER ST')
    (1970, 1, 6480252.362000001, 1841539.989, '22500A', '715 S COLUMBIA AVE')
    (1970, 1, 6480431.271000001, 1841970.98, '80.56E4+', '1348 W INGRAHAM ST')
    (1970, 1, 6480139.978999999, 1841923.698, '80.56E4+', '689 S VALENCIA ST')
    (1970, 1, 6480700.081, 1841824.5669999998, '5204A-', '1319 W INGRAHAM ST')
    (1970, 1, 6480700.081, 1841824.5669999998, '80.61', '1319 W INGRAHAM ST')
    (1970, 1, 6480700.081, 1841824.5669999998, '80.61', '1319 W INGRAHAM ST')
    (1970, 1, 6480095.991, 1843660.0280000002, '80.56E4+', '530 UNION AVE S')
    (1970, 1, 6480274.922, 1843741.4540000001, '22502A', '1620 5TH ST W')
    (1970, 1, 6480274.922, 1843741.4540000001, '80.56E4+', '1620 5TH ST W')
    (1970, 1, 6480301.711, 1843727.0480000002, '80.56E4+', '1600 5TH ST W')
    (1970, 1, 6479716.927999999, 1843876.7319999998, '80.56E4+', '1801 5TH ST W')
    (1970, 1, 6479768.79, 1843971.802, '80.56E4+', '460 BURLINGTON AVE S')
    (1970, 1, 6479768.79, 1843971.802, '80.56E4+', '460 BURLINGTON AVE S')
    (1970, 1, 6481020.057, 1845596.355, '22500E', '215 UNION AVE S')
    (1970, 1, 6480731.482999999, 1845047.89, '80.61', '260 UNION AVE S')
    (1970, 1, 6480731.482999999, 1845047.89, '80.61', '260 UNION AVE S')
    (1970, 1, 6481604.789, 1845513.4009999998, '80.61', '133 S UNION PL')
    (1970, 1, 6481387.217, 1845313.8930000002, '80.61', '150 S UNION PL')
    (1970, 1, 6481387.217, 1845313.8930000002, '80.61', '150 S UNION PL')
    (1970, 1, 6430794.714, 1828461.1709999999, '5204A-', '11736 WOODBINE STREET')
    (1970, 1, 6387241.847999999, 1898255.852, '5200', '20404 COHASSET STREET')
    (1970, 1, 6387241.847999999, 1898255.852, '22514', '20404 COHASSET STREET')
    (1970, 1, 6386964.247, 1898696.77, '80.69B', '20404 SATICOY STREET')
    (1970, 1, 6400894.475, 1894425.991, '22500E', '6946 ETIWANDA AVE')
    (1970, 1, 6400339.9229999995, 1893101.0969999998, '22500F', '6741 DARBY AVENUE')
    (1970, 1, 6400337.726, 1892542.7019999998, '22500F', '6615 DARBY AVENUE')
    (1970, 1, 6399369.291, 1886322.951, '22500E', '18525 COLLINS STREET')
    (1970, 1, 6425663.215, 1898547.917, '80.56E4+', '14542 SATICOY STREET')
    (1970, 1, 6426756.266, 1896740.906, '80.56E4+', '7320 LENNOX AVENUE')
    (1970, 1, 6428631.75, 1897542.354, '80.56E4+', '14100 RUNNYMEDE STREET')
    (1970, 1, 6428631.75, 1897542.354, '80.56E4+', '14100 RUNNYMEDE STREET')
    (1970, 1, 6428623.092, 1895219.1169999999, '5204A-', '14100 GAULT STREET')
    (1970, 1, 6427961.906, 1894942.9419999998, '80.56E4+', '7056 CALHOUN AVENUE')
    (1970, 1, 6428624.118, 1895480.311, '22500H', '7139 HAZELTINE AVENUE')
    (1970, 1, 6448020.938999999, 1836302.096, '805.6', '6041 CADILLAC AVE')
    (1970, 1, 6448020.938999999, 1836302.096, '805.6', '6041 CADILLAC AVE')
    (1970, 1, 6461663.41, 1840537.876, '22514', '1245 PLYMOUTH BLVD')
    (1970, 1, 6452328.102000001, 1835031.7659999998, '80.56E4+', '5400 APPLE ST')
    (1970, 1, 6459300.106000001, 1838801.9019999998, '22500E', '1667 VINEYARD AVE')
    (1970, 1, 6456825.371, 1845528.78, '22500E', '664 CLOVERDALE AVE')
    (1970, 1, 6471693.886, 1845655.5469999998, '80.69B', '3466 6TH ST W')
    (1970, 1, 6471693.886, 1845655.5469999998, '80.69B', '3466 6TH ST W')
    (1970, 1, 6456185.873, 1846061.3180000002, '80.56E4+', '613 DUNSMUIR AVE')
    (1970, 1, 6469244.325, 1851269.116, '80.56E4+', '4626 ROSEWOOD AVE W')
    (1970, 1, 6469083.456, 1851970.918, '80.56E4+', '557 HOBART BLVD N')
    (1970, 1, 6469433.746, 1852264.8909999998, '80.56E4+', '603 HARVARD BLVD N')
    (1970, 1, 6452095.365, 1851747.032, '80.56E4+', '7924 ROSEWOOD AVE W')
    (1970, 1, 6451851.845, 1851889.052, '80.56E4+', '526 HAYWORTH AVE N')
    (1970, 1, 6500393.782000001, 1861688.5480000002, '5204A-', '300 AVENUE 51 N')
    (1970, 1, 6500393.782000001, 1861688.5480000002, '80.56E4+', '300 AVENUE 51 N')
    (1970, 1, 6503141.165, 1862557.497, '22500E', '126 AVENUE 57 N')
    (1970, 1, 6502380.703, 1862926.404, '22514', '317 AVENUE 56 S')
    (1970, 1, 6503451.012999999, 1860227.9319999998, '80.56E4+', '5703 VIA MARISOL')
    (1970, 1, 6502800.602000001, 1863135.7959999999, '80.56E4+', '303 AVENUE 57 S')
    (1970, 1, 6502117.199, 1862452.189, '5204A-', '250 AVENUE 55 S')
    (1970, 1, 6502117.199, 1862452.189, '22514', '250 AVENUE 55 S')
    (1970, 1, 6487523.501, 1860368.503, '80.56E4+', '3001 NORTH COOLIDGE AVE')
    (1970, 1, 6487336.22, 1860158.0080000001, '80.56E4+', '2951 NORTH COOLIDGE AVE')
    (1970, 1, 6484589.012, 1852002.235, '80.56E4+', '1556 MORTON AVE')
    (1970, 1, 6484007.48, 1850928.4530000002, '80.56E4+', '1400 FAIRBANKS PL')
    (1970, 1, 6484007.48, 1850928.4530000002, '80.56E4+', '1400 FAIRBANKS PL')
    (1970, 1, 6484007.48, 1850928.4530000002, '80.56E4+', '1400 FAIRBANKS PL')
    (1970, 1, 6482630.757999999, 1837353.755, '80.56E4+', '301 11TH ST E')
    (1970, 1, 6480048.393999999, 1839610.3090000001, '22514', '1236 OLYMPIC BLVD E')
    (1970, 1, 6487687.866, 1834132.62, '80.56E4+', '903 CENTRAL AVE S')
    (1970, 1, 6480054.172, 1839607.1819999998, '22514', '1234 OLYMPIC BLVD E')
    (1970, 1, 6489664.696, 1844363.781, '22502E', '716 SPRING ST S')
    (1970, 1, 6423281.741, 1879908.604, '22500E', '4750 KESTER AVE')
    (1970, 1, 6429329.721, 1893245.791, '80.56E4+', '13990 VANOWEN STREET')
    (1970, 1, 6426967.557, 1893925.025, '80.56E4+', '6901 LENNOX AVENUE')
    (1970, 1, 6389647.301, 1904601.2480000001, '80.56E4+', '14780 CHASE STREET')
    (1970, 1, 6424092.756, 1904477.085, '80.56E4+', '14789 CHASE STREET')
    (1970, 1, 99999.0, 99999.0, '80.56E4+', '8701 NOBLE AVENUE')
    (1970, 1, 6426541.107999999, 1897220.81, '80.56E4+', '14400 VALERIO STREET')
    (1970, 1, 6426358.862000001, 1897221.584, '5200', '14435 VALERIO STREET')
    (1970, 1, 6426358.862000001, 1897221.584, '80.56E4+', '14435 VALERIO STREET')
    (1970, 1, 6426468.315, 1897221.096, '5200', '14417 VALERIO STREET')
    (1970, 1, 6426468.315, 1897221.096, '80.56E4+', '14417 VALERIO STREET')
    (1970, 1, 6418529.39, 1817510.753, '80.69B', '1827 SPEEDWAY')
    (1970, 1, 6418327.6620000005, 1818107.78, '5204A-', '52 WINDWARD AVE')
    (1970, 1, 6418327.6620000005, 1818107.78, '805.6', '52 WINDWARD AVE')
    (1970, 1, 6418032.762999999, 1818514.677, '80.56E4+', '44 HORIZON AVE')
    (1970, 1, 6418086.998, 1819707.525, '22514', '1011 MAIN ST')
    (1970, 1, 6437034.231000001, 1829591.007, '22514', '3700 WESTWOOD BLVD')
    (1970, 1, 6436767.128, 1830001.458, '22500F', '3640 WESTWOOD BLVD')
    (1970, 1, 6436674.602999999, 1829410.7869999998, '80.56E4+', '3700 MIDVALE AVE')
    (1970, 1, 6416631.312999999, 1820653.606, '80.69B', '51 DUDLEY CT')
    (1970, 1, 99999.0, 99999.0, '80.69AA+', 'HURRICANE/ SPEEDWAY')
    (1970, 1, 6417451.174, 1819848.826, '80.69AA+', '807 PACIFIC AVE')
    (1970, 1, 6423794.973999999, 1823203.0680000002, '22502A', '1246 PALMS BLVD')
    (1970, 1, 6473115.297, 1823848.5019999999, '80.69.2', '1029 VERNON AVE E')
    (1970, 1, 6477987.017000001, 1821885.389, '80.56E4+', '197 49TH ST E')
    (1970, 1, 6477946.97, 1821885.344, '80.56E4+', '203 49TH ST E')
    (1970, 1, 6481278.685, 1820938.979, '80.56E4+', '5200 AVALON BLVD S')
    (1970, 1, 6472070.502, 1823855.0269999998, '5204A-', '1180 VERNON AVE E')
    (1970, 1, 6472070.502, 1823855.0269999998, '22500E', '1180 VERNON AVE E')
    (1970, 1, 6478053.708, 1822196.98, '22500H', '187 48TH ST E')
    (1970, 1, 6478013.661, 1822196.935, '22500H', '193 48TH ST E')
    (1970, 1, 6478013.661, 1822196.935, '22500H', '193 48TH ST E')
    (1970, 1, 6478093.754, 1822197.024, '22500H', '181 48TH ST E')
    (1970, 1, 6474802.201, 1812562.7230000002, '80.56E4+', '759 74TH ST E')
    (1970, 1, 6474802.201, 1812562.7230000002, '80.56E4+', '758 74TH ST E')
    (1970, 1, 6471271.382999999, 1820382.6730000002, '22500E', '1309 53RD ST W')
    (1970, 1, 6471095.517999999, 1816748.834, '22507.8A-', '1333 61ST ST W')
    (1970, 1, 6474466.453, 1810394.34, '80.61', '822 80TH ST W')
    (1970, 1, 6474466.453, 1810394.34, '80.61', '822 80TH ST W')
    (1970, 1, 6456559.392999999, 1828067.866, '80.61', '3878 POTOMAC AVE')
    (1970, 1, 6456559.392999999, 1828067.866, '80.61', '3878 POTOMAC AVE')
    (1970, 1, 6468891.347, 1830487.384, '22500E', '1603 WEST 36TH PLACE')
    (1970, 1, 6471992.73, 1827654.509, '22500E', '3919 SOUTH BUDLONG AVENUE')
    (1970, 1, 6455226.192000001, 1827437.031, '80.61', '4040 NICOLET AVENUE')
    (1970, 1, 6455226.192000001, 1827437.031, '80.61', '4040 NICOLET AVENUE')
    (1970, 1, 6455575.025, 1827529.365, '80.61', '4025 COCO AVE')
    (1970, 1, 6455194.531, 1827179.48, '80.61', '4061 NICOLET AVE')
    (1970, 1, 6455461.5770000005, 1827253.005, '80.61', '4065 COCO AVENUE')
    (1970, 1, 6455325.121, 1828262.521, '5204A-', '3939 NICOLET AVENUE')
    (1970, 1, 6455325.121, 1828262.521, '80.61', '3939 NICOLET AVENUE')
    (1970, 1, 6455325.121, 1828262.521, '80.61', '3939 NICOLET AVENUE')
    (1970, 1, 6454864.481000001, 1828351.7040000001, '80.61', '3930 URSULA AVE')
    (1970, 1, 6457067.087, 1829939.294, '80.71.3', '3640 CHESAPEAKE AVENUE')
    (1970, 1, 6465731.432999999, 1831134.846, '5204A-', '2050 WEST 35TH PLACE')
    (1970, 1, 6465731.432999999, 1831134.846, '22500E', '2050 WEST 35TH PLACE')
    (1970, 1, 6471115.782000001, 1841031.581, '80.56E4+', '1101 SOUTH MARIPOSA AVENUE')
    (1970, 1, 6471432.694, 1841084.871, '80.56E4+', '1091 FEDORA ST')
    (1970, 1, 6468706.413, 1835745.541, '80.56E4+', '2025 WEST 22ND STREET')
    (1970, 1, 6471989.947000001, 1826831.094, '22500E', '3980 SOUTH BUDLONG AVENUE')
    (1970, 1, 6471989.947000001, 1826831.094, '22500E', '3980 BUDLONG AVENUE')
    (1970, 1, 6440401.435, 1882622.935, '80.56E4+', '12300 MAGNOLIA AVE')
    
