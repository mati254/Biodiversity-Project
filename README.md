# Introduction

The National Parks Service plays a pivotal role in the preservation and conservation of the diverse ecosystems that make up the natural heritage of the United States. These ecosystems house a rich array of plant and animal species, each with its unique characteristics and conservation status. In this data analysis project, we delve into the vital task of understanding and protecting endangered species within our national parks.

## Project Overview

For this project, we will analyse data provided by the National Parks Service concerning endangered species in various national parks. Our aim is to uncover insights, patterns, and themes related to the conservation statuses of these species. By conducting data analysis, cleaning, and visualisation, we will address questions about which types of species tend to become endangered and seek to answer these questions in a meaningful way.

## Scoping

### Project Goals

### Data

### Analysis

### Evaluation



## Import Python Modules
Firstly, import the primary modules that will be used to analyse data in this project:


```python
import pandas as pd
import numpy as np

import matplotlib.pyplot as plt
import seaborn as sns

%matplotlib inline
```

## Loading the Data

To analyse the status of conservation of species and their observations in national parks, load the datasets into `DataFrames`. Once loaded as `DataFrames` the data can be explored and visualised with Python.

In the next steps, `Observations.csv` and `Species_info.csv` are read in as `DataFrames` called `observations` and `species` respectively. The newly created `DataFrames` are glimpsed with `.head()` to check its contents.

**species**

The `species_info.csv` dataset provides information about different species in the National Parks. 

Column Names include:
- **category**: The category or type of species (e.g., Mammal, Bird).
- **scientific_name**: The scientific name of the species.
- **common_names**: The common names of the species.
- **conservation_status**: The conservation status of the species, which may include values like "Endangered," "Species of Concern," or others.


```python
species = pd.read_csv('species_info.csv', encoding='utf-8')
species.head()
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
      <th>category</th>
      <th>scientific_name</th>
      <th>common_names</th>
      <th>conservation_status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Mammal</td>
      <td>Clethrionomys gapperi gapperi</td>
      <td>Gapper's Red-Backed Vole</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mammal</td>
      <td>Bos bison</td>
      <td>American Bison, Bison</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mammal</td>
      <td>Bos taurus</td>
      <td>Aurochs, Aurochs, Domestic Cattle (Feral), Dom...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mammal</td>
      <td>Ovis aries</td>
      <td>Domestic Sheep, Mouflon, Red Sheep, Sheep (Feral)</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Mammal</td>
      <td>Cervus elaphus</td>
      <td>Wapiti Or Elk</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



**observations**

The `observations.csv` dataset records observations of various species in different national parks in the past 7 days. 

Column Names include:
- **scientific_name**: 
- **park_name**: 
- **observations**: 


```python
observations = pd.read_csv('observations.csv')
observations.head()
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
      <th>scientific_name</th>
      <th>park_name</th>
      <th>observations</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Vicia benghalensis</td>
      <td>Great Smoky Mountains National Park</td>
      <td>68</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Neovison vison</td>
      <td>Great Smoky Mountains National Park</td>
      <td>77</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Prunus subcordata</td>
      <td>Yosemite National Park</td>
      <td>138</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Abutilon theophrasti</td>
      <td>Bryce National Park</td>
      <td>84</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Githopsis specularioides</td>
      <td>Great Smoky Mountains National Park</td>
      <td>85</td>
    </tr>
  </tbody>
</table>
</div>



#### Data characteristics

Now, we will check the dimensions of the data sets, for `species` there are 5,824 rows and 4 columns while `observations` has 23,296 rows and 3 columns.


```python
print(f"species shape: {species.shape}")
print(f"observations shape: {observations.shape}")
```

    species shape: (5824, 4)
    observations shape: (23296, 3)


## Explore the data

Let's delve deeper into the `species` data. Let's begin by determining the count of unique species within the dataset. Use the `scientific_name` column to identify 5,541 distinct species. It appears that the national parks host a diverse array of species!


```python
print(f"number of species: {species.scientific_name.nunique()}")
```

    number of species: 5541


Next, let's move to identify the number of categories represented in the dataset. There are a total of seven categories, including both animals and plants.


```python
print(f"number of categories: {species.category.nunique()}")
print(f"categories: {species.category.unique()}")
```

    number of categories: 7
    categories: ['Mammal' 'Bird' 'Reptile' 'Amphibian' 'Fish' 'Vascular Plant'
     'Nonvascular Plant']


Let's further investigate by examining the count of each `category` within the dataset. Vascular plants dominate with 4,470 species, making them the most abundant, while reptiles are the least numerous, with only 79 species.


```python
species.groupby("category").size()
```




    category
    Amphibian              80
    Bird                  521
    Fish                  127
    Mammal                214
    Nonvascular Plant     333
    Reptile                79
    Vascular Plant       4470
    dtype: int64



We can also explore the `conservation_status` column, which comprises four categories: `Species of Concern`, `Endangered`, `Threatened`, and `In Recovery`, in addition to `NaN` values.


```python
print(f"number of conservation statuses: {species.conservation_status.nunique()}")
print(f"unique conservation statuses: {species.conservation_status.unique()}")
```

    number of conservation statuses: 4
    unique conservation statuses: [nan 'Species of Concern' 'Endangered' 'Threatened' 'In Recovery']





```python

```


```python

```


```python

```
