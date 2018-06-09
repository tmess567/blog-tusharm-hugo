---
title: Jupyter Notebook as Output
author: tusharm
type: post
date: '2018-06-10'
categories:
  - kaggle
  - python
tags:
  - kaggle
  - python
  - ipython
  - jupyter
  - notebook
  - exectuable
  - development
---
# Data Analytics stuff (Sample Python Notebook)

```
python
# This Python 3 environment comes with many helpful analytics libraries installed
# It is defined by the kaggle/python docker image: https://github.com/kaggle/docker-python
# For example, here's several helpful packages to load in 

import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)

# Input data files are available in the "../input/" directory.
# For example, running this (by clicking run or pressing Shift+Enter) will list the files in the input directory

import os
print(os.listdir("../input"))

# Any results you write to the current directory are saved as output.
```

```
['file1.txt', 'file3.txt', 'file2.txt']
```

```python
file1 = pd.read_csv('../input/file1.txt', '\t', header=None, names = ['GCF', 'WP'])
file1.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

```
.dataframe tbody tr th {
    vertical-align: top;
}

.dataframe thead th {
    text-align: right;
}
```

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GCF</th>
      <th>WP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>GCF_000011405.1</td>
      <td>WP_010030797.1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>GCF_001632845.1</td>
      <td>WP_063465093.1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GCF_002848565.1</td>
      <td>WP_002883307.1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>GCF_002848565.1</td>
      <td>WP_004175258.1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>GCF_002393465.1</td>
      <td>WP_000676056.1</td>
    </tr>
  </tbody>
</table>
</div>

Need to add index to file1 so that it can be joined with the index below

This needs to be done since we will be joining on file line numbers

```python
file1['ind'] = file1.index + 1
file1['ind'] = 'C' + file1['ind'].astype(str) + ' '
file1.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

```
.dataframe tbody tr th {
    vertical-align: top;
}

.dataframe thead th {
    text-align: right;
}
```

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GCF</th>
      <th>WP</th>
      <th>ind</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>GCF_000011405.1</td>
      <td>WP_010030797.1</td>
      <td>C1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>GCF_001632845.1</td>
      <td>WP_063465093.1</td>
      <td>C2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GCF_002848565.1</td>
      <td>WP_002883307.1</td>
      <td>C3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>GCF_002848565.1</td>
      <td>WP_004175258.1</td>
      <td>C4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>GCF_002393465.1</td>
      <td>WP_000676056.1</td>
      <td>C5</td>
    </tr>
  </tbody>
</table>
</div>

```python
file2 = pd.read_csv('../input/file2.txt', '\t', header=None, names = [
    'ind', 'col1', 'col2', 'GCF', 'col4', 'col5', 'col6', 'col7', 'col8', 'col9', 'col10', 'WP', 'col12', 'col13', 'col14', 'col15', 'col16', 'col17', 'col18', 'col19', 'col20'])
file2.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

```
.dataframe tbody tr th {
    vertical-align: top;
}

.dataframe thead th {
    text-align: right;
}
```

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ind</th>
      <th>col1</th>
      <th>col2</th>
      <th>GCF</th>
      <th>col4</th>
      <th>col5</th>
      <th>col6</th>
      <th>col7</th>
      <th>col8</th>
      <th>col9</th>
      <th>...</th>
      <th>WP</th>
      <th>col12</th>
      <th>col13</th>
      <th>col14</th>
      <th>col15</th>
      <th>col16</th>
      <th>col17</th>
      <th>col18</th>
      <th>col19</th>
      <th>col20</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>C1</td>
      <td>CDS</td>
      <td>with_protein</td>
      <td>GCF_000005845.2</td>
      <td>Primary Assembly</td>
      <td>chromosome</td>
      <td>NaN</td>
      <td>NC_000913.3</td>
      <td>190</td>
      <td>255</td>
      <td>...</td>
      <td>NP_414542.1</td>
      <td>WP_001386572.1</td>
      <td>NaN</td>
      <td>thr operon leader peptide</td>
      <td>thrL</td>
      <td>944742.0</td>
      <td>b0001</td>
      <td>66</td>
      <td>21.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C2</td>
      <td>CDS</td>
      <td>with_protein</td>
      <td>GCF_000005845.2</td>
      <td>Primary Assembly</td>
      <td>chromosome</td>
      <td>NaN</td>
      <td>NC_000913.3</td>
      <td>337</td>
      <td>2799</td>
      <td>...</td>
      <td>NP_414543.1</td>
      <td>WP_001264707.1</td>
      <td>NaN</td>
      <td>Bifunctional aspartokinase/homoserine dehydrog...</td>
      <td>thrA</td>
      <td>945803.0</td>
      <td>b0002</td>
      <td>2463</td>
      <td>820.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C3</td>
      <td>CDS</td>
      <td>with_protein</td>
      <td>GCF_000005845.2</td>
      <td>Primary Assembly</td>
      <td>chromosome</td>
      <td>NaN</td>
      <td>NC_000913.3</td>
      <td>2801</td>
      <td>3733</td>
      <td>...</td>
      <td>NP_414544.1</td>
      <td>WP_000241662.1</td>
      <td>NaN</td>
      <td>homoserine kinase</td>
      <td>thrB</td>
      <td>947498.0</td>
      <td>b0003</td>
      <td>933</td>
      <td>310.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>C4</td>
      <td>CDS</td>
      <td>with_protein</td>
      <td>GCF_000005845.2</td>
      <td>Primary Assembly</td>
      <td>chromosome</td>
      <td>NaN</td>
      <td>NC_000913.3</td>
      <td>3734</td>
      <td>5020</td>
      <td>...</td>
      <td>NP_414545.1</td>
      <td>WP_000781074.1</td>
      <td>NaN</td>
      <td>L-threonine synthase</td>
      <td>thrC</td>
      <td>945198.0</td>
      <td>b0004</td>
      <td>1287</td>
      <td>428.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>C5</td>
      <td>CDS</td>
      <td>with_protein</td>
      <td>GCF_000005845.2</td>
      <td>Primary Assembly</td>
      <td>chromosome</td>
      <td>NaN</td>
      <td>NC_000913.3</td>
      <td>5234</td>
      <td>5530</td>
      <td>...</td>
      <td>NP_414546.1</td>
      <td>WP_000738719.1</td>
      <td>NaN</td>
      <td>DUF2502 family putative periplasmic protein</td>
      <td>yaaX</td>
      <td>944747.0</td>
      <td>b0005</td>
      <td>297</td>
      <td>98.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 21 columns</p>
</div>

Need to set DType of Columns as String before joining

```python
file1.GCF = file1.GCF.astype(str).apply(lambda x: x.strip())
file1.WP = file1.WP.astype(str).apply(lambda x: x.strip())

file2.GCF = file2.GCF.astype(str).apply(lambda x: x.strip())
file2.WP = file2.WP.astype(str).apply(lambda x: x.strip())
```

Now joining based on Columns and index.

```python
pd.merge(file1, file2, on = ['ind', 'GCF', 'WP'], how = 'inner')
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

```
.dataframe tbody tr th {
    vertical-align: top;
}

.dataframe thead th {
    text-align: right;
}
```

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GCF</th>
      <th>WP</th>
      <th>ind</th>
      <th>col1</th>
      <th>col2</th>
      <th>col4</th>
      <th>col5</th>
      <th>col6</th>
      <th>col7</th>
      <th>col8</th>
      <th>...</th>
      <th>col10</th>
      <th>col12</th>
      <th>col13</th>
      <th>col14</th>
      <th>col15</th>
      <th>col16</th>
      <th>col17</th>
      <th>col18</th>
      <th>col19</th>
      <th>col20</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
<p>0 rows × 21 columns</p>
</div>

```python
pd.merge(file1, file2, on = ['GCF', 'WP'], how = 'inner')
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

```
.dataframe tbody tr th {
    vertical-align: top;
}

.dataframe thead th {
    text-align: right;
}
```

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GCF</th>
      <th>WP</th>
      <th>ind_x</th>
      <th>ind_y</th>
      <th>col1</th>
      <th>col2</th>
      <th>col4</th>
      <th>col5</th>
      <th>col6</th>
      <th>col7</th>
      <th>...</th>
      <th>col10</th>
      <th>col12</th>
      <th>col13</th>
      <th>col14</th>
      <th>col15</th>
      <th>col16</th>
      <th>col17</th>
      <th>col18</th>
      <th>col19</th>
      <th>col20</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>GCF_000005845.2</td>
      <td>NP_416543.1</td>
      <td>C932</td>
      <td>C2091</td>
      <td>CDS</td>
      <td>with_protein</td>
      <td>Primary Assembly</td>
      <td>chromosome</td>
      <td>NaN</td>
      <td>NC_000913.3</td>
      <td>...</td>
      <td>-</td>
      <td>WP_000783975.1</td>
      <td>NaN</td>
      <td>glucose-1-phosphate thymidylyltransferase</td>
      <td>rfbA</td>
      <td>945154.0</td>
      <td>b2039</td>
      <td>882</td>
      <td>293.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>GCF_000005845.2</td>
      <td>NP_418236.1</td>
      <td>C933</td>
      <td>C3869</td>
      <td>CDS</td>
      <td>with_protein</td>
      <td>Primary Assembly</td>
      <td>chromosome</td>
      <td>NaN</td>
      <td>NC_000913.3</td>
      <td>...</td>
      <td>+</td>
      <td>WP_000676056.1</td>
      <td>NaN</td>
      <td>glucose-1-phosphate thymidylyltransferase</td>
      <td>rffH</td>
      <td>948299.0</td>
      <td>b3789</td>
      <td>882</td>
      <td>293.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GCF_000397205.1</td>
      <td>WP_015633785.1</td>
      <td>C3011</td>
      <td>C317</td>
      <td>CDS</td>
      <td>with_protein</td>
      <td>Primary Assembly</td>
      <td>chromosome</td>
      <td>NaN</td>
      <td>NC_021237.1</td>
      <td>...</td>
      <td>-</td>
      <td>WP_015633785.1</td>
      <td>NaN</td>
      <td>glucose-1-phosphate thymidylyltransferase</td>
      <td>NaN</td>
      <td>29827969.0</td>
      <td>PFLCHA0_RS01550</td>
      <td>876</td>
      <td>291.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>GCF_000006605.1</td>
      <td>WP_005292098.1</td>
      <td>C5239</td>
      <td>C1949</td>
      <td>CDS</td>
      <td>with_protein</td>
      <td>Primary Assembly</td>
      <td>chromosome</td>
      <td>NaN</td>
      <td>NC_007164.1</td>
      <td>...</td>
      <td>-</td>
      <td>WP_005292098.1</td>
      <td>NaN</td>
      <td>glucose-1-phosphate thymidylyltransferase</td>
      <td>NaN</td>
      <td>3433212.0</td>
      <td>JK_RS09615</td>
      <td>876</td>
      <td>291.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>GCF_000006925.2</td>
      <td>NP_707934.1</td>
      <td>C6853</td>
      <td>C1957</td>
      <td>CDS</td>
      <td>with_protein</td>
      <td>Primary Assembly</td>
      <td>chromosome</td>
      <td>NaN</td>
      <td>NC_004337.2</td>
      <td>...</td>
      <td>-</td>
      <td>WP_000857518.1</td>
      <td>NaN</td>
      <td>glucose-1-phosphate thymidylyltransferase</td>
      <td>rfbA</td>
      <td>1025289.0</td>
      <td>SF2102</td>
      <td>879</td>
      <td>292.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>GCF_000006925.2</td>
      <td>NP_709593.1</td>
      <td>C6854</td>
      <td>C3613</td>
      <td>CDS</td>
      <td>with_protein</td>
      <td>Primary Assembly</td>
      <td>chromosome</td>
      <td>NaN</td>
      <td>NC_004337.2</td>
      <td>...</td>
      <td>+</td>
      <td>WP_000676056.1</td>
      <td>NaN</td>
      <td>glucose-1-phosphate thymidylyltransferase</td>
      <td>rffH</td>
      <td>1025982.0</td>
      <td>SF3863</td>
      <td>882</td>
      <td>293.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>6 rows × 22 columns</p>
</div>

```python
output = pd.merge(file1, file2, on = ['GCF', 'WP'], how = 'inner')
output.to_csv('output_1.csv')
```

To make sure this works, I tried joining on just index which I knew was intersecting

```python
pd.merge(file1, file2, on = ['ind'], how = 'inner').head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

```
.dataframe tbody tr th {
    vertical-align: top;
}

.dataframe thead th {
    text-align: right;
}
```

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GCF_x</th>
      <th>WP_x</th>
      <th>ind</th>
      <th>col1</th>
      <th>col2</th>
      <th>GCF_y</th>
      <th>col4</th>
      <th>col5</th>
      <th>col6</th>
      <th>col7</th>
      <th>...</th>
      <th>WP_y</th>
      <th>col12</th>
      <th>col13</th>
      <th>col14</th>
      <th>col15</th>
      <th>col16</th>
      <th>col17</th>
      <th>col18</th>
      <th>col19</th>
      <th>col20</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>GCF_000011405.1</td>
      <td>WP_010030797.1</td>
      <td>C1</td>
      <td>CDS</td>
      <td>with_protein</td>
      <td>GCF_000005845.2</td>
      <td>Primary Assembly</td>
      <td>chromosome</td>
      <td>NaN</td>
      <td>NC_000913.3</td>
      <td>...</td>
      <td>NP_414542.1</td>
      <td>WP_001386572.1</td>
      <td>NaN</td>
      <td>thr operon leader peptide</td>
      <td>thrL</td>
      <td>944742.0</td>
      <td>b0001</td>
      <td>66</td>
      <td>21.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>GCF_000011405.1</td>
      <td>WP_010030797.1</td>
      <td>C1</td>
      <td>CDS</td>
      <td>with_protein</td>
      <td>GCF_000006605.1</td>
      <td>Primary Assembly</td>
      <td>chromosome</td>
      <td>NaN</td>
      <td>NC_007164.1</td>
      <td>...</td>
      <td>WP_011272776.1</td>
      <td>WP_011272776.1</td>
      <td>NaN</td>
      <td>chromosomal replication initiator protein DnaA</td>
      <td>NaN</td>
      <td>3433707.0</td>
      <td>JK_RS00005</td>
      <td>1752</td>
      <td>583.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GCF_000011405.1</td>
      <td>WP_010030797.1</td>
      <td>C1</td>
      <td>CDS</td>
      <td>with_protein</td>
      <td>GCF_000006925.2</td>
      <td>Primary Assembly</td>
      <td>chromosome</td>
      <td>NaN</td>
      <td>NC_004337.2</td>
      <td>...</td>
      <td>NP_705961.1</td>
      <td>WP_001386572.1</td>
      <td>NaN</td>
      <td>thr operon leader peptide</td>
      <td>thrL</td>
      <td>1027248.0</td>
      <td>SF0001</td>
      <td>66</td>
      <td>21.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>GCF_000011405.1</td>
      <td>WP_010030797.1</td>
      <td>C1</td>
      <td>CDS</td>
      <td>with_protein</td>
      <td>GCF_000397185.1</td>
      <td>Primary Assembly</td>
      <td>chromosome</td>
      <td>NaN</td>
      <td>NC_021236.1</td>
      <td>...</td>
      <td>WP_012358634.1</td>
      <td>WP_012358634.1</td>
      <td>NaN</td>
      <td>chromosomal replication initiator protein DnaA</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>SLY_RS00005</td>
      <td>1368</td>
      <td>455.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>GCF_000011405.1</td>
      <td>WP_010030797.1</td>
      <td>C1</td>
      <td>CDS</td>
      <td>with_protein</td>
      <td>GCF_000397205.1</td>
      <td>Primary Assembly</td>
      <td>chromosome</td>
      <td>NaN</td>
      <td>NC_021237.1</td>
      <td>...</td>
      <td>WP_011058391.1</td>
      <td>WP_011058391.1</td>
      <td>NaN</td>
      <td>chromosomal replication initiator protein DnaA</td>
      <td>NaN</td>
      <td>29824842.0</td>
      <td>PFLCHA0_RS00005</td>
      <td>1542</td>
      <td>513.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 23 columns</p>
</div>

```python
file3 = pd.read_csv('../input/file3.txt', '\t')
file3.fillna(-9999, inplace=True)
file3
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

```
.dataframe tbody tr th {
    vertical-align: top;
}

.dataframe thead th {
    text-align: right;
}
```

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Genome</th>
      <th>rmlA</th>
      <th>rmlB</th>
      <th>rmlC35</th>
      <th>rmlC3</th>
      <th>rmlD</th>
      <th>output</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>GCF_000385905.1</td>
      <td>56</td>
      <td>65</td>
      <td>54</td>
      <td>50</td>
      <td>57</td>
      <td>neighbour</td>
    </tr>
    <tr>
      <th>1</th>
      <td>GCF_000385925.1</td>
      <td>45, 25</td>
      <td>100</td>
      <td>-9999</td>
      <td>40</td>
      <td>49</td>
      <td>neighbour</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GCF_000006725.1</td>
      <td>18982</td>
      <td>18981</td>
      <td>18983</td>
      <td>18983</td>
      <td>18984</td>
      <td>neighbour</td>
    </tr>
    <tr>
      <th>3</th>
      <td>GCF_000006765.1</td>
      <td>30294</td>
      <td>30292</td>
      <td>30295</td>
      <td>30295</td>
      <td>30293</td>
      <td>neighbour</td>
    </tr>
    <tr>
      <th>4</th>
      <td>GCF_000006785.2</td>
      <td>31460</td>
      <td>31462</td>
      <td>31461</td>
      <td>31461</td>
      <td>31333</td>
      <td>not</td>
    </tr>
    <tr>
      <th>5</th>
      <td>GCF_000006845.1</td>
      <td>38991</td>
      <td>38990</td>
      <td>38992</td>
      <td>38992</td>
      <td>37600</td>
      <td>not</td>
    </tr>
    <tr>
      <th>6</th>
      <td>GCF_000006865.1</td>
      <td>39470</td>
      <td>39474</td>
      <td>-9999</td>
      <td>39472</td>
      <td>39475</td>
      <td>neighbour</td>
    </tr>
    <tr>
      <th>7</th>
      <td>GCF_000006905.1</td>
      <td>45112</td>
      <td>47623</td>
      <td>47627</td>
      <td>47627</td>
      <td>45111, 47608</td>
      <td>not</td>
    </tr>
    <tr>
      <th>8</th>
      <td>GCF_000016285.1</td>
      <td>1528899, 1529277</td>
      <td>1528897, 1529279</td>
      <td>1528896, 1529280</td>
      <td>1528230, 1528896, 1529280</td>
      <td>1528898, 1529278</td>
      <td>neighbour</td>
    </tr>
  </tbody>
</table>
</div>

Resolving each num value / comma separared as array

```python
def resolve_as_arr(val):
    return str(val).split(',')
    
file3['rmlA'] = file3['rmlA'].apply(resolve_as_arr)
file3['rmlB'] = file3['rmlB'].apply(resolve_as_arr)
file3['rmlC35'] = file3['rmlC35'].apply(resolve_as_arr)
file3['rmlC3'] = file3['rmlC3'].apply(resolve_as_arr)
file3['rmlD'] = file3['rmlD'].apply(resolve_as_arr)

file3
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

```
.dataframe tbody tr th {
    vertical-align: top;
}

.dataframe thead th {
    text-align: right;
}
```

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Genome</th>
      <th>rmlA</th>
      <th>rmlB</th>
      <th>rmlC35</th>
      <th>rmlC3</th>
      <th>rmlD</th>
      <th>output</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>GCF_000385905.1</td>
      <td>\\\[56]</td>
      <td>\\\[65]</td>
      <td>\\\[54]</td>
      <td>\\\[50]</td>
      <td>\\\[57]</td>
      <td>neighbour</td>
    </tr>
    <tr>
      <th>1</th>
      <td>GCF_000385925.1</td>
      <td>\\\[45,  25]</td>
      <td>\\\[100]</td>
      <td>\\\[-9999]</td>
      <td>\\\[40]</td>
      <td>\\\[49]</td>
      <td>neighbour</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GCF_000006725.1</td>
      <td>\\\[18982]</td>
      <td>\\\[18981]</td>
      <td>\\\[18983]</td>
      <td>\\\[18983]</td>
      <td>\\\[18984]</td>
      <td>neighbour</td>
    </tr>
    <tr>
      <th>3</th>
      <td>GCF_000006765.1</td>
      <td>\\\[30294]</td>
      <td>\\\[30292]</td>
      <td>\\\[30295]</td>
      <td>\\\[30295]</td>
      <td>\\\[30293]</td>
      <td>neighbour</td>
    </tr>
    <tr>
      <th>4</th>
      <td>GCF_000006785.2</td>
      <td>\\\[31460]</td>
      <td>\\\[31462]</td>
      <td>\\\[31461]</td>
      <td>\\\[31461]</td>
      <td>\\\[31333]</td>
      <td>not</td>
    </tr>
    <tr>
      <th>5</th>
      <td>GCF_000006845.1</td>
      <td>\\\[38991]</td>
      <td>\\\[38990]</td>
      <td>\\\[38992]</td>
      <td>\\\[38992]</td>
      <td>\\\[37600]</td>
      <td>not</td>
    </tr>
    <tr>
      <th>6</th>
      <td>GCF_000006865.1</td>
      <td>\\\[39470]</td>
      <td>\\\[39474]</td>
      <td>\\\[-9999]</td>
      <td>\\\[39472]</td>
      <td>\\\[39475]</td>
      <td>neighbour</td>
    </tr>
    <tr>
      <th>7</th>
      <td>GCF_000006905.1</td>
      <td>\\\[45112]</td>
      <td>\\\[47623]</td>
      <td>\\\[47627]</td>
      <td>\\\[47627]</td>
      <td>\\\[45111,  47608]</td>
      <td>not</td>
    </tr>
    <tr>
      <th>8</th>
      <td>GCF_000016285.1</td>
      <td>\\\[1528899,  1529277]</td>
      <td>\\\[1528897,  1529279]</td>
      <td>\\\[1528896,  1529280]</td>
      <td>\\\[1528230,  1528896,  1529280]</td>
      <td>\\\[1528898,  1529278]</td>
      <td>neighbour</td>
    </tr>
  </tbody>
</table>
</div>

Now we add a column that finds the range between these values

Since any value in array can be used so we cross join the arrays to get all combinations of 5 integers

```python
import itertools
a = [1, 2, 3]
b = [4, 5, 6]
list(itertools.product(a,b))
```

```
[(1, 4), (1, 5), (1, 6), (2, 4), (2, 5), (2, 6), (3, 4), (3, 5), (3, 6)]
```

```python
arr = [2,1,3,5,7]
arr.sort()
print(arr)

diff = []
for i in range(1, len(arr)):
    diff.append(arr[i] - arr[i-1])
max(diff)
```

```
[1, 2, 3, 5, 7]





2
```

```python
def findRange(arr_of_nums):
    arr_of_nums = list(arr_of_nums)
    arr_of_nums = [a for a in arr_of_nums if a != -9999]
    arr_of_nums.sort()
    
    diff = []
    for i in range(1, len(arr_of_nums)):
        diff.append(arr_of_nums[i] - arr_of_nums[i-1])
    return max(diff) 

def findMinRangeVal(arr_of_arr_of_nums):
    return min(arr_of_arr_of_nums, key=findRange)

def findMinRange(arr_of_arr_of_nums):
    print(findMinRangeVal(arr_of_arr_of_nums))
    return findRange(min(arr_of_arr_of_nums, key=findRange))
        
a = (10, 20, 30)
b = (15, 4, -9999)
d = (2, 3, 11)
c = list(itertools.product(a,b,d))


print("Range =>")
print(a)
print(findRange(a))
print("-------")
print(b)
print(findRange(b))
print("-------")
print(d)
print(findRange(d))
print("-------")

print("Combinations =>")
print(c)
print("Min Combination Range =>" )
print( findMinRange(c))
```

```
Range =>
(10, 20, 30)
10
-------
(15, 4, -9999)
11
-------
(2, 3, 11)
8
-------
Combinations =>
[(10, 15, 2), (10, 15, 3), (10, 15, 11), (10, 4, 2), (10, 4, 3), (10, 4, 11), (10, -9999, 2), (10, -9999, 3), (10, -9999, 11), (20, 15, 2), (20, 15, 3), (20, 15, 11), (20, 4, 2), (20, 4, 3), (20, 4, 11), (20, -9999, 2), (20, -9999, 3), (20, -9999, 11), (30, 15, 2), (30, 15, 3), (30, 15, 11), (30, 4, 2), (30, 4, 3), (30, 4, 11), (30, -9999, 2), (30, -9999, 3), (30, -9999, 11)]
Min Combination Range =>
(10, -9999, 11)
1
```

```python
file3
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

```
.dataframe tbody tr th {
    vertical-align: top;
}

.dataframe thead th {
    text-align: right;
}
```

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Genome</th>
      <th>rmlA</th>
      <th>rmlB</th>
      <th>rmlC35</th>
      <th>rmlC3</th>
      <th>rmlD</th>
      <th>output</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>GCF_000385905.1</td>
      <td>\\\[56]</td>
      <td>\\\[65]</td>
      <td>\\\[54]</td>
      <td>\\\[50]</td>
      <td>\\\[57]</td>
      <td>neighbour</td>
    </tr>
    <tr>
      <th>1</th>
      <td>GCF_000385925.1</td>
      <td>\\\[45,  25]</td>
      <td>\\\[100]</td>
      <td>\\\[-9999]</td>
      <td>\\\[40]</td>
      <td>\\\[49]</td>
      <td>neighbour</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GCF_000006725.1</td>
      <td>\\\[18982]</td>
      <td>\\\[18981]</td>
      <td>\\\[18983]</td>
      <td>\\\[18983]</td>
      <td>\\\[18984]</td>
      <td>neighbour</td>
    </tr>
    <tr>
      <th>3</th>
      <td>GCF_000006765.1</td>
      <td>\\\[30294]</td>
      <td>\\\[30292]</td>
      <td>\\\[30295]</td>
      <td>\\\[30295]</td>
      <td>\\\[30293]</td>
      <td>neighbour</td>
    </tr>
    <tr>
      <th>4</th>
      <td>GCF_000006785.2</td>
      <td>\\\[31460]</td>
      <td>\\\[31462]</td>
      <td>\\\[31461]</td>
      <td>\\\[31461]</td>
      <td>\\\[31333]</td>
      <td>not</td>
    </tr>
    <tr>
      <th>5</th>
      <td>GCF_000006845.1</td>
      <td>\\\[38991]</td>
      <td>\\\[38990]</td>
      <td>\\\[38992]</td>
      <td>\\\[38992]</td>
      <td>\\\[37600]</td>
      <td>not</td>
    </tr>
    <tr>
      <th>6</th>
      <td>GCF_000006865.1</td>
      <td>\\\[39470]</td>
      <td>\\\[39474]</td>
      <td>\\\[-9999]</td>
      <td>\\\[39472]</td>
      <td>\\\[39475]</td>
      <td>neighbour</td>
    </tr>
    <tr>
      <th>7</th>
      <td>GCF_000006905.1</td>
      <td>\\\[45112]</td>
      <td>\\\[47623]</td>
      <td>\\\[47627]</td>
      <td>\\\[47627]</td>
      <td>\\\[45111,  47608]</td>
      <td>not</td>
    </tr>
    <tr>
      <th>8</th>
      <td>GCF_000016285.1</td>
      <td>\\\[1528899,  1529277]</td>
      <td>\\\[1528897,  1529279]</td>
      <td>\\\[1528896,  1529280]</td>
      <td>\\\[1528230,  1528896,  1529280]</td>
      <td>\\\[1528898,  1529278]</td>
      <td>neighbour</td>
    </tr>
  </tbody>
</table>
</div>

```python
def findMinRangeInRow(row):
    col_names = ['rmlA','rmlB','rmlC35','rmlC3','rmlD']
    for col_name in col_names:
        row[col_name] = map(int, row[col_name])
    combinations = list(itertools.product(row['rmlA'], row['rmlB'], row['rmlC35'], row['rmlC3'], row['rmlD']))
    return findMinRange(combinations)

def isNeighbour(row):
    return row['minRange']<=10

file3['minRange'] = file3.apply(findMinRangeInRow, axis=1)
file3['output_2'] = file3.apply(isNeighbour, axis=1)
file3
```

```
(56, 65, 54, 50, 57)
(45, 100, -9999, 40, 49)
(18982, 18981, 18983, 18983, 18984)
(30294, 30292, 30295, 30295, 30293)
(31460, 31462, 31461, 31461, 31333)
(38991, 38990, 38992, 38992, 37600)
(39470, 39474, -9999, 39472, 39475)
(45112, 47623, 47627, 47627, 47608)
(1528899, 1528897, 1528896, 1528896, 1528898)
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

```
.dataframe tbody tr th {
    vertical-align: top;
}

.dataframe thead th {
    text-align: right;
}
```

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Genome</th>
      <th>rmlA</th>
      <th>rmlB</th>
      <th>rmlC35</th>
      <th>rmlC3</th>
      <th>rmlD</th>
      <th>output</th>
      <th>minRange</th>
      <th>output_2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>GCF_000385905.1</td>
      <td>\\\[56]</td>
      <td>\\\[65]</td>
      <td>\\\[54]</td>
      <td>\\\[50]</td>
      <td>\\\[57]</td>
      <td>neighbour</td>
      <td>8</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>GCF_000385925.1</td>
      <td>\\\[45,  25]</td>
      <td>\\\[100]</td>
      <td>\\\[-9999]</td>
      <td>\\\[40]</td>
      <td>\\\[49]</td>
      <td>neighbour</td>
      <td>51</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GCF_000006725.1</td>
      <td>\\\[18982]</td>
      <td>\\\[18981]</td>
      <td>\\\[18983]</td>
      <td>\\\[18983]</td>
      <td>\\\[18984]</td>
      <td>neighbour</td>
      <td>1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>GCF_000006765.1</td>
      <td>\\\[30294]</td>
      <td>\\\[30292]</td>
      <td>\\\[30295]</td>
      <td>\\\[30295]</td>
      <td>\\\[30293]</td>
      <td>neighbour</td>
      <td>1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>GCF_000006785.2</td>
      <td>\\\[31460]</td>
      <td>\\\[31462]</td>
      <td>\\\[31461]</td>
      <td>\\\[31461]</td>
      <td>\\\[31333]</td>
      <td>not</td>
      <td>127</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>GCF_000006845.1</td>
      <td>\\\[38991]</td>
      <td>\\\[38990]</td>
      <td>\\\[38992]</td>
      <td>\\\[38992]</td>
      <td>\\\[37600]</td>
      <td>not</td>
      <td>1390</td>
      <td>False</td>
    </tr>
    <tr>
      <th>6</th>
      <td>GCF_000006865.1</td>
      <td>\\\[39470]</td>
      <td>\\\[39474]</td>
      <td>\\\[-9999]</td>
      <td>\\\[39472]</td>
      <td>\\\[39475]</td>
      <td>neighbour</td>
      <td>2</td>
      <td>True</td>
    </tr>
    <tr>
      <th>7</th>
      <td>GCF_000006905.1</td>
      <td>\\\[45112]</td>
      <td>\\\[47623]</td>
      <td>\\\[47627]</td>
      <td>\\\[47627]</td>
      <td>\\\[45111,  47608]</td>
      <td>not</td>
      <td>2496</td>
      <td>False</td>
    </tr>
    <tr>
      <th>8</th>
      <td>GCF_000016285.1</td>
      <td>\\\[1528899,  1529277]</td>
      <td>\\\[1528897,  1529279]</td>
      <td>\\\[1528896,  1529280]</td>
      <td>\\\[1528230,  1528896,  1529280]</td>
      <td>\\\[1528898,  1529278]</td>
      <td>neighbour</td>
      <td>1</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>

```python
file3.to_csv('output_2.csv')
```
