---
title: Maps
---

```python
#Importing all necessary libraries

!pip install --upgrade pyshp
!pip install --upgrade shapely
!pip install --upgrade descartes
!pip install plotly-geo
!pip install -c plotly plotly-geo
!pip install plotly-geo
!pip install plotly==4.8.0



from urllib.request import urlopen
import pandas as pd
import matplotlib.pyplot as plt
from plotly import graph_objects
import plotly.figure_factory as ff
import json

with urlopen('https://raw.githubusercontent.com/plotly/datasets/master/geojson-counties-fips.json') as response:
    counties = json.load(response)
```

```python
newer_pd = pd.read_csv("https://raw.githubusercontent.com/aditisingh2019/cdc2021/main/datasets/uninsured_census.csv",dtype={'FIPS Code':str})

#df['p'] = np.where(df['hours'] < 1, df['hours'], df['$']/df['hours'])

newer_pd['AA_FEMALE']/newer_pd['TOT_POP']

l = ['WA_MALE', 'WA_FEMALE', 'BA_MALE', 'BA_FEMALE', 'IA_MALE', 'IA_FEMALE',
       'AA_MALE', 'AA_FEMALE', 'NA_MALE', 'NA_FEMALE', 'TOM_MALE',
       'TOM_FEMALE', 'WAC_MALE', 'WAC_FEMALE', 'BAC_MALE', 'BAC_FEMALE',
       'IAC_MALE', 'IAC_FEMALE', 'AAC_MALE', 'AAC_FEMALE', 'NAC_MALE',
       'NAC_FEMALE', 'NH_MALE', 'NH_FEMALE', 'NHWA_MALE', 'NHWA_FEMALE',
       'NHBA_MALE', 'NHBA_FEMALE', 'NHIA_MALE', 'NHIA_FEMALE', 'NHAA_MALE',
       'NHAA_FEMALE', 'NHNA_MALE', 'NHNA_FEMALE', 'NHTOM_MALE', 'NHTOM_FEMALE',
       'NHWAC_MALE', 'NHWAC_FEMALE', 'NHBAC_MALE', 'NHBAC_FEMALE',
       'NHIAC_MALE', 'NHIAC_FEMALE', 'NHAAC_MALE', 'NHAAC_FEMALE',
       'NHNAC_MALE', 'NHNAC_FEMALE', 'H_MALE', 'H_FEMALE', 'HWA_MALE',
       'HWA_FEMALE', 'HBA_MALE', 'HBA_FEMALE', 'HIA_MALE', 'HIA_FEMALE',
       'HAA_MALE', 'HAA_FEMALE', 'HNA_MALE', 'HNA_FEMALE', 'HTOM_MALE',
       'HTOM_FEMALE', 'HWAC_MALE', 'HWAC_FEMALE', 'HBAC_MALE', 'HBAC_FEMALE',
       'HIAC_MALE', 'HIAC_FEMALE', 'HAAC_MALE', 'HAAC_FEMALE', 'HNAC_MALE',
       'HNAC_FEMALE']

for i in l:
  newer_pd[i] = newer_pd[i]/newer_pd['TOT_POP']



his_l = ['HWA_MALE',
       'HWA_FEMALE', 'HBA_MALE', 'HBA_FEMALE', 'HIA_MALE', 'HIA_FEMALE',
       'HAA_MALE', 'HAA_FEMALE', 'HNA_MALE', 'HNA_FEMALE', 'HTOM_MALE',
       'HTOM_FEMALE', 'HWAC_MALE', 'HWAC_FEMALE', 'HBAC_MALE', 'HBAC_FEMALE',
       'HIAC_MALE', 'HIAC_FEMALE', 'HAAC_MALE', 'HAAC_FEMALE', 'HNAC_MALE',
       'HNAC_FEMALE']



newer_pd["TOT_H"] = newer_pd['H_MALE']+newer_pd['H_FEMALE']
newer_pd["TOT_IA"] = newer_pd['IA_MALE']+newer_pd['IA_FEMALE']+newer_pd['HIA_MALE']+newer_pd['HIA_FEMALE']+newer_pd['HIAC_MALE']+newer_pd['HIAC_FEMALE']

print(newer_pd["TOT_H"])

newer_pd['TOT_H']
```

    0       0.029909
    1       0.047188
    2       0.045248
    3       0.027820
    4       0.096531
              ...
    3100    0.159932
    3101    0.151466
    3102    0.092505
    3103    0.141960
    3104    0.041143
    Name: TOT_H, Length: 3105, dtype: float64





    0       0.029909
    1       0.047188
    2       0.045248
    3       0.027820
    4       0.096531
              ...
    3100    0.159932
    3101    0.151466
    3102    0.092505
    3103    0.141960
    3104    0.041143
    Name: TOT_H, Length: 3105, dtype: float64

```python
import plotly.express as px

fig = px.choropleth_mapbox(newer_pd, geojson=counties, locations='FIPS Code', color='TOT_H',
                           color_continuous_scale=["#fffff0","#ff1e04"],
                           range_color=(0, 1),                           mapbox_style="carto-positron",
                           zoom=2.5, center = {"lat": 37.0902, "lon": -95.7129},
                           opacity=0.5,
                           labels={'Percent Uninsured':'Percent Uninsured', 'TOT_H':'Total Hispanic Population'}
                          )

fig.update_layout(margin={"r":0,"t":0,"l":0,"b":0})
fig.show()
```

![png]({{site.baseurl}}/assets/Maps_images/newplot4.png)

```python
import plotly.express as px

fig = px.choropleth_mapbox(newer_pd, geojson=counties, locations='FIPS Code', color='TOT_IA',
                           color_continuous_scale=["#fffff0","#006400"],
                           range_color=(0, .5),                           mapbox_style="carto-positron",
                           zoom=2.5, center = {"lat": 37.0902, "lon": -95.7129},
                           opacity=0.5,
                           labels={'Percent Uninsured':'Percent Uninsured', 'TOT_IA':'Total Indigenous Population'}
                          )

fig.update_layout(margin={"r":0,"t":0,"l":0,"b":0})
fig.show()
```

![png]({{site.baseurl}}/assets/Maps_images/newplot3.png)

```python
import plotly.express as px

fig = px.choropleth_mapbox(newer_pd, geojson=counties, locations='FIPS Code', color='Percent Uninsured',
                           color_continuous_scale=["#FFA500","#000064"],
                           range_color=(0, .3),                           mapbox_style="carto-positron",
                           zoom=2.5, center = {"lat": 37.0902, "lon": -95.7129},
                           opacity=0.5,
                           labels={'Percent Uninsured':'Percent Uninsured', 'NoEd':'% of People Without HS diploma'}
                          )

fig.update_layout(margin={"r":0,"t":0,"l":0,"b":0})
fig.show()
```

![png]({{site.baseurl}}/assets/Maps_images/newplot2.png)

```python
import plotly.express as px

fig = px.choropleth_mapbox(newer_pd, geojson=counties, locations='FIPS Code', color='NoEd',
                           color_continuous_scale=["#fffff0","#000064"],
                           range_color=(0, 50),                           mapbox_style="carto-positron",
                           zoom=2.5, center = {"lat": 37.0902, "lon": -95.7129},
                           opacity=0.5,
                           labels={'Percent Uninsured':'Percent Uninsured', 'NoEd':'% of People w/o HS Diploma'}
                          )

fig.update_layout(margin={"r":0,"t":0,"l":0,"b":0})
fig.show()
```

![png]({{site.baseurl}}/assets/Maps_images/newplot.png)
