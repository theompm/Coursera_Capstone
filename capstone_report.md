### Report

# Capstone Project - The Battle of Neighborhoods

Matthäus Morhart
  
March 2021

## Introduction

Munich is the capital of bavaria. It is a global centre of:

- art
- science
- technology
- finance
- publishing
- culture
- innovation
- education
- business
- tourism

Because of these attributes a friend of mine decided moving to munich. He asked me helping him choosing the right district to live in.


## Data

### Data Sources
The first dataset is from [https://www.dasoertliche.de](https://www.dasoertliche.de/Themen/Postleitzahlen/M%C3%BCnchen.html).

Including:

- postal code
- town name
- district
- borough
- state


```python
import pandas as pd 

url = 'https://www.dasoertliche.de/Themen/Postleitzahlen/M%C3%BCnchen.html'
df = pd.read_html(url, flavor='bs4')[0]

df.head()
```
|PLZ|Ortsname|Ortsteil|Landkreis|Bundesland|
|---|--------|--------|---------|----------|
|80331 	|München 	|AltstadtIsarvorstadtLehelLudwigsvorstadt 	  |Stadt München 	|Bayern|
|80333 	|München 	|AltstadtMaxvorstadtSchwabing-West 	          |Stadt München 	|Bayern|
|80335 	|München 	|AltstadtLudwigsvorstadtMaxvorstadtNeuhausen 	|Stadt München 	|Bayern|
|80336 	|München 	|AltstadtIsarvorstadtLudwigsvorstadtSendling 	|Stadt München 	|Bayern|
|80337 	|München 	|IsarvorstadtLudwigsvorstadtSendling 	        |Stadt München 	|Bayern|

The next code creates a new column *location*.
```python
df['location'] = df.Bundesland + ', ' + df.Ortsname + ', ' + df.PLZ.astype(str)
```
Possible output of column *location*:

`Bayern, München, 80331`

With *Nominatim* through the library *geopandas* we will get the centered geographical coordinates of districts.

```python
import geopandas as gpd

user_agent = 'coursera_capstone_munich'

gdf = gpd.tools.geocode(df.location, provider='nominatim', user_agent=user_agent)
```
|geometry|address|
|--------|-------|
|POINT (11.57344 48.13606)|Altstadt-Lehel, München, Bayern, 80331, Deutschland|

Get the venues from *Foursquare API* searching by coordinates.

With this data we will create a map and information chart of clusters to solve the problem.

### Data Cleaning

The following rows were selected by including *Stadt München* and excluding *Flughafen-München*.

```python
df = df.loc[df.Landkreis == 'Stadt München']
df = df.loc[~(df.Ortsname == 'München-Flughafen')].reset_index(drop=True)
```

## Methodology

After merging all dataframes and using OneHotEncoder to binarize the venues categories, we used *KMeans* from *sklearn.cluster* to cluster the entries into 5 clusters.

This made the following clusters in decreasing order:

|Cluster Labels    |   1 |   0 |   2 |   3 |   4 |
|:---------------|----:|----:|----:|----:|----:|
| n |  35 |  22 |   8 |   8 |   1 |


## Results

## Discussion

## Conclusion
