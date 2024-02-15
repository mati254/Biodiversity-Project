{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Introduction\n",
    "\n",
    "The National Parks Service plays a pivotal role in the preservation and conservation of the diverse ecosystems that make up the natural heritage of the United States. These ecosystems house a rich array of plant and animal species, each with its unique characteristics and conservation status. In this data analysis project, we delve into the vital task of understanding and protecting endangered species within our national parks.\n",
    "\n",
    "## Project Overview\n",
    "\n",
    "For this project, we will analyse data provided by the National Parks Service concerning endangered species in various national parks. Our aim is to uncover insights, patterns, and themes related to the conservation statuses of these species. By conducting data analysis, cleaning, and visualization, we will address questions about which types of species tend to become endangered and seek to answer these questions in a meaningful way."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Import Python Modules\n",
    "Firstly, import modules that will be used to analyse data related to species."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [],
   "source": [
    "import pandas as pd\n",
    "import numpy as np\n",
    "\n",
    "import matplotlib.pyplot as plt\n",
    "import seaborn as sns\n",
    "\n",
    "%matplotlib inline"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Loading the Data"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**species**\n",
    "\n",
    "The `species_info.csv` dataset provides information about different species, including their categories (e.g., Mammal, Bird), scientific names, common names, and conservation statuses. \n",
    "\n",
    "Column Names include:\n",
    "1. category: The category or type of species (e.g., Mammal, Bird).\n",
    "2. scientific_name: The scientific name of the species.\n",
    "3. common_names: Common names of the species.\n",
    "4. conservation_status: The conservation status of the species, which may include values like \"Endangered,\" \"Species of Concern,\" or others."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**observations**\n",
    "The `observations.csv` dataset records observations of various species in different national parks, providing insight into the presence and behavior of these species. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3 (ipykernel)",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.9.13"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
