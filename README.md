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
- **scientific_name**: The scientific name assigned to each species.
- **park_name**: The name of the national park where the observations were made.
- **observations**: The count of observations recorded for each species within the specified national park over the past 7 days.


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


Let's proceed by conducting a count of the number of observations within each category of the `conservation_status.` There are 5,633 `NaN` values, indicating species without conservation concerns. In contrast, there are 161 species of concern, 16 endangered, 10 threatened, and 4 in recovery. It's important to note that in this context, the presence of `NaN` values signifies that these species do not currently have any assigned conservation status.


```python
print(f"NaN values: {species.conservation_status.isna().sum()}")
print(species.groupby("conservation_status").size())
```

    NaN values: 5633
    conservation_status
    Endangered             16
    In Recovery             4
    Species of Concern    161
    Threatened             10
    dtype: int64


#### observations

In the `observations` data section, let's begin by determining the number of parks present in the dataset. It appears that there are only four national parks included in the `observations` data.


```python
print(f"number of parks: {observations.park_name.nunique()}")
print(f"unique parks: {observations.park_name.unique()}")
```

    number of parks: 4
    unique parks: ['Great Smoky Mountains National Park' 'Yosemite National Park'
     'Bryce National Park' 'Yellowstone National Park']


The total number of observations logged in the parks is substantial, reaching 3,314,739 sightings in the last 7 days. This signifies a considerable volume of recorded observations!


```python
print(f"number of observations: {observations.observations.sum()}")
```

    number of observations: 3314739


## Analysis

In this phase of the analysis, the focus is on cleaning and exploring the `conservation_status` column in the `species` dataset. The `conservation_status` column contains various values, such as:

 - `Species of Concern`: declining or appear to be in need of conservation
 - `Threatened`: vulnerable to endangerment in the near future
 - `Endangered`: seriously at risk of extinction
 - `In Recovery`: formerly `Endangered`, but currently neither in danger of extinction throughout all or a significant portion of its range
 
During the initial exploration, numerous `NaN` values were identified. To address this, these `NaN` values will be converted to `No Intervention` for clarity and completeness in the analysis.


```python
species.fillna('No Intervention', inplace = True)
species.groupby("conservation_status").size()
```




    conservation_status
    Endangered              16
    In Recovery              4
    No Intervention       5633
    Species of Concern     161
    Threatened              10
    dtype: int64



Now, let's delve into the various categories nested within the `conservation_status` column, excluding those species that do not necessitate intervention. Below, you'll find both a table and a chart for exploration.

Examining the species classified as `Endangered`, we observe 7 mammals and 4 birds. In the `In Recovery` status, there are 3 birds and 1 mammal. This observation suggests a potential trend wherein birds might be experiencing a more pronounced recovery compared to mammals.


```python
conservationCategory = species[species.conservation_status != "No Intervention"]\
    .groupby(["conservation_status", "category"])["scientific_name"].count().unstack()

conservationCategory
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
      <th>category</th>
      <th>Amphibian</th>
      <th>Bird</th>
      <th>Fish</th>
      <th>Mammal</th>
      <th>Nonvascular Plant</th>
      <th>Reptile</th>
      <th>Vascular Plant</th>
    </tr>
    <tr>
      <th>conservation_status</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Endangered</th>
      <td>1.0</td>
      <td>4.0</td>
      <td>3.0</td>
      <td>7.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>In Recovery</th>
      <td>NaN</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Species of Concern</th>
      <td>4.0</td>
      <td>72.0</td>
      <td>4.0</td>
      <td>28.0</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>43.0</td>
    </tr>
    <tr>
      <th>Threatened</th>
      <td>2.0</td>
      <td>NaN</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
ax = conservationCategory.plot(kind = "bar", stacked = True, figsize = (8,6))
ax.set_xlabel("Conservation Status")
ax.set_ylabel("Number of Species");
```


    
![png](output_32_0.png)
    


#### In conservation

The next question is whether specific types of species are more prone to being endangered? This can be answered by creating a new column called `is_protected` and include any species that had a value other than `No Intervention`.


```python
species['is_protected'] = species.conservation_status != 'No Intervention'
```

Following the creation of the new column, we will group the data by category and `is_protected` to present a detailed breakdown of each species type and its protection status. The analysis readily indicates that Birds, Vascular Plants, and Mammals exhibit a notably higher count of species under protection.


```python
category_counts = species.groupby(["category", "is_protected"])\
                        .scientific_name.nunique().reset_index()\
                        .pivot(columns = 'is_protected',
                              index = 'category',
                              values = 'scientific_name')\
                        .reset_index()
category_counts.columns = ['category', 'not_protected', 'protected']

category_counts
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
      <th>not_protected</th>
      <th>protected</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Amphibian</td>
      <td>72</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bird</td>
      <td>413</td>
      <td>75</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Fish</td>
      <td>115</td>
      <td>11</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mammal</td>
      <td>146</td>
      <td>30</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nonvascular Plant</td>
      <td>328</td>
      <td>5</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Reptile</td>
      <td>73</td>
      <td>5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Vascular Plant</td>
      <td>4216</td>
      <td>46</td>
    </tr>
  </tbody>
</table>
</div>



Focusing on absolute numbers may not always provide the most informative statistics. Hence, it becomes crucial to compute the protection rate for each `category` within the dataset. Through this analysis, it becomes evident that approximately 17 percent of mammals and around 15 percent of birds are under protection.


```python
category_counts['percent_protected'] = round(category_counts.protected / \
                                          (category_counts.not_protected + category_counts.protected) * 100, 2)

category_counts
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
      <th>not_protected</th>
      <th>protected</th>
      <th>percent_protected</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Amphibian</td>
      <td>72</td>
      <td>7</td>
      <td>8.86</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bird</td>
      <td>413</td>
      <td>75</td>
      <td>15.37</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Fish</td>
      <td>115</td>
      <td>11</td>
      <td>8.73</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mammal</td>
      <td>146</td>
      <td>30</td>
      <td>17.05</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nonvascular Plant</td>
      <td>328</td>
      <td>5</td>
      <td>1.50</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Reptile</td>
      <td>73</td>
      <td>5</td>
      <td>6.41</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Vascular Plant</td>
      <td>4216</td>
      <td>46</td>
      <td>1.08</td>
    </tr>
  </tbody>
</table>
</div>






```python

```
