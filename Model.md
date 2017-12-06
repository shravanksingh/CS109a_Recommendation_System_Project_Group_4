---
title: Recommendation System Models
notebook: Model.ipynb
nav_include: 2
---

## Contents
{:.no_toc}
*  
{: toc}






As we have large amounf data so we are loading data line by line in dataframe business_df, review_df, user_df



```python
import json

def readjson(filepath):
    data = []
    i=0
    with open(filepath,encoding="utf8") as f:
            for line in f:
                 if i<100000:
                    data.append(json.loads(line))
                    #print(i)
                    i +=1
    return pd.DataFrame(data)

business_df = readjson('./dataset/business.json')
review_df = readjson('./dataset/review.json')
user_df = readjson('./dataset/user.json')
```


Getting reaturants out of business dataframe based on Food category



```python
business_df['categories'] = business_df['categories'].astype(str)
restaurant_df = business_df[business_df['categories'].str.contains('Food')==True]

complete_df = restaurant_df.merge(review_df,on='business_id').merge(user_df,on='user_id')

```




```python
complete_df.head(2)
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
      <th>address</th>
      <th>attributes</th>
      <th>business_id</th>
      <th>categories</th>
      <th>city</th>
      <th>hours</th>
      <th>is_open</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>name_x</th>
      <th>neighborhood</th>
      <th>postal_code</th>
      <th>review_count_x</th>
      <th>stars_x</th>
      <th>state</th>
      <th>cool_x</th>
      <th>date</th>
      <th>funny_x</th>
      <th>review_id</th>
      <th>stars_y</th>
      <th>text</th>
      <th>useful_x</th>
      <th>user_id</th>
      <th>average_stars</th>
      <th>compliment_cool</th>
      <th>compliment_cute</th>
      <th>compliment_funny</th>
      <th>compliment_hot</th>
      <th>compliment_list</th>
      <th>compliment_more</th>
      <th>compliment_note</th>
      <th>compliment_photos</th>
      <th>compliment_plain</th>
      <th>compliment_profile</th>
      <th>compliment_writer</th>
      <th>cool_y</th>
      <th>elite</th>
      <th>fans</th>
      <th>friends</th>
      <th>funny_y</th>
      <th>name_y</th>
      <th>review_count_y</th>
      <th>useful_y</th>
      <th>yelping_since</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1203 E Charleston Blvd, Ste 140</td>
      <td>{'RestaurantsTableService': True, 'GoodForMeal...</td>
      <td>YTqtM2WFhcMZGeAGA08Cfg</td>
      <td>['Seafood', 'Restaurants', 'Specialty Food', '...</td>
      <td>Las Vegas</td>
      <td>{'Monday': '10:30-21:00', 'Tuesday': '10:30-21...</td>
      <td>1</td>
      <td>36.159363</td>
      <td>-115.135949</td>
      <td>Mariscos Playa Escondida</td>
      <td>Downtown</td>
      <td>89104</td>
      <td>330</td>
      <td>4.5</td>
      <td>NV</td>
      <td>0</td>
      <td>2016-09-16</td>
      <td>1</td>
      <td>ZH8g_PoY0Tr3YdQ-RGySrA</td>
      <td>5</td>
      <td>Great place. There was a man here who was very...</td>
      <td>1</td>
      <td>EDe16577dBImA1ypOzPlKg</td>
      <td>5.00</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>0</td>
      <td>Jessica</td>
      <td>1</td>
      <td>0</td>
      <td>2014-07-26</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1203 E Charleston Blvd, Ste 140</td>
      <td>{'RestaurantsTableService': True, 'GoodForMeal...</td>
      <td>YTqtM2WFhcMZGeAGA08Cfg</td>
      <td>['Seafood', 'Restaurants', 'Specialty Food', '...</td>
      <td>Las Vegas</td>
      <td>{'Monday': '10:30-21:00', 'Tuesday': '10:30-21...</td>
      <td>1</td>
      <td>36.159363</td>
      <td>-115.135949</td>
      <td>Mariscos Playa Escondida</td>
      <td>Downtown</td>
      <td>89104</td>
      <td>330</td>
      <td>4.5</td>
      <td>NV</td>
      <td>1</td>
      <td>2014-11-13</td>
      <td>1</td>
      <td>6r2uAJE1dqUq1IHn_3R3qA</td>
      <td>4</td>
      <td>HOT HOT HOT! Real Mexican Food\n\nNO fake wate...</td>
      <td>2</td>
      <td>twx2ZgFUbat87vGQ_tFbPA</td>
      <td>3.55</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>11</td>
      <td>[]</td>
      <td>3</td>
      <td>[eFObFWgDiQJwUiy9WlhOfg, W4KL3Q_AVGfRrWcwR60gK...</td>
      <td>29</td>
      <td>Edwin</td>
      <td>94</td>
      <td>317</td>
      <td>2010-12-30</td>
    </tr>
  </tbody>
</table>
</div>





```python
restaurant_df.describe()
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
      <th>is_open</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>review_count</th>
      <th>stars</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>18503.00000</td>
      <td>18503.000000</td>
      <td>18503.000000</td>
      <td>18503.000000</td>
      <td>18503.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.83073</td>
      <td>39.702568</td>
      <td>-87.807760</td>
      <td>34.804464</td>
      <td>3.546857</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.37500</td>
      <td>5.747548</td>
      <td>27.691971</td>
      <td>82.946472</td>
      <td>0.889710</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.00000</td>
      <td>-34.520401</td>
      <td>-119.551325</td>
      <td>3.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.00000</td>
      <td>35.135615</td>
      <td>-112.013439</td>
      <td>5.000000</td>
      <td>3.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1.00000</td>
      <td>40.440368</td>
      <td>-81.357777</td>
      <td>11.000000</td>
      <td>3.500000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1.00000</td>
      <td>43.665419</td>
      <td>-79.414244</td>
      <td>31.000000</td>
      <td>4.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.00000</td>
      <td>59.438181</td>
      <td>11.769500</td>
      <td>3439.000000</td>
      <td>5.000000</td>
    </tr>
  </tbody>
</table>
</div>





```python
user_df.describe()
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
      <th>average_stars</th>
      <th>compliment_cool</th>
      <th>compliment_cute</th>
      <th>compliment_funny</th>
      <th>compliment_hot</th>
      <th>compliment_list</th>
      <th>compliment_more</th>
      <th>compliment_note</th>
      <th>compliment_photos</th>
      <th>compliment_plain</th>
      <th>compliment_profile</th>
      <th>compliment_writer</th>
      <th>cool</th>
      <th>fans</th>
      <th>funny</th>
      <th>review_count</th>
      <th>useful</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>3.729684</td>
      <td>16.342210</td>
      <td>0.950070</td>
      <td>16.342210</td>
      <td>12.015470</td>
      <td>0.416970</td>
      <td>1.465460</td>
      <td>6.980040</td>
      <td>5.491070</td>
      <td>15.870480</td>
      <td>1.046280</td>
      <td>6.151540</td>
      <td>91.215580</td>
      <td>5.103230</td>
      <td>64.731610</td>
      <td>66.524450</td>
      <td>120.838970</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.835715</td>
      <td>197.424646</td>
      <td>16.639768</td>
      <td>197.424646</td>
      <td>175.458886</td>
      <td>7.165452</td>
      <td>15.762362</td>
      <td>70.410324</td>
      <td>153.225409</td>
      <td>194.113025</td>
      <td>19.474635</td>
      <td>73.883346</td>
      <td>1509.129416</td>
      <td>29.803631</td>
      <td>1049.502721</td>
      <td>178.975429</td>
      <td>1610.123217</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>3.350000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>5.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>3.810000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>16.000000</td>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>4.240000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>3.000000</td>
      <td>50.000000</td>
      <td>13.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>5.000000</td>
      <td>16710.000000</td>
      <td>2146.000000</td>
      <td>16710.000000</td>
      <td>19988.000000</td>
      <td>1265.000000</td>
      <td>1576.000000</td>
      <td>6340.000000</td>
      <td>33297.000000</td>
      <td>13075.000000</td>
      <td>2232.000000</td>
      <td>7117.000000</td>
      <td>175230.000000</td>
      <td>1837.000000</td>
      <td>103514.000000</td>
      <td>11065.000000</td>
      <td>187179.000000</td>
    </tr>
  </tbody>
</table>
</div>





```python
review_df.describe()
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
      <th>cool</th>
      <th>funny</th>
      <th>stars</th>
      <th>useful</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.000000</td>
      <td>100000.00000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.532470</td>
      <td>0.411740</td>
      <td>3.730530</td>
      <td>1.01213</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.992121</td>
      <td>1.655608</td>
      <td>1.418456</td>
      <td>2.46252</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.00000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>3.000000</td>
      <td>0.00000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>4.000000</td>
      <td>0.00000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>5.000000</td>
      <td>1.00000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>104.000000</td>
      <td>114.000000</td>
      <td>5.000000</td>
      <td>113.00000</td>
    </tr>
  </tbody>
</table>
</div>





```python
review_df.head(2)
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
      <th>business_id</th>
      <th>cool</th>
      <th>date</th>
      <th>funny</th>
      <th>review_id</th>
      <th>stars</th>
      <th>text</th>
      <th>useful</th>
      <th>user_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>uYHaNptLzDLoV_JZ_MuzUA</td>
      <td>0</td>
      <td>2016-07-12</td>
      <td>0</td>
      <td>VfBHSwC5Vz_pbFluy07i9Q</td>
      <td>5</td>
      <td>My girlfriend and I stayed here for 3 nights a...</td>
      <td>0</td>
      <td>cjpdDjZyprfyDG3RlkVG3w</td>
    </tr>
    <tr>
      <th>1</th>
      <td>uYHaNptLzDLoV_JZ_MuzUA</td>
      <td>0</td>
      <td>2016-10-02</td>
      <td>0</td>
      <td>3zRpneRKDsOPq92tq7ybAA</td>
      <td>3</td>
      <td>If you need an inexpensive place to stay for a...</td>
      <td>0</td>
      <td>bjTcT8Ty4cJZhEOEo01FGA</td>
    </tr>
  </tbody>
</table>
</div>




##  Creating Baseline Model



```python
complete_df.head(2)
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
      <th>address</th>
      <th>attributes</th>
      <th>business_id</th>
      <th>categories</th>
      <th>city</th>
      <th>hours</th>
      <th>is_open</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>name_x</th>
      <th>neighborhood</th>
      <th>postal_code</th>
      <th>review_count_x</th>
      <th>stars_x</th>
      <th>state</th>
      <th>cool_x</th>
      <th>date</th>
      <th>funny_x</th>
      <th>review_id</th>
      <th>stars_y</th>
      <th>text</th>
      <th>useful_x</th>
      <th>user_id</th>
      <th>average_stars</th>
      <th>compliment_cool</th>
      <th>compliment_cute</th>
      <th>compliment_funny</th>
      <th>compliment_hot</th>
      <th>compliment_list</th>
      <th>compliment_more</th>
      <th>compliment_note</th>
      <th>compliment_photos</th>
      <th>compliment_plain</th>
      <th>compliment_profile</th>
      <th>compliment_writer</th>
      <th>cool_y</th>
      <th>elite</th>
      <th>fans</th>
      <th>friends</th>
      <th>funny_y</th>
      <th>name_y</th>
      <th>review_count_y</th>
      <th>useful_y</th>
      <th>yelping_since</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1203 E Charleston Blvd, Ste 140</td>
      <td>{'RestaurantsTableService': True, 'GoodForMeal...</td>
      <td>YTqtM2WFhcMZGeAGA08Cfg</td>
      <td>['Seafood', 'Restaurants', 'Specialty Food', '...</td>
      <td>Las Vegas</td>
      <td>{'Monday': '10:30-21:00', 'Tuesday': '10:30-21...</td>
      <td>1</td>
      <td>36.159363</td>
      <td>-115.135949</td>
      <td>Mariscos Playa Escondida</td>
      <td>Downtown</td>
      <td>89104</td>
      <td>330</td>
      <td>4.5</td>
      <td>NV</td>
      <td>0</td>
      <td>2016-09-16</td>
      <td>1</td>
      <td>ZH8g_PoY0Tr3YdQ-RGySrA</td>
      <td>5</td>
      <td>Great place. There was a man here who was very...</td>
      <td>1</td>
      <td>EDe16577dBImA1ypOzPlKg</td>
      <td>5.00</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>0</td>
      <td>Jessica</td>
      <td>1</td>
      <td>0</td>
      <td>2014-07-26</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1203 E Charleston Blvd, Ste 140</td>
      <td>{'RestaurantsTableService': True, 'GoodForMeal...</td>
      <td>YTqtM2WFhcMZGeAGA08Cfg</td>
      <td>['Seafood', 'Restaurants', 'Specialty Food', '...</td>
      <td>Las Vegas</td>
      <td>{'Monday': '10:30-21:00', 'Tuesday': '10:30-21...</td>
      <td>1</td>
      <td>36.159363</td>
      <td>-115.135949</td>
      <td>Mariscos Playa Escondida</td>
      <td>Downtown</td>
      <td>89104</td>
      <td>330</td>
      <td>4.5</td>
      <td>NV</td>
      <td>1</td>
      <td>2014-11-13</td>
      <td>1</td>
      <td>6r2uAJE1dqUq1IHn_3R3qA</td>
      <td>4</td>
      <td>HOT HOT HOT! Real Mexican Food\n\nNO fake wate...</td>
      <td>2</td>
      <td>twx2ZgFUbat87vGQ_tFbPA</td>
      <td>3.55</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>11</td>
      <td>[]</td>
      <td>3</td>
      <td>[eFObFWgDiQJwUiy9WlhOfg, W4KL3Q_AVGfRrWcwR60gK...</td>
      <td>29</td>
      <td>Edwin</td>
      <td>94</td>
      <td>317</td>
      <td>2010-12-30</td>
    </tr>
  </tbody>
</table>
</div>



Taking only user_id, business_id, stars_y and using the surprise library(https://pypi.python.org/pypi/scikit-surprise)
Algorithm predicting the baseline estimate for given user and item.



```python
display(Math('r^ui=bui=μ+bu+bi'))
```



$$r^ui=bui=μ+bu+bi$$




```python
baseline_df = complete_df[['user_id','business_id','stars_y']]
```




```python
from surprise import SVD,BaselineOnly, Reader,KNNBaseline
from surprise import Dataset
from surprise import Reader
from surprise import evaluate, print_perf

reader = Reader(rating_scale=(1, 5))
data = Dataset.load_from_df(baseline_df,reader)
data.split(n_folds=3)
```


## BaselineOnly Model

We used Surprise library for Baseline models. Surprise is a Python scikit for building, and analyzing (collaborative-filtering) recommender systems. Various algorithms are built-in, with a focus on rating prediction. 
BaselineOnly is an algorithm predicting the baseline estimate for given user and item 
	Ym = μ + su + sm
where the unknown parameters su and sm indicate the deviations, or biases, of user u and item m respectively from some intercept parameter.

KNNBaseline is a basic collaborative filtering algorithm taking into account a baseline rating.




```python
algo = BaselineOnly()
perf_baseline = evaluate(algo, data, measures=['RMSE', 'MAE'])
print_perf(perf_baseline)
```


    Evaluating RMSE, MAE of algorithm BaselineOnly.
    
    ------------
    Fold 1
    Estimating biases using als...
    RMSE: 1.2452
    MAE:  1.0188
    ------------
    Fold 2
    Estimating biases using als...
    RMSE: 1.2428
    MAE:  1.0015
    ------------
    Fold 3
    Estimating biases using als...
    RMSE: 1.2510
    MAE:  1.0192
    ------------
    ------------
    Mean RMSE: 1.2463
    Mean MAE : 1.0132
    ------------
    ------------
            Fold 1  Fold 2  Fold 3  Mean    
    RMSE    1.2452  1.2428  1.2510  1.2463  
    MAE     1.0188  1.0015  1.0192  1.0132  


## KNNBaseline Model

KNN Based on user restaurant rating



```python
display(Math(r'\hat{r}_{ui} = \mu_u + \sigma_u \frac{ \sum\limits_{v \in N^k_i(u)}\text{sim}(u, v) \cdot (r_{vi} - \mu_v) / \sigma_v} {\sum\limits_{v\in N^k_i(u)} \text{sim}(u, v)}'))

```



$$\hat{r}_{ui} = \mu_u + \sigma_u \frac{ \sum\limits_{v \in N^k_i(u)}\text{sim}(u, v) \cdot (r_{vi} - \mu_v) / \sigma_v} {\sum\limits_{v\in N^k_i(u)} \text{sim}(u, v)}$$




```python
algo = KNNBaseline()

perf_knn_baseline = evaluate(algo, data, measures=['RMSE', 'MAE'])
print_perf(perf_knn_baseline)
```


    Evaluating RMSE, MAE of algorithm KNNBaseline.
    
    ------------
    Fold 1
    Estimating biases using als...
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    RMSE: 1.2509
    MAE:  1.0222
    ------------
    Fold 2
    Estimating biases using als...
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    RMSE: 1.2517
    MAE:  1.0088
    ------------
    Fold 3
    Estimating biases using als...
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    RMSE: 1.2550
    MAE:  1.0203
    ------------
    ------------
    Mean RMSE: 1.2525
    Mean MAE : 1.0171
    ------------
    ------------
            Fold 1  Fold 2  Fold 3  Mean    
    RMSE    1.2509  1.2517  1.2550  1.2525  
    MAE     1.0222  1.0088  1.0203  1.0171  


## Memory Based Collaborative filtering

We used Collaborative filtering. The two primary areas of collaborative filtering are the neighborhood methods and latent factor models. 

Neighborhood methods are centered on computing the relationships between items or, alternatively, between users. The item oriented approach evaluates a user’s preference for an item based on ratings of “neighboring” items by the same user. A product’s neighbors are other products that tend to get similar ratings when rated by the same user. 



```python
n_users = complete_df['user_id'].nunique()
n_restaurants = complete_df['business_id'].nunique()

print('Number of Unique Users: ', n_users)
print('Number of Restaurant: ',n_restaurants)
```


    Number of Unique Users:  11749
    Number of Restaurant:  482


Making user_id and business_id as nominal variable 



```python
unique_user_id = pd.DataFrame(complete_df['user_id'].unique(),columns =['user_id']).reset_index()
unique_user_id['new_user_id'] =unique_user_id['index']
del unique_user_id['index']

unique_business_id = pd.DataFrame(complete_df['business_id'].unique(),columns =['business_id']).reset_index()
unique_business_id['new_business_id'] =unique_business_id['index']
del unique_business_id['index']
```




```python
new_complete_df = complete_df.merge(unique_user_id,on='user_id',how ='left')
new_complete_df = new_complete_df.merge(unique_business_id,on='business_id',how ='left')
```




```python
new_complete_df.head(2)
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
      <th>address</th>
      <th>attributes</th>
      <th>business_id</th>
      <th>categories</th>
      <th>city</th>
      <th>hours</th>
      <th>is_open</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>name_x</th>
      <th>neighborhood</th>
      <th>postal_code</th>
      <th>review_count_x</th>
      <th>stars_x</th>
      <th>state</th>
      <th>cool_x</th>
      <th>date</th>
      <th>funny_x</th>
      <th>review_id</th>
      <th>stars_y</th>
      <th>text</th>
      <th>useful_x</th>
      <th>user_id</th>
      <th>average_stars</th>
      <th>compliment_cool</th>
      <th>compliment_cute</th>
      <th>compliment_funny</th>
      <th>compliment_hot</th>
      <th>compliment_list</th>
      <th>compliment_more</th>
      <th>compliment_note</th>
      <th>compliment_photos</th>
      <th>compliment_plain</th>
      <th>compliment_profile</th>
      <th>compliment_writer</th>
      <th>cool_y</th>
      <th>elite</th>
      <th>fans</th>
      <th>friends</th>
      <th>funny_y</th>
      <th>name_y</th>
      <th>review_count_y</th>
      <th>useful_y</th>
      <th>yelping_since</th>
      <th>new_user_id</th>
      <th>new_business_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1203 E Charleston Blvd, Ste 140</td>
      <td>{'RestaurantsTableService': True, 'GoodForMeal...</td>
      <td>YTqtM2WFhcMZGeAGA08Cfg</td>
      <td>['Seafood', 'Restaurants', 'Specialty Food', '...</td>
      <td>Las Vegas</td>
      <td>{'Monday': '10:30-21:00', 'Tuesday': '10:30-21...</td>
      <td>1</td>
      <td>36.159363</td>
      <td>-115.135949</td>
      <td>Mariscos Playa Escondida</td>
      <td>Downtown</td>
      <td>89104</td>
      <td>330</td>
      <td>4.5</td>
      <td>NV</td>
      <td>0</td>
      <td>2016-09-16</td>
      <td>1</td>
      <td>ZH8g_PoY0Tr3YdQ-RGySrA</td>
      <td>5</td>
      <td>Great place. There was a man here who was very...</td>
      <td>1</td>
      <td>EDe16577dBImA1ypOzPlKg</td>
      <td>5.00</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>[]</td>
      <td>0</td>
      <td>[]</td>
      <td>0</td>
      <td>Jessica</td>
      <td>1</td>
      <td>0</td>
      <td>2014-07-26</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1203 E Charleston Blvd, Ste 140</td>
      <td>{'RestaurantsTableService': True, 'GoodForMeal...</td>
      <td>YTqtM2WFhcMZGeAGA08Cfg</td>
      <td>['Seafood', 'Restaurants', 'Specialty Food', '...</td>
      <td>Las Vegas</td>
      <td>{'Monday': '10:30-21:00', 'Tuesday': '10:30-21...</td>
      <td>1</td>
      <td>36.159363</td>
      <td>-115.135949</td>
      <td>Mariscos Playa Escondida</td>
      <td>Downtown</td>
      <td>89104</td>
      <td>330</td>
      <td>4.5</td>
      <td>NV</td>
      <td>1</td>
      <td>2014-11-13</td>
      <td>1</td>
      <td>6r2uAJE1dqUq1IHn_3R3qA</td>
      <td>4</td>
      <td>HOT HOT HOT! Real Mexican Food\n\nNO fake wate...</td>
      <td>2</td>
      <td>twx2ZgFUbat87vGQ_tFbPA</td>
      <td>3.55</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>11</td>
      <td>[]</td>
      <td>3</td>
      <td>[eFObFWgDiQJwUiy9WlhOfg, W4KL3Q_AVGfRrWcwR60gK...</td>
      <td>29</td>
      <td>Edwin</td>
      <td>94</td>
      <td>317</td>
      <td>2010-12-30</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



### Train Test Split




```python
from sklearn.cross_validation import train_test_split
train_data, test_data = train_test_split(new_complete_df, test_size=0.25)
```




```python
#Creating two,  user and restaurant matrices, one for training and another for testing
train_data_matrix = np.zeros((n_users, n_restaurants))
for row in train_data.itertuples():
    # selecting new_user_id, new_restaurant_id, and rating star
    train_data_matrix[row[45]-1, row[46]-1] = row[20]  

test_data_matrix = np.zeros((n_users, n_restaurants))
for line in test_data.itertuples():
    test_data_matrix[row[45]-1, row[46]-1] = row[20]  
```




```python
from sklearn.metrics.pairwise import pairwise_distances
user_similarity = pairwise_distances(train_data_matrix, metric='cosine')
restaurant_similarity = pairwise_distances(train_data_matrix.T, metric='cosine')
```




```python

def predict_rating(num_rating, sim, type='user'):
    if type == 'user':
        user_rating_avg = num_rating.mean(axis=1)
        ratings_difference = (num_rating - user_rating_avg[:, np.newaxis]) 
        prediction = user_rating_avg[:, np.newaxis] + sim.dot(ratings_difference) / np.array([np.abs(sim).sum(axis=1)]).T
    elif type == 'restaurant':
        prediction = num_rating.dot(sim) / np.array([np.abs(sim).sum(axis=1)])     
    return prediction
```




```python
restaurant_prediction = predict_rating(train_data_matrix, restaurant_similarity, type='restaurant')
user_prediction = predict_rating(train_data_matrix, user_similarity, type='user')

restaurant_prediction_test = predict_rating(test_data_matrix, restaurant_similarity, type='restaurant')
user_prediction_test = predict_rating(test_data_matrix, user_similarity, type='user')
```




```python
model_memory_based_pred_res = restaurant_prediction
model_memory_based_pred_user = user_prediction

model_memory_based_pred_res_test = restaurant_prediction_test
model_memory_based_pred_user_test = user_prediction_test
```


### Evaluation using RMSE




```python
from sklearn.metrics import mean_squared_error
from math import sqrt
def rmse(prediction, true_value):
    prediction = prediction[true_value.nonzero()].flatten() 
    true_value = true_value[true_value.nonzero()].flatten()
    return sqrt(mean_squared_error(prediction, true_value))
```




```python
print('RMSE for training  User based Collaborative filtering:', (rmse(user_prediction, train_data_matrix)))
print('RMSE for training Restaurant based Collaborative filtering: ', (rmse(restaurant_prediction, train_data_matrix)))
print('RMSE for testing  User based Collaborative filtering:', (rmse(user_prediction_test, test_data_matrix)))
print('RMSE for testing Restaurant based Collaborative filtering: ', (rmse(restaurant_prediction_test, test_data_matrix)))
```


    RMSE for training  User based Collaborative filtering: 3.920373589539869
    RMSE for training Restaurant based Collaborative filtering:  3.924467145133183
    RMSE for testing  User based Collaborative filtering: 4.9896265560165975
    RMSE for testing Restaurant based Collaborative filtering:  5.0


## SVD

Latent factor models (aka SVD) are an alternative approach that tries to explain the ratings by characterizing both items and users on number of factors inferred from the ratings patterns. Latent factor models are based on matrix factorization which characterizes both items and users by vectors of factors inferred from item rating patterns. High correspondence between item and user factors leads to a recommendation. From the results, we can see that prediction accuracy has improved by considering also implicit feedback, which provides an additional indication of user preferences.



```python
#Using libraries
import scipy.sparse as sp
from scipy.sparse.linalg import svds

#get SVD components from train matrix. Choose k.
u, s, vt = svds(train_data_matrix, k =10)
s_diag_matrix=np.diag(s)
X_pred = np.dot(np.dot(u, s_diag_matrix), vt)

u_test, s_test, vt_test = svds(test_data_matrix, k =10)
X_pred_test = np.dot(np.dot(u_test, s_diag_matrix), vt)
```




```python
print('RMSE for training User based SVD Collaborative filtering: ', (rmse(X_pred, train_data_matrix)))
print('RMSE for testing User based SVD Collaborative filtering: ', (rmse(X_pred_test, test_data_matrix)))
```


    RMSE for training User based SVD Collaborative filtering:  3.3716947413739393
    RMSE for testing User based SVD Collaborative filtering:  4.999999999650054


## Meta Classifier

We have used multiple models (neighborhoods & SVD) whose individual predictions are combined to classify new examples. Integration should improve predictive accuracy. Each of the models has a mediocre accuracy rate. We would have to increase the importance of the model with high accuracy, and reduce the importance of the models with lower accuracy. To do this in Python, one may use the predicted values as the predictors in a Logistic Regression model, and the corresponding y as the response. Logistic Regression can take the "importance" of each model into account: the "predictors" or models that do well most of the time will have the more significant coefficients.



```python
model_svd_based_pred = X_pred
model_svd_based_pred_test = X_pred_test

model_memory_based_pred_res_flat = model_memory_based_pred_res.ravel()
model_memory_based_pred_user_flat = model_memory_based_pred_user.ravel()
model_svd_based_pred_flat = model_svd_based_pred.ravel()

model_memory_based_pred_res_test_flat = model_memory_based_pred_res_test.ravel()
model_memory_based_pred_user_test_flat = model_memory_based_pred_user_test.ravel()
model_svd_based_pred_test_flat = model_svd_based_pred_test.ravel()

pred_model_array_train =  np.zeros((model_memory_based_pred_res_flat.size,3))
pred_model_array_test =  np.zeros((model_memory_based_pred_res_test_flat.size,3))

pred_model_array_train[:,0] = model_memory_based_pred_res_flat
pred_model_array_train[:,1] = model_memory_based_pred_user_flat 
pred_model_array_train[:,2] = model_svd_based_pred_flat

pred_model_array_test[:,0] = model_memory_based_pred_res_test_flat
pred_model_array_test[:,1] = model_memory_based_pred_user_test_flat 
pred_model_array_test[:,2] = model_svd_based_pred_test_flat

y_train_data_matrix_flat = train_data_matrix.ravel()
y_test_data_matrix_flat = test_data_matrix.ravel()
```




```python
def rmse_new(prediction, true_value):
    return sqrt(mean_squared_error(prediction, true_value))
```




```python
from sklearn.metrics import mean_squared_error
logreg = LogisticRegressionCV()
y_hat_train = logreg.fit(pred_model_array_train[0:100000], y_train_data_matrix_flat[0:100000]).predict(pred_model_array_train)
y_hat_test = logreg.fit(pred_model_array_train[0:100000], y_train_data_matrix_flat[0:100000]).predict(pred_model_array_test)

print("Test LogReg RMSE: ", rmse_new(y_test_data_matrix_flat, y_hat_test))
print("Train LogReg RMSE: ", rmse_new(y_train_data_matrix_flat, y_hat_train))
```


    Test LogReg RMSE:  0.3965122913294842
    Train LogReg RMSE:  0.16192899952388481




```python
print_perf(perf_baseline)
```


            Fold 1  Fold 2  Fold 3  Mean    
    RMSE    1.2452  1.2428  1.2510  1.2463  
    MAE     1.0188  1.0015  1.0192  1.0132  




```python
print_perf(perf_knn_baseline)
```


            Fold 1  Fold 2  Fold 3  Mean    
    RMSE    1.2509  1.2517  1.2550  1.2525  
    MAE     1.0222  1.0088  1.0203  1.0171  


## Model comparison via RMSE



```python
meta_clf_scores_tr = rmse_new(y_train_data_matrix_flat, y_hat_train)
SVD_cf_scores_tr = rmse(X_pred, train_data_matrix)
memory_user_based_cf_scores_tr = rmse(user_prediction, train_data_matrix)
memory_restaurant_based_cf_scores_tr = rmse(restaurant_prediction, train_data_matrix)

meta_clf_scores_ts = rmse_new(y_test_data_matrix_flat, y_hat_test)
SVD_cf_scores_ts = rmse(X_pred_test, test_data_matrix)
memory_user_based_cf_scores_ts = rmse(user_prediction_test, test_data_matrix)
memory_restaurant_based_cf_scores_ts = rmse(restaurant_prediction_test, test_data_matrix)
   
score = [meta_clf_scores_tr,SVD_cf_scores_tr,memory_user_based_cf_scores_tr,memory_restaurant_based_cf_scores_tr,
        meta_clf_scores_ts,SVD_cf_scores_ts,memory_user_based_cf_scores_ts,memory_restaurant_based_cf_scores_ts]


pd.DataFrame(np.array(score).reshape(2,4), columns = ['Meta Classifer','SVD Collaborative Filtetering','Memory Based User Collaborative Filering',
                        'Memory Based Restaurant Collaborative Filtering'], index = ['RMSE in Training','RMSE in Testing'])

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
      <th>Meta Classifer</th>
      <th>SVD Collaborative Filtetering</th>
      <th>Memory Based User Collaborative Filering</th>
      <th>Memory Based Restaurant Collaborative Filtering</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>RMSE in Training</th>
      <td>0.161929</td>
      <td>3.371695</td>
      <td>3.920374</td>
      <td>3.924467</td>
    </tr>
    <tr>
      <th>RMSE in Testing</th>
      <td>0.396512</td>
      <td>5.000000</td>
      <td>4.989627</td>
      <td>5.000000</td>
    </tr>
  </tbody>
</table>
</div>



We can see above that meta Classifier is working better than other models
