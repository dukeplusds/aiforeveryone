---
title: Introduction To Pandas
category: Tutorials
order: 5
---
## Introduction to Pandas

Pandas is a data processing library in python that plays a crucial role in machine learning. Pandas allows users to work with and manipulate dataframes, much like you would in Excel.


```python
import pandas as pd
```

#### Reading data from a CSV file


```python
df = pd.read_csv('data/spotify_top10.csv', encoding="latin1")
```

#### Viewing the CSV data


```python
df
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
      <th>Track.Name</th>
      <th>Artist.Name</th>
      <th>Genre</th>
      <th>Popularity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Señorita</td>
      <td>Shawn Mendes</td>
      <td>canadian pop</td>
      <td>79</td>
    </tr>
    <tr>
      <td>1</td>
      <td>China</td>
      <td>Anuel AA</td>
      <td>reggaeton flow</td>
      <td>92</td>
    </tr>
    <tr>
      <td>2</td>
      <td>boyfriend (with Social House)</td>
      <td>Ariana Grande</td>
      <td>dance pop</td>
      <td>85</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Beautiful People (feat. Khalid)</td>
      <td>Ed Sheeran</td>
      <td>pop</td>
      <td>86</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Goodbyes (Feat. Young Thug)</td>
      <td>Post Malone</td>
      <td>dfw rap</td>
      <td>94</td>
    </tr>
    <tr>
      <td>5</td>
      <td>I Don't Care (with Justin Bieber)</td>
      <td>Ed Sheeran</td>
      <td>pop</td>
      <td>84</td>
    </tr>
    <tr>
      <td>6</td>
      <td>Ransom</td>
      <td>Lil Tecca</td>
      <td>trap music</td>
      <td>92</td>
    </tr>
    <tr>
      <td>7</td>
      <td>How Do You Sleep?</td>
      <td>Sam Smith</td>
      <td>pop</td>
      <td>90</td>
    </tr>
    <tr>
      <td>8</td>
      <td>Old Town Road - Remix</td>
      <td>Lil Nas X</td>
      <td>country rap</td>
      <td>87</td>
    </tr>
  </tbody>
</table>
</div>



#### Selecting a row from the dataframe


```python
df[['Genre']]
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
      <th>Genre</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>canadian pop</td>
    </tr>
    <tr>
      <td>1</td>
      <td>reggaeton flow</td>
    </tr>
    <tr>
      <td>2</td>
      <td>dance pop</td>
    </tr>
    <tr>
      <td>3</td>
      <td>pop</td>
    </tr>
    <tr>
      <td>4</td>
      <td>dfw rap</td>
    </tr>
    <tr>
      <td>5</td>
      <td>pop</td>
    </tr>
    <tr>
      <td>6</td>
      <td>trap music</td>
    </tr>
    <tr>
      <td>7</td>
      <td>pop</td>
    </tr>
    <tr>
      <td>8</td>
      <td>country rap</td>
    </tr>
  </tbody>
</table>
</div>



#### Selecting a row from the dataframe


```python
df[['Artist.Name', 'Genre', 'Popularity']]
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
      <th>Artist.Name</th>
      <th>Genre</th>
      <th>Popularity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Shawn Mendes</td>
      <td>canadian pop</td>
      <td>79</td>
    </tr>
    <tr>
      <td>1</td>
      <td>Anuel AA</td>
      <td>reggaeton flow</td>
      <td>92</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Ariana Grande</td>
      <td>dance pop</td>
      <td>85</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Ed Sheeran</td>
      <td>pop</td>
      <td>86</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Post Malone</td>
      <td>dfw rap</td>
      <td>94</td>
    </tr>
    <tr>
      <td>5</td>
      <td>Ed Sheeran</td>
      <td>pop</td>
      <td>84</td>
    </tr>
    <tr>
      <td>6</td>
      <td>Lil Tecca</td>
      <td>trap music</td>
      <td>92</td>
    </tr>
    <tr>
      <td>7</td>
      <td>Sam Smith</td>
      <td>pop</td>
      <td>90</td>
    </tr>
    <tr>
      <td>8</td>
      <td>Lil Nas X</td>
      <td>country rap</td>
      <td>87</td>
    </tr>
  </tbody>
</table>
</div>



#### Sorting a dataframe by row


```python
df.sort_values(by=['Popularity'], ascending=False)
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
      <th>Track.Name</th>
      <th>Artist.Name</th>
      <th>Genre</th>
      <th>Popularity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>4</td>
      <td>Goodbyes (Feat. Young Thug)</td>
      <td>Post Malone</td>
      <td>dfw rap</td>
      <td>94</td>
    </tr>
    <tr>
      <td>1</td>
      <td>China</td>
      <td>Anuel AA</td>
      <td>reggaeton flow</td>
      <td>92</td>
    </tr>
    <tr>
      <td>6</td>
      <td>Ransom</td>
      <td>Lil Tecca</td>
      <td>trap music</td>
      <td>92</td>
    </tr>
    <tr>
      <td>7</td>
      <td>How Do You Sleep?</td>
      <td>Sam Smith</td>
      <td>pop</td>
      <td>90</td>
    </tr>
    <tr>
      <td>8</td>
      <td>Old Town Road - Remix</td>
      <td>Lil Nas X</td>
      <td>country rap</td>
      <td>87</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Beautiful People (feat. Khalid)</td>
      <td>Ed Sheeran</td>
      <td>pop</td>
      <td>86</td>
    </tr>
    <tr>
      <td>2</td>
      <td>boyfriend (with Social House)</td>
      <td>Ariana Grande</td>
      <td>dance pop</td>
      <td>85</td>
    </tr>
    <tr>
      <td>5</td>
      <td>I Don't Care (with Justin Bieber)</td>
      <td>Ed Sheeran</td>
      <td>pop</td>
      <td>84</td>
    </tr>
    <tr>
      <td>0</td>
      <td>Señorita</td>
      <td>Shawn Mendes</td>
      <td>canadian pop</td>
      <td>79</td>
    </tr>
  </tbody>
</table>
</div>



#### Selecting a row from the dataframe


```python
df.loc[df['Genre'] == 'pop']
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
      <th>Track.Name</th>
      <th>Artist.Name</th>
      <th>Genre</th>
      <th>Popularity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>3</td>
      <td>Beautiful People (feat. Khalid)</td>
      <td>Ed Sheeran</td>
      <td>pop</td>
      <td>86</td>
    </tr>
    <tr>
      <td>5</td>
      <td>I Don't Care (with Justin Bieber)</td>
      <td>Ed Sheeran</td>
      <td>pop</td>
      <td>84</td>
    </tr>
    <tr>
      <td>7</td>
      <td>How Do You Sleep?</td>
      <td>Sam Smith</td>
      <td>pop</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>



#### Selecting a row from the dataframe


```python
df.loc[df['Popularity'] > 90]
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
      <th>Track.Name</th>
      <th>Artist.Name</th>
      <th>Genre</th>
      <th>Popularity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>China</td>
      <td>Anuel AA</td>
      <td>reggaeton flow</td>
      <td>92</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Goodbyes (Feat. Young Thug)</td>
      <td>Post Malone</td>
      <td>dfw rap</td>
      <td>94</td>
    </tr>
    <tr>
      <td>6</td>
      <td>Ransom</td>
      <td>Lil Tecca</td>
      <td>trap music</td>
      <td>92</td>
    </tr>
  </tbody>
</table>
</div>



#### Selecting a row from the dataframe


```python
df.loc[df['Artist.Name'] == 'Ed Sheeran']
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
      <th>Track.Name</th>
      <th>Artist.Name</th>
      <th>Genre</th>
      <th>Popularity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>3</td>
      <td>Beautiful People (feat. Khalid)</td>
      <td>Ed Sheeran</td>
      <td>pop</td>
      <td>86</td>
    </tr>
    <tr>
      <td>5</td>
      <td>I Don't Care (with Justin Bieber)</td>
      <td>Ed Sheeran</td>
      <td>pop</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[['Artist.Name']].where(df['Popularity'] > 85)
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
      <th>Artist.Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>1</td>
      <td>Anuel AA</td>
    </tr>
    <tr>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Ed Sheeran</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Post Malone</td>
    </tr>
    <tr>
      <td>5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>6</td>
      <td>Lil Tecca</td>
    </tr>
    <tr>
      <td>7</td>
      <td>Sam Smith</td>
    </tr>
    <tr>
      <td>8</td>
      <td>Lil Nas X</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['Artist.Name'].tolist()
```




    ['Shawn Mendes',
     'Anuel AA',
     'Ariana Grande',
     'Ed Sheeran',
     'Post Malone',
     'Ed Sheeran',
     'Lil Tecca',
     'Sam Smith',
     'Lil Nas X']




```python
df[['Artist.Name', 'Popularity']].to_dict('records')
```




    [{'Artist.Name': 'Shawn Mendes', 'Popularity': 79},
     {'Artist.Name': 'Anuel AA', 'Popularity': 92},
     {'Artist.Name': 'Ariana Grande', 'Popularity': 85},
     {'Artist.Name': 'Ed Sheeran', 'Popularity': 86},
     {'Artist.Name': 'Post Malone', 'Popularity': 94},
     {'Artist.Name': 'Ed Sheeran', 'Popularity': 84},
     {'Artist.Name': 'Lil Tecca', 'Popularity': 92},
     {'Artist.Name': 'Sam Smith', 'Popularity': 90},
     {'Artist.Name': 'Lil Nas X', 'Popularity': 87}]




```python
import matplotlib.pyplot as plt
import seaborn as sns
```


```python
sns.distplot(df.Popularity)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a1d0f4ed0>




<img src="{{ "/images/tutorials/output_22_1.png" | prepend: site.baseurl }}{{ img }}" alt="">



```python

```
