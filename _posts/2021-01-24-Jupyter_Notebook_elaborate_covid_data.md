---
layout: post
title: Jupyter Notebook Example to Elaborates COVID Italian Data
date: '2021-01-24T16:40:00.000-08:00'
author: MaX
tags:
- Python
- Jupyter
- Notebook
- COVID-19
- Development
- Data Science
modified_time: '2021-01-24T17:04:42.898-08:00'
---


# Elaborate Covid-19 Italian Data
Very simple notebook example that shows how to load data from a CSV, leverage panda's Dataframes tocalculate few extra columns with Covid Pandemic KPIs and then display it using Plotly 




```python
# Import Global Libraries
import pandas as pd
import numpy as np
import io
import requests


```

### Load Data
The data are downloaded from the Italian "Protezione Civile" Covid Data repository on github https://github.com/pcm-dpc/COVID-19


```python
url='https://raw.githubusercontent.com/pcm-dpc/COVID-19/master/dati-andamento-nazionale/dpc-covid19-ita-andamento-nazionale.csv'
s = requests.get(url).text
df = pd.read_csv(io.StringIO(s))
df.tail()

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
      <th>data</th>
      <th>stato</th>
      <th>ricoverati_con_sintomi</th>
      <th>terapia_intensiva</th>
      <th>totale_ospedalizzati</th>
      <th>isolamento_domiciliare</th>
      <th>totale_positivi</th>
      <th>variazione_totale_positivi</th>
      <th>nuovi_positivi</th>
      <th>dimessi_guariti</th>
      <th>...</th>
      <th>tamponi</th>
      <th>casi_testati</th>
      <th>note</th>
      <th>ingressi_terapia_intensiva</th>
      <th>note_test</th>
      <th>note_casi</th>
      <th>totale_positivi_test_molecolare</th>
      <th>totale_positivi_test_antigenico_rapido</th>
      <th>tamponi_test_molecolare</th>
      <th>tamponi_test_antigenico_rapido</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>330</th>
      <td>2021-01-19T17:00:00</td>
      <td>ITA</td>
      <td>22699</td>
      <td>2487</td>
      <td>25186</td>
      <td>510338</td>
      <td>535524</td>
      <td>-11535</td>
      <td>10497</td>
      <td>1781917</td>
      <td>...</td>
      <td>29619436</td>
      <td>16009790.0</td>
      <td>NaN</td>
      <td>176.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2397121.0</td>
      <td>3477.0</td>
      <td>29132944.0</td>
      <td>486492.0</td>
    </tr>
    <tr>
      <th>331</th>
      <td>2021-01-20T17:00:00</td>
      <td>ITA</td>
      <td>22469</td>
      <td>2461</td>
      <td>24930</td>
      <td>498623</td>
      <td>523553</td>
      <td>-11971</td>
      <td>13571</td>
      <td>1806932</td>
      <td>...</td>
      <td>29899198</td>
      <td>16102034.0</td>
      <td>NaN</td>
      <td>152.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2409616.0</td>
      <td>4550.0</td>
      <td>29296422.0</td>
      <td>602776.0</td>
    </tr>
    <tr>
      <th>332</th>
      <td>2021-01-21T17:00:00</td>
      <td>ITA</td>
      <td>22045</td>
      <td>2418</td>
      <td>24463</td>
      <td>492105</td>
      <td>516568</td>
      <td>-6985</td>
      <td>14078</td>
      <td>1827451</td>
      <td>...</td>
      <td>30166765</td>
      <td>16197394.0</td>
      <td>NaN</td>
      <td>155.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2422728.0</td>
      <td>5493.0</td>
      <td>29458875.0</td>
      <td>707890.0</td>
    </tr>
    <tr>
      <th>333</th>
      <td>2021-01-22T17:00:00</td>
      <td>ITA</td>
      <td>21691</td>
      <td>2390</td>
      <td>24081</td>
      <td>477972</td>
      <td>502053</td>
      <td>-14515</td>
      <td>13633</td>
      <td>1855127</td>
      <td>...</td>
      <td>30431493</td>
      <td>16279588.0</td>
      <td>NaN</td>
      <td>144.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2435519.0</td>
      <td>6335.0</td>
      <td>29608567.0</td>
      <td>822926.0</td>
    </tr>
    <tr>
      <th>334</th>
      <td>2021-01-23T17:00:00</td>
      <td>ITA</td>
      <td>21403</td>
      <td>2386</td>
      <td>23789</td>
      <td>475045</td>
      <td>498834</td>
      <td>-3219</td>
      <td>13331</td>
      <td>1871189</td>
      <td>...</td>
      <td>30717824</td>
      <td>16367107.0</td>
      <td>NaN</td>
      <td>174.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2447861.0</td>
      <td>7324.0</td>
      <td>29759716.0</td>
      <td>958108.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 24 columns</p>
</div>



### Build additional columns to calculate pandemics KPIs
Calculating and wrangling a bit the data to fit them in a comparable scale.
#### Additional columns:

$$
infection.rate = nuovi.positivi/nuovi.tamponi
$$
$$
infectedX1000=nuovi.positivi/1000
$$
$$
deadX100=nuovi.deceduti/100
$$

$$
criticalX100=terapia.intensiva/100
$$


```python
df.fillna(0)
df['nuovi_tamponi']=df['tamponi'].diff()
df['nuovi_deceduti']=df['deceduti'].diff()
df['infection_rate']=100*df['nuovi_positivi']/df['nuovi_tamponi']
df['infectedX1000']=df['nuovi_positivi']/1000
df['deadX100']=df['nuovi_deceduti']/100
df['criticalX100']=df['terapia_intensiva']/100
#df[df['data']=='2020-12-17T17:00:00','infection_rate']=0
df.loc[df['data']=='2020-12-17T17:00:00',['infection_rate']]=0

```


```python
# Display the dataframe types with the added columns at the end
df.dtypes
```




    data                                       object
    stato                                      object
    ricoverati_con_sintomi                      int64
    terapia_intensiva                           int64
    totale_ospedalizzati                        int64
    isolamento_domiciliare                      int64
    totale_positivi                             int64
    variazione_totale_positivi                  int64
    nuovi_positivi                              int64
    dimessi_guariti                             int64
    deceduti                                    int64
    casi_da_sospetto_diagnostico              float64
    casi_da_screening                         float64
    totale_casi                                 int64
    tamponi                                     int64
    casi_testati                              float64
    note                                       object
    ingressi_terapia_intensiva                float64
    note_test                                 float64
    note_casi                                 float64
    totale_positivi_test_molecolare           float64
    totale_positivi_test_antigenico_rapido    float64
    tamponi_test_molecolare                   float64
    tamponi_test_antigenico_rapido            float64
    nuovi_tamponi                             float64
    nuovi_deceduti                            float64
    infection_rate                            float64
    infectedX1000                             float64
    deadX100                                  float64
    criticalX100                              float64
    dtype: object



### Display Results


```python
# import graphic libraries
import plotly.express as px
import plotly.io as pio


# Draw Graph
fig = px.line(df, x='data', y=['infection_rate','deadX100','infectedX1000', 'criticalX100'], title='Italy [Rate of infection, deaths/100, infected/1000, critical/100] ')
# write image
pio.write_image(fig, file='covid_graph.png',format='png')

```

# OPTIONAL: save html Graph
```python
 fig.write_html('Infection_Ratio_Chart.html', include_plotlyjs="cdn",auto_open=False)
 ```


```python
fig.show()
```

![COVID Situation Graph](/img/in-post/covid_graph.png)



