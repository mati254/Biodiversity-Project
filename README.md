# Introduction

The National Parks Service plays a pivotal role in the preservation and conservation of the diverse ecosystems that make up the natural heritage of the United States. These ecosystems house a rich array of plant and animal species, each with its unique characteristics and conservation status. In this data analysis project, we delve into the vital task of understanding and protecting endangered species within our national parks.

## Project Overview

For this project, we will analyse data provided by the National Parks Service concerning endangered species in various national parks. Our aim is to uncover insights, patterns, and themes related to the conservation statuses of these species. By conducting data analysis, cleaning, and visualisation, we will address questions about which types of species tend to become endangered and seek to answer these questions in a meaningful way.

## Scoping

Initiating a new project warrants the establishment of a project scope to guide its progression effectively. Four key sections have been outlined below to streamline the project's process and development.

### Project Goals

The primary focus lies in defining high-level objectives and outlining the intentions of the project. As a biodiversity analyst for the National Parks Service, the overarching goal is to ensure the survival of at-risk species and maintain biodiversity levels within the parks. Key objectives include understanding species characteristics, their conservation status, and their relationship with national parks. Several pertinent questions are posed:

- What is the distribution of conservation status for species?
- Are certain types of species more prone to being endangered?
- Are there significant differences between species and their conservation statuses?
- Which animal species are most prevalent, and how are they distributed among parks?

### Data

The project is equipped with two datasets. The first `csv` file contains information about each species, while the second provides observations of species along with park locations. These datasets will serve as the foundation for analysing and achieving the project's goals.

### Analysis

This section encompasses the utilization of descriptive statistics, data visualization techniques, and statistical inference to gain deeper insights into the data. Key metrics to be computed include:

1. distributions
2. counts
3. relationships between species
4. conservation statuses of species
5. observations of species in parks

### Evaluation

In this final section, a comprehensive evaluation of the project's outcomes vis-à-vis the initially outlined goals will be conducted. The analysis will be revisited to ensure alignment with the predefined questions. Reflection on lessons learned, any unanswered questions, limitations, and alternative methodologies will also be addressed to provide a holistic assessment of the project's execution.

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


![output_32_0](https://github.com/mati254/Biodiversity-Project/assets/148381703/84412cae-d714-4380-830d-9ec8db6bb3b7)
    


#### In conservation

The next question is whether specific types of species are more prone to being endangered? This can be answered by creating a new column called `is_protected` and include any species that had a value other than `No Intervention`.


```python
species['is_protected'] = species.conservation_status != 'No Intervention'
```

Following the creation of the new column, we will group the data by `category` and `is_protected` to present a detailed breakdown of each species type and its protection status. The analysis readily indicates that Birds, Vascular Plants, and Mammals exhibit a notably higher count of species under protection.


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



#### Statistical Significance
This section will conduct chi-squared tests to determine if different species exhibit statistically significant differences in conservation status rates. To perform this test, a contingency table will be constructed. The contingency table should be structured as follows:

||protected|not protected|
|-|-|-|
|Mammal|?|?|
|Bird|?|?|


The first chi-squared test, named `contingency1`, will be conducted using the contingency table filled with the correct numbers for mammals and birds. 

The p-value resulting from the chi-squared test is 0.69. The standard threshold for statistical significance is 0.05. As the obtained p-value of 0.69 exceeds this threshold significantly, it indicates that there is no significant relationship between mammals and birds, suggesting that the variables are independent.


```python
from scipy.stats import chi2_contingency

contingency1 = [[30, 146], [75, 413]]
chi2_contingency(contingency1)
```




    (0.1617014831654557,
     0.6875948096661336,
     1,
     array([[ 27.8313253, 148.1686747],
            [ 77.1686747, 410.8313253]]))



For the next chi-squared test, named `contingency2`, the difference between `Reptile` and `Mammal` will be examined. The contingency table format is as follows:

||protected|not protected|
|-|-|-|
|Mammal|?|?|
|Reptile|?|?|

Upon conducting the chi-squared test, the resulting p-value is 0.039. Given that this value is below the standard threshold of 0.05, it suggests that the difference between Reptiles and Mammals is statistically significant. Specifically, Mammals exhibit a statistically significant higher rate of needed protection compared to Reptiles.


```python
contingency2 = [[30, 146], [5, 73]]
chi2_contingency(contingency2)
```




    (4.289183096203645,
     0.03835559022969898,
     1,
     array([[ 24.2519685, 151.7480315],
            [ 10.7480315,  67.2519685]]))



#### Species in parks

The upcoming analysis will utilise data gathered by conservationists, who have been documenting sightings of various species across several national parks over the past 7 days. 

To begin, we'll examine the common names of the `species` to identify the most prevalent animals in the dataset. This involves splitting the data into individual names to gain insights into the species' prevalence.


```python
from itertools import chain
import string

def remove_punctuations(text):
    for punctuation in string.punctuation:
        text = text.replace(punctuation, '')
    return text

common_Names = species[species.category == 'Mammal']\
    .common_names\
    .apply(remove_punctuations)\
    .str.split().tolist()

common_Names[:6]
```




    [['Gappers', 'RedBacked', 'Vole'],
     ['American', 'Bison', 'Bison'],
     ['Aurochs',
      'Aurochs',
      'Domestic',
      'Cattle',
      'Feral',
      'Domesticated',
      'Cattle'],
     ['Domestic', 'Sheep', 'Mouflon', 'Red', 'Sheep', 'Sheep', 'Feral'],
     ['Wapiti', 'Or', 'Elk'],
     ['WhiteTailed', 'Deer']]



The subsequent step involves cleaning up duplicate words within each row of the dataset, as each species should not be counted more than once. This process ensures that each species is accurately represented and avoids overcounting due to duplicates.


```python
cleanRows = []

for item in common_Names:
    item = list(dict.fromkeys(item))
    cleanRows.append(item)
    
cleanRows[:6]
```




    [['Gappers', 'RedBacked', 'Vole'],
     ['American', 'Bison'],
     ['Aurochs', 'Domestic', 'Cattle', 'Feral', 'Domesticated'],
     ['Domestic', 'Sheep', 'Mouflon', 'Red', 'Feral'],
     ['Wapiti', 'Or', 'Elk'],
     ['WhiteTailed', 'Deer']]



After removing duplicate words, the next step is to collapse the individual words into a single list. This consolidation simplifies the dataset, making it more manageable and conducive to further analysis.


```python
res = list(chain.from_iterable(i if isinstance(i, list) else [i] for i in cleanRows))
res[:6]
```




    ['Gappers', 'RedBacked', 'Vole', 'American', 'Bison', 'Aurochs']



Now that the data has been prepared, we can proceed to count the occurrences of each word. Initial analysis reveals that `Bat` appeared 23 times, while `Shrew` was recorded 18 times.


```python
words_counted = []

for i in res:
    x = res.count(i)
    words_counted.append((i,x))

pd.DataFrame(set(words_counted), columns =['Word', 'Count']).sort_values("Count", ascending = False).head(10)
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
      <th>Word</th>
      <th>Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>120</th>
      <td>Bat</td>
      <td>23</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shrew</td>
      <td>18</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Myotis</td>
      <td>17</td>
    </tr>
    <tr>
      <th>99</th>
      <td>Mouse</td>
      <td>16</td>
    </tr>
    <tr>
      <th>54</th>
      <td>Chipmunk</td>
      <td>13</td>
    </tr>
    <tr>
      <th>144</th>
      <td>Squirrel</td>
      <td>12</td>
    </tr>
    <tr>
      <th>105</th>
      <td>American</td>
      <td>12</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Eastern</td>
      <td>11</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Vole</td>
      <td>11</td>
    </tr>
    <tr>
      <th>115</th>
      <td>Western</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>



In the dataset, various scientific names may refer to different types of bats. The subsequent task involves identifying which rows correspond to bats. To accomplish this, a new column consisting of boolean values will be created to indicate whether `is_bat` is `True`.


```python
species['is_bat'] = species.common_names.str.contains(r"\bBat\b", regex = True)

species.head(10)
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
      <th>is_protected</th>
      <th>is_bat</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Mammal</td>
      <td>Clethrionomys gapperi gapperi</td>
      <td>Gapper's Red-Backed Vole</td>
      <td>No Intervention</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mammal</td>
      <td>Bos bison</td>
      <td>American Bison, Bison</td>
      <td>No Intervention</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mammal</td>
      <td>Bos taurus</td>
      <td>Aurochs, Aurochs, Domestic Cattle (Feral), Dom...</td>
      <td>No Intervention</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mammal</td>
      <td>Ovis aries</td>
      <td>Domestic Sheep, Mouflon, Red Sheep, Sheep (Feral)</td>
      <td>No Intervention</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Mammal</td>
      <td>Cervus elaphus</td>
      <td>Wapiti Or Elk</td>
      <td>No Intervention</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Mammal</td>
      <td>Odocoileus virginianus</td>
      <td>White-Tailed Deer</td>
      <td>No Intervention</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Mammal</td>
      <td>Sus scrofa</td>
      <td>Feral Hog, Wild Pig</td>
      <td>No Intervention</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Mammal</td>
      <td>Canis latrans</td>
      <td>Coyote</td>
      <td>Species of Concern</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Mammal</td>
      <td>Canis lupus</td>
      <td>Gray Wolf</td>
      <td>Endangered</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Mammal</td>
      <td>Canis rufus</td>
      <td>Red Wolf</td>
      <td>Endangered</td>
      <td>True</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



Below is a subset of the data where `is_bat` is true, indicating species that are bats. As observed, there are numerous species of bats present in the dataset, encompassing both protected and non-protected species.


```python
species[species.is_bat]
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
      <th>is_protected</th>
      <th>is_bat</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>28</th>
      <td>Mammal</td>
      <td>Corynorhinus rafinesquii</td>
      <td>Rafinesque's Big-Eared Bat</td>
      <td>No Intervention</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Mammal</td>
      <td>Eptesicus fuscus</td>
      <td>Big Brown Bat</td>
      <td>Species of Concern</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Mammal</td>
      <td>Lasionycteris noctivagans</td>
      <td>Silver-Haired Bat</td>
      <td>Species of Concern</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Mammal</td>
      <td>Lasiurus borealis</td>
      <td>Eastern Red Bat, Red Bat</td>
      <td>No Intervention</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Mammal</td>
      <td>Lasiurus cinereus</td>
      <td>Hoary Bat</td>
      <td>No Intervention</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Mammal</td>
      <td>Myotis leibii</td>
      <td>Eastern Small-Footed Bat, Eastern Small-Footed...</td>
      <td>Species of Concern</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Mammal</td>
      <td>Myotis lucifugus</td>
      <td>Little Brown Bat, Little Brown Myotis</td>
      <td>Species of Concern</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Mammal</td>
      <td>Myotis septentrionalis</td>
      <td>Northern Long-Eared Bat, Northern Myotis</td>
      <td>Threatened</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Mammal</td>
      <td>Myotis sodalis</td>
      <td>Indiana Bat, Indiana Or Social Myotis</td>
      <td>Endangered</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Mammal</td>
      <td>Nycticeius humeralis</td>
      <td>Evening Bat</td>
      <td>No Intervention</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3033</th>
      <td>Mammal</td>
      <td>Antrozous pallidus</td>
      <td>Pallid Bat, Pallid Bat</td>
      <td>Species of Concern</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3034</th>
      <td>Mammal</td>
      <td>Corynorhinus townsendii</td>
      <td>Mule-Eared Bat, Pacific Townsend's Big-Eared B...</td>
      <td>No Intervention</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3035</th>
      <td>Mammal</td>
      <td>Eptesicus fuscus</td>
      <td>Big Brown Bat, Big Brown Bat</td>
      <td>Species of Concern</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3036</th>
      <td>Mammal</td>
      <td>Euderma maculatum</td>
      <td>Spotted Bat, Spotted Bat</td>
      <td>Species of Concern</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3037</th>
      <td>Mammal</td>
      <td>Lasionycteris noctivagans</td>
      <td>Silver-Haired Bat, Silver-Haired Bat</td>
      <td>Species of Concern</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3038</th>
      <td>Mammal</td>
      <td>Lasiurus cinereus</td>
      <td>Hoary Bat, Hoary Bat</td>
      <td>No Intervention</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3040</th>
      <td>Mammal</td>
      <td>Myotis ciliolabrum</td>
      <td>Small-Footed Myotis, Western Small-Footed Bat,...</td>
      <td>No Intervention</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3042</th>
      <td>Mammal</td>
      <td>Myotis lucifugus</td>
      <td>Little Brown Bat, Little Brown Myotis, Little ...</td>
      <td>Species of Concern</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4461</th>
      <td>Mammal</td>
      <td>Eumops perotis</td>
      <td>Western Mastiff Bat</td>
      <td>No Intervention</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4462</th>
      <td>Mammal</td>
      <td>Tadarida brasiliensis</td>
      <td>Mexican Free-Tailed Bat</td>
      <td>No Intervention</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4463</th>
      <td>Mammal</td>
      <td>Corynorhinus townsendii</td>
      <td>Townsend's Big-Eared Bat</td>
      <td>No Intervention</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4464</th>
      <td>Mammal</td>
      <td>Lasiurus blossevillii</td>
      <td>Western Red Bat</td>
      <td>Species of Concern</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4468</th>
      <td>Mammal</td>
      <td>Parastrellus hesperus</td>
      <td>Canyon Bat</td>
      <td>No Intervention</td>
      <td>False</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



The next step involves merging the results of the bat species with `observations` to create a `DataFrame` containing observations of bats across the four national parks. This merged `DataFrame` will provide comprehensive insights into the sightings of bats within the national parks.


```python
bat_observations = observations.merge(species[species.is_bat])
bat_observations
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
      <th>category</th>
      <th>common_names</th>
      <th>conservation_status</th>
      <th>is_protected</th>
      <th>is_bat</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Lasiurus blossevillii</td>
      <td>Bryce National Park</td>
      <td>113</td>
      <td>Mammal</td>
      <td>Western Red Bat</td>
      <td>Species of Concern</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Lasiurus blossevillii</td>
      <td>Great Smoky Mountains National Park</td>
      <td>70</td>
      <td>Mammal</td>
      <td>Western Red Bat</td>
      <td>Species of Concern</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Lasiurus blossevillii</td>
      <td>Yosemite National Park</td>
      <td>123</td>
      <td>Mammal</td>
      <td>Western Red Bat</td>
      <td>Species of Concern</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Lasiurus blossevillii</td>
      <td>Yellowstone National Park</td>
      <td>221</td>
      <td>Mammal</td>
      <td>Western Red Bat</td>
      <td>Species of Concern</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Corynorhinus rafinesquii</td>
      <td>Yosemite National Park</td>
      <td>188</td>
      <td>Mammal</td>
      <td>Rafinesque's Big-Eared Bat</td>
      <td>No Intervention</td>
      <td>False</td>
      <td>True</td>
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
    </tr>
    <tr>
      <th>139</th>
      <td>Myotis sodalis</td>
      <td>Yellowstone National Park</td>
      <td>68</td>
      <td>Mammal</td>
      <td>Indiana Bat, Indiana Or Social Myotis</td>
      <td>Endangered</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>140</th>
      <td>Myotis leibii</td>
      <td>Yosemite National Park</td>
      <td>132</td>
      <td>Mammal</td>
      <td>Eastern Small-Footed Bat, Eastern Small-Footed...</td>
      <td>Species of Concern</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>141</th>
      <td>Myotis leibii</td>
      <td>Bryce National Park</td>
      <td>84</td>
      <td>Mammal</td>
      <td>Eastern Small-Footed Bat, Eastern Small-Footed...</td>
      <td>Species of Concern</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>142</th>
      <td>Myotis leibii</td>
      <td>Great Smoky Mountains National Park</td>
      <td>49</td>
      <td>Mammal</td>
      <td>Eastern Small-Footed Bat, Eastern Small-Footed...</td>
      <td>Species of Concern</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>143</th>
      <td>Myotis leibii</td>
      <td>Yellowstone National Park</td>
      <td>233</td>
      <td>Mammal</td>
      <td>Eastern Small-Footed Bat, Eastern Small-Footed...</td>
      <td>Species of Concern</td>
      <td>True</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
<p>144 rows × 8 columns</p>
</div>



Here's the table displaying the total number of bat observations made at each national park over the past 7 days.

As indicated, Yellowstone National Park recorded the highest number of bat observations with 8,362, while the Great Smoky Mountains National Park had the lowest with 2,411 observations.


```python
bat_observations.groupby('park_name').observations.sum().reset_index()
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
      <th>park_name</th>
      <th>observations</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bryce National Park</td>
      <td>3433</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Great Smoky Mountains National Park</td>
      <td>2411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Yellowstone National Park</td>
      <td>8362</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Yosemite National Park</td>
      <td>4786</td>
    </tr>
  </tbody>
</table>
</div>



Here's the breakdown of each park by sightings of protected bats vs. non-protected bats. As noted, every park except for the Great Smoky Mountains National Park has more sightings of protected bats than non-protected bats. This observation could indeed be considered a positive sign for bat populations.


```python
obs_by_park = bat_observations.groupby(['park_name', 'is_protected']).observations.sum().reset_index()
obs_by_park
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
      <th>park_name</th>
      <th>is_protected</th>
      <th>observations</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bryce National Park</td>
      <td>False</td>
      <td>1596</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bryce National Park</td>
      <td>True</td>
      <td>1837</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Great Smoky Mountains National Park</td>
      <td>False</td>
      <td>1299</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Great Smoky Mountains National Park</td>
      <td>True</td>
      <td>1112</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Yellowstone National Park</td>
      <td>False</td>
      <td>4044</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Yellowstone National Park</td>
      <td>True</td>
      <td>4318</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Yosemite National Park</td>
      <td>False</td>
      <td>2345</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Yosemite National Park</td>
      <td>True</td>
      <td>2441</td>
    </tr>
  </tbody>
</table>
</div>



The plot generated from the last data manipulation illustrates a notable trend. Yellowstone and Bryce National Parks appear to excel in their conservation efforts for bat populations, as there are more sightings of protected bats compared to non-protected species. However, the data suggests that the Great Smoky Mountains National Park may need to enhance its conservation efforts, as it has observed more sightings of non-protected species.


```python
plt.figure(figsize=(16, 4))
sns.barplot(x=obs_by_park.park_name, y= obs_by_park.observations, hue=obs_by_park.is_protected)
plt.xlabel('National Parks')
plt.ylabel('Number of Observations')
plt.title('Observations of Bats per Week')
plt.show()
```

 ![output_63_0](https://github.com/mati254/Biodiversity-Project/assets/148381703/28c64a51-52d0-49ae-928f-acddc13f0662)



## Conclusions

The project successfully conducted various data visualizations and made inferences about the different species present in four National Parks within the dataset.

Key Findings:

- Distribution of Conservation Status: The majority of species (5,633 out of 5,824) were not categorised as part of any conservation program, indicating that conservation efforts may not be widespread across all species.

- Likelihood of Endangerment: Mammals and Birds showed the highest percentage of being under protection, suggesting they are more likely to be considered endangered or in need of conservation measures.

- Significant Differences in Conservation Status: While there wasn't a significant difference in conservation percentage between mammals and birds, a statistically significant difference was observed between mammals and reptiles.

- Prevalence and Distribution of Species: Bats were the most prevalent species, and they were predominantly found in Yellowstone National Park.

Overall, the project provided valuable insights into species distribution, conservation statuses, and prevalence across the National Parks, shedding light on potential conservation priorities and areas for further research and action.

## Further Research Suggestions

 - Longitudinal Analysis: Analysing changes in the conservation status of various species over time would provide valuable insights into trends and patterns. Collecting data over longer periods would allow for the examination of how conservation efforts impact species populations and statuses.

 - Area of National Parks: Incorporating information about the size of each national park would provide context for interpreting observations and biodiversity. Understanding the area of each park relative to the number of observations and species richness could yield insights into habitat diversity and conservation needs.

 - Spatial Analysis: Recording precise locations of species sightings would enable spatial analysis to determine if observations are clustered in specific areas within the parks. This analysis could identify hotspots of biodiversity and inform conservation strategies focused on preserving critical habitats.

Addressing these areas of further research would enhance our understanding of species dynamics within national parks and contribute to more informed conservation management practices.
