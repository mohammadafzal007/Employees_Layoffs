```python
#Importing Libraries
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```


```python
# Read dataset
df=pd.read_csv('layoffs.csv')
df.head()
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
      <th>company</th>
      <th>location</th>
      <th>industry</th>
      <th>total_laid_off</th>
      <th>percentage_laid_off</th>
      <th>date</th>
      <th>stage</th>
      <th>country</th>
      <th>funds_raised</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>New Work</td>
      <td>Hamburg</td>
      <td>Consumer</td>
      <td>400.0</td>
      <td>NaN</td>
      <td>2024-01-11</td>
      <td>Post-IPO</td>
      <td>Germany</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Playtika</td>
      <td>Tel Aviv</td>
      <td>Consumer</td>
      <td>300.0</td>
      <td>0.10</td>
      <td>2024-01-11</td>
      <td>Post-IPO</td>
      <td>Israel</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Discord</td>
      <td>SF Bay Area</td>
      <td>Consumer</td>
      <td>170.0</td>
      <td>0.17</td>
      <td>2024-01-11</td>
      <td>Series H</td>
      <td>United States</td>
      <td>995.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Inmobi</td>
      <td>Bengaluru</td>
      <td>Marketing</td>
      <td>125.0</td>
      <td>0.05</td>
      <td>2024-01-11</td>
      <td>Unknown</td>
      <td>India</td>
      <td>320.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Audible</td>
      <td>New York City</td>
      <td>Media</td>
      <td>100.0</td>
      <td>0.05</td>
      <td>2024-01-11</td>
      <td>Acquired</td>
      <td>United States</td>
      <td>14.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 3313 entries, 0 to 3312
    Data columns (total 9 columns):
     #   Column               Non-Null Count  Dtype  
    ---  ------               --------------  -----  
     0   company              3313 non-null   object 
     1   location             3312 non-null   object 
     2   industry             3312 non-null   object 
     3   total_laid_off       2189 non-null   float64
     4   percentage_laid_off  2141 non-null   float64
     5   date                 3313 non-null   object 
     6   stage                3306 non-null   object 
     7   country              3313 non-null   object 
     8   funds_raised         2962 non-null   float64
    dtypes: float64(3), object(6)
    memory usage: 233.1+ KB
    

# Data Cleaning


```python
df=df.dropna()
df=df.reset_index(drop=True)
```


```python
df.head()
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
      <th>company</th>
      <th>location</th>
      <th>industry</th>
      <th>total_laid_off</th>
      <th>percentage_laid_off</th>
      <th>date</th>
      <th>stage</th>
      <th>country</th>
      <th>funds_raised</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Discord</td>
      <td>SF Bay Area</td>
      <td>Consumer</td>
      <td>170.0</td>
      <td>0.17</td>
      <td>2024-01-11</td>
      <td>Series H</td>
      <td>United States</td>
      <td>995.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Inmobi</td>
      <td>Bengaluru</td>
      <td>Marketing</td>
      <td>125.0</td>
      <td>0.05</td>
      <td>2024-01-11</td>
      <td>Unknown</td>
      <td>India</td>
      <td>320.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Audible</td>
      <td>New York City</td>
      <td>Media</td>
      <td>100.0</td>
      <td>0.05</td>
      <td>2024-01-11</td>
      <td>Acquired</td>
      <td>United States</td>
      <td>14.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Sisense</td>
      <td>New York City</td>
      <td>Data</td>
      <td>60.0</td>
      <td>0.13</td>
      <td>2024-01-11</td>
      <td>Series F</td>
      <td>United States</td>
      <td>274.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Twitch</td>
      <td>SF Bay Area</td>
      <td>Consumer</td>
      <td>500.0</td>
      <td>0.35</td>
      <td>2024-01-09</td>
      <td>Acquired</td>
      <td>United States</td>
      <td>35.0</td>
    </tr>
  </tbody>
</table>
</div>



# Data Transformation


```python
df['date']=pd.to_datetime(df['date'])
```


```python
df.dtypes
```




    company                        object
    location                       object
    industry                       object
    total_laid_off                float64
    percentage_laid_off           float64
    date                   datetime64[ns]
    stage                          object
    country                        object
    funds_raised                  float64
    dtype: object




```python
df['Year']=df['date'].dt.year
df['Month']=df['date'].dt.month_name()
df=df.drop('date',axis=1)
```


```python
df.head()
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
      <th>company</th>
      <th>location</th>
      <th>industry</th>
      <th>total_laid_off</th>
      <th>percentage_laid_off</th>
      <th>stage</th>
      <th>country</th>
      <th>funds_raised</th>
      <th>Year</th>
      <th>Month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Discord</td>
      <td>SF Bay Area</td>
      <td>Consumer</td>
      <td>170.0</td>
      <td>0.17</td>
      <td>Series H</td>
      <td>United States</td>
      <td>995.0</td>
      <td>2024</td>
      <td>January</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Inmobi</td>
      <td>Bengaluru</td>
      <td>Marketing</td>
      <td>125.0</td>
      <td>0.05</td>
      <td>Unknown</td>
      <td>India</td>
      <td>320.0</td>
      <td>2024</td>
      <td>January</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Audible</td>
      <td>New York City</td>
      <td>Media</td>
      <td>100.0</td>
      <td>0.05</td>
      <td>Acquired</td>
      <td>United States</td>
      <td>14.0</td>
      <td>2024</td>
      <td>January</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Sisense</td>
      <td>New York City</td>
      <td>Data</td>
      <td>60.0</td>
      <td>0.13</td>
      <td>Series F</td>
      <td>United States</td>
      <td>274.0</td>
      <td>2024</td>
      <td>January</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Twitch</td>
      <td>SF Bay Area</td>
      <td>Consumer</td>
      <td>500.0</td>
      <td>0.35</td>
      <td>Acquired</td>
      <td>United States</td>
      <td>35.0</td>
      <td>2024</td>
      <td>January</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['Year'].unique()
```




    array([2024, 2023, 2022, 2021, 2020])



## Company with High Layoffs


```python
big_lay_offs=df[['company','country','total_laid_off','Year']][df['total_laid_off']>1000].sort_values(by='total_laid_off',ascending=False).reset_index(drop=True)
```


```python
big_lay_offs.head()
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
      <th>company</th>
      <th>country</th>
      <th>total_laid_off</th>
      <th>Year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Google</td>
      <td>United States</td>
      <td>12000.0</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Meta</td>
      <td>United States</td>
      <td>11000.0</td>
      <td>2022</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Microsoft</td>
      <td>United States</td>
      <td>10000.0</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Amazon</td>
      <td>United States</td>
      <td>10000.0</td>
      <td>2022</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Ericsson</td>
      <td>Sweden</td>
      <td>8500.0</td>
      <td>2023</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Combining company layoff from all years
big_lay_offs.Year=big_lay_offs.Year.apply(lambda x:str(x))
big_lay_offs=big_lay_offs.groupby('company').agg({'Year':','.join,'total_laid_off':'sum'})

```


```python
Years=[year for year,df in df.groupby('Year')]
Years
```




    [2020, 2021, 2022, 2023, 2024]




```python
big_lay_offs=big_lay_offs.sort_values('total_laid_off',ascending=False)
```


```python
big_lay_offs.head()
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
      <th>Year</th>
      <th>total_laid_off</th>
    </tr>
    <tr>
      <th>company</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Amazon</th>
      <td>2022,2023</td>
      <td>18000.0</td>
    </tr>
    <tr>
      <th>Google</th>
      <td>2023</td>
      <td>12000.0</td>
    </tr>
    <tr>
      <th>Meta</th>
      <td>2022</td>
      <td>11000.0</td>
    </tr>
    <tr>
      <th>Microsoft</th>
      <td>2023</td>
      <td>10000.0</td>
    </tr>
    <tr>
      <th>Ericsson</th>
      <td>2023</td>
      <td>8500.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
high_lay_offs=big_lay_offs.head(10)
high_lay_offs
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
      <th>Year</th>
      <th>total_laid_off</th>
    </tr>
    <tr>
      <th>company</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Amazon</th>
      <td>2022,2023</td>
      <td>18000.0</td>
    </tr>
    <tr>
      <th>Google</th>
      <td>2023</td>
      <td>12000.0</td>
    </tr>
    <tr>
      <th>Meta</th>
      <td>2022</td>
      <td>11000.0</td>
    </tr>
    <tr>
      <th>Microsoft</th>
      <td>2023</td>
      <td>10000.0</td>
    </tr>
    <tr>
      <th>Ericsson</th>
      <td>2023</td>
      <td>8500.0</td>
    </tr>
    <tr>
      <th>Salesforce</th>
      <td>2023</td>
      <td>8000.0</td>
    </tr>
    <tr>
      <th>Flink</th>
      <td>2023</td>
      <td>8000.0</td>
    </tr>
    <tr>
      <th>Micron</th>
      <td>2023,2023</td>
      <td>7200.0</td>
    </tr>
    <tr>
      <th>Uber</th>
      <td>2020,2020</td>
      <td>6700.0</td>
    </tr>
    <tr>
      <th>Cisco</th>
      <td>2022</td>
      <td>4100.0</td>
    </tr>
  </tbody>
</table>
</div>



# Data Visualization

## Top 10 companies with High Layoffs from 2020-2024


```python
plt.figure(figsize=(10,5))
plt.title("Top 10 Countries with High Lay Offs from 2020-2024")
sns.barplot(x='company',y='total_laid_off',data=high_lay_offs,hue='company',palette="husl")
plt.show()
```


    
![png](output_22_0.png)
    


###  Insight
- High Layoff Company
1. Amazon - 17500+
2. Google - 11000+
3. Meta   - 10000+


```python
df.head()
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
      <th>company</th>
      <th>location</th>
      <th>industry</th>
      <th>total_laid_off</th>
      <th>percentage_laid_off</th>
      <th>stage</th>
      <th>country</th>
      <th>funds_raised</th>
      <th>Year</th>
      <th>Month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Discord</td>
      <td>SF Bay Area</td>
      <td>Consumer</td>
      <td>170.0</td>
      <td>0.17</td>
      <td>Series H</td>
      <td>United States</td>
      <td>995.0</td>
      <td>2024</td>
      <td>January</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Inmobi</td>
      <td>Bengaluru</td>
      <td>Marketing</td>
      <td>125.0</td>
      <td>0.05</td>
      <td>Unknown</td>
      <td>India</td>
      <td>320.0</td>
      <td>2024</td>
      <td>January</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Audible</td>
      <td>New York City</td>
      <td>Media</td>
      <td>100.0</td>
      <td>0.05</td>
      <td>Acquired</td>
      <td>United States</td>
      <td>14.0</td>
      <td>2024</td>
      <td>January</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Sisense</td>
      <td>New York City</td>
      <td>Data</td>
      <td>60.0</td>
      <td>0.13</td>
      <td>Series F</td>
      <td>United States</td>
      <td>274.0</td>
      <td>2024</td>
      <td>January</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Twitch</td>
      <td>SF Bay Area</td>
      <td>Consumer</td>
      <td>500.0</td>
      <td>0.35</td>
      <td>Acquired</td>
      <td>United States</td>
      <td>35.0</td>
      <td>2024</td>
      <td>January</td>
    </tr>
  </tbody>
</table>
</div>



## Analysis Layoffs 2020-2024


```python
Yearly_distribution_layoffs=df.groupby('Year')['total_laid_off'].sum()
years=[year for year,df in df.groupby('Year')]
```


```python
plt.pie(Yearly_distribution_layoffs,labels=years,autopct="%.2f%%",startangle=270)
plt.legend(loc='upper left')
plt.title("Total Layoffs 2020-2024")
```




    Text(0.5, 1.0, 'Total Layoffs 2020-2024')




    
![png](output_27_1.png)
    


###  Year-wise Layoffs
- 2023 (44.3%) and 2022 (35.76%) Highest layoffs


```python
plt.plot(years,Yearly_distribution_layoffs,color='red',marker='.',markersize=10,linestyle='solid')
plt.grid()
plt.xticks(years,rotation='vertical')
plt.xlabel('Years')
plt.ylabel('Total Laid offs')
plt.title("Total Layoffs 2020-2024")
```




    Text(0.5, 1.0, 'Total Layoffs 2020-2024')




    
![png](output_29_1.png)
    



```python
# Analysis of Company layoff multile years
company_count=df.groupby('company').size()
```


```python
company_count
```




    company
    #Paid           1
    &Open           1
    10X Genomics    1
    1stdibs         1
    23andMe         2
                   ..
    iFood           1
    iPrice Group    1
    iRobot          2
    nCino           1
    uShip           1
    Length: 1135, dtype: int64



## Analysis of Layoffs  in Multiple Years


```python
repeated_company=df[df['company'].isin(company_count[company_count>1].index)]
```


```python
repeated_company.head()
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
      <th>company</th>
      <th>location</th>
      <th>industry</th>
      <th>total_laid_off</th>
      <th>percentage_laid_off</th>
      <th>stage</th>
      <th>country</th>
      <th>funds_raised</th>
      <th>Year</th>
      <th>Month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Discord</td>
      <td>SF Bay Area</td>
      <td>Consumer</td>
      <td>170.0</td>
      <td>0.17</td>
      <td>Series H</td>
      <td>United States</td>
      <td>995.0</td>
      <td>2024</td>
      <td>January</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Sisense</td>
      <td>New York City</td>
      <td>Data</td>
      <td>60.0</td>
      <td>0.13</td>
      <td>Series F</td>
      <td>United States</td>
      <td>274.0</td>
      <td>2024</td>
      <td>January</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Unity</td>
      <td>SF Bay Area</td>
      <td>Other</td>
      <td>1800.0</td>
      <td>0.25</td>
      <td>Post-IPO</td>
      <td>United States</td>
      <td>1300.0</td>
      <td>2024</td>
      <td>January</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Pitch</td>
      <td>Berlin</td>
      <td>Other</td>
      <td>80.0</td>
      <td>0.67</td>
      <td>Series B</td>
      <td>Germany</td>
      <td>138.0</td>
      <td>2024</td>
      <td>January</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Frontdesk</td>
      <td>Milwaukee</td>
      <td>Travel</td>
      <td>200.0</td>
      <td>1.00</td>
      <td>Unknown</td>
      <td>United States</td>
      <td>26.0</td>
      <td>2024</td>
      <td>January</td>
    </tr>
  </tbody>
</table>
</div>




```python
l=['Amazon','Salesforce','Twitter','Swiggy','Better.com','Coinbase','Groupon','DocuSign',
   'Katerra','Lyft','Wayfair','Rivian','Better.com','Unity','Twilio','Splunk','Zillow',
   'Stitch Fix','Redfin','Coinbase',]
repeated_company=repeated_company[repeated_company['company'].isin(l)]
```


```python
df_pivot=repeated_company.pivot_table(index='company',columns='Year',values='total_laid_off',aggfunc='sum')
```


```python
df_pivot
```


```python
plt.figure(figsize=(20,2))
df_pivot.plot(kind='bar',width=1)
plt.title('Layoff of Company in Multiple Years')
```




    Text(0.5, 1.0, 'Layoff of Company in Multiple Years')




    <Figure size 2000x200 with 0 Axes>



    
![png](output_38_2.png)
    


### Analysis of Year wise Layoffs


```python
df_2020=df[df['Year']==2020].reset_index(drop=True)
df_2021=df[df['Year']==2021].reset_index(drop=True)
df_2022=df[df['Year']==2022].reset_index(drop=True)
df_2023=df[df['Year']==2023].reset_index(drop=True)
df_2024=df[df['Year']==2024].reset_index(drop=True)   
```


```python
analysis_2020=df_2020[df_2020['total_laid_off']>800].sort_values('total_laid_off',ascending=False).reset_index(drop=True)
sns.barplot(x='company',y='total_laid_off',data=analysis_2020,color='red')
sns.set_context('notebook')
plt.xticks(analysis_2020['company'],rotation='vertical')
plt.title('Layoffs Analysis 2020')
plt.show()
```


    
![png](output_41_0.png)
    



```python
analysis_2021=df_2021[df_2021['total_laid_off']>800].sort_values('total_laid_off',ascending=False).reset_index(drop=True)
sns.barplot(x='company',y='total_laid_off',data=analysis_2021,color='green')
sns.set_context('notebook')
plt.xticks(analysis_2021['company'],rotation='vertical')
plt.title('Layoffs Analysis 2021')
plt.show()
```


    
![png](output_42_0.png)
    



```python
analysis_2022=df_2022[df_2022['total_laid_off']>800].sort_values('total_laid_off',ascending=False).reset_index(drop=True)
sns.barplot(x='company',y='total_laid_off',data=analysis_2022,color='blue')
sns.set_context('notebook')
plt.xticks(analysis_2022['company'],rotation='vertical')
plt.title('Layoffs Analysis 2022')
plt.show()
```


    
![png](output_43_0.png)
    



```python
analysis_2023=df_2023[df_2023['total_laid_off']>800].sort_values('total_laid_off',ascending=False).reset_index(drop=True)
sns.barplot(x='company',y='total_laid_off',data=analysis_2023,color='yellow')
sns.set_context('notebook')
plt.xticks(analysis_2023['company'],rotation='vertical')
plt.title('Layoffs Analysis 2023')
plt.show()
```


    
![png](output_44_0.png)
    



```python
analysis_2024=df_2024[df_2024['total_laid_off']>800].sort_values('total_laid_off',ascending=False).reset_index(drop=True)
sns.barplot(x='company',y='total_laid_off',data=analysis_2024,color='green')
plt.xticks(analysis_2024['company'],rotation='vertical')
plt.title('Layoffs Analysis 2024')
plt.show()
```


    
![png](output_45_0.png)
    


## Analysis of Industry-wise Layoffs


```python
industries=[industry for industry,df in df.groupby('industry')]
industry_layoffs=df.groupby('industry')['total_laid_off'].sum()
plt.figure(figsize=(10,3))
plt.bar(industries,industry_layoffs,color='#CC0000')
plt.title('Industry wise Layoffs') 
plt.xticks(industries,rotation='vertical')
plt.xlabel('Industry')
plt.ylabel('Total-Laid_offs')
plt.show()
```


    
![png](output_47_0.png)
    


## Analysis of Country-wise Layoffs


```python
low_layoffs=df.groupby('country')['total_laid_off'].sum()
low_layoffs_countries=list(low_layoffs[low_layoffs<1000].index)
```


```python
low_layoffs_countries
country_data=df
country_data['country']=country_data['country'].replace(low_layoffs_countries,"Other")
```


```python
country_data
```


```python
countries=[country for country,country_data in country_data.groupby('country')]
country_layoffs=country_data.groupby('country')['total_laid_off'].sum()
plt.pie(country_layoffs,labels=countries,autopct="%.2f%%",startangle=90,radius=5,explode=[.3,.5,.3,.5,.3,.5,.3,.5,.3,.5,.3,.5,1])
plt.figure(figsize=(10,4))
plt.show()
country_layoffs
plt.show()
```


    
![png](output_52_0.png)
    



    <Figure size 1000x400 with 0 Axes>


## Analysis of Stages-wise Layoffs


```python
stages=[stage for stage,df in df.groupby('stage')]
stages_layoffs=df.groupby('stage')['total_laid_off'].sum()
plt.bar(stages,stages_layoffs,color='#CC0000')
plt.title('Stages wise Layoffs') 
plt.xticks(stages,rotation='vertical')
plt.xlabel('Stage')
plt.ylabel('Total-Laid_offs')
plt.show()
```


    
![png](output_54_0.png)
    


## Analysis Indian companies Layoffs Monthly


```python
df_indian_companies=df[['company','total_laid_off','Year']][df['country']=='India']
```


```python
df_indian_companies
```


```python
df_indian_companies['Year']=df_indian_companies['Year'].apply(lambda x:str(x))
```


```python
df_indian_companies=df_indian_companies.groupby('company').agg({'Year':','.join,'total_laid_off':'sum'}).reset_index()
```


```python
df_indian_companies=df_indian_companies.sort_values(by='total_laid_off',ascending=False).head(20)
```


```python
# df_indian_companies=df_indian_companies.drop('Year',axis=1)
```


```python
df_indian_companies=df_indian_companies.reset_index()
```


```python
plt.barh(df_indian_companies['company'],df_indian_companies['total_laid_off'],color='violet')
plt.title('Indian Companies Layoffs')
```




    Text(0.5, 1.0, 'Indian Companies Layoffs')




    
![png](output_63_1.png)
    


## Analysis Month-wise layoffs


```python
Month=df['Month'].unique()
Month
```




    array(['January', 'December', 'November', 'October', 'September',
           'August', 'July', 'June', 'May', 'April', 'March', 'February'],
          dtype=object)




```python
analysis_year = df.groupby('Year')
for year, dfx in analysis_year:
    Months=['January', 'February', 'March','April','May', 'June','July','August','September','October','November','December']
    layoff_permonth=dfx.groupby('Month')['total_laid_off'].sum()
    layoff_permonth=layoff_permonth.reindex(Months,fill_value=0)

    # plt.figure(figsize=(10,4))
    plt.plot(Months,layoff_permonth,color='k')
    plt.fill_between(Months,layoff_permonth,color='#CC0000',alpha=0.2)
    plt.xticks(Months,rotation='vertical')
    plt.xlabel("Month")
    plt.ylabel('Total Layoff')
    plt.title(f"Layoff Analysis for Year {year}")
    plt.show()
```


    
![png](output_66_0.png)
    



    
![png](output_66_1.png)
    



    
![png](output_66_2.png)
    



    
![png](output_66_3.png)
    



    
![png](output_66_4.png)
    


# Insights

**High Layoffs Companies from 2020-2024**
1. Amazon
2. Google
3. Meta
4. Microsoft

**Companies Layoff Multiples Years**
1. Amazon-2
2. SaleaForce-3
3. Twitter-2
4. Unity-3

**Year with High Layoffs**
- 2023 44.3%
- 2022 35.7%

**Company with High Layoff in 2020**
1. Uber
2. Groupon
3. Airbnb
4. PaisaBazaar

**Company with High Layoff in 2021**
1. Katerra
2. Zellow
3. Better.com

**Company with High Layoff in 2022**
1. Meta
2. Amazon
3. Cisco
4. Twitter

**Company with High Layoff in 2023**
1. Google
2. Microsoft
3. Ericsson
4. Flink

**Company with High Layoff in 2024**
1. Unity

**Industry with High Layoffs**
1. Consumer
2. Retail
3. Other
4. Transportation
5. Food
6. Finance

**Country with High Layoffs**
1. United States  71.4%
2. India          6.97%
3. Germany        4.15%
4. Sweden         3.45%
5. United Kingdom 2.97%

**HighLayoffs based on Company Stages**
1. Post-IPO
2. Other
3. Series-B
4. Series-D
5. Acquired

**Indian Companies with High Layoffs**
1. Byju
2. Swiggy
3. Unacademy
4. PaisaBazaar
5. Ola


```python

```

