# Top 5 Leagues(Soccer) Case Study (2022/23 Season)
By: Job Monita
Data source from: https://www.kaggle.com/datasets/oles04/top-leagues-player
The dataset used in this case study is all about soccer, soccer that is considered the most popular sport in the world, with over 3.5 billion fans worldwidetop. This dataset containt the 5 top soccer leagues in the Europe, which are the English Premier League, Spanish La Liga, German Bundesliga, Italian Serie A, and French Ligue 1. My choice about this dataset came from my biggest passion about soccer, I have always been a huge fan of soccer since i was a kid.
### Questions to consider
1. who is the most expensives players in all league?
2. which nationality has the most player in all league?
3. who was the youngest players in all league? 
## Exploratory Data Analysis


```python
import pandas as pd
import matplotlib
import matplotlib.pyplot as plt
import numpy as np
import plotly.express as px
import plotly.graph_objects as go

```


```python
df = pd.read_csv("Downloads/top5_leagues_player.csv")
```


```python
df.head(10)
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
      <th>Unnamed: 0</th>
      <th>name</th>
      <th>full_name</th>
      <th>age</th>
      <th>height</th>
      <th>nationality</th>
      <th>place_of_birth</th>
      <th>price</th>
      <th>max_price</th>
      <th>position</th>
      <th>shirt_nr</th>
      <th>foot</th>
      <th>club</th>
      <th>contract_expires</th>
      <th>joined_club</th>
      <th>player_agent</th>
      <th>outfitter</th>
      <th>league</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Ederson</td>
      <td>NaN</td>
      <td>29</td>
      <td>1.88</td>
      <td>Brazil  Portugal</td>
      <td>Osasco (SP)</td>
      <td>45.00</td>
      <td>70.0</td>
      <td>Goalkeeper</td>
      <td>31</td>
      <td>left</td>
      <td>Man City</td>
      <td>2026-06-30</td>
      <td>2017-07-01</td>
      <td>Gestifute</td>
      <td>Puma</td>
      <td>EPL</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Stefan Ortega</td>
      <td>Stefan Ortega Moreno</td>
      <td>30</td>
      <td>1.85</td>
      <td>Germany  Spain</td>
      <td>Hofgeismar</td>
      <td>6.00</td>
      <td>6.0</td>
      <td>Goalkeeper</td>
      <td>18</td>
      <td>right</td>
      <td>Man City</td>
      <td>2025-06-30</td>
      <td>2022-07-01</td>
      <td>neblung ...</td>
      <td>NaN</td>
      <td>EPL</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Scott Carson</td>
      <td>Scott Paul Carson</td>
      <td>37</td>
      <td>1.88</td>
      <td>England</td>
      <td>Whitehaven</td>
      <td>0.25</td>
      <td>6.0</td>
      <td>Goalkeeper</td>
      <td>33</td>
      <td>right</td>
      <td>Man City</td>
      <td>2023-06-30</td>
      <td>2021-07-20</td>
      <td>Wasserman</td>
      <td>Puma</td>
      <td>EPL</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Rúben Dias</td>
      <td>Rúben Santos Gato Alves Dias</td>
      <td>26</td>
      <td>1.87</td>
      <td>Portugal</td>
      <td>Amadora</td>
      <td>75.00</td>
      <td>75.0</td>
      <td>Defender - Centre-Back</td>
      <td>3</td>
      <td>right</td>
      <td>Man City</td>
      <td>2027-06-30</td>
      <td>2020-09-29</td>
      <td>Gestifute</td>
      <td>Nike</td>
      <td>EPL</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Nathan Aké</td>
      <td>Nathan Benjamin Aké</td>
      <td>28</td>
      <td>1.80</td>
      <td>Netherlands  Cote d'Ivoire</td>
      <td>Den Haag</td>
      <td>35.00</td>
      <td>40.0</td>
      <td>Defender - Centre-Back</td>
      <td>6</td>
      <td>left</td>
      <td>Man City</td>
      <td>2025-06-30</td>
      <td>2020-08-05</td>
      <td>Wasserman</td>
      <td>Nike</td>
      <td>EPL</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>John Stones</td>
      <td>NaN</td>
      <td>28</td>
      <td>1.88</td>
      <td>England</td>
      <td>Barnsley</td>
      <td>30.00</td>
      <td>60.0</td>
      <td>Defender - Centre-Back</td>
      <td>5</td>
      <td>right</td>
      <td>Man City</td>
      <td>2026-06-30</td>
      <td>2016-08-09</td>
      <td>Wasserman</td>
      <td>Nike</td>
      <td>EPL</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Aymeric Laporte</td>
      <td>Aymeric Jean Louis Gerard Alphonse Laporte</td>
      <td>28</td>
      <td>1.89</td>
      <td>Spain  France</td>
      <td>Agen</td>
      <td>30.00</td>
      <td>75.0</td>
      <td>Defender - Centre-Back</td>
      <td>14</td>
      <td>left</td>
      <td>Man City</td>
      <td>2025-06-30</td>
      <td>2018-01-30</td>
      <td>NaN</td>
      <td>adidas</td>
      <td>EPL</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>Manuel Akanji</td>
      <td>Manuel Obafemi Akanji</td>
      <td>27</td>
      <td>1.88</td>
      <td>Switzerland  Nigeria</td>
      <td>Wiesendangen</td>
      <td>30.00</td>
      <td>40.0</td>
      <td>Defender - Centre-Back</td>
      <td>25</td>
      <td>right</td>
      <td>Man City</td>
      <td>2027-06-30</td>
      <td>2022-09-01</td>
      <td>IFM</td>
      <td>Nike</td>
      <td>EPL</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Sergio Gómez</td>
      <td>Sergio Gómez Martín</td>
      <td>22</td>
      <td>1.71</td>
      <td>Spain</td>
      <td>Badalona</td>
      <td>15.00</td>
      <td>15.0</td>
      <td>Defender - Left-Back</td>
      <td>21</td>
      <td>left</td>
      <td>Man City</td>
      <td>2026-06-30</td>
      <td>2022-08-16</td>
      <td>SEG</td>
      <td>NaN</td>
      <td>EPL</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Benjamin Mendy</td>
      <td>NaN</td>
      <td>28</td>
      <td>1.85</td>
      <td>France  Senegal</td>
      <td>Longjumeau</td>
      <td>NaN</td>
      <td>45.0</td>
      <td>Defender - Left-Back</td>
      <td>22</td>
      <td>left</td>
      <td>Man City</td>
      <td>2023-06-30</td>
      <td>2017-07-24</td>
      <td>Sport Cover</td>
      <td>adidas</td>
      <td>EPL</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.tail(10)
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
      <th>Unnamed: 0</th>
      <th>name</th>
      <th>full_name</th>
      <th>age</th>
      <th>height</th>
      <th>nationality</th>
      <th>place_of_birth</th>
      <th>price</th>
      <th>max_price</th>
      <th>position</th>
      <th>shirt_nr</th>
      <th>foot</th>
      <th>club</th>
      <th>contract_expires</th>
      <th>joined_club</th>
      <th>player_agent</th>
      <th>outfitter</th>
      <th>league</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2602</th>
      <td>2602</td>
      <td>Kevin Spadanuda</td>
      <td>NaN</td>
      <td>26</td>
      <td>1.77</td>
      <td>Switzerland  Italy</td>
      <td>Bülach</td>
      <td>0.80</td>
      <td>0.80</td>
      <td>Attack - Left Winger</td>
      <td>27</td>
      <td>right</td>
      <td>AC Ajaccio</td>
      <td>2025-06-30</td>
      <td>2022-07-01</td>
      <td>Soccer Mondial AG</td>
      <td>NaN</td>
      <td>Other</td>
    </tr>
    <tr>
      <th>2603</th>
      <td>2603</td>
      <td>Jean Botué</td>
      <td>Kouame Jean Fiacre Botué</td>
      <td>20</td>
      <td>1.84</td>
      <td>Burkina Faso</td>
      <td>Marcory</td>
      <td>0.50</td>
      <td>0.90</td>
      <td>Attack - Left Winger</td>
      <td>18</td>
      <td>left</td>
      <td>AC Ajaccio</td>
      <td>2023-06-30</td>
      <td>2021-02-16</td>
      <td>SVF FOOT</td>
      <td>NaN</td>
      <td>Other</td>
    </tr>
    <tr>
      <th>2604</th>
      <td>2604</td>
      <td>Cyrille Bayala</td>
      <td>Cyrille Barros Bayala</td>
      <td>26</td>
      <td>1.81</td>
      <td>Burkina Faso</td>
      <td>Ouagadougou</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>Attack - Right Winger</td>
      <td>14</td>
      <td>right</td>
      <td>AC Ajaccio</td>
      <td>2024-06-30</td>
      <td>2021-01-15</td>
      <td>SVF FOOT</td>
      <td>NaN</td>
      <td>Other</td>
    </tr>
    <tr>
      <th>2605</th>
      <td>2605</td>
      <td>Riad Nouri</td>
      <td>NaN</td>
      <td>37</td>
      <td>1.78</td>
      <td>France  Algeria</td>
      <td>Marseille</td>
      <td>0.25</td>
      <td>0.70</td>
      <td>Attack - Right Winger</td>
      <td>5</td>
      <td>right</td>
      <td>AC Ajaccio</td>
      <td>2024-06-30</td>
      <td>2020-09-07</td>
      <td>Just 4 player Group</td>
      <td>NaN</td>
      <td>Other</td>
    </tr>
    <tr>
      <th>2606</th>
      <td>2606</td>
      <td>Ruan Levine</td>
      <td>NaN</td>
      <td>24</td>
      <td>1.77</td>
      <td>Brazil</td>
      <td>NaN</td>
      <td>0.10</td>
      <td>0.10</td>
      <td>Attack - Right Winger</td>
      <td>24</td>
      <td>right</td>
      <td>AC Ajaccio</td>
      <td>2023-06-30</td>
      <td>2022-09-20</td>
      <td>Talents Sports</td>
      <td>NaN</td>
      <td>Other</td>
    </tr>
    <tr>
      <th>2607</th>
      <td>2607</td>
      <td>Moussa Djitté</td>
      <td>Moussa Kalilou Djitté</td>
      <td>23</td>
      <td>1.80</td>
      <td>Senegal</td>
      <td>Diattouma</td>
      <td>2.00</td>
      <td>2.00</td>
      <td>Attack - Centre-Forward</td>
      <td>28</td>
      <td>right</td>
      <td>AC Ajaccio</td>
      <td>2023-06-30</td>
      <td>2023-01-31</td>
      <td>FS Management</td>
      <td>NaN</td>
      <td>Other</td>
    </tr>
    <tr>
      <th>2608</th>
      <td>2608</td>
      <td>Mounaïm El Idrissy</td>
      <td>منعم الإدريسي</td>
      <td>24</td>
      <td>1.81</td>
      <td>France  Morocco</td>
      <td>Martigues</td>
      <td>1.80</td>
      <td>1.80</td>
      <td>Attack - Centre-Forward</td>
      <td>7</td>
      <td>right</td>
      <td>AC Ajaccio</td>
      <td>2023-06-30</td>
      <td>2019-07-01</td>
      <td>N.Agency</td>
      <td>NaN</td>
      <td>Other</td>
    </tr>
    <tr>
      <th>2609</th>
      <td>2609</td>
      <td>Moussa Soumano</td>
      <td>NaN</td>
      <td>17</td>
      <td>NaN</td>
      <td>France  Mali</td>
      <td>NaN</td>
      <td>0.90</td>
      <td>0.90</td>
      <td>Attack - Centre-Forward</td>
      <td>34</td>
      <td>NaN</td>
      <td>AC Ajaccio</td>
      <td>2026-06-30</td>
      <td>2023-01-01</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Other</td>
    </tr>
    <tr>
      <th>2610</th>
      <td>2610</td>
      <td>Romain Hamouma</td>
      <td>NaN</td>
      <td>36</td>
      <td>1.79</td>
      <td>France  Algeria</td>
      <td>Montbéliard</td>
      <td>0.60</td>
      <td>7.00</td>
      <td>Attack - Centre-Forward</td>
      <td>17</td>
      <td>right</td>
      <td>AC Ajaccio</td>
      <td>2023-06-30</td>
      <td>2022-07-01</td>
      <td>Gallea Gestion S.A</td>
      <td>NaN</td>
      <td>Other</td>
    </tr>
    <tr>
      <th>2611</th>
      <td>2611</td>
      <td>Yoann Touzghar</td>
      <td>NaN</td>
      <td>36</td>
      <td>1.80</td>
      <td>Tunisia  France</td>
      <td>Avignon</td>
      <td>0.50</td>
      <td>1.75</td>
      <td>Attack - Centre-Forward</td>
      <td>9</td>
      <td>right</td>
      <td>AC Ajaccio</td>
      <td>2024-06-30</td>
      <td>2022-08-24</td>
      <td>AGJ SP MGMT</td>
      <td>NaN</td>
      <td>Other</td>
    </tr>
  </tbody>
</table>
</div>




```python
num_rows = df.shape[0]
num_cols = df.shape[1]
```


```python
print(f"Number of rows: {num_rows}")
print(f"Number of columns: {num_cols}")
```

    Number of rows: 2612
    Number of columns: 18



```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 2612 entries, 0 to 2611
    Data columns (total 18 columns):
     #   Column            Non-Null Count  Dtype  
    ---  ------            --------------  -----  
     0   Unnamed: 0        2612 non-null   int64  
     1   name              2612 non-null   object 
     2   full_name         1480 non-null   object 
     3   age               2612 non-null   int64  
     4   height            2601 non-null   float64
     5   nationality       2612 non-null   object 
     6   place_of_birth    2595 non-null   object 
     7   price             2602 non-null   float64
     8   max_price         2606 non-null   float64
     9   position          2612 non-null   object 
     10  shirt_nr          2612 non-null   int64  
     11  foot              2576 non-null   object 
     12  club              2612 non-null   object 
     13  contract_expires  2544 non-null   object 
     14  joined_club       2612 non-null   object 
     15  player_agent      2353 non-null   object 
     16  outfitter         1003 non-null   object 
     17  league            2612 non-null   object 
    dtypes: float64(3), int64(3), object(12)
    memory usage: 367.4+ KB


## 1. The most expensive players in all league (2022/23 Season)


```python
df_exp = df[['name','max_price']].head(10)
df_exp.sort_values('max_price', ascending=False, inplace=True)
```


```python
df_exp
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
      <th>name</th>
      <th>max_price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>Rúben Dias</td>
      <td>75.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Aymeric Laporte</td>
      <td>75.0</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Ederson</td>
      <td>70.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>John Stones</td>
      <td>60.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Benjamin Mendy</td>
      <td>45.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nathan Aké</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Manuel Akanji</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Sergio Gómez</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Stefan Ortega</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Scott Carson</td>
      <td>6.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure(figsize=(15,5))
plt.bar(list(df_exp['name'].value_counts()[0:10].keys()),list(df_exp['max_price'][0:10]),color=["blue","green","red","gray","yellow","purple","orange","brown","black"])
plt.xlabel("Name of the players")
plt.ylabel("Maximum Price")
plt.title("10 most expensive players in all league (Maximum price in Million)")
plt.show() 
```


    
![png](output_17_0.png)
    


## 2. Which nationality has the most player in all league (2022/23 Season)


```python
df['nationality'].value_counts()[0:10]
```




    nationality
    Spain               311
    Italy               201
    Germany             191
    France              117
    England             117
    Brazil               66
    Portugal             38
    Argentina  Italy     38
    Denmark              35
    Poland               33
    Name: count, dtype: int64




```python
plt.figure(figsize=(15,5))
plt.bar(list(df['nationality'].value_counts()[0:10].keys()),list(df['nationality'].value_counts()[0:10]),color=["blue","green","red","gray","yellow","purple","orange","brown","black",])
plt.xlabel("Nationality of the players")
plt.ylabel("Maximum Price")
plt.title("10 country with most expensive players(Maximum price in Million)")
plt.show() 
```


    
![png](output_20_0.png)
    


## 3. The youngest player in all league


```python
df_yg = df[['age', 'name']].head(10)
df_yg.sort_values('age', ascending=True, inplace=True)
df_yg
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
      <th>age</th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>8</th>
      <td>22</td>
      <td>Sergio Gómez</td>
    </tr>
    <tr>
      <th>3</th>
      <td>26</td>
      <td>Rúben Dias</td>
    </tr>
    <tr>
      <th>7</th>
      <td>27</td>
      <td>Manuel Akanji</td>
    </tr>
    <tr>
      <th>4</th>
      <td>28</td>
      <td>Nathan Aké</td>
    </tr>
    <tr>
      <th>5</th>
      <td>28</td>
      <td>John Stones</td>
    </tr>
    <tr>
      <th>6</th>
      <td>28</td>
      <td>Aymeric Laporte</td>
    </tr>
    <tr>
      <th>9</th>
      <td>28</td>
      <td>Benjamin Mendy</td>
    </tr>
    <tr>
      <th>0</th>
      <td>29</td>
      <td>Ederson</td>
    </tr>
    <tr>
      <th>1</th>
      <td>30</td>
      <td>Stefan Ortega</td>
    </tr>
    <tr>
      <th>2</th>
      <td>37</td>
      <td>Scott Carson</td>
    </tr>
  </tbody>
</table>
</div>



## Summary
1. According to my study, The most expensive player in all league is "Kevin Debrune", with a maximum price of 150 Million
2. My study as shown me that the nationality that has most of player in all league are Spainish people
3. Data as shown Sergio Gomez was the youngest of them all