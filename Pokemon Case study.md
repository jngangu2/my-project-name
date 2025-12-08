# Pokémon Case Study

By: Job Monita

Data soruce from: https://www.kaggle.com/datasets/abcsds/pokemon

The dataset used in this case study is about all the Pokémon from a series of video games called "Pokémon" developed by Game Freak and published by Nintendo and The Pokémon Company under the Pokémon media franchise, which was first released in February 27, 1996 in Japan. I have chose this dataset because me and my siblings are the biggest fans of pokemon, Our childhood was rocked by this cartoon.



### Questions to Consider

1. Which Pokémon is the strongest one?
2. Which Pokémon is the fastest one?
3. Is there any relationship between speed and strongness?

### Exploratory Data Analysis


```python
pip install plotly==5.11.0
```

    Requirement already satisfied: plotly==5.11.0 in /opt/anaconda3/lib/python3.12/site-packages (5.11.0)
    Requirement already satisfied: tenacity>=6.2.0 in /opt/anaconda3/lib/python3.12/site-packages (from plotly==5.11.0) (8.2.2)
    Note: you may need to restart the kernel to use updated packages.



```python
import pandas as pd
import numpy as np
import plotly
import plotly.express as px
import plotly.graph_objects as go
from matplotlib import pyplot as plt
```


```python
df_poke = pd.read_csv('https://github.com/jobngangu2/my-project-name/raw/main/Pokemon.csv')
display(df_poke)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>318</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>405</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>525</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>625</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>309</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>795</th>
      <td>719</td>
      <td>Diancie</td>
      <td>Rock</td>
      <td>Fairy</td>
      <td>600</td>
      <td>50</td>
      <td>100</td>
      <td>150</td>
      <td>100</td>
      <td>150</td>
      <td>50</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>796</th>
      <td>719</td>
      <td>DiancieMega Diancie</td>
      <td>Rock</td>
      <td>Fairy</td>
      <td>700</td>
      <td>50</td>
      <td>160</td>
      <td>110</td>
      <td>160</td>
      <td>110</td>
      <td>110</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>797</th>
      <td>720</td>
      <td>HoopaHoopa Confined</td>
      <td>Psychic</td>
      <td>Ghost</td>
      <td>600</td>
      <td>80</td>
      <td>110</td>
      <td>60</td>
      <td>150</td>
      <td>130</td>
      <td>70</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>798</th>
      <td>720</td>
      <td>HoopaHoopa Unbound</td>
      <td>Psychic</td>
      <td>Dark</td>
      <td>680</td>
      <td>80</td>
      <td>160</td>
      <td>60</td>
      <td>170</td>
      <td>130</td>
      <td>80</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>799</th>
      <td>721</td>
      <td>Volcanion</td>
      <td>Fire</td>
      <td>Water</td>
      <td>600</td>
      <td>80</td>
      <td>110</td>
      <td>120</td>
      <td>130</td>
      <td>90</td>
      <td>70</td>
      <td>6</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
<p>800 rows × 13 columns</p>
</div>



```python
df_poke.head(10)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>318</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>405</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>525</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>625</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>309</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Charmeleon</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>405</td>
      <td>58</td>
      <td>64</td>
      <td>58</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Charizard</td>
      <td>Fire</td>
      <td>Flying</td>
      <td>534</td>
      <td>78</td>
      <td>84</td>
      <td>78</td>
      <td>109</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>7</th>
      <td>6</td>
      <td>CharizardMega Charizard X</td>
      <td>Fire</td>
      <td>Dragon</td>
      <td>634</td>
      <td>78</td>
      <td>130</td>
      <td>111</td>
      <td>130</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>8</th>
      <td>6</td>
      <td>CharizardMega Charizard Y</td>
      <td>Fire</td>
      <td>Flying</td>
      <td>634</td>
      <td>78</td>
      <td>104</td>
      <td>78</td>
      <td>159</td>
      <td>115</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7</td>
      <td>Squirtle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>314</td>
      <td>44</td>
      <td>48</td>
      <td>65</td>
      <td>50</td>
      <td>64</td>
      <td>43</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_poke.tail(10)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>790</th>
      <td>714</td>
      <td>Noibat</td>
      <td>Flying</td>
      <td>Dragon</td>
      <td>245</td>
      <td>40</td>
      <td>30</td>
      <td>35</td>
      <td>45</td>
      <td>40</td>
      <td>55</td>
      <td>6</td>
      <td>False</td>
    </tr>
    <tr>
      <th>791</th>
      <td>715</td>
      <td>Noivern</td>
      <td>Flying</td>
      <td>Dragon</td>
      <td>535</td>
      <td>85</td>
      <td>70</td>
      <td>80</td>
      <td>97</td>
      <td>80</td>
      <td>123</td>
      <td>6</td>
      <td>False</td>
    </tr>
    <tr>
      <th>792</th>
      <td>716</td>
      <td>Xerneas</td>
      <td>Fairy</td>
      <td>NaN</td>
      <td>680</td>
      <td>126</td>
      <td>131</td>
      <td>95</td>
      <td>131</td>
      <td>98</td>
      <td>99</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>793</th>
      <td>717</td>
      <td>Yveltal</td>
      <td>Dark</td>
      <td>Flying</td>
      <td>680</td>
      <td>126</td>
      <td>131</td>
      <td>95</td>
      <td>131</td>
      <td>98</td>
      <td>99</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>794</th>
      <td>718</td>
      <td>Zygarde50% Forme</td>
      <td>Dragon</td>
      <td>Ground</td>
      <td>600</td>
      <td>108</td>
      <td>100</td>
      <td>121</td>
      <td>81</td>
      <td>95</td>
      <td>95</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>795</th>
      <td>719</td>
      <td>Diancie</td>
      <td>Rock</td>
      <td>Fairy</td>
      <td>600</td>
      <td>50</td>
      <td>100</td>
      <td>150</td>
      <td>100</td>
      <td>150</td>
      <td>50</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>796</th>
      <td>719</td>
      <td>DiancieMega Diancie</td>
      <td>Rock</td>
      <td>Fairy</td>
      <td>700</td>
      <td>50</td>
      <td>160</td>
      <td>110</td>
      <td>160</td>
      <td>110</td>
      <td>110</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>797</th>
      <td>720</td>
      <td>HoopaHoopa Confined</td>
      <td>Psychic</td>
      <td>Ghost</td>
      <td>600</td>
      <td>80</td>
      <td>110</td>
      <td>60</td>
      <td>150</td>
      <td>130</td>
      <td>70</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>798</th>
      <td>720</td>
      <td>HoopaHoopa Unbound</td>
      <td>Psychic</td>
      <td>Dark</td>
      <td>680</td>
      <td>80</td>
      <td>160</td>
      <td>60</td>
      <td>170</td>
      <td>130</td>
      <td>80</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>799</th>
      <td>721</td>
      <td>Volcanion</td>
      <td>Fire</td>
      <td>Water</td>
      <td>600</td>
      <td>80</td>
      <td>110</td>
      <td>120</td>
      <td>130</td>
      <td>90</td>
      <td>70</td>
      <td>6</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
num_rows = df_poke.shape[0]
num_cols = df_poke.shape[1]
```


```python
print(f"Number of rows: {num_rows}")
print(f"Number of columns: {num_cols}")
```

    Number of rows: 800
    Number of columns: 13



```python
for columns in df_poke.columns:
    print(columns)
```

    #
    Name
    Type 1
    Type 2
    Total
    HP
    Attack
    Defense
    Sp. Atk
    Sp. Def
    Speed
    Generation
    Legendary



```python
df_poke.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 800 entries, 0 to 799
    Data columns (total 13 columns):
     #   Column      Non-Null Count  Dtype 
    ---  ------      --------------  ----- 
     0   #           800 non-null    int64 
     1   Name        800 non-null    object
     2   Type 1      800 non-null    object
     3   Type 2      414 non-null    object
     4   Total       800 non-null    int64 
     5   HP          800 non-null    int64 
     6   Attack      800 non-null    int64 
     7   Defense     800 non-null    int64 
     8   Sp. Atk     800 non-null    int64 
     9   Sp. Def     800 non-null    int64 
     10  Speed       800 non-null    int64 
     11  Generation  800 non-null    int64 
     12  Legendary   800 non-null    bool  
    dtypes: bool(1), int64(9), object(3)
    memory usage: 75.9+ KB


### The 20 highest Pokemon Attack


```python
df_hpd = df_poke[['Name', 'Attack' ]].head(20)
df_hpd.sort_values('Attack', ascending=False, inplace=True)

df_top_highest_attack_pokemon = df_hpd.rename(columns={'Name':'Pokemon_Name',})

df_top_highest_attack_pokemon
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
      <th>Pokemon_Name</th>
      <th>Attack</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>19</th>
      <td>BeedrillMega Beedrill</td>
      <td>150</td>
    </tr>
    <tr>
      <th>7</th>
      <td>CharizardMega Charizard X</td>
      <td>130</td>
    </tr>
    <tr>
      <th>8</th>
      <td>CharizardMega Charizard Y</td>
      <td>104</td>
    </tr>
    <tr>
      <th>12</th>
      <td>BlastoiseMega Blastoise</td>
      <td>103</td>
    </tr>
    <tr>
      <th>3</th>
      <td>VenusaurMega Venusaur</td>
      <td>100</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Beedrill</td>
      <td>90</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Charizard</td>
      <td>84</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Blastoise</td>
      <td>83</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Venusaur</td>
      <td>82</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Charmeleon</td>
      <td>64</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Wartortle</td>
      <td>63</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ivysaur</td>
      <td>62</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Charmander</td>
      <td>52</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Bulbasaur</td>
      <td>49</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Squirtle</td>
      <td>48</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Butterfree</td>
      <td>45</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Weedle</td>
      <td>35</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Caterpie</td>
      <td>30</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Kakuna</td>
      <td>25</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Metapod</td>
      <td>20</td>
    </tr>
  </tbody>
</table>
</div>


fig = px.bar(df_top_highest_attack_pokemon
    , 
    x='Pokemon_Name', 
    y='Attack',
    color = 'Pokemon_Name',
    title='The 20 highest Pokemon Attack',
    text = 'Attack',
    width = 900,
    height = 600
)
fig.show()
### The 20 highest Pokemon Defense


```python
df_hpd = df_poke[['Name', 'Defense','Sp. Atk','Sp. Def' ]].head(20)
df_hpd.sort_values('Defense', ascending=False, inplace=True)

df_top_Defense = df_hpd.rename(columns={'Name':'Pokemon_Name',})

df_top_Defense
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
      <th>Pokemon_Name</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>VenusaurMega Venusaur</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
    </tr>
    <tr>
      <th>12</th>
      <td>BlastoiseMega Blastoise</td>
      <td>120</td>
      <td>135</td>
      <td>115</td>
    </tr>
    <tr>
      <th>7</th>
      <td>CharizardMega Charizard X</td>
      <td>111</td>
      <td>130</td>
      <td>85</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Blastoise</td>
      <td>100</td>
      <td>85</td>
      <td>105</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Venusaur</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Wartortle</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Charizard</td>
      <td>78</td>
      <td>109</td>
      <td>85</td>
    </tr>
    <tr>
      <th>8</th>
      <td>CharizardMega Charizard Y</td>
      <td>78</td>
      <td>159</td>
      <td>115</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Squirtle</td>
      <td>65</td>
      <td>50</td>
      <td>64</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ivysaur</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Charmeleon</td>
      <td>58</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Metapod</td>
      <td>55</td>
      <td>25</td>
      <td>25</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Kakuna</td>
      <td>50</td>
      <td>25</td>
      <td>25</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Butterfree</td>
      <td>50</td>
      <td>90</td>
      <td>80</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Bulbasaur</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Charmander</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Beedrill</td>
      <td>40</td>
      <td>45</td>
      <td>80</td>
    </tr>
    <tr>
      <th>19</th>
      <td>BeedrillMega Beedrill</td>
      <td>40</td>
      <td>15</td>
      <td>80</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Caterpie</td>
      <td>35</td>
      <td>20</td>
      <td>20</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Weedle</td>
      <td>30</td>
      <td>20</td>
      <td>20</td>
    </tr>
  </tbody>
</table>
</div>




```python
fig = px.bar(df_top_Defense
    , 
    x='Pokemon_Name', 
    y='Defense',
    color = 'Pokemon_Name',
    title='The 20 highest Pokemon Defense',
    text = 'Defense',
    width = 900,
    height = 600
)
fig.show()

```

    /opt/anaconda3/lib/python3.12/site-packages/plotly/express/_core.py:1979: FutureWarning:
    
    When grouping with a length-1 list-like, you will need to pass a length-1 tuple to get_group in a future version of pandas. Pass `(name,)` instead of `name` to silence this warning.
    



<div>                            <div id="8ee17153-395d-42ee-b1d9-27b185d0032e" class="plotly-graph-div" style="height:600px; width:900px;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("8ee17153-395d-42ee-b1d9-27b185d0032e")) {                    Plotly.newPlot(                        "8ee17153-395d-42ee-b1d9-27b185d0032e",                        [{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"VenusaurMega Venusaur","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"VenusaurMega Venusaur","offsetgroup":"VenusaurMega Venusaur","orientation":"v","showlegend":true,"text":[123.0],"textposition":"auto","x":["VenusaurMega Venusaur"],"xaxis":"x","y":[123],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"BlastoiseMega Blastoise","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"BlastoiseMega Blastoise","offsetgroup":"BlastoiseMega Blastoise","orientation":"v","showlegend":true,"text":[120.0],"textposition":"auto","x":["BlastoiseMega Blastoise"],"xaxis":"x","y":[120],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"CharizardMega Charizard X","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"CharizardMega Charizard X","offsetgroup":"CharizardMega Charizard X","orientation":"v","showlegend":true,"text":[111.0],"textposition":"auto","x":["CharizardMega Charizard X"],"xaxis":"x","y":[111],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"Blastoise","marker":{"color":"#ab63fa","pattern":{"shape":""}},"name":"Blastoise","offsetgroup":"Blastoise","orientation":"v","showlegend":true,"text":[100.0],"textposition":"auto","x":["Blastoise"],"xaxis":"x","y":[100],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"Venusaur","marker":{"color":"#FFA15A","pattern":{"shape":""}},"name":"Venusaur","offsetgroup":"Venusaur","orientation":"v","showlegend":true,"text":[83.0],"textposition":"auto","x":["Venusaur"],"xaxis":"x","y":[83],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"Wartortle","marker":{"color":"#19d3f3","pattern":{"shape":""}},"name":"Wartortle","offsetgroup":"Wartortle","orientation":"v","showlegend":true,"text":[80.0],"textposition":"auto","x":["Wartortle"],"xaxis":"x","y":[80],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"Charizard","marker":{"color":"#FF6692","pattern":{"shape":""}},"name":"Charizard","offsetgroup":"Charizard","orientation":"v","showlegend":true,"text":[78.0],"textposition":"auto","x":["Charizard"],"xaxis":"x","y":[78],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"CharizardMega Charizard Y","marker":{"color":"#B6E880","pattern":{"shape":""}},"name":"CharizardMega Charizard Y","offsetgroup":"CharizardMega Charizard Y","orientation":"v","showlegend":true,"text":[78.0],"textposition":"auto","x":["CharizardMega Charizard Y"],"xaxis":"x","y":[78],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"Squirtle","marker":{"color":"#FF97FF","pattern":{"shape":""}},"name":"Squirtle","offsetgroup":"Squirtle","orientation":"v","showlegend":true,"text":[65.0],"textposition":"auto","x":["Squirtle"],"xaxis":"x","y":[65],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"Ivysaur","marker":{"color":"#FECB52","pattern":{"shape":""}},"name":"Ivysaur","offsetgroup":"Ivysaur","orientation":"v","showlegend":true,"text":[63.0],"textposition":"auto","x":["Ivysaur"],"xaxis":"x","y":[63],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"Charmeleon","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"Charmeleon","offsetgroup":"Charmeleon","orientation":"v","showlegend":true,"text":[58.0],"textposition":"auto","x":["Charmeleon"],"xaxis":"x","y":[58],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"Metapod","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"Metapod","offsetgroup":"Metapod","orientation":"v","showlegend":true,"text":[55.0],"textposition":"auto","x":["Metapod"],"xaxis":"x","y":[55],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"Kakuna","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"Kakuna","offsetgroup":"Kakuna","orientation":"v","showlegend":true,"text":[50.0],"textposition":"auto","x":["Kakuna"],"xaxis":"x","y":[50],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"Butterfree","marker":{"color":"#ab63fa","pattern":{"shape":""}},"name":"Butterfree","offsetgroup":"Butterfree","orientation":"v","showlegend":true,"text":[50.0],"textposition":"auto","x":["Butterfree"],"xaxis":"x","y":[50],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"Bulbasaur","marker":{"color":"#FFA15A","pattern":{"shape":""}},"name":"Bulbasaur","offsetgroup":"Bulbasaur","orientation":"v","showlegend":true,"text":[49.0],"textposition":"auto","x":["Bulbasaur"],"xaxis":"x","y":[49],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"Charmander","marker":{"color":"#19d3f3","pattern":{"shape":""}},"name":"Charmander","offsetgroup":"Charmander","orientation":"v","showlegend":true,"text":[43.0],"textposition":"auto","x":["Charmander"],"xaxis":"x","y":[43],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"Beedrill","marker":{"color":"#FF6692","pattern":{"shape":""}},"name":"Beedrill","offsetgroup":"Beedrill","orientation":"v","showlegend":true,"text":[40.0],"textposition":"auto","x":["Beedrill"],"xaxis":"x","y":[40],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"BeedrillMega Beedrill","marker":{"color":"#B6E880","pattern":{"shape":""}},"name":"BeedrillMega Beedrill","offsetgroup":"BeedrillMega Beedrill","orientation":"v","showlegend":true,"text":[40.0],"textposition":"auto","x":["BeedrillMega Beedrill"],"xaxis":"x","y":[40],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"Caterpie","marker":{"color":"#FF97FF","pattern":{"shape":""}},"name":"Caterpie","offsetgroup":"Caterpie","orientation":"v","showlegend":true,"text":[35.0],"textposition":"auto","x":["Caterpie"],"xaxis":"x","y":[35],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Defense=%{text}<extra></extra>","legendgroup":"Weedle","marker":{"color":"#FECB52","pattern":{"shape":""}},"name":"Weedle","offsetgroup":"Weedle","orientation":"v","showlegend":true,"text":[30.0],"textposition":"auto","x":["Weedle"],"xaxis":"x","y":[30],"yaxis":"y","type":"bar"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"xaxis":{"anchor":"y","domain":[0.0,1.0],"title":{"text":"Pokemon_Name"},"categoryorder":"array","categoryarray":["VenusaurMega Venusaur","BlastoiseMega Blastoise","CharizardMega Charizard X","Blastoise","Venusaur","Wartortle","Charizard","CharizardMega Charizard Y","Squirtle","Ivysaur","Charmeleon","Metapod","Kakuna","Butterfree","Bulbasaur","Charmander","Beedrill","BeedrillMega Beedrill","Caterpie","Weedle"]},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"Defense"}},"legend":{"title":{"text":"Pokemon_Name"},"tracegroupgap":0},"title":{"text":"The 20 highest Pokemon Defense"},"barmode":"relative","height":600,"width":900},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('8ee17153-395d-42ee-b1d9-27b185d0032e');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>


### Attack and Defense


```python
fig = px.scatter_3d(
    df_poke,
    title='Attack, Defense, Price 3D Scatter Plot',
    x="Attack",
    y="Defense",
    z="Total",
    color="Total",
    template='plotly_dark',
    width=800,
    height=600
)
fig.show()

```


<div>                            <div id="94689c34-6367-4ed1-8cad-6ebc43215b9a" class="plotly-graph-div" style="height:600px; width:800px;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("94689c34-6367-4ed1-8cad-6ebc43215b9a")) {                    Plotly.newPlot(                        "94689c34-6367-4ed1-8cad-6ebc43215b9a",                        [{"hovertemplate":"Attack=%{x}<br>Defense=%{y}<br>Total=%{marker.color}<extra></extra>","legendgroup":"","marker":{"color":[318,405,525,625,309,405,534,634,634,314,405,530,630,195,205,395,195,205,395,495,251,349,479,579,253,413,262,442,288,438,320,485,300,450,275,365,505,273,365,505,323,483,299,505,270,435,245,455,320,395,490,285,405,305,450,265,405,290,440,320,500,305,455,350,555,300,385,510,310,400,500,590,305,405,505,300,390,490,335,515,300,390,495,410,500,315,490,590,325,465,352,310,460,325,475,325,500,305,525,310,405,500,600,385,328,483,325,475,330,480,325,520,320,425,455,455,385,340,490,345,485,450,435,490,590,295,440,320,450,340,520,460,500,455,490,495,500,600,490,200,540,640,535,288,325,525,525,525,395,355,495,355,495,515,615,540,580,580,580,300,420,600,680,780,780,600,318,405,525,309,405,534,314,405,530,215,415,262,442,265,390,250,390,535,330,460,205,218,210,245,405,320,470,280,365,510,610,490,250,420,410,500,250,340,460,360,180,425,390,210,430,525,525,405,490,435,336,405,455,290,465,415,430,510,610,300,450,430,500,600,505,500,600,430,330,500,250,410,250,450,380,300,480,330,465,465,330,500,600,540,330,500,515,465,250,210,455,305,360,365,490,540,580,580,580,300,410,600,700,680,680,600,310,405,530,630,310,405,530,630,310,405,535,635,220,420,240,420,195,205,395,205,385,220,340,480,220,340,480,270,430,270,430,198,278,518,618,269,414,295,460,280,440,670,266,456,236,240,360,490,237,474,190,375,260,380,380,480,380,480,330,430,530,630,280,410,510,295,475,575,405,405,400,400,400,302,467,305,460,560,400,500,305,460,560,470,330,470,360,290,340,520,335,475,310,490,590,458,458,440,440,288,468,308,468,300,500,355,495,355,495,200,540,420,440,295,455,555,295,455,460,425,465,565,260,300,480,580,290,410,530,345,485,485,485,330,300,420,600,700,300,420,600,700,580,580,580,600,700,600,700,670,770,670,770,680,780,600,600,600,600,600,318,405,525,309,405,534,314,405,530,245,340,485,250,410,194,384,263,363,523,280,515,350,495,350,495,224,424,424,424,424,244,474,405,330,495,275,450,325,475,482,348,498,350,480,580,495,505,310,452,285,329,479,300,500,290,310,220,411,485,300,410,600,700,390,285,525,625,330,525,330,500,300,490,454,330,460,345,334,494,594,510,535,515,535,535,540,540,545,515,525,525,510,530,535,518,618,525,525,480,440,520,520,520,520,520,580,580,580,680,680,600,670,680,680,600,480,600,600,600,600,720,600,308,413,528,308,418,528,308,413,528,255,420,275,370,500,281,446,316,498,316,498,316,498,292,487,264,358,488,295,497,280,390,515,313,425,328,508,445,545,305,405,505,294,384,509,465,465,310,380,500,260,360,485,280,480,280,480,460,292,351,519,315,480,540,461,325,475,348,488,490,303,483,355,495,401,567,329,474,330,510,300,470,290,390,490,290,370,490,305,473,305,395,535,335,475,428,315,495,294,464,335,480,470,319,472,305,489,300,440,520,275,405,515,335,485,275,370,520,320,410,540,305,485,485,305,495,471,350,510,485,303,483,340,490,490,350,510,370,510,484,484,300,420,600,360,550,580,580,580,580,580,580,580,680,680,600,600,660,700,700,580,580,600,600,600,313,405,530,307,409,534,314,405,530,237,423,278,382,499,200,213,411,369,507,303,371,552,350,531,348,495,472,355,466,466,325,448,520,520,341,462,341,480,288,482,306,500,320,494,330,500,289,481,362,521,362,521,525,500,431,500,300,452,600,470,309,474,335,335,335,335,494,494,494,494,304,514,245,535,680,680,600,600,700,600,680,600],"coloraxis":"coloraxis","symbol":"circle"},"mode":"markers","name":"","scene":"scene","showlegend":false,"x":[49,62,82,100,52,64,84,130,104,48,63,83,103,30,20,45,35,25,90,150,45,60,80,80,56,81,60,90,60,85,55,90,75,100,47,62,92,57,72,102,45,70,41,76,45,70,45,80,50,65,80,70,95,55,65,55,80,45,70,52,82,80,105,70,110,50,65,95,20,35,50,50,80,100,130,75,90,105,40,70,80,95,120,85,100,65,75,75,35,60,65,85,110,45,70,80,105,65,95,35,50,65,65,45,48,73,105,130,30,50,40,95,50,80,120,105,55,65,90,85,130,5,55,95,125,40,65,67,92,45,75,45,110,50,83,95,125,155,100,10,125,155,85,48,55,65,65,130,60,40,60,80,115,105,135,110,85,90,100,64,84,134,110,190,150,100,49,62,82,52,64,84,65,80,105,46,76,30,50,20,35,60,90,90,38,58,40,25,30,20,40,50,75,40,55,75,95,80,20,50,100,75,35,45,55,70,30,75,65,45,85,65,65,85,75,60,72,33,80,65,90,70,75,85,125,80,120,95,130,150,10,125,185,95,80,130,40,50,50,100,55,65,105,55,40,80,60,90,90,95,60,120,80,95,20,35,95,30,63,75,80,10,85,115,75,64,84,134,164,90,130,100,45,65,85,110,60,85,120,160,70,85,110,150,55,90,30,70,45,35,70,35,50,30,50,70,40,70,100,55,85,30,50,25,35,65,85,30,60,40,130,60,80,160,45,90,90,51,71,91,60,120,20,45,45,65,75,85,85,105,70,90,110,140,40,60,100,45,75,75,50,40,73,47,60,43,73,90,120,140,70,90,60,100,120,85,25,45,60,100,70,100,85,115,40,70,110,115,100,55,95,48,78,80,120,40,70,41,81,95,125,15,60,70,90,75,115,165,40,70,68,50,130,150,23,50,80,120,40,60,80,64,104,84,90,30,75,95,135,145,55,75,135,145,100,50,75,80,100,90,130,100,150,150,180,150,180,100,150,180,70,95,68,89,109,58,78,104,51,66,86,55,75,120,45,85,25,85,65,85,120,30,70,125,165,42,52,29,59,79,69,94,30,80,45,65,105,35,60,48,83,100,50,80,66,76,136,60,125,55,82,30,63,93,24,89,80,25,5,65,92,70,90,130,170,85,70,110,145,72,112,50,90,61,106,100,49,69,20,62,92,132,120,70,85,140,100,123,95,50,76,110,60,95,130,80,125,165,55,100,80,50,65,65,65,65,65,75,105,125,120,120,90,160,100,120,70,80,100,90,100,103,120,100,45,60,75,63,93,123,55,75,100,55,85,60,80,110,50,88,53,98,53,98,53,98,25,55,55,77,115,60,100,75,105,135,45,57,85,135,60,60,80,105,140,50,65,95,100,125,53,63,103,45,55,100,27,67,35,60,92,72,82,117,90,140,30,86,65,95,75,90,58,30,50,78,108,112,140,50,95,65,105,50,95,30,45,55,30,40,65,44,87,50,65,95,60,100,75,75,135,55,85,40,60,75,47,77,50,94,55,80,100,55,85,115,55,75,30,40,55,87,117,147,70,110,50,40,70,66,85,125,120,74,124,85,125,110,83,123,55,65,97,109,65,85,105,85,60,90,129,90,115,100,115,105,120,150,125,145,130,170,120,72,72,77,128,120,61,78,107,45,59,69,56,63,95,36,56,50,73,81,35,22,52,50,68,38,45,65,65,100,82,124,80,48,48,48,80,110,150,50,52,72,48,80,54,92,52,105,60,75,53,73,38,55,89,121,59,77,65,92,58,50,50,75,100,80,70,110,66,66,66,66,90,85,95,100,69,117,30,70,131,131,100,100,160,110,160,110],"y":[49,63,83,123,43,58,78,111,78,65,80,100,120,35,55,50,30,50,40,40,40,55,75,80,35,60,30,65,44,69,40,55,85,110,52,67,87,40,57,77,48,73,40,75,20,45,35,70,55,70,85,55,80,50,60,25,50,35,60,48,78,35,60,45,80,40,65,95,15,30,45,65,50,70,80,35,50,65,35,65,100,115,130,55,70,65,110,180,70,95,55,45,70,55,80,50,75,100,180,30,45,60,80,160,45,70,90,115,50,70,80,85,95,110,53,79,75,95,120,95,120,5,115,80,100,70,95,60,65,55,85,65,80,35,57,57,100,120,95,55,79,109,80,48,50,60,60,60,70,100,125,90,105,65,85,65,100,85,90,45,65,95,90,100,70,100,65,80,100,43,58,78,64,80,100,34,64,30,50,30,50,40,70,80,38,58,15,28,15,65,85,45,70,40,55,85,105,95,50,80,115,75,40,50,70,55,30,55,45,45,85,60,110,42,80,60,48,58,65,90,140,70,105,200,230,50,75,75,100,140,230,75,115,55,50,75,40,120,40,80,85,35,75,45,70,140,30,50,90,95,60,120,90,62,35,35,95,15,37,37,105,10,75,85,115,50,70,110,150,130,90,100,35,45,65,75,40,60,70,80,50,70,90,110,35,70,41,61,35,55,50,55,70,30,50,70,50,40,60,30,60,30,100,25,35,65,65,32,62,60,80,60,80,100,90,45,45,23,43,63,30,60,40,135,45,65,75,125,85,125,100,140,180,230,55,75,85,40,60,80,40,50,55,55,45,53,83,20,40,70,35,45,40,70,100,140,35,65,60,45,50,80,40,60,60,90,110,60,60,65,85,43,73,65,85,55,105,77,97,50,100,20,79,70,70,35,65,75,90,130,83,70,60,60,48,50,80,80,50,70,90,85,105,105,130,55,60,100,80,130,80,100,130,150,200,100,150,90,120,80,100,90,90,140,160,90,100,100,50,20,160,90,64,85,105,44,52,71,53,68,88,30,50,70,40,60,41,51,34,49,79,35,65,40,60,118,168,45,85,105,95,50,42,102,70,35,55,45,70,48,68,66,34,44,44,84,94,60,52,42,64,50,47,67,86,116,95,45,5,45,108,45,65,95,115,40,40,70,88,78,118,90,110,40,65,72,56,76,50,50,75,105,65,115,95,130,125,67,67,95,86,130,110,125,80,70,65,95,145,135,70,77,107,107,107,107,107,130,105,70,120,100,106,110,120,100,120,80,100,90,100,75,120,100,55,75,95,45,55,65,45,60,85,39,69,45,65,90,37,50,48,63,48,63,48,63,45,85,50,62,80,32,63,85,105,130,43,55,40,60,86,126,55,85,95,40,55,75,85,75,70,90,80,59,99,89,60,85,50,75,65,35,45,80,45,55,105,67,85,125,70,115,80,85,145,103,133,45,65,62,82,40,60,40,60,50,70,95,40,50,75,50,63,50,65,85,50,70,60,45,105,45,70,50,70,80,50,60,91,131,70,95,115,40,70,80,55,75,55,60,90,60,70,90,40,80,30,85,40,84,50,60,90,50,80,70,100,95,50,75,75,105,66,112,50,70,90,55,65,129,90,72,70,80,70,70,100,120,90,90,90,100,90,90,90,77,90,95,65,95,122,40,58,72,40,52,67,38,77,43,55,71,40,60,50,58,72,39,47,68,48,62,62,78,60,54,76,76,100,150,50,150,60,72,66,86,53,88,67,115,60,90,62,88,33,52,77,119,50,72,65,75,57,150,35,53,70,91,48,76,70,70,70,70,122,122,122,122,85,184,35,80,95,95,121,150,110,60,60,120],"z":[318,405,525,625,309,405,534,634,634,314,405,530,630,195,205,395,195,205,395,495,251,349,479,579,253,413,262,442,288,438,320,485,300,450,275,365,505,273,365,505,323,483,299,505,270,435,245,455,320,395,490,285,405,305,450,265,405,290,440,320,500,305,455,350,555,300,385,510,310,400,500,590,305,405,505,300,390,490,335,515,300,390,495,410,500,315,490,590,325,465,352,310,460,325,475,325,500,305,525,310,405,500,600,385,328,483,325,475,330,480,325,520,320,425,455,455,385,340,490,345,485,450,435,490,590,295,440,320,450,340,520,460,500,455,490,495,500,600,490,200,540,640,535,288,325,525,525,525,395,355,495,355,495,515,615,540,580,580,580,300,420,600,680,780,780,600,318,405,525,309,405,534,314,405,530,215,415,262,442,265,390,250,390,535,330,460,205,218,210,245,405,320,470,280,365,510,610,490,250,420,410,500,250,340,460,360,180,425,390,210,430,525,525,405,490,435,336,405,455,290,465,415,430,510,610,300,450,430,500,600,505,500,600,430,330,500,250,410,250,450,380,300,480,330,465,465,330,500,600,540,330,500,515,465,250,210,455,305,360,365,490,540,580,580,580,300,410,600,700,680,680,600,310,405,530,630,310,405,530,630,310,405,535,635,220,420,240,420,195,205,395,205,385,220,340,480,220,340,480,270,430,270,430,198,278,518,618,269,414,295,460,280,440,670,266,456,236,240,360,490,237,474,190,375,260,380,380,480,380,480,330,430,530,630,280,410,510,295,475,575,405,405,400,400,400,302,467,305,460,560,400,500,305,460,560,470,330,470,360,290,340,520,335,475,310,490,590,458,458,440,440,288,468,308,468,300,500,355,495,355,495,200,540,420,440,295,455,555,295,455,460,425,465,565,260,300,480,580,290,410,530,345,485,485,485,330,300,420,600,700,300,420,600,700,580,580,580,600,700,600,700,670,770,670,770,680,780,600,600,600,600,600,318,405,525,309,405,534,314,405,530,245,340,485,250,410,194,384,263,363,523,280,515,350,495,350,495,224,424,424,424,424,244,474,405,330,495,275,450,325,475,482,348,498,350,480,580,495,505,310,452,285,329,479,300,500,290,310,220,411,485,300,410,600,700,390,285,525,625,330,525,330,500,300,490,454,330,460,345,334,494,594,510,535,515,535,535,540,540,545,515,525,525,510,530,535,518,618,525,525,480,440,520,520,520,520,520,580,580,580,680,680,600,670,680,680,600,480,600,600,600,600,720,600,308,413,528,308,418,528,308,413,528,255,420,275,370,500,281,446,316,498,316,498,316,498,292,487,264,358,488,295,497,280,390,515,313,425,328,508,445,545,305,405,505,294,384,509,465,465,310,380,500,260,360,485,280,480,280,480,460,292,351,519,315,480,540,461,325,475,348,488,490,303,483,355,495,401,567,329,474,330,510,300,470,290,390,490,290,370,490,305,473,305,395,535,335,475,428,315,495,294,464,335,480,470,319,472,305,489,300,440,520,275,405,515,335,485,275,370,520,320,410,540,305,485,485,305,495,471,350,510,485,303,483,340,490,490,350,510,370,510,484,484,300,420,600,360,550,580,580,580,580,580,580,580,680,680,600,600,660,700,700,580,580,600,600,600,313,405,530,307,409,534,314,405,530,237,423,278,382,499,200,213,411,369,507,303,371,552,350,531,348,495,472,355,466,466,325,448,520,520,341,462,341,480,288,482,306,500,320,494,330,500,289,481,362,521,362,521,525,500,431,500,300,452,600,470,309,474,335,335,335,335,494,494,494,494,304,514,245,535,680,680,600,600,700,600,680,600],"type":"scatter3d"}],                        {"template":{"data":{"barpolar":[{"marker":{"line":{"color":"rgb(17,17,17)","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"bar":[{"error_x":{"color":"#f2f5fa"},"error_y":{"color":"#f2f5fa"},"marker":{"line":{"color":"rgb(17,17,17)","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"carpet":[{"aaxis":{"endlinecolor":"#A2B1C6","gridcolor":"#506784","linecolor":"#506784","minorgridcolor":"#506784","startlinecolor":"#A2B1C6"},"baxis":{"endlinecolor":"#A2B1C6","gridcolor":"#506784","linecolor":"#506784","minorgridcolor":"#506784","startlinecolor":"#A2B1C6"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"contour"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"heatmapgl"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"heatmap"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"histogram2dcontour"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"histogram2d"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"line":{"color":"#283442"}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatter":[{"marker":{"line":{"color":"#283442"}},"type":"scatter"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#506784"},"line":{"color":"rgb(17,17,17)"}},"header":{"fill":{"color":"#2a3f5f"},"line":{"color":"rgb(17,17,17)"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#f2f5fa","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#f2f5fa"},"geo":{"bgcolor":"rgb(17,17,17)","lakecolor":"rgb(17,17,17)","landcolor":"rgb(17,17,17)","showlakes":true,"showland":true,"subunitcolor":"#506784"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"dark"},"paper_bgcolor":"rgb(17,17,17)","plot_bgcolor":"rgb(17,17,17)","polar":{"angularaxis":{"gridcolor":"#506784","linecolor":"#506784","ticks":""},"bgcolor":"rgb(17,17,17)","radialaxis":{"gridcolor":"#506784","linecolor":"#506784","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"rgb(17,17,17)","gridcolor":"#506784","gridwidth":2,"linecolor":"#506784","showbackground":true,"ticks":"","zerolinecolor":"#C8D4E3"},"yaxis":{"backgroundcolor":"rgb(17,17,17)","gridcolor":"#506784","gridwidth":2,"linecolor":"#506784","showbackground":true,"ticks":"","zerolinecolor":"#C8D4E3"},"zaxis":{"backgroundcolor":"rgb(17,17,17)","gridcolor":"#506784","gridwidth":2,"linecolor":"#506784","showbackground":true,"ticks":"","zerolinecolor":"#C8D4E3"}},"shapedefaults":{"line":{"color":"#f2f5fa"}},"sliderdefaults":{"bgcolor":"#C8D4E3","bordercolor":"rgb(17,17,17)","borderwidth":1,"tickwidth":0},"ternary":{"aaxis":{"gridcolor":"#506784","linecolor":"#506784","ticks":""},"baxis":{"gridcolor":"#506784","linecolor":"#506784","ticks":""},"bgcolor":"rgb(17,17,17)","caxis":{"gridcolor":"#506784","linecolor":"#506784","ticks":""}},"title":{"x":0.05},"updatemenudefaults":{"bgcolor":"#506784","borderwidth":0},"xaxis":{"automargin":true,"gridcolor":"#283442","linecolor":"#506784","ticks":"","title":{"standoff":15},"zerolinecolor":"#283442","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"#283442","linecolor":"#506784","ticks":"","title":{"standoff":15},"zerolinecolor":"#283442","zerolinewidth":2}}},"scene":{"domain":{"x":[0.0,1.0],"y":[0.0,1.0]},"xaxis":{"title":{"text":"Attack"}},"yaxis":{"title":{"text":"Defense"}},"zaxis":{"title":{"text":"Total"}}},"coloraxis":{"colorbar":{"title":{"text":"Total"}},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]},"legend":{"tracegroupgap":0},"title":{"text":"Attack, Defense, Price 3D Scatter Plot"},"height":600,"width":800},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('94689c34-6367-4ed1-8cad-6ebc43215b9a');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>


### 20 Fastest Pokemon


```python
df_sa = df_poke[['Name', 'Speed' ]].head(20)
df_sa.sort_values('Speed', ascending=False, inplace=True)

df_speed = df_sa.rename(columns={'Name':'Pokemon_Name',})

df_speed
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
      <th>Pokemon_Name</th>
      <th>Speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>19</th>
      <td>BeedrillMega Beedrill</td>
      <td>145</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Charizard</td>
      <td>100</td>
    </tr>
    <tr>
      <th>7</th>
      <td>CharizardMega Charizard X</td>
      <td>100</td>
    </tr>
    <tr>
      <th>8</th>
      <td>CharizardMega Charizard Y</td>
      <td>100</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Venusaur</td>
      <td>80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>VenusaurMega Venusaur</td>
      <td>80</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Charmeleon</td>
      <td>80</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Blastoise</td>
      <td>78</td>
    </tr>
    <tr>
      <th>12</th>
      <td>BlastoiseMega Blastoise</td>
      <td>78</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Beedrill</td>
      <td>75</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Butterfree</td>
      <td>70</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Charmander</td>
      <td>65</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ivysaur</td>
      <td>60</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Wartortle</td>
      <td>58</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Weedle</td>
      <td>50</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Caterpie</td>
      <td>45</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Bulbasaur</td>
      <td>45</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Squirtle</td>
      <td>43</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Kakuna</td>
      <td>35</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Metapod</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
</div>




```python
fig = px.bar(df_speed
    , 
    x='Pokemon_Name', 
    y='Speed',
    color = 'Pokemon_Name',
    title='The 20 Fastest Pokemon',
    text = 'Speed',
    width = 900,
    height = 600
)
fig.show()
```

    /opt/anaconda3/lib/python3.12/site-packages/plotly/express/_core.py:1979: FutureWarning:
    
    When grouping with a length-1 list-like, you will need to pass a length-1 tuple to get_group in a future version of pandas. Pass `(name,)` instead of `name` to silence this warning.
    



<div>                            <div id="fd06e10e-3b13-4f19-bfa3-6fbb4ecf3ced" class="plotly-graph-div" style="height:600px; width:900px;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("fd06e10e-3b13-4f19-bfa3-6fbb4ecf3ced")) {                    Plotly.newPlot(                        "fd06e10e-3b13-4f19-bfa3-6fbb4ecf3ced",                        [{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"BeedrillMega Beedrill","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"BeedrillMega Beedrill","offsetgroup":"BeedrillMega Beedrill","orientation":"v","showlegend":true,"text":[145.0],"textposition":"auto","x":["BeedrillMega Beedrill"],"xaxis":"x","y":[145],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"Charizard","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"Charizard","offsetgroup":"Charizard","orientation":"v","showlegend":true,"text":[100.0],"textposition":"auto","x":["Charizard"],"xaxis":"x","y":[100],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"CharizardMega Charizard X","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"CharizardMega Charizard X","offsetgroup":"CharizardMega Charizard X","orientation":"v","showlegend":true,"text":[100.0],"textposition":"auto","x":["CharizardMega Charizard X"],"xaxis":"x","y":[100],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"CharizardMega Charizard Y","marker":{"color":"#ab63fa","pattern":{"shape":""}},"name":"CharizardMega Charizard Y","offsetgroup":"CharizardMega Charizard Y","orientation":"v","showlegend":true,"text":[100.0],"textposition":"auto","x":["CharizardMega Charizard Y"],"xaxis":"x","y":[100],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"Venusaur","marker":{"color":"#FFA15A","pattern":{"shape":""}},"name":"Venusaur","offsetgroup":"Venusaur","orientation":"v","showlegend":true,"text":[80.0],"textposition":"auto","x":["Venusaur"],"xaxis":"x","y":[80],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"VenusaurMega Venusaur","marker":{"color":"#19d3f3","pattern":{"shape":""}},"name":"VenusaurMega Venusaur","offsetgroup":"VenusaurMega Venusaur","orientation":"v","showlegend":true,"text":[80.0],"textposition":"auto","x":["VenusaurMega Venusaur"],"xaxis":"x","y":[80],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"Charmeleon","marker":{"color":"#FF6692","pattern":{"shape":""}},"name":"Charmeleon","offsetgroup":"Charmeleon","orientation":"v","showlegend":true,"text":[80.0],"textposition":"auto","x":["Charmeleon"],"xaxis":"x","y":[80],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"Blastoise","marker":{"color":"#B6E880","pattern":{"shape":""}},"name":"Blastoise","offsetgroup":"Blastoise","orientation":"v","showlegend":true,"text":[78.0],"textposition":"auto","x":["Blastoise"],"xaxis":"x","y":[78],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"BlastoiseMega Blastoise","marker":{"color":"#FF97FF","pattern":{"shape":""}},"name":"BlastoiseMega Blastoise","offsetgroup":"BlastoiseMega Blastoise","orientation":"v","showlegend":true,"text":[78.0],"textposition":"auto","x":["BlastoiseMega Blastoise"],"xaxis":"x","y":[78],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"Beedrill","marker":{"color":"#FECB52","pattern":{"shape":""}},"name":"Beedrill","offsetgroup":"Beedrill","orientation":"v","showlegend":true,"text":[75.0],"textposition":"auto","x":["Beedrill"],"xaxis":"x","y":[75],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"Butterfree","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"Butterfree","offsetgroup":"Butterfree","orientation":"v","showlegend":true,"text":[70.0],"textposition":"auto","x":["Butterfree"],"xaxis":"x","y":[70],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"Charmander","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"Charmander","offsetgroup":"Charmander","orientation":"v","showlegend":true,"text":[65.0],"textposition":"auto","x":["Charmander"],"xaxis":"x","y":[65],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"Ivysaur","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"Ivysaur","offsetgroup":"Ivysaur","orientation":"v","showlegend":true,"text":[60.0],"textposition":"auto","x":["Ivysaur"],"xaxis":"x","y":[60],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"Wartortle","marker":{"color":"#ab63fa","pattern":{"shape":""}},"name":"Wartortle","offsetgroup":"Wartortle","orientation":"v","showlegend":true,"text":[58.0],"textposition":"auto","x":["Wartortle"],"xaxis":"x","y":[58],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"Weedle","marker":{"color":"#FFA15A","pattern":{"shape":""}},"name":"Weedle","offsetgroup":"Weedle","orientation":"v","showlegend":true,"text":[50.0],"textposition":"auto","x":["Weedle"],"xaxis":"x","y":[50],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"Caterpie","marker":{"color":"#19d3f3","pattern":{"shape":""}},"name":"Caterpie","offsetgroup":"Caterpie","orientation":"v","showlegend":true,"text":[45.0],"textposition":"auto","x":["Caterpie"],"xaxis":"x","y":[45],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"Bulbasaur","marker":{"color":"#FF6692","pattern":{"shape":""}},"name":"Bulbasaur","offsetgroup":"Bulbasaur","orientation":"v","showlegend":true,"text":[45.0],"textposition":"auto","x":["Bulbasaur"],"xaxis":"x","y":[45],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"Squirtle","marker":{"color":"#B6E880","pattern":{"shape":""}},"name":"Squirtle","offsetgroup":"Squirtle","orientation":"v","showlegend":true,"text":[43.0],"textposition":"auto","x":["Squirtle"],"xaxis":"x","y":[43],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"Kakuna","marker":{"color":"#FF97FF","pattern":{"shape":""}},"name":"Kakuna","offsetgroup":"Kakuna","orientation":"v","showlegend":true,"text":[35.0],"textposition":"auto","x":["Kakuna"],"xaxis":"x","y":[35],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Speed=%{text}<extra></extra>","legendgroup":"Metapod","marker":{"color":"#FECB52","pattern":{"shape":""}},"name":"Metapod","offsetgroup":"Metapod","orientation":"v","showlegend":true,"text":[30.0],"textposition":"auto","x":["Metapod"],"xaxis":"x","y":[30],"yaxis":"y","type":"bar"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"xaxis":{"anchor":"y","domain":[0.0,1.0],"title":{"text":"Pokemon_Name"},"categoryorder":"array","categoryarray":["BeedrillMega Beedrill","Charizard","CharizardMega Charizard X","CharizardMega Charizard Y","Venusaur","VenusaurMega Venusaur","Charmeleon","Blastoise","BlastoiseMega Blastoise","Beedrill","Butterfree","Charmander","Ivysaur","Wartortle","Weedle","Caterpie","Bulbasaur","Squirtle","Kakuna","Metapod"]},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"Speed"}},"legend":{"title":{"text":"Pokemon_Name"},"tracegroupgap":0},"title":{"text":"The 20 Fastest Pokemon"},"barmode":"relative","height":600,"width":900},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('fd06e10e-3b13-4f19-bfa3-6fbb4ecf3ced');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>


### Speed Attack vs Speed Defense


```python
fig = px.scatter_3d(
    df_poke,
    title='Speed Attack, Speed Attack, Price 3D Scatter Plot',
    x="Sp. Atk",
    y="Sp. Def",
    z="Total",
    color="Total",
    template='plotly_dark',
    width=800,
    height=600
)
fig.show()

```


<div>                            <div id="d8c26a16-900c-451a-82d1-07471ea9141b" class="plotly-graph-div" style="height:600px; width:800px;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("d8c26a16-900c-451a-82d1-07471ea9141b")) {                    Plotly.newPlot(                        "d8c26a16-900c-451a-82d1-07471ea9141b",                        [{"hovertemplate":"Sp. Atk=%{x}<br>Sp. Def=%{y}<br>Total=%{marker.color}<extra></extra>","legendgroup":"","marker":{"color":[318,405,525,625,309,405,534,634,634,314,405,530,630,195,205,395,195,205,395,495,251,349,479,579,253,413,262,442,288,438,320,485,300,450,275,365,505,273,365,505,323,483,299,505,270,435,245,455,320,395,490,285,405,305,450,265,405,290,440,320,500,305,455,350,555,300,385,510,310,400,500,590,305,405,505,300,390,490,335,515,300,390,495,410,500,315,490,590,325,465,352,310,460,325,475,325,500,305,525,310,405,500,600,385,328,483,325,475,330,480,325,520,320,425,455,455,385,340,490,345,485,450,435,490,590,295,440,320,450,340,520,460,500,455,490,495,500,600,490,200,540,640,535,288,325,525,525,525,395,355,495,355,495,515,615,540,580,580,580,300,420,600,680,780,780,600,318,405,525,309,405,534,314,405,530,215,415,262,442,265,390,250,390,535,330,460,205,218,210,245,405,320,470,280,365,510,610,490,250,420,410,500,250,340,460,360,180,425,390,210,430,525,525,405,490,435,336,405,455,290,465,415,430,510,610,300,450,430,500,600,505,500,600,430,330,500,250,410,250,450,380,300,480,330,465,465,330,500,600,540,330,500,515,465,250,210,455,305,360,365,490,540,580,580,580,300,410,600,700,680,680,600,310,405,530,630,310,405,530,630,310,405,535,635,220,420,240,420,195,205,395,205,385,220,340,480,220,340,480,270,430,270,430,198,278,518,618,269,414,295,460,280,440,670,266,456,236,240,360,490,237,474,190,375,260,380,380,480,380,480,330,430,530,630,280,410,510,295,475,575,405,405,400,400,400,302,467,305,460,560,400,500,305,460,560,470,330,470,360,290,340,520,335,475,310,490,590,458,458,440,440,288,468,308,468,300,500,355,495,355,495,200,540,420,440,295,455,555,295,455,460,425,465,565,260,300,480,580,290,410,530,345,485,485,485,330,300,420,600,700,300,420,600,700,580,580,580,600,700,600,700,670,770,670,770,680,780,600,600,600,600,600,318,405,525,309,405,534,314,405,530,245,340,485,250,410,194,384,263,363,523,280,515,350,495,350,495,224,424,424,424,424,244,474,405,330,495,275,450,325,475,482,348,498,350,480,580,495,505,310,452,285,329,479,300,500,290,310,220,411,485,300,410,600,700,390,285,525,625,330,525,330,500,300,490,454,330,460,345,334,494,594,510,535,515,535,535,540,540,545,515,525,525,510,530,535,518,618,525,525,480,440,520,520,520,520,520,580,580,580,680,680,600,670,680,680,600,480,600,600,600,600,720,600,308,413,528,308,418,528,308,413,528,255,420,275,370,500,281,446,316,498,316,498,316,498,292,487,264,358,488,295,497,280,390,515,313,425,328,508,445,545,305,405,505,294,384,509,465,465,310,380,500,260,360,485,280,480,280,480,460,292,351,519,315,480,540,461,325,475,348,488,490,303,483,355,495,401,567,329,474,330,510,300,470,290,390,490,290,370,490,305,473,305,395,535,335,475,428,315,495,294,464,335,480,470,319,472,305,489,300,440,520,275,405,515,335,485,275,370,520,320,410,540,305,485,485,305,495,471,350,510,485,303,483,340,490,490,350,510,370,510,484,484,300,420,600,360,550,580,580,580,580,580,580,580,680,680,600,600,660,700,700,580,580,600,600,600,313,405,530,307,409,534,314,405,530,237,423,278,382,499,200,213,411,369,507,303,371,552,350,531,348,495,472,355,466,466,325,448,520,520,341,462,341,480,288,482,306,500,320,494,330,500,289,481,362,521,362,521,525,500,431,500,300,452,600,470,309,474,335,335,335,335,494,494,494,494,304,514,245,535,680,680,600,600,700,600,680,600],"coloraxis":"coloraxis","symbol":"circle"},"mode":"markers","name":"","scene":"scene","showlegend":false,"x":[65,80,100,122,60,80,109,130,159,50,65,85,135,20,25,90,20,25,45,15,35,50,70,135,25,50,31,61,40,65,50,90,20,45,40,55,75,40,55,85,60,95,50,81,45,85,30,65,75,85,110,45,60,40,90,35,50,40,65,65,95,35,60,70,100,40,50,70,105,120,135,175,35,50,65,70,85,100,50,80,30,45,55,65,80,40,100,130,95,120,58,35,60,45,70,40,65,45,85,100,115,130,170,30,43,73,25,50,55,80,60,125,40,50,35,35,60,60,85,30,45,35,100,40,60,70,95,35,65,70,100,100,55,115,95,100,55,65,40,15,60,70,85,48,45,110,110,95,85,90,115,55,65,60,70,65,95,125,125,50,70,100,154,154,194,100,49,63,83,60,80,109,44,59,79,35,45,36,76,40,55,40,60,70,56,76,35,45,40,40,80,70,95,65,80,115,165,90,20,60,30,90,35,45,55,40,30,105,75,25,65,130,60,85,100,85,72,33,90,35,60,65,35,55,55,40,60,55,55,65,10,40,40,35,50,75,70,80,30,60,65,65,105,65,80,40,80,110,140,95,40,60,105,85,20,35,35,85,65,70,40,75,115,90,90,45,65,95,95,90,110,100,65,85,105,145,70,85,110,130,50,60,85,95,30,60,30,50,20,25,100,25,50,40,60,90,30,60,90,30,50,55,85,45,65,125,165,50,80,40,60,35,55,95,30,50,30,51,71,91,20,40,20,45,35,55,65,85,55,55,40,50,60,60,40,60,80,65,105,135,85,75,47,73,100,43,73,65,95,110,70,90,65,105,145,85,70,90,60,45,50,80,85,115,40,70,110,60,100,95,55,46,76,50,90,40,70,61,81,40,70,10,100,70,60,63,83,93,30,60,72,95,75,115,23,50,80,120,55,75,95,74,94,114,45,40,40,60,110,120,35,55,95,105,50,100,75,110,140,130,160,150,180,100,150,150,180,100,150,180,70,95,45,55,75,58,78,104,61,81,111,30,40,50,35,55,25,55,40,60,95,50,125,30,65,42,47,29,79,59,69,94,30,80,45,60,85,62,87,57,92,60,60,90,44,54,54,105,105,42,64,65,41,71,24,79,10,70,15,92,92,40,50,80,120,40,35,115,140,38,68,30,60,61,86,90,49,69,60,62,92,132,45,130,80,55,110,95,125,120,116,60,130,45,70,135,65,65,75,65,80,95,105,105,105,105,105,75,105,125,150,150,130,80,100,120,75,80,100,135,100,120,120,100,45,60,75,45,70,100,63,83,108,35,60,25,35,45,50,88,53,98,53,98,53,98,67,107,36,50,65,50,80,25,50,60,55,77,30,50,60,80,25,40,55,50,65,85,30,30,40,50,70,30,40,55,37,77,70,110,80,35,45,65,15,30,140,106,35,65,35,45,103,55,95,53,83,74,112,40,60,80,120,40,65,55,75,95,105,125,125,44,87,65,80,110,40,60,75,40,60,55,85,65,85,40,57,97,24,54,45,70,70,45,75,105,85,125,65,95,145,30,40,60,60,70,95,40,100,81,55,95,60,35,55,40,60,40,37,57,45,55,105,48,45,65,125,50,135,90,72,90,125,110,125,145,150,120,115,105,130,120,170,129,129,128,77,120,48,56,74,62,90,114,62,83,103,32,50,40,56,74,27,27,90,73,109,61,75,112,62,97,46,69,65,63,83,83,35,45,150,50,63,99,59,85,37,68,39,54,60,97,58,120,61,109,45,69,67,99,110,74,81,50,55,83,110,80,50,65,44,44,44,44,58,58,58,58,32,44,45,97,131,131,81,100,160,150,170,130],"y":[65,80,100,120,50,65,85,85,115,64,80,105,115,20,25,80,20,25,80,80,35,50,70,80,35,70,31,61,54,79,50,80,30,55,40,55,85,40,55,75,65,90,65,100,25,50,40,75,65,75,90,55,80,55,75,45,70,40,65,50,80,45,70,50,80,40,50,90,55,70,95,95,35,60,85,30,45,70,100,120,30,45,65,65,80,40,80,80,55,70,62,35,60,70,95,50,100,25,45,35,55,75,95,45,90,115,25,50,55,80,45,65,50,80,110,110,75,45,70,30,45,105,40,80,100,25,45,50,80,55,85,120,80,95,85,85,70,90,70,20,100,130,95,48,65,95,95,110,75,55,70,45,70,75,95,110,125,90,85,50,70,100,90,100,120,100,65,80,100,50,65,85,48,63,83,45,55,56,96,80,110,40,60,80,56,76,35,55,20,65,105,45,70,45,60,90,110,100,50,80,65,100,55,65,95,55,30,85,45,25,65,95,130,42,110,85,48,58,65,35,60,65,65,65,95,40,60,55,80,100,230,95,105,75,50,75,40,80,30,60,85,35,75,45,140,70,50,80,90,95,40,60,95,65,45,35,110,65,55,55,70,135,100,75,115,50,70,100,120,154,154,100,55,65,85,85,50,60,70,80,50,70,90,110,30,60,41,61,30,25,50,25,90,50,70,100,30,40,60,30,50,30,70,35,55,115,135,52,82,60,60,35,55,65,30,50,30,23,43,73,30,60,40,90,35,55,65,115,55,95,40,50,60,80,55,75,85,40,60,80,75,85,75,75,80,53,83,20,40,65,35,45,45,75,105,70,80,110,60,45,50,80,40,60,75,105,105,60,60,85,65,41,71,35,55,70,120,87,107,50,80,55,125,70,120,33,63,83,90,130,87,80,60,60,48,50,80,80,50,70,90,55,75,75,65,65,30,50,80,90,60,80,90,110,100,200,150,130,150,110,120,140,160,90,90,90,100,100,50,20,160,90,55,65,85,44,52,71,56,76,101,30,40,60,40,60,41,51,34,49,79,70,105,30,50,88,138,45,105,85,95,50,42,102,90,30,50,53,78,62,82,66,44,54,56,96,96,105,52,37,59,50,41,61,86,116,45,90,65,42,108,45,55,85,95,85,40,70,70,42,72,55,75,40,65,72,61,86,120,60,85,105,85,90,95,55,50,85,95,115,56,65,95,75,60,75,115,115,150,135,70,77,107,107,107,107,107,130,105,70,100,120,106,110,120,100,130,80,100,90,100,75,120,100,55,75,95,45,55,65,45,60,70,39,69,45,65,90,37,50,48,63,48,63,48,63,55,95,30,42,55,32,63,25,40,80,43,55,45,65,86,126,35,50,65,40,55,75,85,75,60,80,80,39,79,69,50,75,50,75,55,35,45,70,45,55,105,67,35,75,70,115,80,65,105,45,65,45,65,62,82,40,60,40,60,65,85,110,50,60,85,50,63,60,75,95,50,70,60,45,105,55,80,85,105,45,50,60,86,116,60,85,85,40,70,80,55,95,55,60,90,40,50,70,40,80,135,65,60,99,50,60,90,50,80,40,70,95,50,75,65,95,66,48,50,70,90,55,105,72,90,129,80,90,80,80,120,100,80,80,90,90,100,90,90,128,77,95,45,58,75,60,70,100,44,56,71,36,77,38,52,69,25,30,50,54,66,79,98,154,57,81,48,71,90,60,81,81,37,49,50,150,65,89,57,75,46,75,56,86,60,123,63,89,43,94,45,59,63,92,130,63,67,150,75,113,150,87,60,82,55,55,55,55,75,75,75,75,35,46,40,80,98,98,95,150,110,130,130,90],"z":[318,405,525,625,309,405,534,634,634,314,405,530,630,195,205,395,195,205,395,495,251,349,479,579,253,413,262,442,288,438,320,485,300,450,275,365,505,273,365,505,323,483,299,505,270,435,245,455,320,395,490,285,405,305,450,265,405,290,440,320,500,305,455,350,555,300,385,510,310,400,500,590,305,405,505,300,390,490,335,515,300,390,495,410,500,315,490,590,325,465,352,310,460,325,475,325,500,305,525,310,405,500,600,385,328,483,325,475,330,480,325,520,320,425,455,455,385,340,490,345,485,450,435,490,590,295,440,320,450,340,520,460,500,455,490,495,500,600,490,200,540,640,535,288,325,525,525,525,395,355,495,355,495,515,615,540,580,580,580,300,420,600,680,780,780,600,318,405,525,309,405,534,314,405,530,215,415,262,442,265,390,250,390,535,330,460,205,218,210,245,405,320,470,280,365,510,610,490,250,420,410,500,250,340,460,360,180,425,390,210,430,525,525,405,490,435,336,405,455,290,465,415,430,510,610,300,450,430,500,600,505,500,600,430,330,500,250,410,250,450,380,300,480,330,465,465,330,500,600,540,330,500,515,465,250,210,455,305,360,365,490,540,580,580,580,300,410,600,700,680,680,600,310,405,530,630,310,405,530,630,310,405,535,635,220,420,240,420,195,205,395,205,385,220,340,480,220,340,480,270,430,270,430,198,278,518,618,269,414,295,460,280,440,670,266,456,236,240,360,490,237,474,190,375,260,380,380,480,380,480,330,430,530,630,280,410,510,295,475,575,405,405,400,400,400,302,467,305,460,560,400,500,305,460,560,470,330,470,360,290,340,520,335,475,310,490,590,458,458,440,440,288,468,308,468,300,500,355,495,355,495,200,540,420,440,295,455,555,295,455,460,425,465,565,260,300,480,580,290,410,530,345,485,485,485,330,300,420,600,700,300,420,600,700,580,580,580,600,700,600,700,670,770,670,770,680,780,600,600,600,600,600,318,405,525,309,405,534,314,405,530,245,340,485,250,410,194,384,263,363,523,280,515,350,495,350,495,224,424,424,424,424,244,474,405,330,495,275,450,325,475,482,348,498,350,480,580,495,505,310,452,285,329,479,300,500,290,310,220,411,485,300,410,600,700,390,285,525,625,330,525,330,500,300,490,454,330,460,345,334,494,594,510,535,515,535,535,540,540,545,515,525,525,510,530,535,518,618,525,525,480,440,520,520,520,520,520,580,580,580,680,680,600,670,680,680,600,480,600,600,600,600,720,600,308,413,528,308,418,528,308,413,528,255,420,275,370,500,281,446,316,498,316,498,316,498,292,487,264,358,488,295,497,280,390,515,313,425,328,508,445,545,305,405,505,294,384,509,465,465,310,380,500,260,360,485,280,480,280,480,460,292,351,519,315,480,540,461,325,475,348,488,490,303,483,355,495,401,567,329,474,330,510,300,470,290,390,490,290,370,490,305,473,305,395,535,335,475,428,315,495,294,464,335,480,470,319,472,305,489,300,440,520,275,405,515,335,485,275,370,520,320,410,540,305,485,485,305,495,471,350,510,485,303,483,340,490,490,350,510,370,510,484,484,300,420,600,360,550,580,580,580,580,580,580,580,680,680,600,600,660,700,700,580,580,600,600,600,313,405,530,307,409,534,314,405,530,237,423,278,382,499,200,213,411,369,507,303,371,552,350,531,348,495,472,355,466,466,325,448,520,520,341,462,341,480,288,482,306,500,320,494,330,500,289,481,362,521,362,521,525,500,431,500,300,452,600,470,309,474,335,335,335,335,494,494,494,494,304,514,245,535,680,680,600,600,700,600,680,600],"type":"scatter3d"}],                        {"template":{"data":{"barpolar":[{"marker":{"line":{"color":"rgb(17,17,17)","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"bar":[{"error_x":{"color":"#f2f5fa"},"error_y":{"color":"#f2f5fa"},"marker":{"line":{"color":"rgb(17,17,17)","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"carpet":[{"aaxis":{"endlinecolor":"#A2B1C6","gridcolor":"#506784","linecolor":"#506784","minorgridcolor":"#506784","startlinecolor":"#A2B1C6"},"baxis":{"endlinecolor":"#A2B1C6","gridcolor":"#506784","linecolor":"#506784","minorgridcolor":"#506784","startlinecolor":"#A2B1C6"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"contour"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"heatmapgl"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"heatmap"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"histogram2dcontour"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"histogram2d"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"line":{"color":"#283442"}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatter":[{"marker":{"line":{"color":"#283442"}},"type":"scatter"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#506784"},"line":{"color":"rgb(17,17,17)"}},"header":{"fill":{"color":"#2a3f5f"},"line":{"color":"rgb(17,17,17)"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#f2f5fa","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#f2f5fa"},"geo":{"bgcolor":"rgb(17,17,17)","lakecolor":"rgb(17,17,17)","landcolor":"rgb(17,17,17)","showlakes":true,"showland":true,"subunitcolor":"#506784"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"dark"},"paper_bgcolor":"rgb(17,17,17)","plot_bgcolor":"rgb(17,17,17)","polar":{"angularaxis":{"gridcolor":"#506784","linecolor":"#506784","ticks":""},"bgcolor":"rgb(17,17,17)","radialaxis":{"gridcolor":"#506784","linecolor":"#506784","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"rgb(17,17,17)","gridcolor":"#506784","gridwidth":2,"linecolor":"#506784","showbackground":true,"ticks":"","zerolinecolor":"#C8D4E3"},"yaxis":{"backgroundcolor":"rgb(17,17,17)","gridcolor":"#506784","gridwidth":2,"linecolor":"#506784","showbackground":true,"ticks":"","zerolinecolor":"#C8D4E3"},"zaxis":{"backgroundcolor":"rgb(17,17,17)","gridcolor":"#506784","gridwidth":2,"linecolor":"#506784","showbackground":true,"ticks":"","zerolinecolor":"#C8D4E3"}},"shapedefaults":{"line":{"color":"#f2f5fa"}},"sliderdefaults":{"bgcolor":"#C8D4E3","bordercolor":"rgb(17,17,17)","borderwidth":1,"tickwidth":0},"ternary":{"aaxis":{"gridcolor":"#506784","linecolor":"#506784","ticks":""},"baxis":{"gridcolor":"#506784","linecolor":"#506784","ticks":""},"bgcolor":"rgb(17,17,17)","caxis":{"gridcolor":"#506784","linecolor":"#506784","ticks":""}},"title":{"x":0.05},"updatemenudefaults":{"bgcolor":"#506784","borderwidth":0},"xaxis":{"automargin":true,"gridcolor":"#283442","linecolor":"#506784","ticks":"","title":{"standoff":15},"zerolinecolor":"#283442","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"#283442","linecolor":"#506784","ticks":"","title":{"standoff":15},"zerolinecolor":"#283442","zerolinewidth":2}}},"scene":{"domain":{"x":[0.0,1.0],"y":[0.0,1.0]},"xaxis":{"title":{"text":"Sp. Atk"}},"yaxis":{"title":{"text":"Sp. Def"}},"zaxis":{"title":{"text":"Total"}}},"coloraxis":{"colorbar":{"title":{"text":"Total"}},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]},"legend":{"tracegroupgap":0},"title":{"text":"Speed Attack, Speed Attack, Price 3D Scatter Plot"},"height":600,"width":800},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('d8c26a16-900c-451a-82d1-07471ea9141b');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>


### Top 20 Strongest Pokemon


```python
df_strongest_poke = df_poke[['Name', 'Total', 'Type 1', 'Type 2' ]].head(20)
df_strongest_poke.sort_values('Total', ascending=False, inplace=True)

df_top_strongest_pokemon = df_strongest_poke.rename(columns={'Name':'Pokemon_Name', 'Total': 'Total_Points',})

df_top_strongest_pokemon

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
      <th>Pokemon_Name</th>
      <th>Total_Points</th>
      <th>Type 1</th>
      <th>Type 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>7</th>
      <td>CharizardMega Charizard X</td>
      <td>634</td>
      <td>Fire</td>
      <td>Dragon</td>
    </tr>
    <tr>
      <th>8</th>
      <td>CharizardMega Charizard Y</td>
      <td>634</td>
      <td>Fire</td>
      <td>Flying</td>
    </tr>
    <tr>
      <th>12</th>
      <td>BlastoiseMega Blastoise</td>
      <td>630</td>
      <td>Water</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>VenusaurMega Venusaur</td>
      <td>625</td>
      <td>Grass</td>
      <td>Poison</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Charizard</td>
      <td>534</td>
      <td>Fire</td>
      <td>Flying</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Blastoise</td>
      <td>530</td>
      <td>Water</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Venusaur</td>
      <td>525</td>
      <td>Grass</td>
      <td>Poison</td>
    </tr>
    <tr>
      <th>19</th>
      <td>BeedrillMega Beedrill</td>
      <td>495</td>
      <td>Bug</td>
      <td>Poison</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ivysaur</td>
      <td>405</td>
      <td>Grass</td>
      <td>Poison</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Wartortle</td>
      <td>405</td>
      <td>Water</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Charmeleon</td>
      <td>405</td>
      <td>Fire</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Butterfree</td>
      <td>395</td>
      <td>Bug</td>
      <td>Flying</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Beedrill</td>
      <td>395</td>
      <td>Bug</td>
      <td>Poison</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Bulbasaur</td>
      <td>318</td>
      <td>Grass</td>
      <td>Poison</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Squirtle</td>
      <td>314</td>
      <td>Water</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Charmander</td>
      <td>309</td>
      <td>Fire</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Metapod</td>
      <td>205</td>
      <td>Bug</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Kakuna</td>
      <td>205</td>
      <td>Bug</td>
      <td>Poison</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Caterpie</td>
      <td>195</td>
      <td>Bug</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Weedle</td>
      <td>195</td>
      <td>Bug</td>
      <td>Poison</td>
    </tr>
  </tbody>
</table>
</div>




```python
fig = px.bar(df_top_strongest_pokemon
    , 
    x='Pokemon_Name', 
    y='Total_Points',
    color = 'Pokemon_Name',
    title='Top 20 Strongest Pokemon',
    text = 'Total_Points',
    width = 900,
    height = 600
)
fig.show()

```

    /opt/anaconda3/lib/python3.12/site-packages/plotly/express/_core.py:1979: FutureWarning:
    
    When grouping with a length-1 list-like, you will need to pass a length-1 tuple to get_group in a future version of pandas. Pass `(name,)` instead of `name` to silence this warning.
    



<div>                            <div id="bb9e4da2-2df9-406e-8264-d2a2b1ffa5a2" class="plotly-graph-div" style="height:600px; width:900px;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("bb9e4da2-2df9-406e-8264-d2a2b1ffa5a2")) {                    Plotly.newPlot(                        "bb9e4da2-2df9-406e-8264-d2a2b1ffa5a2",                        [{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"CharizardMega Charizard X","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"CharizardMega Charizard X","offsetgroup":"CharizardMega Charizard X","orientation":"v","showlegend":true,"text":[634.0],"textposition":"auto","x":["CharizardMega Charizard X"],"xaxis":"x","y":[634],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"CharizardMega Charizard Y","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"CharizardMega Charizard Y","offsetgroup":"CharizardMega Charizard Y","orientation":"v","showlegend":true,"text":[634.0],"textposition":"auto","x":["CharizardMega Charizard Y"],"xaxis":"x","y":[634],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"BlastoiseMega Blastoise","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"BlastoiseMega Blastoise","offsetgroup":"BlastoiseMega Blastoise","orientation":"v","showlegend":true,"text":[630.0],"textposition":"auto","x":["BlastoiseMega Blastoise"],"xaxis":"x","y":[630],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"VenusaurMega Venusaur","marker":{"color":"#ab63fa","pattern":{"shape":""}},"name":"VenusaurMega Venusaur","offsetgroup":"VenusaurMega Venusaur","orientation":"v","showlegend":true,"text":[625.0],"textposition":"auto","x":["VenusaurMega Venusaur"],"xaxis":"x","y":[625],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"Charizard","marker":{"color":"#FFA15A","pattern":{"shape":""}},"name":"Charizard","offsetgroup":"Charizard","orientation":"v","showlegend":true,"text":[534.0],"textposition":"auto","x":["Charizard"],"xaxis":"x","y":[534],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"Blastoise","marker":{"color":"#19d3f3","pattern":{"shape":""}},"name":"Blastoise","offsetgroup":"Blastoise","orientation":"v","showlegend":true,"text":[530.0],"textposition":"auto","x":["Blastoise"],"xaxis":"x","y":[530],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"Venusaur","marker":{"color":"#FF6692","pattern":{"shape":""}},"name":"Venusaur","offsetgroup":"Venusaur","orientation":"v","showlegend":true,"text":[525.0],"textposition":"auto","x":["Venusaur"],"xaxis":"x","y":[525],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"BeedrillMega Beedrill","marker":{"color":"#B6E880","pattern":{"shape":""}},"name":"BeedrillMega Beedrill","offsetgroup":"BeedrillMega Beedrill","orientation":"v","showlegend":true,"text":[495.0],"textposition":"auto","x":["BeedrillMega Beedrill"],"xaxis":"x","y":[495],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"Ivysaur","marker":{"color":"#FF97FF","pattern":{"shape":""}},"name":"Ivysaur","offsetgroup":"Ivysaur","orientation":"v","showlegend":true,"text":[405.0],"textposition":"auto","x":["Ivysaur"],"xaxis":"x","y":[405],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"Wartortle","marker":{"color":"#FECB52","pattern":{"shape":""}},"name":"Wartortle","offsetgroup":"Wartortle","orientation":"v","showlegend":true,"text":[405.0],"textposition":"auto","x":["Wartortle"],"xaxis":"x","y":[405],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"Charmeleon","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"Charmeleon","offsetgroup":"Charmeleon","orientation":"v","showlegend":true,"text":[405.0],"textposition":"auto","x":["Charmeleon"],"xaxis":"x","y":[405],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"Butterfree","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"Butterfree","offsetgroup":"Butterfree","orientation":"v","showlegend":true,"text":[395.0],"textposition":"auto","x":["Butterfree"],"xaxis":"x","y":[395],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"Beedrill","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"Beedrill","offsetgroup":"Beedrill","orientation":"v","showlegend":true,"text":[395.0],"textposition":"auto","x":["Beedrill"],"xaxis":"x","y":[395],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"Bulbasaur","marker":{"color":"#ab63fa","pattern":{"shape":""}},"name":"Bulbasaur","offsetgroup":"Bulbasaur","orientation":"v","showlegend":true,"text":[318.0],"textposition":"auto","x":["Bulbasaur"],"xaxis":"x","y":[318],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"Squirtle","marker":{"color":"#FFA15A","pattern":{"shape":""}},"name":"Squirtle","offsetgroup":"Squirtle","orientation":"v","showlegend":true,"text":[314.0],"textposition":"auto","x":["Squirtle"],"xaxis":"x","y":[314],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"Charmander","marker":{"color":"#19d3f3","pattern":{"shape":""}},"name":"Charmander","offsetgroup":"Charmander","orientation":"v","showlegend":true,"text":[309.0],"textposition":"auto","x":["Charmander"],"xaxis":"x","y":[309],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"Metapod","marker":{"color":"#FF6692","pattern":{"shape":""}},"name":"Metapod","offsetgroup":"Metapod","orientation":"v","showlegend":true,"text":[205.0],"textposition":"auto","x":["Metapod"],"xaxis":"x","y":[205],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"Kakuna","marker":{"color":"#B6E880","pattern":{"shape":""}},"name":"Kakuna","offsetgroup":"Kakuna","orientation":"v","showlegend":true,"text":[205.0],"textposition":"auto","x":["Kakuna"],"xaxis":"x","y":[205],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"Caterpie","marker":{"color":"#FF97FF","pattern":{"shape":""}},"name":"Caterpie","offsetgroup":"Caterpie","orientation":"v","showlegend":true,"text":[195.0],"textposition":"auto","x":["Caterpie"],"xaxis":"x","y":[195],"yaxis":"y","type":"bar"},{"alignmentgroup":"True","hovertemplate":"Pokemon_Name=%{x}<br>Total_Points=%{text}<extra></extra>","legendgroup":"Weedle","marker":{"color":"#FECB52","pattern":{"shape":""}},"name":"Weedle","offsetgroup":"Weedle","orientation":"v","showlegend":true,"text":[195.0],"textposition":"auto","x":["Weedle"],"xaxis":"x","y":[195],"yaxis":"y","type":"bar"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"xaxis":{"anchor":"y","domain":[0.0,1.0],"title":{"text":"Pokemon_Name"},"categoryorder":"array","categoryarray":["CharizardMega Charizard X","CharizardMega Charizard Y","BlastoiseMega Blastoise","VenusaurMega Venusaur","Charizard","Blastoise","Venusaur","BeedrillMega Beedrill","Ivysaur","Wartortle","Charmeleon","Butterfree","Beedrill","Bulbasaur","Squirtle","Charmander","Metapod","Kakuna","Caterpie","Weedle"]},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"Total_Points"}},"legend":{"title":{"text":"Pokemon_Name"},"tracegroupgap":0},"title":{"text":"Top 20 Strongest Pokemon"},"barmode":"relative","height":600,"width":900},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('bb9e4da2-2df9-406e-8264-d2a2b1ffa5a2');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>


### 20 Highest Hit Points


```python
df_highest_poke = df_poke[['Name', 'HP' ]].head(20)
df_highest_poke.sort_values('HP', ascending=False, inplace=True)

df_top_highest_points_pokemon = df_highest_poke.rename(columns={'Name':'Pokemon_Name', 'HP': 'Hit_points',})

df_top_highest_points_pokemon
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
      <th>Pokemon_Name</th>
      <th>Hit_points</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Venusaur</td>
      <td>80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>VenusaurMega Venusaur</td>
      <td>80</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Blastoise</td>
      <td>79</td>
    </tr>
    <tr>
      <th>12</th>
      <td>BlastoiseMega Blastoise</td>
      <td>79</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Charizard</td>
      <td>78</td>
    </tr>
    <tr>
      <th>7</th>
      <td>CharizardMega Charizard X</td>
      <td>78</td>
    </tr>
    <tr>
      <th>8</th>
      <td>CharizardMega Charizard Y</td>
      <td>78</td>
    </tr>
    <tr>
      <th>19</th>
      <td>BeedrillMega Beedrill</td>
      <td>65</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Beedrill</td>
      <td>65</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Butterfree</td>
      <td>60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ivysaur</td>
      <td>60</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Wartortle</td>
      <td>59</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Charmeleon</td>
      <td>58</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Metapod</td>
      <td>50</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Caterpie</td>
      <td>45</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Kakuna</td>
      <td>45</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Bulbasaur</td>
      <td>45</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Squirtle</td>
      <td>44</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Weedle</td>
      <td>40</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Charmander</td>
      <td>39</td>
    </tr>
  </tbody>
</table>
</div>




```python
fig = px.pie(
    df_top_highest_points_pokemon, 
    values='Hit_points', 
    names='Pokemon_Name',
    title= 'breakdown of Hit Points'
)
fig.show()

```


<div>                            <div id="3ff2cbe1-8400-4a5f-aeb9-d5de22528690" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("3ff2cbe1-8400-4a5f-aeb9-d5de22528690")) {                    Plotly.newPlot(                        "3ff2cbe1-8400-4a5f-aeb9-d5de22528690",                        [{"domain":{"x":[0.0,1.0],"y":[0.0,1.0]},"hovertemplate":"Pokemon_Name=%{label}<br>Hit_points=%{value}<extra></extra>","labels":["Venusaur","VenusaurMega Venusaur","Blastoise","BlastoiseMega Blastoise","Charizard","CharizardMega Charizard X","CharizardMega Charizard Y","BeedrillMega Beedrill","Beedrill","Butterfree","Ivysaur","Wartortle","Charmeleon","Metapod","Caterpie","Kakuna","Bulbasaur","Squirtle","Weedle","Charmander"],"legendgroup":"","name":"","showlegend":true,"values":[80,80,79,79,78,78,78,65,65,60,60,59,58,50,45,45,45,44,40,39],"type":"pie"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"legend":{"tracegroupgap":0},"title":{"text":"breakdown of Hit Points"}},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('3ff2cbe1-8400-4a5f-aeb9-d5de22528690');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>


### Treemap of The Strongest Pokemon


```python
fig = px.treemap(
    df_top_strongest_pokemon,
    path= ['Pokemon_Name'],
    title='Strongest Pokemon Breakdown',
    values='Total_Points',
    height=700
)

fig.show()

```


<div>                            <div id="7f3638be-525d-4fe4-80ba-a6aa9a08d929" class="plotly-graph-div" style="height:700px; width:100%;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("7f3638be-525d-4fe4-80ba-a6aa9a08d929")) {                    Plotly.newPlot(                        "7f3638be-525d-4fe4-80ba-a6aa9a08d929",                        [{"branchvalues":"total","domain":{"x":[0.0,1.0],"y":[0.0,1.0]},"hovertemplate":"labels=%{label}<br>Total_Points=%{value}<br>parent=%{parent}<br>id=%{id}<extra></extra>","ids":["Beedrill","BeedrillMega Beedrill","Blastoise","BlastoiseMega Blastoise","Bulbasaur","Butterfree","Caterpie","Charizard","CharizardMega Charizard X","CharizardMega Charizard Y","Charmander","Charmeleon","Ivysaur","Kakuna","Metapod","Squirtle","Venusaur","VenusaurMega Venusaur","Wartortle","Weedle"],"labels":["Beedrill","BeedrillMega Beedrill","Blastoise","BlastoiseMega Blastoise","Bulbasaur","Butterfree","Caterpie","Charizard","CharizardMega Charizard X","CharizardMega Charizard Y","Charmander","Charmeleon","Ivysaur","Kakuna","Metapod","Squirtle","Venusaur","VenusaurMega Venusaur","Wartortle","Weedle"],"name":"","parents":["","","","","","","","","","","","","","","","","","","",""],"values":[395,495,530,630,318,395,195,534,634,634,309,405,405,205,205,314,525,625,405,195],"type":"treemap"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"legend":{"tracegroupgap":0},"title":{"text":"Strongest Pokemon Breakdown"},"height":700},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('7f3638be-525d-4fe4-80ba-a6aa9a08d929');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>



```python
fig = px.box(df_poke, x= 'Attack', orientation='h', title='Pokemon Attack (Horizontal)')
fig.show()

```


<div>                            <div id="2e7d4309-a972-40bf-ace6-396fe338aeea" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("2e7d4309-a972-40bf-ace6-396fe338aeea")) {                    Plotly.newPlot(                        "2e7d4309-a972-40bf-ace6-396fe338aeea",                        [{"alignmentgroup":"True","hovertemplate":"Attack=%{x}<extra></extra>","legendgroup":"","marker":{"color":"#636efa"},"name":"","notched":false,"offsetgroup":"","orientation":"h","showlegend":false,"x":[49,62,82,100,52,64,84,130,104,48,63,83,103,30,20,45,35,25,90,150,45,60,80,80,56,81,60,90,60,85,55,90,75,100,47,62,92,57,72,102,45,70,41,76,45,70,45,80,50,65,80,70,95,55,65,55,80,45,70,52,82,80,105,70,110,50,65,95,20,35,50,50,80,100,130,75,90,105,40,70,80,95,120,85,100,65,75,75,35,60,65,85,110,45,70,80,105,65,95,35,50,65,65,45,48,73,105,130,30,50,40,95,50,80,120,105,55,65,90,85,130,5,55,95,125,40,65,67,92,45,75,45,110,50,83,95,125,155,100,10,125,155,85,48,55,65,65,130,60,40,60,80,115,105,135,110,85,90,100,64,84,134,110,190,150,100,49,62,82,52,64,84,65,80,105,46,76,30,50,20,35,60,90,90,38,58,40,25,30,20,40,50,75,40,55,75,95,80,20,50,100,75,35,45,55,70,30,75,65,45,85,65,65,85,75,60,72,33,80,65,90,70,75,85,125,80,120,95,130,150,10,125,185,95,80,130,40,50,50,100,55,65,105,55,40,80,60,90,90,95,60,120,80,95,20,35,95,30,63,75,80,10,85,115,75,64,84,134,164,90,130,100,45,65,85,110,60,85,120,160,70,85,110,150,55,90,30,70,45,35,70,35,50,30,50,70,40,70,100,55,85,30,50,25,35,65,85,30,60,40,130,60,80,160,45,90,90,51,71,91,60,120,20,45,45,65,75,85,85,105,70,90,110,140,40,60,100,45,75,75,50,40,73,47,60,43,73,90,120,140,70,90,60,100,120,85,25,45,60,100,70,100,85,115,40,70,110,115,100,55,95,48,78,80,120,40,70,41,81,95,125,15,60,70,90,75,115,165,40,70,68,50,130,150,23,50,80,120,40,60,80,64,104,84,90,30,75,95,135,145,55,75,135,145,100,50,75,80,100,90,130,100,150,150,180,150,180,100,150,180,70,95,68,89,109,58,78,104,51,66,86,55,75,120,45,85,25,85,65,85,120,30,70,125,165,42,52,29,59,79,69,94,30,80,45,65,105,35,60,48,83,100,50,80,66,76,136,60,125,55,82,30,63,93,24,89,80,25,5,65,92,70,90,130,170,85,70,110,145,72,112,50,90,61,106,100,49,69,20,62,92,132,120,70,85,140,100,123,95,50,76,110,60,95,130,80,125,165,55,100,80,50,65,65,65,65,65,75,105,125,120,120,90,160,100,120,70,80,100,90,100,103,120,100,45,60,75,63,93,123,55,75,100,55,85,60,80,110,50,88,53,98,53,98,53,98,25,55,55,77,115,60,100,75,105,135,45,57,85,135,60,60,80,105,140,50,65,95,100,125,53,63,103,45,55,100,27,67,35,60,92,72,82,117,90,140,30,86,65,95,75,90,58,30,50,78,108,112,140,50,95,65,105,50,95,30,45,55,30,40,65,44,87,50,65,95,60,100,75,75,135,55,85,40,60,75,47,77,50,94,55,80,100,55,85,115,55,75,30,40,55,87,117,147,70,110,50,40,70,66,85,125,120,74,124,85,125,110,83,123,55,65,97,109,65,85,105,85,60,90,129,90,115,100,115,105,120,150,125,145,130,170,120,72,72,77,128,120,61,78,107,45,59,69,56,63,95,36,56,50,73,81,35,22,52,50,68,38,45,65,65,100,82,124,80,48,48,48,80,110,150,50,52,72,48,80,54,92,52,105,60,75,53,73,38,55,89,121,59,77,65,92,58,50,50,75,100,80,70,110,66,66,66,66,90,85,95,100,69,117,30,70,131,131,100,100,160,110,160,110],"x0":" ","xaxis":"x","y0":" ","yaxis":"y","type":"box"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"xaxis":{"anchor":"y","domain":[0.0,1.0],"title":{"text":"Attack"}},"yaxis":{"anchor":"x","domain":[0.0,1.0]},"legend":{"tracegroupgap":0},"title":{"text":"Pokemon Attack (Horizontal)"},"boxmode":"group"},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('2e7d4309-a972-40bf-ace6-396fe338aeea');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>



```python
fig = px.box(df_poke, y= 'Attack', title='Pokemon Attack (Vertical)')
fig.show()
```


<div>                            <div id="72bff55c-9293-47e9-90a5-1ff2d537568a" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("72bff55c-9293-47e9-90a5-1ff2d537568a")) {                    Plotly.newPlot(                        "72bff55c-9293-47e9-90a5-1ff2d537568a",                        [{"alignmentgroup":"True","hovertemplate":"Attack=%{y}<extra></extra>","legendgroup":"","marker":{"color":"#636efa"},"name":"","notched":false,"offsetgroup":"","orientation":"v","showlegend":false,"x0":" ","xaxis":"x","y":[49,62,82,100,52,64,84,130,104,48,63,83,103,30,20,45,35,25,90,150,45,60,80,80,56,81,60,90,60,85,55,90,75,100,47,62,92,57,72,102,45,70,41,76,45,70,45,80,50,65,80,70,95,55,65,55,80,45,70,52,82,80,105,70,110,50,65,95,20,35,50,50,80,100,130,75,90,105,40,70,80,95,120,85,100,65,75,75,35,60,65,85,110,45,70,80,105,65,95,35,50,65,65,45,48,73,105,130,30,50,40,95,50,80,120,105,55,65,90,85,130,5,55,95,125,40,65,67,92,45,75,45,110,50,83,95,125,155,100,10,125,155,85,48,55,65,65,130,60,40,60,80,115,105,135,110,85,90,100,64,84,134,110,190,150,100,49,62,82,52,64,84,65,80,105,46,76,30,50,20,35,60,90,90,38,58,40,25,30,20,40,50,75,40,55,75,95,80,20,50,100,75,35,45,55,70,30,75,65,45,85,65,65,85,75,60,72,33,80,65,90,70,75,85,125,80,120,95,130,150,10,125,185,95,80,130,40,50,50,100,55,65,105,55,40,80,60,90,90,95,60,120,80,95,20,35,95,30,63,75,80,10,85,115,75,64,84,134,164,90,130,100,45,65,85,110,60,85,120,160,70,85,110,150,55,90,30,70,45,35,70,35,50,30,50,70,40,70,100,55,85,30,50,25,35,65,85,30,60,40,130,60,80,160,45,90,90,51,71,91,60,120,20,45,45,65,75,85,85,105,70,90,110,140,40,60,100,45,75,75,50,40,73,47,60,43,73,90,120,140,70,90,60,100,120,85,25,45,60,100,70,100,85,115,40,70,110,115,100,55,95,48,78,80,120,40,70,41,81,95,125,15,60,70,90,75,115,165,40,70,68,50,130,150,23,50,80,120,40,60,80,64,104,84,90,30,75,95,135,145,55,75,135,145,100,50,75,80,100,90,130,100,150,150,180,150,180,100,150,180,70,95,68,89,109,58,78,104,51,66,86,55,75,120,45,85,25,85,65,85,120,30,70,125,165,42,52,29,59,79,69,94,30,80,45,65,105,35,60,48,83,100,50,80,66,76,136,60,125,55,82,30,63,93,24,89,80,25,5,65,92,70,90,130,170,85,70,110,145,72,112,50,90,61,106,100,49,69,20,62,92,132,120,70,85,140,100,123,95,50,76,110,60,95,130,80,125,165,55,100,80,50,65,65,65,65,65,75,105,125,120,120,90,160,100,120,70,80,100,90,100,103,120,100,45,60,75,63,93,123,55,75,100,55,85,60,80,110,50,88,53,98,53,98,53,98,25,55,55,77,115,60,100,75,105,135,45,57,85,135,60,60,80,105,140,50,65,95,100,125,53,63,103,45,55,100,27,67,35,60,92,72,82,117,90,140,30,86,65,95,75,90,58,30,50,78,108,112,140,50,95,65,105,50,95,30,45,55,30,40,65,44,87,50,65,95,60,100,75,75,135,55,85,40,60,75,47,77,50,94,55,80,100,55,85,115,55,75,30,40,55,87,117,147,70,110,50,40,70,66,85,125,120,74,124,85,125,110,83,123,55,65,97,109,65,85,105,85,60,90,129,90,115,100,115,105,120,150,125,145,130,170,120,72,72,77,128,120,61,78,107,45,59,69,56,63,95,36,56,50,73,81,35,22,52,50,68,38,45,65,65,100,82,124,80,48,48,48,80,110,150,50,52,72,48,80,54,92,52,105,60,75,53,73,38,55,89,121,59,77,65,92,58,50,50,75,100,80,70,110,66,66,66,66,90,85,95,100,69,117,30,70,131,131,100,100,160,110,160,110],"y0":" ","yaxis":"y","type":"box"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"xaxis":{"anchor":"y","domain":[0.0,1.0]},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"Attack"}},"legend":{"tracegroupgap":0},"title":{"text":"Pokemon Attack (Vertical)"},"boxmode":"group"},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('72bff55c-9293-47e9-90a5-1ff2d537568a');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>


### Hit Points Histogram


```python
fig = px.histogram(df_poke, x='HP', y='Total', title='Hit Points')
fig.show()
```


<div>                            <div id="9bd8ddd4-472d-47cf-9209-33a9f1936d61" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("9bd8ddd4-472d-47cf-9209-33a9f1936d61")) {                    Plotly.newPlot(                        "9bd8ddd4-472d-47cf-9209-33a9f1936d61",                        [{"alignmentgroup":"True","bingroup":"x","histfunc":"sum","hovertemplate":"HP=%{x}<br>sum of Total=%{y}<extra></extra>","legendgroup":"","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"","offsetgroup":"","orientation":"v","showlegend":false,"x":[45,60,80,80,39,58,78,78,78,44,59,79,79,45,50,60,40,45,65,65,40,63,83,83,30,55,40,65,35,60,35,60,50,75,55,70,90,46,61,81,70,95,38,73,115,140,40,75,45,60,75,35,60,60,70,10,35,40,65,50,80,40,65,55,90,40,65,90,25,40,55,55,70,80,90,50,65,80,40,80,40,55,80,50,65,90,95,95,25,50,52,35,60,65,90,80,105,30,50,30,45,60,60,35,60,85,30,55,40,60,60,95,50,60,50,50,90,40,65,80,105,250,65,105,105,30,55,45,80,30,60,40,70,65,65,65,65,65,75,20,95,95,130,48,55,130,65,65,65,35,70,30,60,80,80,160,90,90,90,41,61,91,106,106,106,100,45,60,80,39,58,78,50,65,85,35,85,60,100,40,55,40,70,85,75,125,20,50,90,35,55,40,65,55,70,90,90,75,70,100,70,90,35,55,75,55,30,75,65,55,95,65,95,60,95,60,48,190,70,50,75,100,65,75,75,60,90,65,70,70,20,80,80,55,60,90,40,50,50,100,55,35,75,45,65,65,45,75,75,75,90,90,85,73,55,35,50,45,45,45,95,255,90,115,100,50,70,100,100,106,106,100,40,50,70,70,45,60,80,80,50,70,100,100,35,70,38,78,45,50,60,50,60,40,60,80,40,70,90,40,60,40,60,28,38,68,68,40,70,60,60,60,80,150,31,61,1,64,84,104,72,144,50,30,50,70,50,50,50,50,50,60,70,70,30,60,60,40,70,70,60,60,65,65,50,70,100,45,70,70,130,170,60,70,70,70,60,80,60,45,50,80,50,70,45,75,75,73,73,70,70,50,110,43,63,40,60,66,86,45,75,20,95,70,60,44,64,64,20,40,99,65,65,65,95,50,80,80,70,90,110,35,55,55,100,43,45,65,95,95,40,60,80,80,80,80,80,80,80,80,80,100,100,100,100,105,105,100,50,50,50,50,55,75,95,44,64,76,53,64,84,40,55,85,59,79,37,77,45,60,80,40,60,67,97,30,60,40,60,60,60,70,30,70,60,55,85,45,70,76,111,75,90,150,55,65,65,60,100,49,71,45,63,103,57,67,50,20,100,76,50,58,68,108,108,135,40,70,70,68,108,40,70,48,83,74,49,69,45,60,90,90,70,70,110,115,100,75,75,85,86,65,65,75,110,85,68,68,60,45,70,50,50,50,50,50,50,75,80,75,100,90,91,110,150,150,120,80,100,70,100,100,120,100,45,60,75,65,90,110,55,75,95,45,60,45,65,85,41,64,50,75,50,75,50,75,76,116,50,62,80,45,75,55,70,85,55,67,60,110,103,103,75,85,105,50,75,105,120,75,45,55,75,30,40,60,40,60,45,70,70,50,60,95,70,105,105,75,50,70,50,65,72,38,58,54,74,55,75,50,80,40,60,55,75,45,60,70,45,65,110,62,75,36,51,71,60,80,55,50,70,69,114,55,100,165,50,70,44,74,40,60,60,35,65,85,55,75,50,60,60,46,66,76,55,95,70,50,80,109,45,65,77,59,89,45,65,95,70,100,70,110,85,58,52,72,92,55,85,91,91,91,79,79,79,79,100,100,89,89,125,125,125,91,91,100,100,71,56,61,88,40,59,75,41,54,72,38,85,45,62,78,38,45,80,62,86,44,54,78,66,123,67,95,75,62,74,74,45,59,60,60,78,101,62,82,53,86,42,72,50,65,50,71,44,62,58,82,77,123,95,78,67,50,45,68,90,57,43,85,49,44,54,59,65,55,75,85,55,95,40,85,126,126,108,50,50,80,80,80],"xaxis":"x","y":[318,405,525,625,309,405,534,634,634,314,405,530,630,195,205,395,195,205,395,495,251,349,479,579,253,413,262,442,288,438,320,485,300,450,275,365,505,273,365,505,323,483,299,505,270,435,245,455,320,395,490,285,405,305,450,265,405,290,440,320,500,305,455,350,555,300,385,510,310,400,500,590,305,405,505,300,390,490,335,515,300,390,495,410,500,315,490,590,325,465,352,310,460,325,475,325,500,305,525,310,405,500,600,385,328,483,325,475,330,480,325,520,320,425,455,455,385,340,490,345,485,450,435,490,590,295,440,320,450,340,520,460,500,455,490,495,500,600,490,200,540,640,535,288,325,525,525,525,395,355,495,355,495,515,615,540,580,580,580,300,420,600,680,780,780,600,318,405,525,309,405,534,314,405,530,215,415,262,442,265,390,250,390,535,330,460,205,218,210,245,405,320,470,280,365,510,610,490,250,420,410,500,250,340,460,360,180,425,390,210,430,525,525,405,490,435,336,405,455,290,465,415,430,510,610,300,450,430,500,600,505,500,600,430,330,500,250,410,250,450,380,300,480,330,465,465,330,500,600,540,330,500,515,465,250,210,455,305,360,365,490,540,580,580,580,300,410,600,700,680,680,600,310,405,530,630,310,405,530,630,310,405,535,635,220,420,240,420,195,205,395,205,385,220,340,480,220,340,480,270,430,270,430,198,278,518,618,269,414,295,460,280,440,670,266,456,236,240,360,490,237,474,190,375,260,380,380,480,380,480,330,430,530,630,280,410,510,295,475,575,405,405,400,400,400,302,467,305,460,560,400,500,305,460,560,470,330,470,360,290,340,520,335,475,310,490,590,458,458,440,440,288,468,308,468,300,500,355,495,355,495,200,540,420,440,295,455,555,295,455,460,425,465,565,260,300,480,580,290,410,530,345,485,485,485,330,300,420,600,700,300,420,600,700,580,580,580,600,700,600,700,670,770,670,770,680,780,600,600,600,600,600,318,405,525,309,405,534,314,405,530,245,340,485,250,410,194,384,263,363,523,280,515,350,495,350,495,224,424,424,424,424,244,474,405,330,495,275,450,325,475,482,348,498,350,480,580,495,505,310,452,285,329,479,300,500,290,310,220,411,485,300,410,600,700,390,285,525,625,330,525,330,500,300,490,454,330,460,345,334,494,594,510,535,515,535,535,540,540,545,515,525,525,510,530,535,518,618,525,525,480,440,520,520,520,520,520,580,580,580,680,680,600,670,680,680,600,480,600,600,600,600,720,600,308,413,528,308,418,528,308,413,528,255,420,275,370,500,281,446,316,498,316,498,316,498,292,487,264,358,488,295,497,280,390,515,313,425,328,508,445,545,305,405,505,294,384,509,465,465,310,380,500,260,360,485,280,480,280,480,460,292,351,519,315,480,540,461,325,475,348,488,490,303,483,355,495,401,567,329,474,330,510,300,470,290,390,490,290,370,490,305,473,305,395,535,335,475,428,315,495,294,464,335,480,470,319,472,305,489,300,440,520,275,405,515,335,485,275,370,520,320,410,540,305,485,485,305,495,471,350,510,485,303,483,340,490,490,350,510,370,510,484,484,300,420,600,360,550,580,580,580,580,580,580,580,680,680,600,600,660,700,700,580,580,600,600,600,313,405,530,307,409,534,314,405,530,237,423,278,382,499,200,213,411,369,507,303,371,552,350,531,348,495,472,355,466,466,325,448,520,520,341,462,341,480,288,482,306,500,320,494,330,500,289,481,362,521,362,521,525,500,431,500,300,452,600,470,309,474,335,335,335,335,494,494,494,494,304,514,245,535,680,680,600,600,700,600,680,600],"yaxis":"y","type":"histogram"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"xaxis":{"anchor":"y","domain":[0.0,1.0],"title":{"text":"HP"}},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"sum of Total"}},"legend":{"tracegroupgap":0},"title":{"text":"Hit Points"},"barmode":"relative"},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('9bd8ddd4-472d-47cf-9209-33a9f1936d61');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>


## Summary


```python
1.According to my analysis CharizardMega Charizard X and CharizardMega Charizard Y are the strongest of all the Pokémon by total points, including attack, defense, hit points, speed attack and defense, and speed.

2.According to my analysis BeedrillMega Beedrill is the fastest Pokémon according to the speed

3.There is a relationship between speed and strongness, because most of the Pokémon that are strong also has a high speed
```


      Cell In[43], line 1
        1.According to my analysis CharizardMega Charizard X and CharizardMega Charizard Y are the strongest of all the Pokémon by total points, including attack, defense, hit points, speed attack and defense, and speed.
         ^
    SyntaxError: invalid decimal literal


