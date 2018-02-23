

```python
import pandas as pd


```


```python
#read file
purchase_data = pd.read_json('C:\\Users\\ushuel00\\Desktop\\purchase_data.json')
purchase_data.head(5)
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
purchase_data.dtypes
```




    Age            int64
    Gender        object
    Item ID        int64
    Item Name     object
    Price        float64
    SN            object
    dtype: object




```python
#total number of players
total_number_players = purchase_data['SN'].count()
pd.DataFrame({"Total Number Players": [total_number_players]})

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
      <th>Total Number Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>780</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis (Total)**
#Number of Unique Items
#Average Purchase Price
#Total Number of Purchases
#Total Revenue
unique_item_count = len(purchase_data['Item Name'].unique())
average_purchase_price = purchase_data["Price"].mean()
total_number_of_purchase = purchase_data['Item Name'].count()
total_revenue = purchase_data["Price"].sum()

purchasing_analysis_table = pd.DataFrame({"Number of Unique Items": [unique_item_count],"Average Purchase Price": [average_purchase_price],"Total Number of Purchases": [total_number_of_purchase],"Total Revenue": [total_revenue]})
purchasing_analysis_table
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
      <th>Average Purchase Price</th>
      <th>Number of Unique Items</th>
      <th>Total Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2.931192</td>
      <td>179</td>
      <td>780</td>
      <td>2286.33</td>
    </tr>
  </tbody>
</table>
</div>




```python
purchasing_analysis_table['Average Purchase Price'] = pd.to_numeric(purchasing_analysis_table['Average Purchase Price'])
purchasing_analysis_table['Total Revenue'] = pd.to_numeric(purchasing_analysis_table['Total Revenue'])
purchasing_analysis_table["Average Purchase Price"] = purchasing_analysis_table["Average Purchase Price"].map("${:.2f}".format)
purchasing_analysis_table["Total Revenue"] = purchasing_analysis_table["Total Revenue"].map("${:.2f}".format)

purchasing_analysis_table
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
      <th>Average Purchase Price</th>
      <th>Number of Unique Items</th>
      <th>Total Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>$2.93</td>
      <td>179</td>
      <td>780</td>
      <td>$2286.33</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Gender Demographics**

#Percentage and Count of Male Players
#Percentage and Count of Female Players
#Percentage and Count of Other / Non-Disclosed

male = purchase_data["Gender"].value_counts()['Male']
female = purchase_data["Gender"].value_counts()['Female']
non_gender_specific = total_number_players - male - female


male_percent = ((male/total_number_players) * 100).round(2)
female_percent = ((female/total_number_players) * 100).round(2)
non_gender_specific_percent = ((non_gender_specific/total_number_players) * 100).round(2)
Gender_Demographics_table=pd.DataFrame({"":["Male", "Female", "Other/Non Disclosed"], "Percentage of Players": [male_percent, female_percent, non_gender_specific_percent ],"Total Count": [male, female, non_gender_specific]})
Gender_Demographics_table

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
      <th></th>
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Male</td>
      <td>81.15</td>
      <td>633</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Female</td>
      <td>17.44</td>
      <td>136</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other/Non Disclosed</td>
      <td>1.41</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
Gender_Demographics_table = Gender_Demographics_table.set_index("")
Gender_Demographics_table

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
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>81.15</td>
      <td>633</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>17.44</td>
      <td>136</td>
    </tr>
    <tr>
      <th>Other/Non Disclosed</th>
      <td>1.41</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis (Gender)** 
#The below each broken by gender
#Purchase Count = total number of purchase group by gender
#Average Purchase Price = average purchase price group by gender
#Total Purchase Value = total revenue by gender
#Normalized Totals. I dont know how to do this one, i dont understand what this is.  
count_by_gender = purchase_data.groupby(['Gender'])[['Item ID']].count().reset_index()
count_by_gender
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
      <th>Gender</th>
      <th>Item ID</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>136</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>633</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
average_price_by_gender = purchase_data.groupby(['Gender'])[["Price"]].mean().reset_index()
average_price_by_gender
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
      <th>Gender</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>2.815515</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>2.950521</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>3.249091</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_revenue_by_gender = purchase_data.groupby(['Gender'])[["Price"]].sum().reset_index()
total_revenue_by_gender
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
      <th>Gender</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>382.91</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>1867.68</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>35.74</td>
    </tr>
  </tbody>
</table>
</div>




```python
count_avg_price = pd.merge(count_by_gender, average_price_by_gender, on="Gender", how = "outer")
count_avg_price = count_avg_price.rename(columns={'Price':'Total Revenue', 'Item ID':'Purchase Count',})
count_avg_price
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
      <th>Gender</th>
      <th>Purchase Count</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>136</td>
      <td>2.815515</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>633</td>
      <td>2.950521</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>11</td>
      <td>3.249091</td>
    </tr>
  </tbody>
</table>
</div>




```python
purchasing_analysis_gender = pd.merge(count_avg_price, total_revenue_by_gender, on="Gender", how = "outer")
purchasing_analysis_gender = purchasing_analysis_gender.rename(columns={'Price':'Average Purchase Price', 'Total Revenue':'Total Purchase Value'})
purchasing_analysis_gender
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
      <th>Gender</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
      <th>Average Purchase Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>136</td>
      <td>2.815515</td>
      <td>382.91</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>633</td>
      <td>2.950521</td>
      <td>1867.68</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>11</td>
      <td>3.249091</td>
      <td>35.74</td>
    </tr>
  </tbody>
</table>
</div>




```python
purchasing_analysis_gender.set_index("Gender")
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
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
      <th>Average Purchase Price</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>136</td>
      <td>2.815515</td>
      <td>382.91</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>633</td>
      <td>2.950521</td>
      <td>1867.68</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
      <td>3.249091</td>
      <td>35.74</td>
    </tr>
  </tbody>
</table>
</div>




```python
bins = [0, 10, 14, 19, 24, 29, 34, 39, 100]
group_names = ['<10', '10-14', '15-19', '20-24', '25-29', '30-34', '35-39', '40+']
pd.cut(Gender_Demographics_table["Percentage of Players"], bins, labels=group_names)
purchase_data["age bins"] = pd.cut(purchase_data["Age"], bins, labels=group_names)
purchase_data.head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>age bins</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
      <td>35-39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
      <td>30-34</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
  # Purchase Count
  # Average Purchase Price
  # Total Purchase Value
  # Normalized Totals
count_by_age = purchase_data.groupby(['age bins'])[['Item ID']].count().reset_index()

average_price_by_age = purchase_data.groupby(['age bins'])[["Price"]].mean().reset_index().round(2)

merge_by_age = pd.merge(count_by_age, average_price_by_age, on="age bins", how = "outer")

merge_by_age = merge_by_age.rename(columns={'Item ID':'Purchase Count', 'Price':'Average Purchase Price'})
merge_by_age

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
      <th>age bins</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>32</td>
      <td>3.02</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>31</td>
      <td>2.70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>133</td>
      <td>2.91</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>336</td>
      <td>2.91</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>125</td>
      <td>2.96</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>64</td>
      <td>3.08</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>42</td>
      <td>2.84</td>
    </tr>
    <tr>
      <th>7</th>
      <td>40+</td>
      <td>17</td>
      <td>3.16</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_revenue_by_age = purchase_data.groupby(['age bins'])[["Price"]].sum().reset_index()
combined = pd.merge(merge_by_age, total_revenue_by_age, on="age bins", how = "outer")
combined = combined.set_index("age bins")
combined = combined.rename(columns={'Price':'Total Purchase Value'})
combined
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>age bins</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>32</td>
      <td>3.02</td>
      <td>96.62</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>31</td>
      <td>2.70</td>
      <td>83.79</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>133</td>
      <td>2.91</td>
      <td>386.42</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>336</td>
      <td>2.91</td>
      <td>978.77</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>125</td>
      <td>2.96</td>
      <td>370.33</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>64</td>
      <td>3.08</td>
      <td>197.25</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>42</td>
      <td>2.84</td>
      <td>119.40</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>17</td>
      <td>3.16</td>
      <td>53.75</td>
    </tr>
  </tbody>
</table>
</div>




```python
sum_by_SN = purchase_data.groupby(["SN"])[["Price"]].sum().reset_index()
sum_by_SN.head()

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
      <th>SN</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Adairialis76</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>6.70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aeduera68</td>
      <td>5.80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aela59</td>
      <td>1.27</td>
    </tr>
  </tbody>
</table>
</div>




```python
top_spenders_sorted = sum_by_SN.sort_values("Price", ascending=False).reset_index()
top_spenders_sorted.head()
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
      <th>index</th>
      <th>SN</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>538</td>
      <td>Undirrala66</td>
      <td>17.06</td>
    </tr>
    <tr>
      <th>1</th>
      <td>428</td>
      <td>Saedue76</td>
      <td>13.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>354</td>
      <td>Mindimnya67</td>
      <td>12.74</td>
    </tr>
    <tr>
      <th>3</th>
      <td>181</td>
      <td>Haellysu29</td>
      <td>12.73</td>
    </tr>
    <tr>
      <th>4</th>
      <td>120</td>
      <td>Eoda93</td>
      <td>11.58</td>
    </tr>
  </tbody>
</table>
</div>




```python
purchase_data_SN_indexed = purchase_data.set_index("SN")
top_5_spenders = purchase_data_SN_indexed.loc[["Undirrala66", "Saedue76", "Mindimnya67", "Haellysu29", "Eoda93"], ["Item ID"]]
top_5_spenders.reset_index()
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
      <th>SN</th>
      <th>Item ID</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Undirrala66</td>
      <td>144</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Undirrala66</td>
      <td>115</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Undirrala66</td>
      <td>62</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Undirrala66</td>
      <td>18</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Undirrala66</td>
      <td>133</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Saedue76</td>
      <td>13</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Saedue76</td>
      <td>140</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Saedue76</td>
      <td>7</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Saedue76</td>
      <td>73</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Mindimnya67</td>
      <td>140</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Mindimnya67</td>
      <td>163</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Mindimnya67</td>
      <td>145</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Mindimnya67</td>
      <td>161</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Haellysu29</td>
      <td>96</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Haellysu29</td>
      <td>166</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Haellysu29</td>
      <td>91</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Eoda93</td>
      <td>35</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Eoda93</td>
      <td>173</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Eoda93</td>
      <td>76</td>
    </tr>
  </tbody>
</table>
</div>




```python
top_spenders_count = top_5_spenders.groupby(["SN"])[["Item ID"]].count().reset_index()
top_spenders_count
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
      <th>SN</th>
      <th>Item ID</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Eoda93</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Haellysu29</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mindimnya67</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Saedue76</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Undirrala66</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
top_spenders = pd.merge(top_spenders_sorted, top_spenders_count, on="SN", how = "inner")
top_spenders = top_spenders.rename(columns={'Item ID':'Purchase Count'})
top_spenders = top_spenders.rename(columns={'Price':'Total Purchase Value'})
top_spenders['Total Purchase Value'] = pd.to_numeric(top_spenders['Total Purchase Value'])
top_spenders['Purchase Count'] = pd.to_numeric(top_spenders['Purchase Count'])
top_spenders

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
      <th>index</th>
      <th>SN</th>
      <th>Total Purchase Value</th>
      <th>Purchase Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>538</td>
      <td>Undirrala66</td>
      <td>17.06</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>428</td>
      <td>Saedue76</td>
      <td>13.56</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>354</td>
      <td>Mindimnya67</td>
      <td>12.74</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>181</td>
      <td>Haellysu29</td>
      <td>12.73</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>120</td>
      <td>Eoda93</td>
      <td>11.58</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Top Spenders**

#Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
  # SN
  # Purchase Count
  # Average Purchase Price
  # Total Purchase Value
top_spenders["Average Purchase Price"] = (top_spenders["Total Purchase Value"] / top_spenders["Purchase Count"]).round(2)
top_spenders
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
      <th>index</th>
      <th>SN</th>
      <th>Total Purchase Value</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>538</td>
      <td>Undirrala66</td>
      <td>17.06</td>
      <td>5</td>
      <td>3.41</td>
    </tr>
    <tr>
      <th>1</th>
      <td>428</td>
      <td>Saedue76</td>
      <td>13.56</td>
      <td>4</td>
      <td>3.39</td>
    </tr>
    <tr>
      <th>2</th>
      <td>354</td>
      <td>Mindimnya67</td>
      <td>12.74</td>
      <td>4</td>
      <td>3.18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>181</td>
      <td>Haellysu29</td>
      <td>12.73</td>
      <td>3</td>
      <td>4.24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>120</td>
      <td>Eoda93</td>
      <td>11.58</td>
      <td>3</td>
      <td>3.86</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Most Popular Items**

# Identify the 5 most popular items by purchase count, then list (in a table):
  # Item ID
  # Item Name
  # Purchase Count
  # Item Price
  # Total Purchase Value
popular_count = purchase_data.groupby(["Item Name"])[["Item ID"]].count().sort_values("Item ID", ascending=False).reset_index()
popular_count = popular_count.rename(columns={'Item ID':'Purchase Count'})
popular_count["Item ID"] = purchase_data["Item ID"]
popular_count["Item Price"] = purchase_data ["Price"]
popular_count["Total Purchase Value"]= popular_count["Item Price"]*popular_count["Purchase Count"]
popular_count.head()
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
      <th>Item Name</th>
      <th>Purchase Count</th>
      <th>Item ID</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Final Critic</td>
      <td>14</td>
      <td>165</td>
      <td>3.37</td>
      <td>47.18</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Arcane Gem</td>
      <td>11</td>
      <td>119</td>
      <td>2.32</td>
      <td>25.52</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Betrayal, Whisper of Grieving Widows</td>
      <td>11</td>
      <td>174</td>
      <td>2.46</td>
      <td>27.06</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Stormcaller</td>
      <td>10</td>
      <td>92</td>
      <td>1.36</td>
      <td>13.60</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Woeful Adamantite Claymore</td>
      <td>9</td>
      <td>63</td>
      <td>1.27</td>
      <td>11.43</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Most Profitable Items**

# Identify the 5 most profitable items by total purchase value, then list (in a table):
  # Item ID
  # Item Name
  # Purchase Count
  # Item Price
  # Total Purchase Value
profitable = popular_count.sort_values("Total Purchase Value", ascending=False)
profitable = profitable.set_index("Item ID")
profitable.head()

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
      <th>Item Name</th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>165</th>
      <td>Final Critic</td>
      <td>14</td>
      <td>3.37</td>
      <td>47.18</td>
    </tr>
    <tr>
      <th>153</th>
      <td>Trickster</td>
      <td>9</td>
      <td>4.57</td>
      <td>41.13</td>
    </tr>
    <tr>
      <th>99</th>
      <td>Darkheart</td>
      <td>8</td>
      <td>4.53</td>
      <td>36.24</td>
    </tr>
    <tr>
      <th>177</th>
      <td>Alpha</td>
      <td>7</td>
      <td>4.89</td>
      <td>34.23</td>
    </tr>
    <tr>
      <th>96</th>
      <td>Brimstone</td>
      <td>7</td>
      <td>4.77</td>
      <td>33.39</td>
    </tr>
  </tbody>
</table>
</div>


