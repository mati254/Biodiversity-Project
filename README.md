#!/usr/bin/env python
# coding: utf-8

# # Introduction
# 
# The National Parks Service plays a pivotal role in the preservation and conservation of the diverse ecosystems that make up the natural heritage of the United States. These ecosystems house a rich array of plant and animal species, each with its unique characteristics and conservation status. In this data analysis project, we delve into the vital task of understanding and protecting endangered species within our national parks.
# 
# ## Project Overview
# 
# For this project, we will analyse data provided by the National Parks Service concerning endangered species in various national parks. Our aim is to uncover insights, patterns, and themes related to the conservation statuses of these species. By conducting data analysis, cleaning, and visualization, we will address questions about which types of species tend to become endangered and seek to answer these questions in a meaningful way.

# ## Import Python Modules
# Firstly, import modules that will be used to analyse data related to species.

# In[1]:


import pandas as pd
import numpy as np

import matplotlib.pyplot as plt
import seaborn as sns

get_ipython().run_line_magic('matplotlib', 'inline')


# ## Loading the Data

# **species**
# 
# The `species_info.csv` dataset provides information about different species, including their categories (e.g., Mammal, Bird), scientific names, common names, and conservation statuses. 
# 
# Column Names include:
# 1. category: The category or type of species (e.g., Mammal, Bird).
# 2. scientific_name: The scientific name of the species.
# 3. common_names: Common names of the species.
# 4. conservation_status: The conservation status of the species, which may include values like "Endangered," "Species of Concern," or others.

# In[ ]:





# **observations**
# The `observations.csv` dataset records observations of various species in different national parks, providing insight into the presence and behavior of these species. 

# In[ ]:



