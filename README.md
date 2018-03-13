

```python
from citipy import citipy
from random import uniform
import pandas as pd
import numpy as np
import csv
import random
import matplotlib.pyplot as plt
import requests
import json
from datetime import datetime as dt

from config import maps_key, place_key, api_key
```

Overall, the maximum temperture increases as the latitude gets closer to 0. The temperature decreases as the latitude gets further from 0. Since 0 is where the equator is, this suggests that temperature is hotter by the equator!






```python
##generate random lat, long

city = {}
cities = []
#country = []
def newpoint():
    return uniform(-180,180), uniform(-90, 90)

while len(cities) < 850:
    points = []
    points = list((newpoint() for x in range(850)))
    for i in range(len(points)):
        lat = points[i][0]
        long = points[i][1]
        city[citipy.nearest_city(lat,long).city_name] = points[i]
#        country.append(citipy.nearest_city(lat,long).country_code)
    cities = list(set(city))
    
```


```python
a = list(city.keys())

city_df = pd.DataFrame([city for city in a], columns=["City"])

# city_df = pd.DataFrame.from_dict(city, orient='columns', dtype=None)
#city_df
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
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ushuaia</td>
    </tr>
    <tr>
      <th>1</th>
      <td>longyearbyen</td>
    </tr>
    <tr>
      <th>2</th>
      <td>sault sainte marie</td>
    </tr>
    <tr>
      <th>3</th>
      <td>albany</td>
    </tr>
    <tr>
      <th>4</th>
      <td>shubarkuduk</td>
    </tr>
    <tr>
      <th>5</th>
      <td>hermanus</td>
    </tr>
    <tr>
      <th>6</th>
      <td>illoqqortoormiut</td>
    </tr>
    <tr>
      <th>7</th>
      <td>jamestown</td>
    </tr>
    <tr>
      <th>8</th>
      <td>qaanaaq</td>
    </tr>
    <tr>
      <th>9</th>
      <td>vardo</td>
    </tr>
    <tr>
      <th>10</th>
      <td>belushya guba</td>
    </tr>
    <tr>
      <th>11</th>
      <td>tapaua</td>
    </tr>
    <tr>
      <th>12</th>
      <td>tatawin</td>
    </tr>
    <tr>
      <th>13</th>
      <td>hithadhoo</td>
    </tr>
    <tr>
      <th>14</th>
      <td>kambove</td>
    </tr>
    <tr>
      <th>15</th>
      <td>berbera</td>
    </tr>
    <tr>
      <th>16</th>
      <td>constantine</td>
    </tr>
    <tr>
      <th>17</th>
      <td>port elizabeth</td>
    </tr>
    <tr>
      <th>18</th>
      <td>nkoteng</td>
    </tr>
    <tr>
      <th>19</th>
      <td>dikson</td>
    </tr>
    <tr>
      <th>20</th>
      <td>lebu</td>
    </tr>
    <tr>
      <th>21</th>
      <td>inhambane</td>
    </tr>
    <tr>
      <th>22</th>
      <td>bredasdorp</td>
    </tr>
    <tr>
      <th>23</th>
      <td>comodoro rivadavia</td>
    </tr>
    <tr>
      <th>24</th>
      <td>barentsburg</td>
    </tr>
    <tr>
      <th>25</th>
      <td>port alfred</td>
    </tr>
    <tr>
      <th>26</th>
      <td>narsaq</td>
    </tr>
    <tr>
      <th>27</th>
      <td>kutum</td>
    </tr>
    <tr>
      <th>28</th>
      <td>taolanaro</td>
    </tr>
    <tr>
      <th>29</th>
      <td>marcona</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>804</th>
      <td>severnyy</td>
    </tr>
    <tr>
      <th>805</th>
      <td>beawar</td>
    </tr>
    <tr>
      <th>806</th>
      <td>jaleswar</td>
    </tr>
    <tr>
      <th>807</th>
      <td>gurgan</td>
    </tr>
    <tr>
      <th>808</th>
      <td>nioro</td>
    </tr>
    <tr>
      <th>809</th>
      <td>boende</td>
    </tr>
    <tr>
      <th>810</th>
      <td>mozelos</td>
    </tr>
    <tr>
      <th>811</th>
      <td>coruripe</td>
    </tr>
    <tr>
      <th>812</th>
      <td>kegayli</td>
    </tr>
    <tr>
      <th>813</th>
      <td>beloha</td>
    </tr>
    <tr>
      <th>814</th>
      <td>rio do sul</td>
    </tr>
    <tr>
      <th>815</th>
      <td>novyy urengoy</td>
    </tr>
    <tr>
      <th>816</th>
      <td>kaniv</td>
    </tr>
    <tr>
      <th>817</th>
      <td>amli</td>
    </tr>
    <tr>
      <th>818</th>
      <td>thrapsanon</td>
    </tr>
    <tr>
      <th>819</th>
      <td>lagos</td>
    </tr>
    <tr>
      <th>820</th>
      <td>keti bandar</td>
    </tr>
    <tr>
      <th>821</th>
      <td>muramvya</td>
    </tr>
    <tr>
      <th>822</th>
      <td>sidi ali</td>
    </tr>
    <tr>
      <th>823</th>
      <td>lisakovsk</td>
    </tr>
    <tr>
      <th>824</th>
      <td>liniere</td>
    </tr>
    <tr>
      <th>825</th>
      <td>coyaima</td>
    </tr>
    <tr>
      <th>826</th>
      <td>falmouth</td>
    </tr>
    <tr>
      <th>827</th>
      <td>wahran</td>
    </tr>
    <tr>
      <th>828</th>
      <td>yuryevets</td>
    </tr>
    <tr>
      <th>829</th>
      <td>kasane</td>
    </tr>
    <tr>
      <th>830</th>
      <td>endicott</td>
    </tr>
    <tr>
      <th>831</th>
      <td>aquiraz</td>
    </tr>
    <tr>
      <th>832</th>
      <td>adra</td>
    </tr>
    <tr>
      <th>833</th>
      <td>kalininsk</td>
    </tr>
  </tbody>
</table>
<p>834 rows × 1 columns</p>
</div>




```python



for index, row in city_df.iterrows():
    lat = city[a[index]][0]
    long = city[a[index]][1]
   # country1 = country[index]
    city_df.set_value(index, "Lat", lat)
    city_df.set_value(index, "Long", long)
#    city_df.set_value(index, "Country", country1)
```


```python
city_df
```


```python

city_df["Country"] = ""
city_df["Lat"] = ""
city_df["Long"] = ""
for index, row in city_df.iterrows():
    target_city = city_df["City"][index]
    target_url = "https://maps.googleapis.com/maps/api/geocode/json?" \
    "address=%s&key=%s" % (target_city, maps_key)
    geo_data = requests.get(target_url).json()
    try:
        lat = geo_data["results"][0]["geometry"]["location"]["lat"]
        lng = geo_data["results"][0]["geometry"]["location"]["lng"]
        country = geo_data["results"][0]["address_components"][3]["long_name"]
    except IndexError:
        lat = np.NaN
        lng = np.NaN
        country = np.NaN
    #print("settings values " +city_df["City"][index])
    city_df.set_value(index, "Country", country)
    city_df.set_value(index, "Lat", lat)
    city_df.set_value(index, "Long", lng)
```


```python

geo_data["results"]
```




    []




```python
target_city
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
      <th>City</th>
      <th>Country</th>
      <th>Lat</th>
      <th>Long</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ushuaia</td>
      <td>Argentina</td>
      <td>-54.8019</td>
      <td>-68.303</td>
    </tr>
    <tr>
      <th>1</th>
      <td>longyearbyen</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>sault sainte marie</td>
      <td>United States</td>
      <td>46.4977</td>
      <td>-84.3476</td>
    </tr>
    <tr>
      <th>3</th>
      <td>albany</td>
      <td>United States</td>
      <td>42.6526</td>
      <td>-73.7562</td>
    </tr>
    <tr>
      <th>4</th>
      <td>shubarkuduk</td>
      <td>Kazakhstan</td>
      <td>49.143</td>
      <td>56.4817</td>
    </tr>
    <tr>
      <th>5</th>
      <td>hermanus</td>
      <td>South Africa</td>
      <td>-34.4092</td>
      <td>19.2504</td>
    </tr>
    <tr>
      <th>6</th>
      <td>illoqqortoormiut</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>jamestown</td>
      <td>Virginia</td>
      <td>37.2116</td>
      <td>-76.7752</td>
    </tr>
    <tr>
      <th>8</th>
      <td>qaanaaq</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>vardo</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10</th>
      <td>belushya guba</td>
      <td>Russia</td>
      <td>71.5456</td>
      <td>52.3203</td>
    </tr>
    <tr>
      <th>11</th>
      <td>tapaua</td>
      <td>69480-000</td>
      <td>-5.62504</td>
      <td>-63.189</td>
    </tr>
    <tr>
      <th>12</th>
      <td>tatawin</td>
      <td>Tunisia</td>
      <td>32.9211</td>
      <td>10.4509</td>
    </tr>
    <tr>
      <th>13</th>
      <td>hithadhoo</td>
      <td>Maldives</td>
      <td>-0.606057</td>
      <td>73.0892</td>
    </tr>
    <tr>
      <th>14</th>
      <td>kambove</td>
      <td>Democratic Republic of the Congo</td>
      <td>-10.8779</td>
      <td>26.5964</td>
    </tr>
    <tr>
      <th>15</th>
      <td>berbera</td>
      <td>Somalia</td>
      <td>10.4348</td>
      <td>45.014</td>
    </tr>
    <tr>
      <th>16</th>
      <td>constantine</td>
      <td>Michigan</td>
      <td>41.8412</td>
      <td>-85.6686</td>
    </tr>
    <tr>
      <th>17</th>
      <td>port elizabeth</td>
      <td>South Africa</td>
      <td>-33.7139</td>
      <td>25.5207</td>
    </tr>
    <tr>
      <th>18</th>
      <td>nkoteng</td>
      <td>Cameroon</td>
      <td>4.53856</td>
      <td>12.0204</td>
    </tr>
    <tr>
      <th>19</th>
      <td>dikson</td>
      <td>Russia</td>
      <td>73.5049</td>
      <td>80.5809</td>
    </tr>
    <tr>
      <th>20</th>
      <td>lebu</td>
      <td>Bío Bío Region</td>
      <td>-37.6097</td>
      <td>-73.6483</td>
    </tr>
    <tr>
      <th>21</th>
      <td>inhambane</td>
      <td>Mozambique</td>
      <td>-23.888</td>
      <td>35.396</td>
    </tr>
    <tr>
      <th>22</th>
      <td>bredasdorp</td>
      <td>Western Cape</td>
      <td>-34.5385</td>
      <td>20.0569</td>
    </tr>
    <tr>
      <th>23</th>
      <td>comodoro rivadavia</td>
      <td>Argentina</td>
      <td>-45.8656</td>
      <td>-67.4822</td>
    </tr>
    <tr>
      <th>24</th>
      <td>barentsburg</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>25</th>
      <td>port alfred</td>
      <td>South Africa</td>
      <td>-33.5864</td>
      <td>26.8851</td>
    </tr>
    <tr>
      <th>26</th>
      <td>narsaq</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>27</th>
      <td>kutum</td>
      <td>Sudan</td>
      <td>14.2025</td>
      <td>24.6638</td>
    </tr>
    <tr>
      <th>28</th>
      <td>taolanaro</td>
      <td>Madagascar</td>
      <td>-25.0225</td>
      <td>46.9854</td>
    </tr>
    <tr>
      <th>29</th>
      <td>marcona</td>
      <td>Peru</td>
      <td>-15.344</td>
      <td>-75.0845</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>804</th>
      <td>severnyy</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>805</th>
      <td>beawar</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>806</th>
      <td>jaleswar</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>807</th>
      <td>gurgan</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>808</th>
      <td>nioro</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>809</th>
      <td>boende</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>810</th>
      <td>mozelos</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>811</th>
      <td>coruripe</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>812</th>
      <td>kegayli</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>813</th>
      <td>beloha</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>814</th>
      <td>rio do sul</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>815</th>
      <td>novyy urengoy</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>816</th>
      <td>kaniv</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>817</th>
      <td>amli</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>818</th>
      <td>thrapsanon</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>819</th>
      <td>lagos</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>820</th>
      <td>keti bandar</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>821</th>
      <td>muramvya</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>822</th>
      <td>sidi ali</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>823</th>
      <td>lisakovsk</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>824</th>
      <td>liniere</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>825</th>
      <td>coyaima</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>826</th>
      <td>falmouth</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>827</th>
      <td>wahran</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>828</th>
      <td>yuryevets</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>829</th>
      <td>kasane</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>830</th>
      <td>endicott</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>831</th>
      <td>aquiraz</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>832</th>
      <td>adra</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>833</th>
      <td>kalininsk</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>834 rows × 4 columns</p>
</div>




```python

city_df1 = city_df.dropna(axis = 0,how = "any",inplace = False)
# city_df["Country"].dtype
len(city_df1)
```




    479




```python
# city_df["Country"]
```


```python
if len(city_df1)>500:
    city_df_sample = city_df1.sample(500)
else:
    city_df_sample = city_df1

city_df_sample["Temp"] = ""
city_df_sample["Humidity"] = ""
city_df_sample["Date"] = ""
city_df_sample["Wind Speed"] = ""
city_df_sample["Cloudiness"] = ""

city_df_sample
```

    C:\Users\gizmo\Anaconda3\lib\site-packages\ipykernel_launcher.py:6: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      
    C:\Users\gizmo\Anaconda3\lib\site-packages\ipykernel_launcher.py:7: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      import sys
    C:\Users\gizmo\Anaconda3\lib\site-packages\ipykernel_launcher.py:8: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      
    C:\Users\gizmo\Anaconda3\lib\site-packages\ipykernel_launcher.py:9: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      if __name__ == '__main__':
    C:\Users\gizmo\Anaconda3\lib\site-packages\ipykernel_launcher.py:10: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      # Remove the CWD from sys.path while we load stuff.
    




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
      <th>City</th>
      <th>Country</th>
      <th>Lat</th>
      <th>Long</th>
      <th>Temp</th>
      <th>Humidity</th>
      <th>Date</th>
      <th>Wind Speed</th>
      <th>Cloudiness</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ushuaia</td>
      <td>Argentina</td>
      <td>-54.8019</td>
      <td>-68.303</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>2</th>
      <td>sault sainte marie</td>
      <td>United States</td>
      <td>46.4977</td>
      <td>-84.3476</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>3</th>
      <td>albany</td>
      <td>United States</td>
      <td>42.6526</td>
      <td>-73.7562</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>4</th>
      <td>shubarkuduk</td>
      <td>Kazakhstan</td>
      <td>49.143</td>
      <td>56.4817</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>5</th>
      <td>hermanus</td>
      <td>South Africa</td>
      <td>-34.4092</td>
      <td>19.2504</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>7</th>
      <td>jamestown</td>
      <td>Virginia</td>
      <td>37.2116</td>
      <td>-76.7752</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>10</th>
      <td>belushya guba</td>
      <td>Russia</td>
      <td>71.5456</td>
      <td>52.3203</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>11</th>
      <td>tapaua</td>
      <td>69480-000</td>
      <td>-5.62504</td>
      <td>-63.189</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>12</th>
      <td>tatawin</td>
      <td>Tunisia</td>
      <td>32.9211</td>
      <td>10.4509</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>13</th>
      <td>hithadhoo</td>
      <td>Maldives</td>
      <td>-0.606057</td>
      <td>73.0892</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>14</th>
      <td>kambove</td>
      <td>Democratic Republic of the Congo</td>
      <td>-10.8779</td>
      <td>26.5964</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>15</th>
      <td>berbera</td>
      <td>Somalia</td>
      <td>10.4348</td>
      <td>45.014</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>16</th>
      <td>constantine</td>
      <td>Michigan</td>
      <td>41.8412</td>
      <td>-85.6686</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>17</th>
      <td>port elizabeth</td>
      <td>South Africa</td>
      <td>-33.7139</td>
      <td>25.5207</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>18</th>
      <td>nkoteng</td>
      <td>Cameroon</td>
      <td>4.53856</td>
      <td>12.0204</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>19</th>
      <td>dikson</td>
      <td>Russia</td>
      <td>73.5049</td>
      <td>80.5809</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>20</th>
      <td>lebu</td>
      <td>Bío Bío Region</td>
      <td>-37.6097</td>
      <td>-73.6483</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>21</th>
      <td>inhambane</td>
      <td>Mozambique</td>
      <td>-23.888</td>
      <td>35.396</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>22</th>
      <td>bredasdorp</td>
      <td>Western Cape</td>
      <td>-34.5385</td>
      <td>20.0569</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>23</th>
      <td>comodoro rivadavia</td>
      <td>Argentina</td>
      <td>-45.8656</td>
      <td>-67.4822</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>25</th>
      <td>port alfred</td>
      <td>South Africa</td>
      <td>-33.5864</td>
      <td>26.8851</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>27</th>
      <td>kutum</td>
      <td>Sudan</td>
      <td>14.2025</td>
      <td>24.6638</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>28</th>
      <td>taolanaro</td>
      <td>Madagascar</td>
      <td>-25.0225</td>
      <td>46.9854</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>29</th>
      <td>marcona</td>
      <td>Peru</td>
      <td>-15.344</td>
      <td>-75.0845</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>30</th>
      <td>podor</td>
      <td>Senegal</td>
      <td>16.6601</td>
      <td>-14.9593</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>31</th>
      <td>druzhba</td>
      <td>Ukraine</td>
      <td>52.0402</td>
      <td>33.9294</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>33</th>
      <td>east london</td>
      <td>South Africa</td>
      <td>-33.0292</td>
      <td>27.8546</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>34</th>
      <td>franklin park</td>
      <td>Illinois</td>
      <td>41.9349</td>
      <td>-87.8795</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>35</th>
      <td>richards bay</td>
      <td>South Africa</td>
      <td>-28.7807</td>
      <td>32.0383</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>36</th>
      <td>salta</td>
      <td>Argentina</td>
      <td>-24.7821</td>
      <td>-65.4232</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>628</th>
      <td>yarensk</td>
      <td>Russia</td>
      <td>62.179</td>
      <td>49.0931</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>632</th>
      <td>puerto carreno</td>
      <td>Colombia</td>
      <td>6.18477</td>
      <td>-67.4885</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>634</th>
      <td>bermejo</td>
      <td>Bolivia</td>
      <td>-22.682</td>
      <td>-64.3135</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>635</th>
      <td>jaciara</td>
      <td>78820-000</td>
      <td>-15.956</td>
      <td>-54.9752</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>636</th>
      <td>rafaela</td>
      <td>Argentina</td>
      <td>-31.2526</td>
      <td>-61.4916</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>637</th>
      <td>general pico</td>
      <td>Argentina</td>
      <td>-35.6593</td>
      <td>-63.7578</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>638</th>
      <td>rancho veloz</td>
      <td>Cuba</td>
      <td>22.8795</td>
      <td>-80.3909</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>640</th>
      <td>puerto montt</td>
      <td>Los Lagos Region</td>
      <td>-41.4689</td>
      <td>-72.9411</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>641</th>
      <td>jijiga</td>
      <td>Ethiopia</td>
      <td>9.35678</td>
      <td>42.7955</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>642</th>
      <td>tiznit</td>
      <td>Morocco</td>
      <td>29.6934</td>
      <td>-9.73216</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>644</th>
      <td>tulu bolo</td>
      <td>Ethiopia</td>
      <td>8.66328</td>
      <td>38.2164</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>645</th>
      <td>cordoba</td>
      <td>Spain</td>
      <td>37.8882</td>
      <td>-4.77938</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>648</th>
      <td>paracatu</td>
      <td>38600-000</td>
      <td>-17.2175</td>
      <td>-46.8711</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>649</th>
      <td>buta</td>
      <td>Democratic Republic of the Congo</td>
      <td>2.80453</td>
      <td>24.7499</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>650</th>
      <td>jurm</td>
      <td>Afghanistan</td>
      <td>36.8667</td>
      <td>70.835</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>652</th>
      <td>cayenne</td>
      <td>French Guiana</td>
      <td>4.92242</td>
      <td>-52.3135</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>655</th>
      <td>sindor</td>
      <td>Russia</td>
      <td>65.15</td>
      <td>57.2167</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>656</th>
      <td>srivardhan</td>
      <td>India</td>
      <td>18.0594</td>
      <td>73.0228</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>657</th>
      <td>bafoulabe</td>
      <td>Mali</td>
      <td>13.8093</td>
      <td>-10.8346</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>664</th>
      <td>mitsamiouli</td>
      <td>Comoros</td>
      <td>-11.3872</td>
      <td>43.2981</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>665</th>
      <td>uyuni</td>
      <td>Bolivia</td>
      <td>-20.4604</td>
      <td>-66.8261</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>673</th>
      <td>kalabo</td>
      <td>Zambia</td>
      <td>-14.9932</td>
      <td>22.678</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>674</th>
      <td>gulu</td>
      <td>Uganda</td>
      <td>2.7724</td>
      <td>32.2881</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>706</th>
      <td>thompson</td>
      <td>California</td>
      <td>33.6455</td>
      <td>-117.641</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>715</th>
      <td>gamboula</td>
      <td>Central African Republic</td>
      <td>4.1192</td>
      <td>15.1347</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>718</th>
      <td>waw</td>
      <td>Myanmar (Burma)</td>
      <td>17.477</td>
      <td>96.6772</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>727</th>
      <td>pauini</td>
      <td>69860-000</td>
      <td>-7.7292</td>
      <td>-68.3339</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>731</th>
      <td>iranshahr</td>
      <td>Iran</td>
      <td>27.2012</td>
      <td>60.6866</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>733</th>
      <td>mrirt</td>
      <td>Morocco</td>
      <td>33.1627</td>
      <td>-5.56698</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>739</th>
      <td>guarapari</td>
      <td>Brazil</td>
      <td>-20.6741</td>
      <td>-40.4997</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
  </tbody>
</table>
<p>479 rows × 9 columns</p>
</div>




```python
##Using the weather api

url = "http://api.openweathermap.org/data/2.5/weather?"
units = "Imperial"
```


```python

count = 0
for index, row in city_df_sample.iterrows():
    target_url = "http://api.openweathermap.org/data/2.5/weather?units=%s&APPID=%s&q=%s" % (units,api_key, row['City'])
    cities_weather = requests.get(target_url).json()
    try:
        city_df_sample.set_value(index, "Temp", cities_weather["main"]["temp_max"])
        city_df_sample.set_value(index, "Humidity", cities_weather["main"]["humidity"])
        city_df_sample.set_value(index, "Date", cities_weather["dt"])
        city_df_sample.set_value(index, "Wind Speed", cities_weather["wind"]["speed"])
        city_df_sample.set_value(index, "Cloudiness", cities_weather["clouds"]["all"])
    except KeyError:
        city_df_sample.set_value(index, "Temp", np.NaN)
        city_df_sample.set_value(index, "Humidity", np.NaN)
        city_df_sample.set_value(index, "Date",np.NaN)
        city_df_sample.set_value(index, "Wind Speed", np.NaN)
        city_df_sample.set_value(index, "Cloudiness", np.NaN)
        continue
        
    count = count + 1
       
    print("------------------------")
    print("Processing Information: " , count, 'With City: ' , cities_weather["name"])
    print(target_url)
```

    ------------------------
    Processing Information:  1 With City:  Ushuaia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ushuaia
    ------------------------
    Processing Information:  2 With City:  Sault Sainte Marie
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sault sainte marie
    ------------------------
    Processing Information:  3 With City:  Albany
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=albany
    ------------------------
    Processing Information:  4 With City:  Shubarkuduk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=shubarkuduk
    ------------------------
    Processing Information:  5 With City:  Hermanus
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=hermanus
    ------------------------
    Processing Information:  6 With City:  Jamestown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=jamestown
    ------------------------
    Processing Information:  7 With City:  Hithadhoo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=hithadhoo
    ------------------------
    Processing Information:  8 With City:  Kambove
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kambove
    ------------------------
    Processing Information:  9 With City:  Constantine
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=constantine
    ------------------------
    Processing Information:  10 With City:  Port Elizabeth
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=port elizabeth
    ------------------------
    Processing Information:  11 With City:  Nkoteng
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=nkoteng
    ------------------------
    Processing Information:  12 With City:  Dikson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=dikson
    ------------------------
    Processing Information:  13 With City:  Lebu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=lebu
    ------------------------
    Processing Information:  14 With City:  Inhambane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=inhambane
    ------------------------
    Processing Information:  15 With City:  Bredasdorp
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=bredasdorp
    ------------------------
    Processing Information:  16 With City:  Comodoro Rivadavia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=comodoro rivadavia
    ------------------------
    Processing Information:  17 With City:  Port Alfred
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=port alfred
    ------------------------
    Processing Information:  18 With City:  Kutum
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kutum
    ------------------------
    Processing Information:  19 With City:  Podor
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=podor
    ------------------------
    Processing Information:  20 With City:  Druzhba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=druzhba
    ------------------------
    Processing Information:  21 With City:  East London
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=east london
    ------------------------
    Processing Information:  22 With City:  Franklin Park
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=franklin park
    ------------------------
    Processing Information:  23 With City:  Richards Bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=richards bay
    ------------------------
    Processing Information:  24 With City:  Salta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=salta
    ------------------------
    Processing Information:  25 With City:  Saint-Joseph
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=saint-joseph
    ------------------------
    Processing Information:  26 With City:  Laguna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=laguna
    ------------------------
    Processing Information:  27 With City:  Mar del Plata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=mar del plata
    ------------------------
    Processing Information:  28 With City:  Mbandaka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=mbandaka
    ------------------------
    Processing Information:  29 With City:  Staryy Nadym
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=staryy nadym
    ------------------------
    Processing Information:  30 With City:  Sheoganj
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sheoganj
    ------------------------
    Processing Information:  31 With City:  Georgetown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=georgetown
    ------------------------
    Processing Information:  32 With City:  Margate
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=margate
    ------------------------
    Processing Information:  33 With City:  Iqaluit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=iqaluit
    ------------------------
    Processing Information:  34 With City:  Punta Arenas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=punta arenas
    ------------------------
    Processing Information:  35 With City:  Busselton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=busselton
    ------------------------
    Processing Information:  36 With City:  Asyut
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=asyut
    ------------------------
    Processing Information:  37 With City:  Kattivakkam
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kattivakkam
    ------------------------
    Processing Information:  38 With City:  Ribeira Grande
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ribeira grande
    ------------------------
    Processing Information:  39 With City:  Namibe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=namibe
    ------------------------
    Processing Information:  40 With City:  Tazovskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=tazovskiy
    ------------------------
    Processing Information:  41 With City:  Kongolo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kongolo
    ------------------------
    Processing Information:  42 With City:  Vila Velha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=vila velha
    ------------------------
    Processing Information:  43 With City:  Cape Town
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=cape town
    ------------------------
    Processing Information:  44 With City:  Ambagarh Chauki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ambagarh chauki
    ------------------------
    Processing Information:  45 With City:  Upata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=upata
    ------------------------
    Processing Information:  46 With City:  Soyo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=soyo
    ------------------------
    Processing Information:  47 With City:  Rio Gallegos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=rio gallegos
    ------------------------
    Processing Information:  48 With City:  Pokhara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=pokhara
    ------------------------
    Processing Information:  49 With City:  Kruisfontein
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kruisfontein
    ------------------------
    Processing Information:  50 With City:  Cockburn Town
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=cockburn town
    ------------------------
    Processing Information:  51 With City:  Tucupita
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=tucupita
    ------------------------
    Processing Information:  52 With City:  Valparaiso
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=valparaiso
    ------------------------
    Processing Information:  53 With City:  Siniscola
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=siniscola
    ------------------------
    Processing Information:  54 With City:  Point Pedro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=point pedro
    ------------------------
    Processing Information:  55 With City:  Carnarvon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=carnarvon
    ------------------------
    Processing Information:  56 With City:  Aksu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=aksu
    ------------------------
    Processing Information:  57 With City:  Chalinze
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=chalinze
    ------------------------
    Processing Information:  58 With City:  Arraial do Cabo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=arraial do cabo
    ------------------------
    Processing Information:  59 With City:  Saint-Denis
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=saint-denis
    ------------------------
    Processing Information:  60 With City:  Souillac
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=souillac
    ------------------------
    Processing Information:  61 With City:  Saint Anthony
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=saint anthony
    ------------------------
    Processing Information:  62 With City:  Vila Franca do Campo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=vila franca do campo
    ------------------------
    Processing Information:  63 With City:  Prestea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=prestea
    ------------------------
    Processing Information:  64 With City:  Lokosovo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=lokosovo
    ------------------------
    Processing Information:  65 With City:  Muros
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=muros
    ------------------------
    Processing Information:  66 With City:  Ambovombe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ambovombe
    ------------------------
    Processing Information:  67 With City:  Gat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=gat
    ------------------------
    Processing Information:  68 With City:  Red Bank
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=red bank
    ------------------------
    Processing Information:  69 With City:  Clyde River
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=clyde river
    ------------------------
    Processing Information:  70 With City:  Chojnow
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=chojnow
    ------------------------
    Processing Information:  71 With City:  Lagoa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=lagoa
    ------------------------
    Processing Information:  72 With City:  Mogadishu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=mogadishu
    ------------------------
    Processing Information:  73 With City:  Santa Maria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=santa maria
    ------------------------
    Processing Information:  74 With City:  Harper
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=harper
    ------------------------
    Processing Information:  75 With City:  Victoria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=victoria
    ------------------------
    Processing Information:  76 With City:  Leo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=leo
    ------------------------
    Processing Information:  77 With City:  Cambados
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=cambados
    ------------------------
    Processing Information:  78 With City:  Bhawana
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=bhawana
    ------------------------
    Processing Information:  79 With City:  Strezhevoy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=strezhevoy
    ------------------------
    Processing Information:  80 With City:  Norwich
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=norwich
    ------------------------
    Processing Information:  81 With City:  Hambantota
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=hambantota
    ------------------------
    Processing Information:  82 With City:  Zapolyarnyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=zapolyarnyy
    ------------------------
    Processing Information:  83 With City:  Pabrade
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=pabrade
    ------------------------
    Processing Information:  84 With City:  Gangtok
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=gangtok
    ------------------------
    Processing Information:  85 With City:  Ramhormoz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ramhormoz
    ------------------------
    Processing Information:  86 With City:  Cidreira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=cidreira
    ------------------------
    Processing Information:  87 With City:  Saint George
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=saint george
    ------------------------
    Processing Information:  88 With City:  Geraldton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=geraldton
    ------------------------
    Processing Information:  89 With City:  Sao Joao da Barra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sao joao da barra
    ------------------------
    Processing Information:  90 With City:  Sawakin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sawakin
    ------------------------
    Processing Information:  91 With City:  Kulhudhuffushi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kulhudhuffushi
    ------------------------
    Processing Information:  92 With City:  Fenelon Falls
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=fenelon falls
    ------------------------
    Processing Information:  93 With City:  Weligama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=weligama
    ------------------------
    Processing Information:  94 With City:  Shipunovo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=shipunovo
    ------------------------
    Processing Information:  95 With City:  Saurimo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=saurimo
    ------------------------
    Processing Information:  96 With City:  Krasnoufimsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=krasnoufimsk
    ------------------------
    Processing Information:  97 With City:  Bandarbeyla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=bandarbeyla
    ------------------------
    Processing Information:  98 With City:  Sokolka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sokolka
    ------------------------
    Processing Information:  99 With City:  Takoradi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=takoradi
    ------------------------
    Processing Information:  100 With City:  Leninsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=leninsk
    ------------------------
    Processing Information:  101 With City:  Bull Savanna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=bull savanna
    ------------------------
    Processing Information:  102 With City:  Faya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=faya
    ------------------------
    Processing Information:  103 With City:  Tabou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=tabou
    ------------------------
    Processing Information:  104 With City:  Teguise
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=teguise
    ------------------------
    Processing Information:  105 With City:  Ostrovnoy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ostrovnoy
    ------------------------
    Processing Information:  106 With City:  Marovoay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=marovoay
    ------------------------
    Processing Information:  107 With City:  Daur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=daur
    ------------------------
    Processing Information:  108 With City:  Sneek
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sneek
    ------------------------
    Processing Information:  109 With City:  San Juan de Uraba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=san juan de uraba
    ------------------------
    Processing Information:  110 With City:  Chuy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=chuy
    ------------------------
    Processing Information:  111 With City:  Robertsport
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=robertsport
    ------------------------
    Processing Information:  112 With City:  Czluchow
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=czluchow
    ------------------------
    Processing Information:  113 With City:  Apam
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=apam
    ------------------------
    Processing Information:  114 With City:  Urucara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=urucara
    ------------------------
    Processing Information:  115 With City:  Goderich
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=goderich
    ------------------------
    Processing Information:  116 With City:  Honavar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=honavar
    ------------------------
    Processing Information:  117 With City:  Vikulovo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=vikulovo
    ------------------------
    Processing Information:  118 With City:  Pisco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=pisco
    ------------------------
    Processing Information:  119 With City:  Williamsport
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=williamsport
    ------------------------
    Processing Information:  120 With City:  Lev Tolstoy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=lev tolstoy
    ------------------------
    Processing Information:  121 With City:  Prado
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=prado
    ------------------------
    Processing Information:  122 With City:  Mercedes
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=mercedes
    ------------------------
    Processing Information:  123 With City:  Sao Felix do Xingu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sao felix do xingu
    ------------------------
    Processing Information:  124 With City:  Ati
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ati
    ------------------------
    Processing Information:  125 With City:  Edirne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=edirne
    ------------------------
    Processing Information:  126 With City:  Maracaibo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=maracaibo
    ------------------------
    Processing Information:  127 With City:  Edd
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=edd
    ------------------------
    Processing Information:  128 With City:  Sur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sur
    ------------------------
    Processing Information:  129 With City:  Rawson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=rawson
    ------------------------
    Processing Information:  130 With City:  Dwarka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=dwarka
    ------------------------
    Processing Information:  131 With City:  Kabalo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kabalo
    ------------------------
    Processing Information:  132 With City:  Tallahassee
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=tallahassee
    ------------------------
    Processing Information:  133 With City:  Formosa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=formosa
    ------------------------
    Processing Information:  134 With City:  Bilma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=bilma
    ------------------------
    Processing Information:  135 With City:  Tubmanburg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=tubmanburg
    ------------------------
    Processing Information:  136 With City:  Stolin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=stolin
    ------------------------
    Processing Information:  137 With City:  Barreirinha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=barreirinha
    ------------------------
    Processing Information:  138 With City:  Selcuk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=selcuk
    ------------------------
    Processing Information:  139 With City:  Machhlishahr
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=machhlishahr
    ------------------------
    Processing Information:  140 With City:  Umm Lajj
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=umm lajj
    ------------------------
    Processing Information:  141 With City:  Moose Factory
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=moose factory
    ------------------------
    Processing Information:  142 With City:  Arica
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=arica
    ------------------------
    Processing Information:  143 With City:  Svetlogorsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=svetlogorsk
    ------------------------
    Processing Information:  144 With City:  Havre-Saint-Pierre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=havre-saint-pierre
    ------------------------
    Processing Information:  145 With City:  Madison
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=madison
    ------------------------
    Processing Information:  146 With City:  Devgarh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=devgarh
    ------------------------
    Processing Information:  147 With City:  La Baule-Escoublac
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=la baule-escoublac
    ------------------------
    Processing Information:  148 With City:  Muscle Shoals
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=muscle shoals
    ------------------------
    Processing Information:  149 With City:  Presidencia Roque Saenz Pena
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=presidencia roque saenz pena
    ------------------------
    Processing Information:  150 With City:  Batticaloa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=batticaloa
    ------------------------
    Processing Information:  151 With City:  Omboue
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=omboue
    ------------------------
    Processing Information:  152 With City:  Porto Novo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=porto novo
    ------------------------
    Processing Information:  153 With City:  Lady Frere
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=lady frere
    ------------------------
    Processing Information:  154 With City:  Filadelfia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=filadelfia
    ------------------------
    Processing Information:  155 With City:  Ubaitaba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ubaitaba
    ------------------------
    Processing Information:  156 With City:  Cervo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=cervo
    ------------------------
    Processing Information:  157 With City:  Yar-Sale
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=yar-sale
    ------------------------
    Processing Information:  158 With City:  Luau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=luau
    ------------------------
    Processing Information:  159 With City:  Bonavista
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=bonavista
    ------------------------
    Processing Information:  160 With City:  Vani
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=vani
    ------------------------
    Processing Information:  161 With City:  Boddam
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=boddam
    ------------------------
    Processing Information:  162 With City:  Huarmey
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=huarmey
    ------------------------
    Processing Information:  163 With City:  Hopeman
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=hopeman
    ------------------------
    Processing Information:  164 With City:  Rosario
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=rosario
    ------------------------
    Processing Information:  165 With City:  Ciudad Bolivar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ciudad bolivar
    ------------------------
    Processing Information:  166 With City:  Kingsport
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kingsport
    ------------------------
    Processing Information:  167 With City:  Hobyo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=hobyo
    ------------------------
    Processing Information:  168 With City:  La Asuncion
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=la asuncion
    ------------------------
    Processing Information:  169 With City:  Luba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=luba
    ------------------------
    Processing Information:  170 With City:  Ellisras
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ellisras
    ------------------------
    Processing Information:  171 With City:  Norden
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=norden
    ------------------------
    Processing Information:  172 With City:  Villarrobledo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=villarrobledo
    ------------------------
    Processing Information:  173 With City:  Coquimbo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=coquimbo
    ------------------------
    Processing Information:  174 With City:  Ostrov
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ostrov
    ------------------------
    Processing Information:  175 With City:  Los Llanos de Aridane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=los llanos de aridane
    ------------------------
    Processing Information:  176 With City:  Kavaratti
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kavaratti
    ------------------------
    Processing Information:  177 With City:  Sarkand
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sarkand
    ------------------------
    Processing Information:  178 With City:  Maceio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=maceio
    ------------------------
    Processing Information:  179 With City:  Lovozero
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=lovozero
    ------------------------
    Processing Information:  180 With City:  Oussouye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=oussouye
    ------------------------
    Processing Information:  181 With City:  Viradouro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=viradouro
    ------------------------
    Processing Information:  182 With City:  Camacari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=camacari
    ------------------------
    Processing Information:  183 With City:  Talnakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=talnakh
    ------------------------
    Processing Information:  184 With City:  Dharchula
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=dharchula
    ------------------------
    Processing Information:  185 With City:  Inta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=inta
    ------------------------
    Processing Information:  186 With City:  Dawlatabad
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=dawlatabad
    ------------------------
    Processing Information:  187 With City:  Saint-Augustin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=saint-augustin
    ------------------------
    Processing Information:  188 With City:  Monrovia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=monrovia
    ------------------------
    Processing Information:  189 With City:  Garowe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=garowe
    ------------------------
    Processing Information:  190 With City:  Lincoln
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=lincoln
    ------------------------
    Processing Information:  191 With City:  Boromo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=boromo
    ------------------------
    Processing Information:  192 With City:  Batala
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=batala
    ------------------------
    Processing Information:  193 With City:  Marsala
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=marsala
    ------------------------
    Processing Information:  194 With City:  Malanje
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=malanje
    ------------------------
    Processing Information:  195 With City:  Quelimane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=quelimane
    ------------------------
    Processing Information:  196 With City:  Mato Verde
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=mato verde
    ------------------------
    Processing Information:  197 With City:  Sinop
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sinop
    ------------------------
    Processing Information:  198 With City:  Salisbury
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=salisbury
    ------------------------
    Processing Information:  199 With City:  Sao Francisco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sao francisco
    ------------------------
    Processing Information:  200 With City:  Bay City
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=bay city
    ------------------------
    Processing Information:  201 With City:  Pangody
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=pangody
    ------------------------
    Processing Information:  202 With City:  Puerto del Rosario
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=puerto del rosario
    ------------------------
    Processing Information:  203 With City:  Blagoyevo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=blagoyevo
    ------------------------
    Processing Information:  204 With City:  Bedesa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=bedesa
    ------------------------
    Processing Information:  205 With City:  Port-Gentil
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=port-gentil
    ------------------------
    Processing Information:  206 With City:  Lubango
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=lubango
    ------------------------
    Processing Information:  207 With City:  At-Bashi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=at-bashi
    ------------------------
    Processing Information:  208 With City:  Bubaque
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=bubaque
    ------------------------
    Processing Information:  209 With City:  Chulym
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=chulym
    ------------------------
    Processing Information:  210 With City:  Beyneu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=beyneu
    ------------------------
    Processing Information:  211 With City:  Taylorville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=taylorville
    ------------------------
    Processing Information:  212 With City:  Talcahuano
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=talcahuano
    ------------------------
    Processing Information:  213 With City:  Bonthe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=bonthe
    ------------------------
    Processing Information:  214 With City:  Jasper
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=jasper
    ------------------------
    Processing Information:  215 With City:  Asosa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=asosa
    ------------------------
    Processing Information:  216 With City:  Melo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=melo
    ------------------------
    Processing Information:  217 With City:  Akhisar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=akhisar
    ------------------------
    Processing Information:  218 With City:  Ansalta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ansalta
    ------------------------
    Processing Information:  219 With City:  Sanchor
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sanchor
    ------------------------
    Processing Information:  220 With City:  Mao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=mao
    ------------------------
    Processing Information:  221 With City:  Pavlohrad
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=pavlohrad
    ------------------------
    Processing Information:  222 With City:  Muli
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=muli
    ------------------------
    Processing Information:  223 With City:  Gopalpur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=gopalpur
    ------------------------
    Processing Information:  224 With City:  Agirish
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=agirish
    ------------------------
    Processing Information:  225 With City:  Maxixe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=maxixe
    ------------------------
    Processing Information:  226 With City:  Borgomanero
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=borgomanero
    ------------------------
    Processing Information:  227 With City:  Senneterre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=senneterre
    ------------------------
    Processing Information:  228 With City:  Touros
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=touros
    ------------------------
    Processing Information:  229 With City:  Ferme-Neuve
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ferme-neuve
    ------------------------
    Processing Information:  230 With City:  Troitsko-Pechorsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=troitsko-pechorsk
    ------------------------
    Processing Information:  231 With City:  Encruzilhada do Sul
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=encruzilhada do sul
    ------------------------
    Processing Information:  232 With City:  Puerto Berrio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=puerto berrio
    ------------------------
    Processing Information:  233 With City:  Itarema
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=itarema
    ------------------------
    Processing Information:  234 With City:  Calama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=calama
    ------------------------
    Processing Information:  235 With City:  Goba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=goba
    ------------------------
    Processing Information:  236 With City:  Fort Myers Beach
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=fort myers beach
    ------------------------
    Processing Information:  237 With City:  Marmande
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=marmande
    ------------------------
    Processing Information:  238 With City:  Salinas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=salinas
    ------------------------
    Processing Information:  239 With City:  Plettenberg Bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=plettenberg bay
    ------------------------
    Processing Information:  240 With City:  Banganapalle
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=banganapalle
    ------------------------
    Processing Information:  241 With City:  Matara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=matara
    ------------------------
    Processing Information:  242 With City:  Plaster Rock
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=plaster rock
    ------------------------
    Processing Information:  243 With City:  Abalak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=abalak
    ------------------------
    Processing Information:  244 With City:  Chitipa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=chitipa
    ------------------------
    Processing Information:  245 With City:  Kodinar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kodinar
    ------------------------
    Processing Information:  246 With City:  Parabel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=parabel
    ------------------------
    Processing Information:  247 With City:  Sao Desiderio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sao desiderio
    ------------------------
    Processing Information:  248 With City:  Shubarshi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=shubarshi
    ------------------------
    Processing Information:  249 With City:  Arbazh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=arbazh
    ------------------------
    Processing Information:  250 With City:  Pedernales
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=pedernales
    ------------------------
    Processing Information:  251 With City:  Taoudenni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=taoudenni
    ------------------------
    Processing Information:  252 With City:  Westport
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=westport
    ------------------------
    Processing Information:  253 With City:  Moratuwa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=moratuwa
    ------------------------
    Processing Information:  254 With City:  Praia da Vitoria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=praia da vitoria
    ------------------------
    Processing Information:  255 With City:  Wilmington
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=wilmington
    ------------------------
    Processing Information:  256 With City:  Ambilobe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ambilobe
    ------------------------
    Processing Information:  257 With City:  Zaysan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=zaysan
    ------------------------
    Processing Information:  258 With City:  Pocoes
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=pocoes
    ------------------------
    Processing Information:  259 With City:  Sindou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sindou
    ------------------------
    Processing Information:  260 With City:  Impfondo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=impfondo
    ------------------------
    Processing Information:  261 With City:  Mantua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=mantua
    ------------------------
    Processing Information:  262 With City:  Ormara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ormara
    ------------------------
    Processing Information:  263 With City:  Aktau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=aktau
    ------------------------
    Processing Information:  264 With City:  Tikamgarh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=tikamgarh
    ------------------------
    Processing Information:  265 With City:  Benoy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=benoy
    ------------------------
    Processing Information:  266 With City:  Sturgis
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sturgis
    ------------------------
    Processing Information:  267 With City:  Yabrud
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=yabrud
    ------------------------
    Processing Information:  268 With City:  Lauterbach
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=lauterbach
    ------------------------
    Processing Information:  269 With City:  Ordzhonikidze
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ordzhonikidze
    ------------------------
    Processing Information:  270 With City:  Hedaru
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=hedaru
    ------------------------
    Processing Information:  271 With City:  Iquique
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=iquique
    ------------------------
    Processing Information:  272 With City:  Marawi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=marawi
    ------------------------
    Processing Information:  273 With City:  Hualmay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=hualmay
    ------------------------
    Processing Information:  274 With City:  Oktyabrskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=oktyabrskoye
    ------------------------
    Processing Information:  275 With City:  Atar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=atar
    ------------------------
    Processing Information:  276 With City:  Barrington
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=barrington
    ------------------------
    Processing Information:  277 With City:  Jutai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=jutai
    ------------------------
    Processing Information:  278 With City:  Izhma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=izhma
    ------------------------
    Processing Information:  279 With City:  Clinton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=clinton
    ------------------------
    Processing Information:  280 With City:  Nantucket
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=nantucket
    ------------------------
    Processing Information:  281 With City:  Ilhabela
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ilhabela
    ------------------------
    Processing Information:  282 With City:  Ambanja
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ambanja
    ------------------------
    Processing Information:  283 With City:  Puerto Leguizamo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=puerto leguizamo
    ------------------------
    Processing Information:  284 With City:  Raducaneni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=raducaneni
    ------------------------
    Processing Information:  285 With City:  Bosaso
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=bosaso
    ------------------------
    Processing Information:  286 With City:  Canavieiras
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=canavieiras
    ------------------------
    Processing Information:  287 With City:  Spoleto
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=spoleto
    ------------------------
    Processing Information:  288 With City:  Kuytun
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kuytun
    ------------------------
    Processing Information:  289 With City:  Millau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=millau
    ------------------------
    Processing Information:  290 With City:  Camocim
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=camocim
    ------------------------
    Processing Information:  291 With City:  Kerewan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kerewan
    ------------------------
    Processing Information:  292 With City:  Laela
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=laela
    ------------------------
    Processing Information:  293 With City:  Tignere
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=tignere
    ------------------------
    Processing Information:  294 With City:  Ekuvukeni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ekuvukeni
    ------------------------
    Processing Information:  295 With City:  Grand-Santi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=grand-santi
    ------------------------
    Processing Information:  296 With City:  Bud
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=bud
    ------------------------
    Processing Information:  297 With City:  Atasu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=atasu
    ------------------------
    Processing Information:  298 With City:  Kizilskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kizilskoye
    ------------------------
    Processing Information:  299 With City:  Normal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=normal
    ------------------------
    Processing Information:  300 With City:  Chernenko
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=chernenko
    ------------------------
    Processing Information:  301 With City:  Namestovo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=namestovo
    ------------------------
    Processing Information:  302 With City:  Kisangani
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kisangani
    ------------------------
    Processing Information:  303 With City:  Puerto Colombia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=puerto colombia
    ------------------------
    Processing Information:  304 With City:  Buribay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=buribay
    ------------------------
    Processing Information:  305 With City:  Sambava
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sambava
    ------------------------
    Processing Information:  306 With City:  Merritt Island
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=merritt island
    ------------------------
    Processing Information:  307 With City:  Kirando
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kirando
    ------------------------
    Processing Information:  308 With City:  Sasykoli
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sasykoli
    ------------------------
    Processing Information:  309 With City:  Aguas Vermelhas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=aguas vermelhas
    ------------------------
    Processing Information:  310 With City:  Ciudad Guayana
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ciudad guayana
    ------------------------
    Processing Information:  311 With City:  Ganta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ganta
    ------------------------
    Processing Information:  312 With City:  Basoko
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=basoko
    ------------------------
    Processing Information:  313 With City:  Goure
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=goure
    ------------------------
    Processing Information:  314 With City:  Lusambo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=lusambo
    ------------------------
    Processing Information:  315 With City:  Megion
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=megion
    ------------------------
    Processing Information:  316 With City:  Certegui
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=certegui
    ------------------------
    Processing Information:  317 With City:  Kachiry
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kachiry
    ------------------------
    Processing Information:  318 With City:  Alta Floresta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=alta floresta
    ------------------------
    Processing Information:  319 With City:  Altos del Rosario
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=altos del rosario
    ------------------------
    Processing Information:  320 With City:  Korem
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=korem
    ------------------------
    Processing Information:  321 With City:  Fomboni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=fomboni
    ------------------------
    Processing Information:  322 With City:  Sao Gabriel da Cachoeira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sao gabriel da cachoeira
    ------------------------
    Processing Information:  323 With City:  Fort Portal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=fort portal
    ------------------------
    Processing Information:  324 With City:  Eydhafushi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=eydhafushi
    ------------------------
    Processing Information:  325 With City:  Lyantonde
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=lyantonde
    ------------------------
    Processing Information:  326 With City:  Breytovo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=breytovo
    ------------------------
    Processing Information:  327 With City:  Tessalit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=tessalit
    ------------------------
    Processing Information:  328 With City:  Poiana Marului
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=poiana marului
    ------------------------
    Processing Information:  329 With City:  Loiza
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=loiza
    ------------------------
    Processing Information:  330 With City:  Campo de Criptana
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=campo de criptana
    ------------------------
    Processing Information:  331 With City:  Dakar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=dakar
    ------------------------
    Processing Information:  332 With City:  Kuryk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kuryk
    ------------------------
    Processing Information:  333 With City:  Saldanha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=saldanha
    ------------------------
    Processing Information:  334 With City:  Brigantine
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=brigantine
    ------------------------
    Processing Information:  335 With City:  Ibirapitanga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ibirapitanga
    ------------------------
    Processing Information:  336 With City:  Chinsali
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=chinsali
    ------------------------
    Processing Information:  337 With City:  Inirida
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=inirida
    ------------------------
    Processing Information:  338 With City:  Puerto Rondon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=puerto rondon
    ------------------------
    Processing Information:  339 With City:  Muyezerskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=muyezerskiy
    ------------------------
    Processing Information:  340 With City:  Cochrane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=cochrane
    ------------------------
    Processing Information:  341 With City:  Monforte de Lemos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=monforte de lemos
    ------------------------
    Processing Information:  342 With City:  Necochea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=necochea
    ------------------------
    Processing Information:  343 With City:  Ciucurova
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ciucurova
    ------------------------
    Processing Information:  344 With City:  Akcakoca
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=akcakoca
    ------------------------
    Processing Information:  345 With City:  Vasai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=vasai
    ------------------------
    Processing Information:  346 With City:  Odienne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=odienne
    ------------------------
    Processing Information:  347 With City:  Sunbury
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sunbury
    ------------------------
    Processing Information:  348 With City:  Colares
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=colares
    ------------------------
    Processing Information:  349 With City:  Nosy Varika
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=nosy varika
    ------------------------
    Processing Information:  350 With City:  Meulaboh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=meulaboh
    ------------------------
    Processing Information:  351 With City:  Chinna Salem
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=chinna salem
    ------------------------
    Processing Information:  352 With City:  Gboko
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=gboko
    ------------------------
    Processing Information:  353 With City:  Ancud
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ancud
    ------------------------
    Processing Information:  354 With City:  Usilampatti
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=usilampatti
    ------------------------
    Processing Information:  355 With City:  Salamanca
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=salamanca
    ------------------------
    Processing Information:  356 With City:  Iskateley
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=iskateley
    ------------------------
    Processing Information:  357 With City:  Iquitos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=iquitos
    ------------------------
    Processing Information:  358 With City:  Kintampo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kintampo
    ------------------------
    Processing Information:  359 With City:  Mahibadhoo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=mahibadhoo
    ------------------------
    Processing Information:  360 With City:  Chapais
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=chapais
    ------------------------
    Processing Information:  361 With City:  Marsa Matruh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=marsa matruh
    ------------------------
    Processing Information:  362 With City:  Vilhena
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=vilhena
    ------------------------
    Processing Information:  363 With City:  Dhrangadhra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=dhrangadhra
    ------------------------
    Processing Information:  364 With City:  Wum
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=wum
    ------------------------
    Processing Information:  365 With City:  Purpe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=purpe
    ------------------------
    Processing Information:  366 With City:  Usinsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=usinsk
    ------------------------
    Processing Information:  367 With City:  Alnashi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=alnashi
    ------------------------
    Processing Information:  368 With City:  Dhidhdhoo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=dhidhdhoo
    ------------------------
    Processing Information:  369 With City:  Antofagasta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=antofagasta
    ------------------------
    Processing Information:  370 With City:  Cape Coast
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=cape coast
    ------------------------
    Processing Information:  371 With City:  Penzance
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=penzance
    ------------------------
    Processing Information:  372 With City:  Santo Antonio do Ica
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=santo antonio do ica
    ------------------------
    Processing Information:  373 With City:  Podlesnoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=podlesnoye
    ------------------------
    Processing Information:  374 With City:  Manono
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=manono
    ------------------------
    Processing Information:  375 With City:  Brae
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=brae
    ------------------------
    Processing Information:  376 With City:  Nyrob
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=nyrob
    ------------------------
    Processing Information:  377 With City:  Marquette
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=marquette
    ------------------------
    Processing Information:  378 With City:  Goianesia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=goianesia
    ------------------------
    Processing Information:  379 With City:  Nampula
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=nampula
    ------------------------
    Processing Information:  380 With City:  Gasa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=gasa
    ------------------------
    Processing Information:  381 With City:  Polunochnoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=polunochnoye
    ------------------------
    Processing Information:  382 With City:  Arona
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=arona
    ------------------------
    Processing Information:  383 With City:  Rey Bouba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=rey bouba
    ------------------------
    Processing Information:  384 With City:  Turukhansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=turukhansk
    ------------------------
    Processing Information:  385 With City:  Sept-Iles
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sept-iles
    ------------------------
    Processing Information:  386 With City:  Puerto Madryn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=puerto madryn
    ------------------------
    Processing Information:  387 With City:  Seville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sevilla
    ------------------------
    Processing Information:  388 With City:  Kudahuvadhoo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kudahuvadhoo
    ------------------------
    Processing Information:  389 With City:  Sioux Lookout
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sioux lookout
    ------------------------
    Processing Information:  390 With City:  Ilo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ilo
    ------------------------
    Processing Information:  391 With City:  Axim
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=axim
    ------------------------
    Processing Information:  392 With City:  Witbank
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=witbank
    ------------------------
    Processing Information:  393 With City:  Yining
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=yining
    ------------------------
    Processing Information:  394 With City:  Kalmunai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kalmunai
    ------------------------
    Processing Information:  395 With City:  Major Isidoro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=major isidoro
    ------------------------
    Processing Information:  396 With City:  Antalaha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=antalaha
    ------------------------
    Processing Information:  397 With City:  Kovdor
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kovdor
    ------------------------
    Processing Information:  398 With City:  Mitu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=mitu
    ------------------------
    Processing Information:  399 With City:  Camacupa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=camacupa
    ------------------------
    Processing Information:  400 With City:  Zhezkazgan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=zhezkazgan
    ------------------------
    Processing Information:  401 With City:  Matagami
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=matagami
    ------------------------
    Processing Information:  402 With City:  Igrim
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=igrim
    ------------------------
    Processing Information:  403 With City:  Belmonte
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=belmonte
    ------------------------
    Processing Information:  404 With City:  Dunmanway
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=dunmanway
    ------------------------
    Processing Information:  405 With City:  Pangnirtung
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=pangnirtung
    ------------------------
    Processing Information:  406 With City:  Ereymentau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=ereymentau
    ------------------------
    Processing Information:  407 With City:  Zermatt
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=zermatt
    ------------------------
    Processing Information:  408 With City:  Verkhnyaya Salda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=verkhnyaya salda
    ------------------------
    Processing Information:  409 With City:  Cabedelo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=cabedelo
    ------------------------
    Processing Information:  410 With City:  Yarensk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=yarensk
    ------------------------
    Processing Information:  411 With City:  Puerto Carreno
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=puerto carreno
    ------------------------
    Processing Information:  412 With City:  Bermejo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=bermejo
    ------------------------
    Processing Information:  413 With City:  Jaciara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=jaciara
    ------------------------
    Processing Information:  414 With City:  Rafaela
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=rafaela
    ------------------------
    Processing Information:  415 With City:  General Pico
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=general pico
    ------------------------
    Processing Information:  416 With City:  Rancho Veloz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=rancho veloz
    ------------------------
    Processing Information:  417 With City:  Puerto Montt
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=puerto montt
    ------------------------
    Processing Information:  418 With City:  Jijiga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=jijiga
    ------------------------
    Processing Information:  419 With City:  Tiznit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=tiznit
    ------------------------
    Processing Information:  420 With City:  Tulu Bolo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=tulu bolo
    ------------------------
    Processing Information:  421 With City:  Cordoba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=cordoba
    ------------------------
    Processing Information:  422 With City:  Paracatu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=paracatu
    ------------------------
    Processing Information:  423 With City:  Buta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=buta
    ------------------------
    Processing Information:  424 With City:  Jurm
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=jurm
    ------------------------
    Processing Information:  425 With City:  Cayenne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=cayenne
    ------------------------
    Processing Information:  426 With City:  Sindor
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=sindor
    ------------------------
    Processing Information:  427 With City:  Srivardhan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=srivardhan
    ------------------------
    Processing Information:  428 With City:  Bafoulabe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=bafoulabe
    ------------------------
    Processing Information:  429 With City:  Mitsamiouli
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=mitsamiouli
    ------------------------
    Processing Information:  430 With City:  Uyuni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=uyuni
    ------------------------
    Processing Information:  431 With City:  Kalabo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=kalabo
    ------------------------
    Processing Information:  432 With City:  Gulu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=gulu
    ------------------------
    Processing Information:  433 With City:  Thompson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=thompson
    ------------------------
    Processing Information:  434 With City:  Gamboula
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=gamboula
    ------------------------
    Processing Information:  435 With City:  Pauini
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=pauini
    ------------------------
    Processing Information:  436 With City:  Iranshahr
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=iranshahr
    ------------------------
    Processing Information:  437 With City:  Guarapari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=796fc7786f1ced770caae62b2b4d5d7b&q=guarapari
    


```python

sample1 = city_df_sample.dropna(axis = 0,how="any",inplace = False)
```


```python
sample1
Date = dt.now().strftime("(%m/%d/%Y)")
```

#Plots:


```python
# Scatter Plot Lat vs Temperature
plt.scatter(sample1["Lat"], sample1["Temp"], marker="o", color = 'b')
plt.title("City Altitude vs Max Temperature " + str(Date))
plt.ylabel("Max Temperature")
plt.xlabel("Latitude")
plt.yticks(np.arange(-40, 120, 20))
plt.grid(True)

plt.savefig("TempCitiesLat.png")

plt.show()
```


![png](output_17_0.png)



```python
#Scatter PLot Lat vs Humidity

# Build a scatter plot for each data type
plt.scatter(sample1["Lat"], sample1["Humidity"], marker="o", color = 'blue')

# # Incorporate the other graph properties
plt.title("City Altitude vs Humidity " + str(Date))
plt.ylabel("Humidity")
plt.xlabel("Latitude")
plt.grid(True)
plt.yticks(np.arange(-40, 120, 20))

# # Save the figure
plt.savefig("HumidityitiesLat.png")

# Show plot
plt.show()

```


![png](output_18_0.png)



```python
##Scatter plot lat vs Clouds
plt.scatter(sample1["Lat"], sample1["Cloudiness"], marker="o", color = 'blue')

plt.title("City Altitude vs Cloudiness " + str(Date))
plt.ylabel("Cloudiness (%)")
plt.xlabel("Latitude")
plt.grid(True)
plt.yticks(np.arange(-40, 120, 20))

plt.savefig("CloudLatCity.png")

plt.show()
```


![png](output_19_0.png)



```python
#Scatter plot lat vs wind

plt.scatter(sample1["Lat"], sample1["Wind Speed"], marker="o", color = 'blue')

plt.title("City Altitude vs Wind Speed " + str(Date))
plt.ylabel("Wind Speed")
plt.xlabel("Latitude")
plt.grid(True)


plt.savefig("WindLatCity.png")

plt.show()
```


![png](output_20_0.png)



```python
# Scatter Plot Long vs Temperature
plt.scatter(sample1["Long"], sample1["Temp"], marker="o", color = 'b')
plt.title("City Altitude vs Max Temperature " + str(Date))
plt.ylabel("Max Temperature")
plt.xlabel("Longitude")
plt.yticks(np.arange(-40, 120, 20))
plt.grid(True)

plt.savefig("TempCitiesLong.png")

plt.show()
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-1-d4dd51871471> in <module>()
          1 # Scatter Plot Long vs Temperature
    ----> 2 plt.scatter(sample1["Long"], sample1["Temp"], marker="o", color = 'b')
          3 plt.title("City Altitude vs Max Temperature " + str(Date))
          4 plt.ylabel("Max Temperature")
          5 plt.xlabel("Longitude")
    

    NameError: name 'plt' is not defined

