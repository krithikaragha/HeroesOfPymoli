

```python
# Import Dependencies
from __future__ import division
import pandas as pd
import numpy as np
import csv
```


```python
# Create a path to read the file
file_path = "Resources/purchase_data.csv"
```


```python
# Read the file using read_csv
pymoli = pd.read_csv(file_path)
pymoli.head()
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
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
    </tr>
  </tbody>
</table>
</div>



### Total Players


```python
total_players = pymoli['SN'].value_counts()
total_players_count = total_players.count()
total_players_df = pd.DataFrame({"Total Players": [total_players_count]})
total_players_df
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
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>576</td>
    </tr>
  </tbody>
</table>
</div>



### Purchasing Analysis (Total)


```python
# No. of Unique Items
items =  pymoli['Item Name'].value_counts()
no_unique_items = len(items)

# Average purchase price
average_purchase_price = pymoli['Price'].mean()
average_purchase_price = round(average_purchase_price, 2)

# Total number of purchases
total_purchases = pymoli['Price'].count()

# Total revenue
total_revenue = pymoli['Price'].sum()

purchase_analysis_total = pd.DataFrame({'Unique Items': [no_unique_items],
                                     'Avg. Purchase Price' : [average_purchase_price],
                                     'Total Purchases' : [total_purchases],
                                     'Total Revenue' : [total_revenue]})
purchase_analysis_total
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
      <th>Unique Items</th>
      <th>Avg. Purchase Price</th>
      <th>Total Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>179</td>
      <td>3.05</td>
      <td>780</td>
      <td>2379.77</td>
    </tr>
  </tbody>
</table>
</div>



### Gender Demographics


```python
# Get unique values from the table
pymoli_clean_df = pymoli.drop_duplicates(subset=['SN', 'Gender'], keep='first')

# Get total count of players of all genders i.e. Male, Female and Other/Non-Disclosed
gender = pymoli_clean_df['Gender'].value_counts()
gender_dict = dict(gender)
total_count = pymoli_clean_df['Gender'].count()

# Get Percentage and Count of Male Players
male_count = gender_dict['Male']
male_perc = (male_count / total_count) * 100
male_perc = round(male_perc, 2)

# Get Percentage and Count of Female Players
female_count = gender_dict['Female']
female_perc = (female_count / total_count) * 100
female_perc = round(female_perc, 2)

# Get Percentage and Count of Other/Non-Disclosed Players
other_count = gender_dict['Other / Non-Disclosed']
other_perc = (other_count / total_count) * 100
other_perc = round(other_perc, 2)

gender_list = [(str(male_count), str(male_perc)), 
                   (str(female_count), str(female_perc)), 
                   (str(other_count), str(other_perc))]

gender_df = pd.DataFrame(gender_list, columns = ['Total Count' , 'Total Percentage',], index=['Male', 'Female', 'Nonbinary'])
gender_df
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
      <th>Total Count</th>
      <th>Total Percentage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>484</td>
      <td>84.03</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>81</td>
      <td>14.06</td>
    </tr>
    <tr>
      <th>Nonbinary</th>
      <td>11</td>
      <td>1.91</td>
    </tr>
  </tbody>
</table>
</div>



### Purchasing Analysis (Gender)


```python
# Purchase Count
purchase = pymoli['Gender'].value_counts()
purchase_dict = dict(purchase)

#-----------------------------------------------------------

# Get purchase count for Male players
male_purchase_count = purchase_dict['Male']

# Get purchase count for Female players
female_purchase_count= purchase_dict['Female']

# Get purchase count for Other/Non-Disclosed players
other_purchase_count = purchase_dict['Other / Non-Disclosed']

# Total Purchase Value
sum_gender = pymoli.groupby('Gender')['Price'].sum()
sum_gender_dict = dict(sum_gender)

#-----------------------------------------------------------

# Get total purchase value for Male players
male_purchase_sum = sum_gender_dict['Male']
male_purchase_sum = round(male_purchase_sum, 2)

# Get total purchase value for Female players
female_purchase_sum = sum_gender_dict['Female']
female_purchase_sum = round(female_purchase_sum, 2)

# Get total purchase value for Other/Non-Disclosed players
other_purchase_sum = sum_gender_dict['Other / Non-Disclosed']
other_purchase_sum = round(other_purchase_sum, 2)

# Average Purchase Price
#-----------------------------------------------------------

# Get average purchase value for Male players
avg_purchase_male = round((male_purchase_sum / male_purchase_count), 2)

# Get average purchase value for Female players
avg_purchase_female = round((female_purchase_sum / female_purchase_count), 2)

# Get average purchase value for Other/Non-Disclosed players
avg_purchase_other = round((other_purchase_sum / other_purchase_count), 2)

# Average Purchase Total Per Person by Gender
#-----------------------------------------------------------

# Get Average Purchase Total per person for Male players
avg_purchase_total_male = round((male_purchase_sum / male_count), 2)

# Get average purchase total per person for Female players
avg_purchase_total_female = round((female_purchase_sum / female_count), 2)

# Get average purchase total per person for Other/Non-disclosed players
avg_purchase_total_other = round((other_purchase_sum / other_count), 2)

#-----------------------------------------------------------

purchase_analysis_gender_list = [(str(male_purchase_count), str(avg_purchase_male), str(male_purchase_sum), str(avg_purchase_total_male)),
                                 (str(female_purchase_count), str(avg_purchase_female), str(female_purchase_sum), str(avg_purchase_total_female)), 
                                 (str(other_purchase_count), str(avg_purchase_other), str(other_purchase_sum), str(avg_purchase_total_other))]

purchase_analysis_gender = pd.DataFrame(purchase_analysis_gender_list, columns = ['Purchase Count', 'Average Purchase Price','Total Purchase Value', 'Avg Total Purchase per Person',], index=['Male', 'Female', 'Other/Non-Disclosed'])
purchase_analysis_gender
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Avg Total Purchase per Person</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>652</td>
      <td>3.02</td>
      <td>1967.64</td>
      <td>4.07</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>113</td>
      <td>3.2</td>
      <td>361.94</td>
      <td>4.47</td>
    </tr>
    <tr>
      <th>Other/Non-Disclosed</th>
      <td>15</td>
      <td>3.35</td>
      <td>50.19</td>
      <td>4.56</td>
    </tr>
  </tbody>
</table>
</div>



### Age Demographics


```python
bins = [0, 9, 14, 19, 24, 29, 34, 39, 45]
names = ['<10', '10-14', '15-19', '20-24', '25-29', '30-34', '35-39', '40+']

pymoli_test = pymoli_clean_df.groupby(pd.cut(pymoli_clean_df['Age'], bins, labels=names))['SN'].count()

# Total Count
sn_count = list(pymoli_test)

# Percentage of Players
sn_perc_count = []
for item in sn_count:
    perc_count = round ( ((item / total_players_count) * 100), 2)
    sn_perc_count.append(perc_count)    

age_df = pd.DataFrame(
           {'Total Count' : sn_count,
            'Percentage of Players' : sn_perc_count
            }, index=names)
age_df
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
      <th>Total Count</th>
      <th>Percentage of Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>17</td>
      <td>2.95</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>22</td>
      <td>3.82</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>107</td>
      <td>18.58</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>258</td>
      <td>44.79</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>77</td>
      <td>13.37</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>52</td>
      <td>9.03</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>31</td>
      <td>5.38</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>12</td>
      <td>2.08</td>
    </tr>
  </tbody>
</table>
</div>



### Purchasing Analysis (Age)


```python
# Purchase Count
pymoli_purchase_count = pymoli.groupby(pd.cut(pymoli['Age'], bins, labels=names))['SN'].count()
pymoli_purchase_count_dict = dict(pymoli_test)
pymoli_purchase_count_list = list(pymoli_purchase_count_dict.values())

# Total Purchase Value
pymoli_purchase_sum = pymoli.groupby(pd.cut(pymoli['Age'], bins, labels=names))['Price'].sum()
pymoli_purchase_sum_dict = dict(pymoli_purchase_sum)
pymoli_purchase_sum_list = list(pymoli_purchase_sum_dict.values())

# Average Purchase Value
combined_lists = [pymoli_purchase_sum_list, pymoli_purchase_count_list]
avg_purchase_price = [(x/y) for x, y in zip(*combined_lists)]

# Average Purchase Total Per Person 
combined_lists2 = [pymoli_purchase_sum_list, sn_count]
avg_purchase_price_per_person = [(x/y) for x, y in zip(*combined_lists2)]

purchase_analysis_age = pd.DataFrame(
    {'Purchase Count': pymoli_purchase_count_list,
     'Average Purchase Price': avg_purchase_price,
     'Total Purchase Value': pymoli_purchase_sum_list,
     'Avg Total Purchase per Person': avg_purchase_price_per_person,
    }, index=names)

purchase_analysis_age
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Avg Total Purchase per Person</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>17</td>
      <td>4.537059</td>
      <td>77.13</td>
      <td>4.537059</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>22</td>
      <td>3.762727</td>
      <td>82.78</td>
      <td>3.762727</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>107</td>
      <td>3.858785</td>
      <td>412.89</td>
      <td>3.858785</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>258</td>
      <td>4.318062</td>
      <td>1114.06</td>
      <td>4.318062</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>77</td>
      <td>3.805195</td>
      <td>293.00</td>
      <td>3.805195</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>52</td>
      <td>4.115385</td>
      <td>214.00</td>
      <td>4.115385</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>31</td>
      <td>4.763548</td>
      <td>147.67</td>
      <td>4.763548</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>12</td>
      <td>3.186667</td>
      <td>38.24</td>
      <td>3.186667</td>
    </tr>
  </tbody>
</table>
</div>



### Top Spenders


```python
# SN
top_spenders = pymoli.groupby('SN')['Price'].sum()
top_spenders_dict = dict(top_spenders)

# Total Purchase Value

top_spenders_sorted_keys = sorted(top_spenders_dict, key=top_spenders_dict.get, reverse=True)[:5]

top_spenders_sorted_values = [top_spenders_dict[top_spenders_sorted_keys[0]], top_spenders_dict[top_spenders_sorted_keys[1]], top_spenders_dict[top_spenders_sorted_keys[2]], top_spenders_dict[top_spenders_sorted_keys[3]], top_spenders_dict[top_spenders_sorted_keys[4]]]

# Purchase Count

top_spenders_count = pymoli.groupby('SN')['Price'].count()
top_spenders_count_dict = dict(top_spenders_count)

top_spenders_count_list = [ top_spenders_count[top_spenders_sorted_keys[0]], top_spenders_count[top_spenders_sorted_keys[1]],
                           top_spenders_count[top_spenders_sorted_keys[2]], top_spenders_count[top_spenders_sorted_keys[3]],
                           top_spenders_count[top_spenders_sorted_keys[4]] ]

# Average Purchase Price

combined_lists3 = [top_spenders_sorted_values, top_spenders_count_list]
top_5_avg_purchase_price = [(x/y) for x, y in zip(*combined_lists3)]

top_5_spenders = pd.DataFrame(
                {'Purchase Count' : top_spenders_count_list,
                 'Average Purchase Price' : top_5_avg_purchase_price,
                 'Total Purchase Value' : top_spenders_sorted_values}, index=top_spenders_sorted_keys)

top_5_spenders
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Lisosia93</th>
      <td>5</td>
      <td>3.792000</td>
      <td>18.96</td>
    </tr>
    <tr>
      <th>Idastidru52</th>
      <td>4</td>
      <td>3.862500</td>
      <td>15.45</td>
    </tr>
    <tr>
      <th>Chamjask73</th>
      <td>3</td>
      <td>4.610000</td>
      <td>13.83</td>
    </tr>
    <tr>
      <th>Iral74</th>
      <td>4</td>
      <td>3.405000</td>
      <td>13.62</td>
    </tr>
    <tr>
      <th>Iskadarya95</th>
      <td>3</td>
      <td>4.366667</td>
      <td>13.10</td>
    </tr>
  </tbody>
</table>
</div>



### Most Popular Items


```python
# Item ID
popularItemIDs = pymoli['Item ID'].value_counts()
popularItemIDs_list = list(popularItemIDs)

# Purchase Count
popularItemIDs_purchase_count = sorted(popularItemIDs_list, reverse=True)[:5]

# Item Name
popularItemNames = pymoli.groupby('Item ID')['Item Name'].value_counts()
popularItemNames_dict = dict(popularItemNames)
popularItemNames_list = sorted(popularItemNames_dict, key=popularItemNames_dict.get, reverse=True)[:5]
popularItemNames_list_dict = dict(popularItemNames_list)
popularItemNames_list_dict_keys = list(popularItemNames_list_dict.keys())
popularItemNames_list_dict_values = list(popularItemNames_list_dict.values())

# Item Price
popularItems_prices = pymoli.groupby('Item ID')['Price'].value_counts()
popularItems_prices_dict = dict(popularItems_prices)
popularItems_prices_list = sorted(popularItems_prices_dict, key=popularItems_prices_dict.get, reverse=True)[:5]
popularItems_prices_list_dict = dict(popularItems_prices_list)
popularItems_prices_list_dict_values = list(popularItems_prices_list_dict.values())

# Total Purchase Value
popularItems_sum = pymoli.groupby('Item ID')['Price'].sum()
popularItems_sum_dict = dict(popularItems_sum)
popularItems_sum_dict_values = list(popularItems_sum_dict.values())
popularItems_sum_dict_list = sorted(popularItems_sum_dict.values(), reverse=True)[:5]

top_5_popular_items = pd.DataFrame(
    {'Item ID': popularItemNames_list_dict_keys,
     'Name': popularItemNames_list_dict_values,
    'Purchase Count': popularItemIDs_purchase_count,
    'Item Price': popularItems_prices_list_dict_values,
    'Total Purchase Value': popularItems_sum_dict_list,
    })

top_5_popular_items
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
      <th>Item ID</th>
      <th>Name</th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>178</td>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>12</td>
      <td>4.23</td>
      <td>50.76</td>
    </tr>
    <tr>
      <th>1</th>
      <td>82</td>
      <td>Nirvana</td>
      <td>9</td>
      <td>4.90</td>
      <td>44.10</td>
    </tr>
    <tr>
      <th>2</th>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>9</td>
      <td>3.53</td>
      <td>41.22</td>
    </tr>
    <tr>
      <th>3</th>
      <td>145</td>
      <td>Fiery Glass Crusader</td>
      <td>9</td>
      <td>4.58</td>
      <td>39.04</td>
    </tr>
    <tr>
      <th>4</th>
      <td>19</td>
      <td>Pursuit, Cudgel of Necromancy</td>
      <td>8</td>
      <td>1.02</td>
      <td>34.80</td>
    </tr>
  </tbody>
</table>
</div>



### Most Profitable Items


```python
# Item ID
profitableItemIDs = pymoli.groupby('Item ID')['Price'].sum()
profitableItemIDs_dict = dict(profitableItemIDs)
profitableItemIDs_dict_list = sorted(profitableItemIDs_dict, key=profitableItemIDs_dict.get, reverse=True)[:5]
profitableItemIDs_dict_sum = [ profitableItemIDs_dict[profitableItemIDs_dict_list[0]],
                       profitableItemIDs_dict[profitableItemIDs_dict_list[1]],
                       profitableItemIDs_dict[profitableItemIDs_dict_list[2]],
                       profitableItemIDs_dict[profitableItemIDs_dict_list[3]],
                       profitableItemIDs_dict[profitableItemIDs_dict_list[4]] ]
# print(profitableItemIDs_dict_sum)

# Item Name
profitableNames = pymoli.groupby(['Item Name','Item ID'])['Price'].sum()
profitableNames_dict = dict(profitableNames)
profitableName_dict_list = sorted(profitableNames_dict, key=profitableNames_dict.get, reverse=True)[:5]
profitableName_dict_list_dict = dict(profitableName_dict_list)
profitableName_dict_list_dict_keys = list(profitableName_dict_list_dict.keys())
profitableName_dict_list_dict_values = list(profitableName_dict_list_dict.values())
# print(profitableName_dict_list_dict_keys)

# Item Price
profitablePrices = pymoli.groupby(['Price','Item ID'])['Price'].sum()
profitablePrices_dict = dict(profitablePrices)
profitablePrices_dict_list = sorted(profitablePrices_dict, key=profitablePrices_dict.get, reverse=True)[:5]
profitablePrices_dict_list_dict = dict(profitablePrices_dict_list)
profitablePrices_dict_list_dict_keys = list(profitablePrices_dict_list_dict.keys())
profitablePrices_dict_list_dict_values = list(profitablePrices_dict_list_dict.values())
# print(profitablePrices_dict_list_dict_keys)

top_5_profitable_items = pd.DataFrame(
    {'Item ID': profitableItemIDs_dict_list,
     'Name': profitableName_dict_list_dict_keys,
     'Purchase Count': popularItemIDs_purchase_count,
     'Item Price': profitablePrices_dict_list_dict_keys,
     'Total Purchase Value': profitableItemIDs_dict_sum,
   },)

top_5_profitable_items
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
      <th>Item ID</th>
      <th>Name</th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>178</td>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>12</td>
      <td>4.23</td>
      <td>50.76</td>
    </tr>
    <tr>
      <th>1</th>
      <td>82</td>
      <td>Nirvana</td>
      <td>9</td>
      <td>4.90</td>
      <td>44.10</td>
    </tr>
    <tr>
      <th>2</th>
      <td>145</td>
      <td>Fiery Glass Crusader</td>
      <td>9</td>
      <td>4.58</td>
      <td>41.22</td>
    </tr>
    <tr>
      <th>3</th>
      <td>92</td>
      <td>Final Critic</td>
      <td>9</td>
      <td>4.88</td>
      <td>39.04</td>
    </tr>
    <tr>
      <th>4</th>
      <td>103</td>
      <td>Singed Scalpel</td>
      <td>8</td>
      <td>4.35</td>
      <td>34.80</td>
    </tr>
  </tbody>
</table>
</div>


