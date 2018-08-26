Analyzing the data for their most recent fantasy game Heroes of Pymoli + generating a report that breaks down the game's purchasing data into meaningful insights. Python, Pandas, Numpy + Matplotlib.

import pandas as pd
import numpy as np


```python
#reading and printing the dataset

heroes_data=pd.read_json('/Users/carolineteti/Desktop/pymoli-challenge/purchase_data.json')
heroes_data.head()

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



# PLAYER COUNT
#computing and printing TOTAL PLAYER COUNT
total_player_count = heroes_data['SN'].value_counts().count()
total_player_count = pd.DataFrame(data=[{'Total Players': total_player_count}]).style.format({'Total Players': '{:}'})
total_player_count


# PURCHASING ANALYSIS
#computing and printing NUMBER OF UNIQUE ITEMS, AVERAGE PURCHASE PRICE, TOTAL NUMBER OF PURCHASES, TOTAL REVENUE
#def variables, getting a count and calculate, avg. and sum
currency = '${0:.2f}'
unique  = len(set(heroes_data['Item Name']))
count   = heroes_data['Price'].count()
average = heroes_data['Price'].mean()
total   = heroes_data['Price'].sum()

player_data = [{'Number of Unique Items': unique,
                'Average Purchase Price': average,
                'Total Number of Purchases':    count,
                'Total Revenue':          total}]

purchase_analysis = pd.DataFrame(player_data).style.format({'Average Purchase Price': currency, 'Total Revenue': currency})
purchase_analysis

# GENDER DEMOGRAPHICS
#computing and printing PERCENTAGE and COUNT by a GroupBy

count      = heroes_data.groupby('Gender').count()
total      = heroes_data['Gender'].count()
percentage = count / total

gender_data = {'Percentage':    percentage['SN'],
          'Total Players': count['SN']}

purchase_analysis = pd.DataFrame(gender_data).style.format({'Percentage': '{:.2%}'})
purchase_analysis


```python
#GENDER DEMOGRAPHICS 2
#PURCHASING ANALYSIS using count, mean, sum 

count   = heroes_data.groupby('Gender').count()
average = heroes_data.groupby('Gender').mean()
total   = heroes_data.groupby('Gender').sum()
max = heroes_data.groupby('Gender').max()
min = heroes_data.groupby('Gender').min()


gender_data = {'Purchase Count':         count['Price'],
           'Average Purchase Price': average['Price'],
           'Total Purchase Value':   total['Price'], 
           'Max Purchase Price':   max['Price'],
           'Min Purchase Price':   min['Price']} 

purchase_analysis = pd.DataFrame(gender_data).style.format({'Average Purchase Price': currency, 'Total Purchase Value': currency})
purchase_analysis
```




<style  type="text/css" >
</style>  
<table id="T_4ee31376_6dce_11e8_84ab_3200e8828b01" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Average Purchase Price</th> 
        <th class="col_heading level0 col1" >Max Purchase Price</th> 
        <th class="col_heading level0 col2" >Min Purchase Price</th> 
        <th class="col_heading level0 col3" >Purchase Count</th> 
        <th class="col_heading level0 col4" >Total Purchase Value</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Gender</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_4ee31376_6dce_11e8_84ab_3200e8828b01level0_row0" class="row_heading level0 row0" >Female</th> 
        <td id="T_4ee31376_6dce_11e8_84ab_3200e8828b01row0_col0" class="data row0 col0" >$2.82</td> 
        <td id="T_4ee31376_6dce_11e8_84ab_3200e8828b01row0_col1" class="data row0 col1" >4.95</td> 
        <td id="T_4ee31376_6dce_11e8_84ab_3200e8828b01row0_col2" class="data row0 col2" >1.03</td> 
        <td id="T_4ee31376_6dce_11e8_84ab_3200e8828b01row0_col3" class="data row0 col3" >136</td> 
        <td id="T_4ee31376_6dce_11e8_84ab_3200e8828b01row0_col4" class="data row0 col4" >$382.91</td> 
    </tr>    <tr> 
        <th id="T_4ee31376_6dce_11e8_84ab_3200e8828b01level0_row1" class="row_heading level0 row1" >Male</th> 
        <td id="T_4ee31376_6dce_11e8_84ab_3200e8828b01row1_col0" class="data row1 col0" >$2.95</td> 
        <td id="T_4ee31376_6dce_11e8_84ab_3200e8828b01row1_col1" class="data row1 col1" >4.95</td> 
        <td id="T_4ee31376_6dce_11e8_84ab_3200e8828b01row1_col2" class="data row1 col2" >1.03</td> 
        <td id="T_4ee31376_6dce_11e8_84ab_3200e8828b01row1_col3" class="data row1 col3" >633</td> 
        <td id="T_4ee31376_6dce_11e8_84ab_3200e8828b01row1_col4" class="data row1 col4" >$1867.68</td> 
    </tr>    <tr> 
        <th id="T_4ee31376_6dce_11e8_84ab_3200e8828b01level0_row2" class="row_heading level0 row2" >Other / Non-Disclosed</th> 
        <td id="T_4ee31376_6dce_11e8_84ab_3200e8828b01row2_col0" class="data row2 col0" >$3.25</td> 
        <td id="T_4ee31376_6dce_11e8_84ab_3200e8828b01row2_col1" class="data row2 col1" >4.32</td> 
        <td id="T_4ee31376_6dce_11e8_84ab_3200e8828b01row2_col2" class="data row2 col2" >1.88</td> 
        <td id="T_4ee31376_6dce_11e8_84ab_3200e8828b01row2_col3" class="data row2 col3" >11</td> 
        <td id="T_4ee31376_6dce_11e8_84ab_3200e8828b01row2_col4" class="data row2 col4" >$35.74</td> 
    </tr></tbody> 
</table> 




```python
#AGE DEMOGRAPHICS
#broken into bins of 4 years <10, 10-14, 15-19, etc.
labels  = [f"{count}-{count + 4}" for count in np.arange(5, 45, 5)]
count   = heroes_data.groupby(pd.cut(heroes_data['Age'], np.arange(5, 50, 5), labels=labels)).count()
average = heroes_data.groupby(pd.cut(heroes_data['Age'], np.arange(5, 50, 5), labels=labels)).mean()
total   = heroes_data.groupby(pd.cut(heroes_data['Age'], np.arange(5, 50, 5), labels=labels)).sum()

age_data = {'Purchase Count':         count['Price'],
            'Average Purchase Price': average['Price'],
            'Total Purchase Value':   total['Price']} 

purchase_analysis = pd.DataFrame(age_data).rename(index={'5-9': '<10', '40-44': '40+'}).style.format({'Average Purchase Price': currency, 'Total Purchase Value': currency})
purchase_analysis
```




<style  type="text/css" >
</style>  
<table id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Average Purchase Price</th> 
        <th class="col_heading level0 col1" >Purchase Count</th> 
        <th class="col_heading level0 col2" >Total Purchase Value</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Age</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01level0_row0" class="row_heading level0 row0" ><10</th> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row0_col0" class="data row0 col0" >$3.02</td> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row0_col1" class="data row0 col1" >32</td> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row0_col2" class="data row0 col2" >$96.62</td> 
    </tr>    <tr> 
        <th id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01level0_row1" class="row_heading level0 row1" >10-14</th> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row1_col0" class="data row1 col0" >$2.87</td> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row1_col1" class="data row1 col1" >78</td> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row1_col2" class="data row1 col2" >$224.15</td> 
    </tr>    <tr> 
        <th id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01level0_row2" class="row_heading level0 row2" >15-19</th> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row2_col0" class="data row2 col0" >$2.87</td> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row2_col1" class="data row2 col1" >184</td> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row2_col2" class="data row2 col2" >$528.74</td> 
    </tr>    <tr> 
        <th id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01level0_row3" class="row_heading level0 row3" >20-24</th> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row3_col0" class="data row3 col0" >$2.96</td> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row3_col1" class="data row3 col1" >305</td> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row3_col2" class="data row3 col2" >$902.61</td> 
    </tr>    <tr> 
        <th id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01level0_row4" class="row_heading level0 row4" >25-29</th> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row4_col0" class="data row4 col0" >$2.89</td> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row4_col1" class="data row4 col1" >76</td> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row4_col2" class="data row4 col2" >$219.82</td> 
    </tr>    <tr> 
        <th id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01level0_row5" class="row_heading level0 row5" >30-34</th> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row5_col0" class="data row5 col0" >$3.07</td> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row5_col1" class="data row5 col1" >58</td> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row5_col2" class="data row5 col2" >$178.26</td> 
    </tr>    <tr> 
        <th id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01level0_row6" class="row_heading level0 row6" >35-39</th> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row6_col0" class="data row6 col0" >$2.90</td> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row6_col1" class="data row6 col1" >44</td> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row6_col2" class="data row6 col2" >$127.49</td> 
    </tr>    <tr> 
        <th id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01level0_row7" class="row_heading level0 row7" >40+</th> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row7_col0" class="data row7 col0" >$2.88</td> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row7_col1" class="data row7 col1" >3</td> 
        <td id="T_4f655aa2_6dce_11e8_a1b5_3200e8828b01row7_col2" class="data row7 col2" >$8.64</td> 
    </tr></tbody> 
</table> 




```python
#TOP SPENDERS, ID top 5 SPENDERS, sorting by PURCHASE COUNT
count = heroes_data.groupby(['Item ID', 'Item Name']).count()
average = heroes_data.groupby(['Item ID', 'Item Name']).mean()
total = heroes_data.groupby(['Item ID', 'Item Name']).sum()



item_data = {'Purchase Count':         count['Price'],
             'Average of Item Price': average['Price'],
             'Total Purchase Value':   total['Price']} # format into currency

purchase_analysis = pd.DataFrame(item_data).sort_values('Purchase Count', ascending=False).head(5).style.format({'Average Purchase Price': currency, 'Total Purchase Value': currency})
purchase_analysis
```




<style  type="text/css" >
</style>  
<table id="T_50130618_6dce_11e8_a5d4_3200e8828b01" > 
<thead>    <tr> 
        <th class="blank" ></th> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Average of Item Price</th> 
        <th class="col_heading level0 col1" >Purchase Count</th> 
        <th class="col_heading level0 col2" >Total Purchase Value</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Item ID</th> 
        <th class="index_name level1" >Item Name</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_50130618_6dce_11e8_a5d4_3200e8828b01level0_row0" class="row_heading level0 row0" >39</th> 
        <th id="T_50130618_6dce_11e8_a5d4_3200e8828b01level1_row0" class="row_heading level1 row0" >Betrayal, Whisper of Grieving Widows</th> 
        <td id="T_50130618_6dce_11e8_a5d4_3200e8828b01row0_col0" class="data row0 col0" >2.35</td> 
        <td id="T_50130618_6dce_11e8_a5d4_3200e8828b01row0_col1" class="data row0 col1" >11</td> 
        <td id="T_50130618_6dce_11e8_a5d4_3200e8828b01row0_col2" class="data row0 col2" >$25.85</td> 
    </tr>    <tr> 
        <th id="T_50130618_6dce_11e8_a5d4_3200e8828b01level0_row1" class="row_heading level0 row1" >84</th> 
        <th id="T_50130618_6dce_11e8_a5d4_3200e8828b01level1_row1" class="row_heading level1 row1" >Arcane Gem</th> 
        <td id="T_50130618_6dce_11e8_a5d4_3200e8828b01row1_col0" class="data row1 col0" >2.23</td> 
        <td id="T_50130618_6dce_11e8_a5d4_3200e8828b01row1_col1" class="data row1 col1" >11</td> 
        <td id="T_50130618_6dce_11e8_a5d4_3200e8828b01row1_col2" class="data row1 col2" >$24.53</td> 
    </tr>    <tr> 
        <th id="T_50130618_6dce_11e8_a5d4_3200e8828b01level0_row2" class="row_heading level0 row2" >31</th> 
        <th id="T_50130618_6dce_11e8_a5d4_3200e8828b01level1_row2" class="row_heading level1 row2" >Trickster</th> 
        <td id="T_50130618_6dce_11e8_a5d4_3200e8828b01row2_col0" class="data row2 col0" >2.07</td> 
        <td id="T_50130618_6dce_11e8_a5d4_3200e8828b01row2_col1" class="data row2 col1" >9</td> 
        <td id="T_50130618_6dce_11e8_a5d4_3200e8828b01row2_col2" class="data row2 col2" >$18.63</td> 
    </tr>    <tr> 
        <th id="T_50130618_6dce_11e8_a5d4_3200e8828b01level0_row3" class="row_heading level0 row3" >175</th> 
        <th id="T_50130618_6dce_11e8_a5d4_3200e8828b01level1_row3" class="row_heading level1 row3" >Woeful Adamantite Claymore</th> 
        <td id="T_50130618_6dce_11e8_a5d4_3200e8828b01row3_col0" class="data row3 col0" >1.24</td> 
        <td id="T_50130618_6dce_11e8_a5d4_3200e8828b01row3_col1" class="data row3 col1" >9</td> 
        <td id="T_50130618_6dce_11e8_a5d4_3200e8828b01row3_col2" class="data row3 col2" >$11.16</td> 
    </tr>    <tr> 
        <th id="T_50130618_6dce_11e8_a5d4_3200e8828b01level0_row4" class="row_heading level0 row4" >13</th> 
        <th id="T_50130618_6dce_11e8_a5d4_3200e8828b01level1_row4" class="row_heading level1 row4" >Serenity</th> 
        <td id="T_50130618_6dce_11e8_a5d4_3200e8828b01row4_col0" class="data row4 col0" >1.49</td> 
        <td id="T_50130618_6dce_11e8_a5d4_3200e8828b01row4_col1" class="data row4 col1" >9</td> 
        <td id="T_50130618_6dce_11e8_a5d4_3200e8828b01row4_col2" class="data row4 col2" >$13.41</td> 
    </tr></tbody> 
</table> 




```python
#MOST POPULAR ITEMS, sorting value by TOTAL PURCHASE VALUE
purchase_analysis = pd.DataFrame(item_data).sort_values('Total Purchase Value', ascending=False).head(5).style.format({'Average Purchase Price': currency, 'Total Purchase Value': currency})
purchase_analysis
```




<style  type="text/css" >
</style>  
<table id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01" > 
<thead>    <tr> 
        <th class="blank" ></th> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Average of Item Price</th> 
        <th class="col_heading level0 col1" >Purchase Count</th> 
        <th class="col_heading level0 col2" >Total Purchase Value</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Item ID</th> 
        <th class="index_name level1" >Item Name</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01level0_row0" class="row_heading level0 row0" >34</th> 
        <th id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01level1_row0" class="row_heading level1 row0" >Retribution Axe</th> 
        <td id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01row0_col0" class="data row0 col0" >4.14</td> 
        <td id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01row0_col1" class="data row0 col1" >9</td> 
        <td id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01row0_col2" class="data row0 col2" >$37.26</td> 
    </tr>    <tr> 
        <th id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01level0_row1" class="row_heading level0 row1" >115</th> 
        <th id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01level1_row1" class="row_heading level1 row1" >Spectral Diamond Doomblade</th> 
        <td id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01row1_col0" class="data row1 col0" >4.25</td> 
        <td id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01row1_col1" class="data row1 col1" >7</td> 
        <td id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01row1_col2" class="data row1 col2" >$29.75</td> 
    </tr>    <tr> 
        <th id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01level0_row2" class="row_heading level0 row2" >32</th> 
        <th id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01level1_row2" class="row_heading level1 row2" >Orenmir</th> 
        <td id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01row2_col0" class="data row2 col0" >4.95</td> 
        <td id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01row2_col1" class="data row2 col1" >6</td> 
        <td id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01row2_col2" class="data row2 col2" >$29.70</td> 
    </tr>    <tr> 
        <th id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01level0_row3" class="row_heading level0 row3" >103</th> 
        <th id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01level1_row3" class="row_heading level1 row3" >Singed Scalpel</th> 
        <td id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01row3_col0" class="data row3 col0" >4.87</td> 
        <td id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01row3_col1" class="data row3 col1" >6</td> 
        <td id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01row3_col2" class="data row3 col2" >$29.22</td> 
    </tr>    <tr> 
        <th id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01level0_row4" class="row_heading level0 row4" >107</th> 
        <th id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01level1_row4" class="row_heading level1 row4" >Splitter, Foe Of Subtlety</th> 
        <td id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01row4_col0" class="data row4 col0" >3.61</td> 
        <td id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01row4_col1" class="data row4 col1" >8</td> 
        <td id="T_50a277ba_6dce_11e8_b4c0_3200e8828b01row4_col2" class="data row4 col2" >$28.88</td> 
    </tr></tbody> 
</table> 



#trend 1: Male customers generate three times as much revenue ($1867.68) as female customers ($382.91) with a similar average price around $2.90. 
#trend 2: Customers in thier early-mid twenties generate the most revenue.
#trend 3: Both in top spenders and top units sold are items pertaining to revenge: Betrayal, Whisper of Grieving Widows and Retribution Axe. 
