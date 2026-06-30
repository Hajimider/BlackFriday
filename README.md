# 黑色星期五案例分析

## 数据清洗

### 查看数据


```python
import pandas as pd

df=pd.read_csv('BlackFriday.csv')
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
      <th>User_ID</th>
      <th>Product_ID</th>
      <th>Gender</th>
      <th>Age</th>
      <th>Occupation</th>
      <th>City_Category</th>
      <th>Stay_In_Current_City_Years</th>
      <th>Marital_Status</th>
      <th>Product_Category_1</th>
      <th>Product_Category_2</th>
      <th>Product_Category_3</th>
      <th>Purchase</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000001</td>
      <td>P00069042</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8370</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1000001</td>
      <td>P00248942</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
      <td>6.0</td>
      <td>14.0</td>
      <td>15200</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1000001</td>
      <td>P00087842</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>12</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1422</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1000001</td>
      <td>P00085442</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>12</td>
      <td>14.0</td>
      <td>NaN</td>
      <td>1057</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1000002</td>
      <td>P00285442</td>
      <td>M</td>
      <td>55+</td>
      <td>16</td>
      <td>C</td>
      <td>4+</td>
      <td>0</td>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>7969</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>537572</th>
      <td>1004737</td>
      <td>P00193542</td>
      <td>M</td>
      <td>36-45</td>
      <td>16</td>
      <td>C</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>11664</td>
    </tr>
    <tr>
      <th>537573</th>
      <td>1004737</td>
      <td>P00111142</td>
      <td>M</td>
      <td>36-45</td>
      <td>16</td>
      <td>C</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>15.0</td>
      <td>16.0</td>
      <td>19196</td>
    </tr>
    <tr>
      <th>537574</th>
      <td>1004737</td>
      <td>P00345942</td>
      <td>M</td>
      <td>36-45</td>
      <td>16</td>
      <td>C</td>
      <td>1</td>
      <td>0</td>
      <td>8</td>
      <td>15.0</td>
      <td>NaN</td>
      <td>8043</td>
    </tr>
    <tr>
      <th>537575</th>
      <td>1004737</td>
      <td>P00285842</td>
      <td>M</td>
      <td>36-45</td>
      <td>16</td>
      <td>C</td>
      <td>1</td>
      <td>0</td>
      <td>5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>7172</td>
    </tr>
    <tr>
      <th>537576</th>
      <td>1004737</td>
      <td>P00118242</td>
      <td>M</td>
      <td>36-45</td>
      <td>16</td>
      <td>C</td>
      <td>1</td>
      <td>0</td>
      <td>5</td>
      <td>8.0</td>
      <td>NaN</td>
      <td>6875</td>
    </tr>
  </tbody>
</table>
<p>537577 rows × 12 columns</p>
</div>




```python
df.shape
```




    (537577, 12)




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 537577 entries, 0 to 537576
    Data columns (total 12 columns):
     #   Column                      Non-Null Count   Dtype  
    ---  ------                      --------------   -----  
     0   User_ID                     537577 non-null  int64  
     1   Product_ID                  537577 non-null  object 
     2   Gender                      537577 non-null  object 
     3   Age                         537577 non-null  object 
     4   Occupation                  537577 non-null  int64  
     5   City_Category               537577 non-null  object 
     6   Stay_In_Current_City_Years  537577 non-null  object 
     7   Marital_Status              537577 non-null  int64  
     8   Product_Category_1          537577 non-null  int64  
     9   Product_Category_2          370591 non-null  float64
     10  Product_Category_3          164278 non-null  float64
     11  Purchase                    537577 non-null  int64  
    dtypes: float64(2), int64(5), object(5)
    memory usage: 49.2+ MB



```python
df=df.rename(
    columns={
        'User_ID': '用户ID',
        'Product_ID': '商品ID',
        'Gender': '性别',
        'Age': '年龄',
        'Occupation': '职业',
        'City_Category': '城市类别',
        'Stay_In_Current_City_Years': '居住城市年数',
        'Marital_Status': '婚姻状况',
        'Product_Category_1': '产品类别1',
        'Product_Category_2': '产品类别2',
        'Product_Category_3': '产品类别3',
        'Purchase': '采购额'
    }
)
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
      <th>用户ID</th>
      <th>商品ID</th>
      <th>性别</th>
      <th>年龄</th>
      <th>职业</th>
      <th>城市类别</th>
      <th>居住城市年数</th>
      <th>婚姻状况</th>
      <th>产品类别1</th>
      <th>产品类别2</th>
      <th>产品类别3</th>
      <th>采购额</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000001</td>
      <td>P00069042</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8370</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1000001</td>
      <td>P00248942</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
      <td>6.0</td>
      <td>14.0</td>
      <td>15200</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1000001</td>
      <td>P00087842</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>12</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1422</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1000001</td>
      <td>P00085442</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>12</td>
      <td>14.0</td>
      <td>NaN</td>
      <td>1057</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1000002</td>
      <td>P00285442</td>
      <td>M</td>
      <td>55+</td>
      <td>16</td>
      <td>C</td>
      <td>4+</td>
      <td>0</td>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>7969</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>537572</th>
      <td>1004737</td>
      <td>P00193542</td>
      <td>M</td>
      <td>36-45</td>
      <td>16</td>
      <td>C</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>11664</td>
    </tr>
    <tr>
      <th>537573</th>
      <td>1004737</td>
      <td>P00111142</td>
      <td>M</td>
      <td>36-45</td>
      <td>16</td>
      <td>C</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>15.0</td>
      <td>16.0</td>
      <td>19196</td>
    </tr>
    <tr>
      <th>537574</th>
      <td>1004737</td>
      <td>P00345942</td>
      <td>M</td>
      <td>36-45</td>
      <td>16</td>
      <td>C</td>
      <td>1</td>
      <td>0</td>
      <td>8</td>
      <td>15.0</td>
      <td>NaN</td>
      <td>8043</td>
    </tr>
    <tr>
      <th>537575</th>
      <td>1004737</td>
      <td>P00285842</td>
      <td>M</td>
      <td>36-45</td>
      <td>16</td>
      <td>C</td>
      <td>1</td>
      <td>0</td>
      <td>5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>7172</td>
    </tr>
    <tr>
      <th>537576</th>
      <td>1004737</td>
      <td>P00118242</td>
      <td>M</td>
      <td>36-45</td>
      <td>16</td>
      <td>C</td>
      <td>1</td>
      <td>0</td>
      <td>5</td>
      <td>8.0</td>
      <td>NaN</td>
      <td>6875</td>
    </tr>
  </tbody>
</table>
<p>537577 rows × 12 columns</p>
</div>




```python
# 查看缺失值
df.dropna().shape[0]/df.shape[0]
```




    0.3055897108693266




```python
# 填充缺失数据
# df.fillna()
```


```python
# 查看重复数据
df.drop_duplicates()    #无重复值
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
      <th>用户ID</th>
      <th>商品ID</th>
      <th>性别</th>
      <th>年龄</th>
      <th>职业</th>
      <th>城市类别</th>
      <th>居住城市年数</th>
      <th>婚姻状况</th>
      <th>产品类别1</th>
      <th>产品类别2</th>
      <th>产品类别3</th>
      <th>采购额</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000001</td>
      <td>P00069042</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8370</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1000001</td>
      <td>P00248942</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
      <td>6.0</td>
      <td>14.0</td>
      <td>15200</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1000001</td>
      <td>P00087842</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>12</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1422</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1000001</td>
      <td>P00085442</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>12</td>
      <td>14.0</td>
      <td>NaN</td>
      <td>1057</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1000002</td>
      <td>P00285442</td>
      <td>M</td>
      <td>55+</td>
      <td>16</td>
      <td>C</td>
      <td>4+</td>
      <td>0</td>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>7969</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>537572</th>
      <td>1004737</td>
      <td>P00193542</td>
      <td>M</td>
      <td>36-45</td>
      <td>16</td>
      <td>C</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>11664</td>
    </tr>
    <tr>
      <th>537573</th>
      <td>1004737</td>
      <td>P00111142</td>
      <td>M</td>
      <td>36-45</td>
      <td>16</td>
      <td>C</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>15.0</td>
      <td>16.0</td>
      <td>19196</td>
    </tr>
    <tr>
      <th>537574</th>
      <td>1004737</td>
      <td>P00345942</td>
      <td>M</td>
      <td>36-45</td>
      <td>16</td>
      <td>C</td>
      <td>1</td>
      <td>0</td>
      <td>8</td>
      <td>15.0</td>
      <td>NaN</td>
      <td>8043</td>
    </tr>
    <tr>
      <th>537575</th>
      <td>1004737</td>
      <td>P00285842</td>
      <td>M</td>
      <td>36-45</td>
      <td>16</td>
      <td>C</td>
      <td>1</td>
      <td>0</td>
      <td>5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>7172</td>
    </tr>
    <tr>
      <th>537576</th>
      <td>1004737</td>
      <td>P00118242</td>
      <td>M</td>
      <td>36-45</td>
      <td>16</td>
      <td>C</td>
      <td>1</td>
      <td>0</td>
      <td>5</td>
      <td>8.0</td>
      <td>NaN</td>
      <td>6875</td>
    </tr>
  </tbody>
</table>
<p>537577 rows × 12 columns</p>
</div>



## 数据分析

### 销售情况统计


```python
# 采购总额
df['采购额'].sum()
```




    np.int64(5017668378)




```python
# 用户人数
df.drop_duplicates('用户ID')['用户ID'].count()
```




    np.int64(5891)




```python
df.drop_duplicates('用户ID').count()
```




    用户ID      5891
    商品ID      5891
    性别        5891
    年龄        5891
    职业        5891
    城市类别      5891
    居住城市年数    5891
    婚姻状况      5891
    产品类别1     5891
    产品类别2     4097
    产品类别3     1914
    采购额       5891
    dtype: int64




```python
# 人均消费
df['采购额'].sum()/df.drop_duplicates('用户ID')['用户ID'].count()
```




    np.float64(851751.5494822611)




```python
# 商品统计
print('商品类目数量:',df.drop_duplicates('商品ID')['商品ID'].count())
print('每个商品类目销量:',df.groupby(by='商品ID')['商品ID'].count().sort_values(ascending=False))
```

    商品类目数量: 3623
    每个商品类目销量: 商品ID
    P00265242    1858
    P00110742    1591
    P00025442    1586
    P00112142    1539
    P00057642    1430
                 ... 
    P00077242       1
    P00074542       1
    P00162742       1
    P00065942       1
    P00215142       1
    Name: 商品ID, Length: 3623, dtype: int64


### 用户画像分析


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
      <th>用户ID</th>
      <th>商品ID</th>
      <th>性别</th>
      <th>年龄</th>
      <th>职业</th>
      <th>城市类别</th>
      <th>居住城市年数</th>
      <th>婚姻状况</th>
      <th>产品类别1</th>
      <th>产品类别2</th>
      <th>产品类别3</th>
      <th>采购额</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000001</td>
      <td>P00069042</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8370</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1000001</td>
      <td>P00248942</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
      <td>6.0</td>
      <td>14.0</td>
      <td>15200</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1000001</td>
      <td>P00087842</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>12</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1422</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1000001</td>
      <td>P00085442</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>12</td>
      <td>14.0</td>
      <td>NaN</td>
      <td>1057</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1000002</td>
      <td>P00285442</td>
      <td>M</td>
      <td>55+</td>
      <td>16</td>
      <td>C</td>
      <td>4+</td>
      <td>0</td>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>7969</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_dd=df.drop_duplicates('用户ID')[
    ['用户ID','商品ID','性别','年龄','职业','城市类别','居住城市年数','婚姻状况']
].sort_values(by='用户ID')
df_dd
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
      <th>用户ID</th>
      <th>商品ID</th>
      <th>性别</th>
      <th>年龄</th>
      <th>职业</th>
      <th>城市类别</th>
      <th>居住城市年数</th>
      <th>婚姻状况</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000001</td>
      <td>P00069042</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1000002</td>
      <td>P00285442</td>
      <td>M</td>
      <td>55+</td>
      <td>16</td>
      <td>C</td>
      <td>4+</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1000003</td>
      <td>P00193542</td>
      <td>M</td>
      <td>26-35</td>
      <td>15</td>
      <td>A</td>
      <td>3</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1000004</td>
      <td>P00184942</td>
      <td>M</td>
      <td>46-50</td>
      <td>7</td>
      <td>B</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1000005</td>
      <td>P00274942</td>
      <td>M</td>
      <td>26-35</td>
      <td>20</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
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
      <th>39124</th>
      <td>1006036</td>
      <td>P00237642</td>
      <td>F</td>
      <td>26-35</td>
      <td>15</td>
      <td>B</td>
      <td>4+</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39153</th>
      <td>1006037</td>
      <td>P00067342</td>
      <td>F</td>
      <td>46-50</td>
      <td>1</td>
      <td>C</td>
      <td>4+</td>
      <td>0</td>
    </tr>
    <tr>
      <th>155550</th>
      <td>1006038</td>
      <td>P00034742</td>
      <td>F</td>
      <td>55+</td>
      <td>1</td>
      <td>C</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>39161</th>
      <td>1006039</td>
      <td>P00114042</td>
      <td>F</td>
      <td>46-50</td>
      <td>0</td>
      <td>B</td>
      <td>4+</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39169</th>
      <td>1006040</td>
      <td>P00184042</td>
      <td>M</td>
      <td>26-35</td>
      <td>6</td>
      <td>B</td>
      <td>2</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5891 rows × 8 columns</p>
</div>




```python
df_dd['采购额']=df.groupby(by='用户ID')['采购额'].sum().sort_values().values
df_dd
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
      <th>用户ID</th>
      <th>商品ID</th>
      <th>性别</th>
      <th>年龄</th>
      <th>职业</th>
      <th>城市类别</th>
      <th>居住城市年数</th>
      <th>婚姻状况</th>
      <th>采购额</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000001</td>
      <td>P00069042</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>44108</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1000002</td>
      <td>P00285442</td>
      <td>M</td>
      <td>55+</td>
      <td>16</td>
      <td>C</td>
      <td>4+</td>
      <td>0</td>
      <td>44432</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1000003</td>
      <td>P00193542</td>
      <td>M</td>
      <td>26-35</td>
      <td>15</td>
      <td>A</td>
      <td>3</td>
      <td>0</td>
      <td>45551</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1000004</td>
      <td>P00184942</td>
      <td>M</td>
      <td>46-50</td>
      <td>7</td>
      <td>B</td>
      <td>2</td>
      <td>1</td>
      <td>46070</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1000005</td>
      <td>P00274942</td>
      <td>M</td>
      <td>26-35</td>
      <td>20</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>46091</td>
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
      <td>...</td>
    </tr>
    <tr>
      <th>39124</th>
      <td>1006036</td>
      <td>P00237642</td>
      <td>F</td>
      <td>26-35</td>
      <td>15</td>
      <td>B</td>
      <td>4+</td>
      <td>1</td>
      <td>6573609</td>
    </tr>
    <tr>
      <th>39153</th>
      <td>1006037</td>
      <td>P00067342</td>
      <td>F</td>
      <td>46-50</td>
      <td>1</td>
      <td>C</td>
      <td>4+</td>
      <td>0</td>
      <td>6817493</td>
    </tr>
    <tr>
      <th>155550</th>
      <td>1006038</td>
      <td>P00034742</td>
      <td>F</td>
      <td>55+</td>
      <td>1</td>
      <td>C</td>
      <td>2</td>
      <td>0</td>
      <td>7577505</td>
    </tr>
    <tr>
      <th>39161</th>
      <td>1006039</td>
      <td>P00114042</td>
      <td>F</td>
      <td>46-50</td>
      <td>0</td>
      <td>B</td>
      <td>4+</td>
      <td>1</td>
      <td>8699232</td>
    </tr>
    <tr>
      <th>39169</th>
      <td>1006040</td>
      <td>P00184042</td>
      <td>M</td>
      <td>26-35</td>
      <td>6</td>
      <td>B</td>
      <td>2</td>
      <td>0</td>
      <td>10536783</td>
    </tr>
  </tbody>
</table>
<p>5891 rows × 9 columns</p>
</div>




```python
df.groupby('用户ID').get_group(1000004)['采购额'].sum()
```




    np.int64(205987)



#### 性别对消费能力的影响


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
      <th>用户ID</th>
      <th>商品ID</th>
      <th>性别</th>
      <th>年龄</th>
      <th>职业</th>
      <th>城市类别</th>
      <th>居住城市年数</th>
      <th>婚姻状况</th>
      <th>产品类别1</th>
      <th>产品类别2</th>
      <th>产品类别3</th>
      <th>采购额</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000001</td>
      <td>P00069042</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8370</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1000001</td>
      <td>P00248942</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
      <td>6.0</td>
      <td>14.0</td>
      <td>15200</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1000001</td>
      <td>P00087842</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>12</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1422</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1000001</td>
      <td>P00085442</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>12</td>
      <td>14.0</td>
      <td>NaN</td>
      <td>1057</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1000002</td>
      <td>P00285442</td>
      <td>M</td>
      <td>55+</td>
      <td>16</td>
      <td>C</td>
      <td>4+</td>
      <td>0</td>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>7969</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_dd['性别'].value_counts()
```




    性别
    M    4225
    F    1666
    Name: count, dtype: int64




```python
df_dd['性别'].value_counts().values
```




    array([4225, 1666])




```python
df_dd['性别'].value_counts().tolist()
```




    [4225, 1666]




```python
df_dd['性别'].value_counts().index
```




    Index(['M', 'F'], dtype='object', name='性别')




```python
# pyecharts
from pyecharts.globals import CurrentConfig,NotebookType
from pyecharts import options as opts
from pyecharts.charts import Pie
from pyecharts.faker import Faker

x=['男性','女性']
y=df_dd['性别'].value_counts().values.tolist()
data_pair=[list(z) for z in zip(x,y)]
c=(
    Pie()
    .add('',data_pair)
    .set_global_opts(title_opts=opts.TitleOpts(title='性别比例图'))
    .set_series_opts(label_opts=opts.LabelOpts(formatter='{b}:{c}-{d}%'))
)
c.render_notebook()
```





<script>
    require.config({
        paths: {
            'echarts':'https://assets.pyecharts.org/assets/v6/echarts.min'
        }
    });
</script>

        <div id="806d6bfa95e94c7aa2a6c390f3fb9174" style="width:900px; height:500px;"></div>

<script>
        require(['echarts'], function(echarts) {
                var chart_806d6bfa95e94c7aa2a6c390f3fb9174 = echarts.init(
                    document.getElementById('806d6bfa95e94c7aa2a6c390f3fb9174'), 'white', {renderer: 'canvas', locale: 'ZH'});
                var option_806d6bfa95e94c7aa2a6c390f3fb9174 = {
    "animation": true,
    "animationThreshold": 2000,
    "animationDuration": 1000,
    "animationEasing": "cubicOut",
    "animationDelay": 0,
    "animationDurationUpdate": 300,
    "animationEasingUpdate": "cubicOut",
    "animationDelayUpdate": 0,
    "aria": {
        "enabled": false
    },
    "series": [
        {
            "type": "pie",
            "colorBy": "data",
            "legendHoverLink": true,
            "selectedMode": false,
            "selectedOffset": 10,
            "clockwise": true,
            "startAngle": 90,
            "minAngle": 0,
            "minShowLabelAngle": 0,
            "avoidLabelOverlap": true,
            "stillShowZeroSum": true,
            "percentPrecision": 2,
            "showEmptyCircle": true,
            "emptyCircleStyle": {
                "color": "lightgray",
                "borderColor": "#000",
                "borderWidth": 0,
                "borderType": "solid",
                "borderDashOffset": 0,
                "borderCap": "butt",
                "borderJoin": "bevel",
                "borderMiterLimit": 10,
                "opacity": 1
            },
            "data": [
                {
                    "name": "\u7537\u6027",
                    "value": 4225
                },
                {
                    "name": "\u5973\u6027",
                    "value": 1666
                }
            ],
            "radius": [
                "0%",
                "75%"
            ],
            "center": [
                "50%",
                "50%"
            ],
            "label": {
                "show": true,
                "margin": 8,
                "formatter": "{b}:{c}-{d}%",
                "richInheritPlainLabel": true,
                "valueAnimation": false
            },
            "labelLine": {
                "show": true,
                "showAbove": false,
                "length": 15,
                "length2": 15,
                "smooth": false,
                "minTurnAngle": 90,
                "maxSurfaceAngle": 90
            },
            "rippleEffect": {
                "show": true,
                "brushType": "stroke",
                "scale": 2.5,
                "period": 4
            }
        }
    ],
    "legend": [
        {
            "data": [
                "\u7537\u6027",
                "\u5973\u6027"
            ],
            "selected": {},
            "show": true,
            "padding": 5,
            "itemGap": 10,
            "itemWidth": 25,
            "itemHeight": 14,
            "backgroundColor": "transparent",
            "borderColor": "#ccc",
            "borderRadius": 0,
            "pageButtonItemGap": 5,
            "pageButtonPosition": "end",
            "pageFormatter": "{current}/{total}",
            "pageIconColor": "#2f4554",
            "pageIconInactiveColor": "#aaa",
            "pageIconSize": 15,
            "animationDurationUpdate": 800,
            "selector": false,
            "selectorPosition": "auto",
            "selectorItemGap": 7,
            "selectorButtonGap": 10,
            "triggerEvent": false
        }
    ],
    "tooltip": {
        "show": true,
        "trigger": "item",
        "triggerOn": "mousemove|click",
        "axisPointer": {
            "type": "line"
        },
        "showContent": true,
        "alwaysShowContent": false,
        "showDelay": 0,
        "hideDelay": 100,
        "enterable": false,
        "confine": false,
        "appendToBody": false,
        "transitionDuration": 0.4,
        "displayTransition": true,
        "textStyle": {
            "fontSize": 14,
            "richInheritPlainLabel": true
        },
        "borderWidth": 0,
        "padding": 5,
        "order": "seriesAsc"
    },
    "title": [
        {
            "show": true,
            "text": "\u6027\u522b\u6bd4\u4f8b\u56fe",
            "target": "blank",
            "subtarget": "blank",
            "padding": 5,
            "itemGap": 10,
            "textAlign": "auto",
            "textVerticalAlign": "auto",
            "triggerEvent": false
        }
    ]
};
                chart_806d6bfa95e94c7aa2a6c390f3fb9174.setOption(option_806d6bfa95e94c7aa2a6c390f3fb9174);
        });
    </script>





```python
# seabron
import matplotlib.pyplot as plt
import seaborn as sns

plt.rcParams["font.family"] = ["SimHei"]  # 中文
plt.rcParams["axes.unicode_minus"] = False  # 负号正常显示
# sns.set_style("whitegrid")  # 设置seaborn样式

plt.figure(figsize=(5,5))

sizes=df_dd['性别'].value_counts().values
labels=['男性','女性']

plt.pie(sizes,explode=(0.05,0),labels=labels,autopct='%1.2f%%',startangle=90,textprops={'fontsize':12})
# plt.pie(sizes,labels=labels,autopct='%1.2f%%')
plt.title('性别比例图',fontsize=14)
plt.axis('equal')
plt.tight_layout()
plt.show()

```


​    
![png](%E9%BB%91%E8%89%B2%E6%98%9F%E6%9C%9F%E4%BA%94_files/%E9%BB%91%E8%89%B2%E6%98%9F%E6%9C%9F%E4%BA%94_29_0.png)
​    



```python
# plotly
import plotly.express as px

data_p=df_dd['性别'].value_counts().tolist()
labels=['男性','女性']
fig=px.pie(values=data_p,names=labels,title='性别占比图')
fig.show()
```




```python
# matplotlib
plt.figure(figsize=(5,5))
data_m=df_dd['性别'].value_counts().values
labels=['男性','女性']
plt.pie(data_m,labels=labels,autopct='%1.2f%%',explode=(0.02,0))
plt.title('性别对比图')
plt.axis('equal')
plt.tight_layout()
plt.show()
```


​    
![png](%E9%BB%91%E8%89%B2%E6%98%9F%E6%9C%9F%E4%BA%94_files/%E9%BB%91%E8%89%B2%E6%98%9F%E6%9C%9F%E4%BA%94_31_0.png)
​    



```python
[list(z) for z in zip(Faker.choose(),Faker.values())]
```




    [['周一', 20],
     ['周二', 95],
     ['周三', 84],
     ['周四', 28],
     ['周五', 25],
     ['周六', 100],
     ['周日', 83]]




```python
data_pair
```




    [['男性', 4225], ['女性', 1666]]




```python
# 不同性别下的采购额
s_gender=df_dd.groupby(by='性别')['采购额'].sum()
s_gender
```




    性别
    F    1571217937
    M    3446450441
    Name: 采购额, dtype: int64




```python
s_gender.values.tolist()
```




    [1571217937, 3446450441]




```python
from pyecharts import options as opts
from pyecharts.charts import Bar
c=(
    Bar()
    .add_xaxis(['男性','女性'])
    .add_yaxis('商家A',s_gender.values.tolist(),bar_width=60)
    .set_global_opts(title_opts=opts.TitleOpts(title='不同性别的采购额'))
)
c.render_notebook()
```





<script>
    require.config({
        paths: {
            'echarts':'https://assets.pyecharts.org/assets/v6/echarts.min'
        }
    });
</script>

        <div id="4e6cc8b10f9c4739ab600aefa7bf99d1" style="width:900px; height:500px;"></div>

<script>
        require(['echarts'], function(echarts) {
                var chart_4e6cc8b10f9c4739ab600aefa7bf99d1 = echarts.init(
                    document.getElementById('4e6cc8b10f9c4739ab600aefa7bf99d1'), 'white', {renderer: 'canvas', locale: 'ZH'});
                var option_4e6cc8b10f9c4739ab600aefa7bf99d1 = {
    "animation": true,
    "animationThreshold": 2000,
    "animationDuration": 1000,
    "animationEasing": "cubicOut",
    "animationDelay": 0,
    "animationDurationUpdate": 300,
    "animationEasingUpdate": "cubicOut",
    "animationDelayUpdate": 0,
    "aria": {
        "enabled": false
    },
    "series": [
        {
            "type": "bar",
            "name": "\u5546\u5bb6A",
            "legendHoverLink": true,
            "data": [
                1571217937,
                3446450441
            ],
            "realtimeSort": false,
            "showBackground": false,
            "stackStrategy": "samesign",
            "cursor": "pointer",
            "barWidth": 60,
            "barMinHeight": 0,
            "barCategoryGap": "20%",
            "barGap": "30%",
            "large": false,
            "largeThreshold": 400,
            "seriesLayoutBy": "column",
            "datasetIndex": 0,
            "clip": true,
            "zlevel": 0,
            "z": 2,
            "label": {
                "show": true,
                "margin": 8,
                "richInheritPlainLabel": true,
                "valueAnimation": false
            }
        }
    ],
    "legend": [
        {
            "data": [
                "\u5546\u5bb6A"
            ],
            "selected": {},
            "show": true,
            "padding": 5,
            "itemGap": 10,
            "itemWidth": 25,
            "itemHeight": 14,
            "backgroundColor": "transparent",
            "borderColor": "#ccc",
            "borderRadius": 0,
            "pageButtonItemGap": 5,
            "pageButtonPosition": "end",
            "pageFormatter": "{current}/{total}",
            "pageIconColor": "#2f4554",
            "pageIconInactiveColor": "#aaa",
            "pageIconSize": 15,
            "animationDurationUpdate": 800,
            "selector": false,
            "selectorPosition": "auto",
            "selectorItemGap": 7,
            "selectorButtonGap": 10,
            "triggerEvent": false
        }
    ],
    "tooltip": {
        "show": true,
        "trigger": "item",
        "triggerOn": "mousemove|click",
        "axisPointer": {
            "type": "line"
        },
        "showContent": true,
        "alwaysShowContent": false,
        "showDelay": 0,
        "hideDelay": 100,
        "enterable": false,
        "confine": false,
        "appendToBody": false,
        "transitionDuration": 0.4,
        "displayTransition": true,
        "textStyle": {
            "fontSize": 14,
            "richInheritPlainLabel": true
        },
        "borderWidth": 0,
        "padding": 5,
        "order": "seriesAsc"
    },
    "xAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0,
            "data": [
                "\u7537\u6027",
                "\u5973\u6027"
            ]
        }
    ],
    "yAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0
        }
    ],
    "title": [
        {
            "show": true,
            "text": "\u4e0d\u540c\u6027\u522b\u7684\u91c7\u8d2d\u989d",
            "target": "blank",
            "subtarget": "blank",
            "padding": 5,
            "itemGap": 10,
            "textAlign": "auto",
            "textVerticalAlign": "auto",
            "triggerEvent": false
        }
    ]
};
                chart_4e6cc8b10f9c4739ab600aefa7bf99d1.setOption(option_4e6cc8b10f9c4739ab600aefa7bf99d1);
        });
    </script>




#### 婚姻状况对消费能力的影响


```python
marry=df['婚姻状况'].value_counts()
marry
```




    婚姻状况
    0    317817
    1    219760
    Name: count, dtype: int64




```python
# 婚姻状况所占比重图
from pyecharts.globals import CurrentConfig,NotebookType
from pyecharts import options as opts
from pyecharts.charts import Pie
x=['未婚','已婚']
y=marry.tolist()
data_pair=[list(z) for z in zip(x,y)]
c=(
    Pie()
    .add('',data_pair)
    .set_global_opts(title_opts=opts.TitleOpts(title='婚姻状况比例饼图'))
    .set_series_opts(lable_opts=opts.LabelOpts(formatter='{b}:{c}-{d}%'))
)
c.render_notebook()
```





<script>
    require.config({
        paths: {
            'echarts':'https://assets.pyecharts.org/assets/v6/echarts.min'
        }
    });
</script>

        <div id="63308bf0cd834005af37fa1049f3efb9" style="width:900px; height:500px;"></div>

<script>
        require(['echarts'], function(echarts) {
                var chart_63308bf0cd834005af37fa1049f3efb9 = echarts.init(
                    document.getElementById('63308bf0cd834005af37fa1049f3efb9'), 'white', {renderer: 'canvas', locale: 'ZH'});
                var option_63308bf0cd834005af37fa1049f3efb9 = {
    "animation": true,
    "animationThreshold": 2000,
    "animationDuration": 1000,
    "animationEasing": "cubicOut",
    "animationDelay": 0,
    "animationDurationUpdate": 300,
    "animationEasingUpdate": "cubicOut",
    "animationDelayUpdate": 0,
    "aria": {
        "enabled": false
    },
    "series": [
        {
            "type": "pie",
            "colorBy": "data",
            "legendHoverLink": true,
            "selectedMode": false,
            "selectedOffset": 10,
            "clockwise": true,
            "startAngle": 90,
            "minAngle": 0,
            "minShowLabelAngle": 0,
            "avoidLabelOverlap": true,
            "stillShowZeroSum": true,
            "percentPrecision": 2,
            "showEmptyCircle": true,
            "emptyCircleStyle": {
                "color": "lightgray",
                "borderColor": "#000",
                "borderWidth": 0,
                "borderType": "solid",
                "borderDashOffset": 0,
                "borderCap": "butt",
                "borderJoin": "bevel",
                "borderMiterLimit": 10,
                "opacity": 1
            },
            "data": [
                {
                    "name": "\u672a\u5a5a",
                    "value": 317817
                },
                {
                    "name": "\u5df2\u5a5a",
                    "value": 219760
                }
            ],
            "radius": [
                "0%",
                "75%"
            ],
            "center": [
                "50%",
                "50%"
            ],
            "label": {
                "show": true,
                "margin": 8,
                "richInheritPlainLabel": true,
                "valueAnimation": false
            },
            "labelLine": {
                "show": true,
                "showAbove": false,
                "length": 15,
                "length2": 15,
                "smooth": false,
                "minTurnAngle": 90,
                "maxSurfaceAngle": 90
            },
            "rippleEffect": {
                "show": true,
                "brushType": "stroke",
                "scale": 2.5,
                "period": 4
            },
            "lable_opts": {
                "show": true,
                "margin": 8,
                "formatter": "{b}:{c}-{d}%",
                "richInheritPlainLabel": true,
                "valueAnimation": false
            }
        }
    ],
    "legend": [
        {
            "data": [
                "\u672a\u5a5a",
                "\u5df2\u5a5a"
            ],
            "selected": {},
            "show": true,
            "padding": 5,
            "itemGap": 10,
            "itemWidth": 25,
            "itemHeight": 14,
            "backgroundColor": "transparent",
            "borderColor": "#ccc",
            "borderRadius": 0,
            "pageButtonItemGap": 5,
            "pageButtonPosition": "end",
            "pageFormatter": "{current}/{total}",
            "pageIconColor": "#2f4554",
            "pageIconInactiveColor": "#aaa",
            "pageIconSize": 15,
            "animationDurationUpdate": 800,
            "selector": false,
            "selectorPosition": "auto",
            "selectorItemGap": 7,
            "selectorButtonGap": 10,
            "triggerEvent": false
        }
    ],
    "tooltip": {
        "show": true,
        "trigger": "item",
        "triggerOn": "mousemove|click",
        "axisPointer": {
            "type": "line"
        },
        "showContent": true,
        "alwaysShowContent": false,
        "showDelay": 0,
        "hideDelay": 100,
        "enterable": false,
        "confine": false,
        "appendToBody": false,
        "transitionDuration": 0.4,
        "displayTransition": true,
        "textStyle": {
            "fontSize": 14,
            "richInheritPlainLabel": true
        },
        "borderWidth": 0,
        "padding": 5,
        "order": "seriesAsc"
    },
    "title": [
        {
            "show": true,
            "text": "\u5a5a\u59fb\u72b6\u51b5\u6bd4\u4f8b\u997c\u56fe",
            "target": "blank",
            "subtarget": "blank",
            "padding": 5,
            "itemGap": 10,
            "textAlign": "auto",
            "textVerticalAlign": "auto",
            "triggerEvent": false
        }
    ]
};
                chart_63308bf0cd834005af37fa1049f3efb9.setOption(option_63308bf0cd834005af37fa1049f3efb9);
        });
    </script>





```python
# 分析不同性别下婚否对应的采购额
# 女性数据
nv_dd=df_dd[df_dd['性别']=='F']
nv_result=nv_dd.groupby(by='婚姻状况')['采购额'].sum()
nv_result
```




    婚姻状况
    0    869259499
    1    701958438
    Name: 采购额, dtype: int64




```python
nan_dd=df_dd[df_dd['性别']=='M']
nan_result=nan_dd.groupby(by='婚姻状况')['采购额'].sum()
nan_result
```




    婚姻状况
    0    2023537268
    1    1422913173
    Name: 采购额, dtype: int64




```python
from pyecharts import options as opts
from pyecharts.charts import Line

c=(
    Line()
    .add_xaxis(['未婚','已婚'])
    .add_yaxis('女性',nv_result.values.tolist())
    .add_yaxis('男性',nan_result.values.tolist())
    .set_global_opts(title_opts=opts.TitleOpts(title='分析不同性别婚否下对应的采购额'))
)
c.render_notebook()
```





<script>
    require.config({
        paths: {
            'echarts':'https://assets.pyecharts.org/assets/v6/echarts.min'
        }
    });
</script>

        <div id="ce76430431c24cefbae4579f800c0572" style="width:900px; height:500px;"></div>

<script>
        require(['echarts'], function(echarts) {
                var chart_ce76430431c24cefbae4579f800c0572 = echarts.init(
                    document.getElementById('ce76430431c24cefbae4579f800c0572'), 'white', {renderer: 'canvas', locale: 'ZH'});
                var option_ce76430431c24cefbae4579f800c0572 = {
    "animation": true,
    "animationThreshold": 2000,
    "animationDuration": 1000,
    "animationEasing": "cubicOut",
    "animationDelay": 0,
    "animationDurationUpdate": 300,
    "animationEasingUpdate": "cubicOut",
    "animationDelayUpdate": 0,
    "aria": {
        "enabled": false
    },
    "series": [
        {
            "type": "line",
            "name": "\u5973\u6027",
            "connectNulls": false,
            "xAxisIndex": 0,
            "symbolSize": 4,
            "showSymbol": true,
            "smooth": false,
            "clip": true,
            "step": false,
            "stackStrategy": "samesign",
            "data": [
                [
                    "\u672a\u5a5a",
                    869259499
                ],
                [
                    "\u5df2\u5a5a",
                    701958438
                ]
            ],
            "hoverAnimation": true,
            "label": {
                "show": true,
                "margin": 8,
                "richInheritPlainLabel": true,
                "valueAnimation": false
            },
            "logBase": 10,
            "seriesLayoutBy": "column",
            "lineStyle": {
                "show": false
            },
            "areaStyle": {
                "opacity": 0
            },
            "zlevel": 0,
            "z": 0
        },
        {
            "type": "line",
            "name": "\u7537\u6027",
            "connectNulls": false,
            "xAxisIndex": 0,
            "symbolSize": 4,
            "showSymbol": true,
            "smooth": false,
            "clip": true,
            "step": false,
            "stackStrategy": "samesign",
            "data": [
                [
                    "\u672a\u5a5a",
                    2023537268
                ],
                [
                    "\u5df2\u5a5a",
                    1422913173
                ]
            ],
            "hoverAnimation": true,
            "label": {
                "show": true,
                "margin": 8,
                "richInheritPlainLabel": true,
                "valueAnimation": false
            },
            "logBase": 10,
            "seriesLayoutBy": "column",
            "lineStyle": {
                "show": false
            },
            "areaStyle": {
                "opacity": 0
            },
            "zlevel": 0,
            "z": 0
        }
    ],
    "legend": [
        {
            "data": [
                "\u5973\u6027",
                "\u7537\u6027"
            ],
            "selected": {},
            "show": true,
            "padding": 5,
            "itemGap": 10,
            "itemWidth": 25,
            "itemHeight": 14,
            "backgroundColor": "transparent",
            "borderColor": "#ccc",
            "borderRadius": 0,
            "pageButtonItemGap": 5,
            "pageButtonPosition": "end",
            "pageFormatter": "{current}/{total}",
            "pageIconColor": "#2f4554",
            "pageIconInactiveColor": "#aaa",
            "pageIconSize": 15,
            "animationDurationUpdate": 800,
            "selector": false,
            "selectorPosition": "auto",
            "selectorItemGap": 7,
            "selectorButtonGap": 10,
            "triggerEvent": false
        }
    ],
    "tooltip": {
        "show": true,
        "trigger": "item",
        "triggerOn": "mousemove|click",
        "axisPointer": {
            "type": "line"
        },
        "showContent": true,
        "alwaysShowContent": false,
        "showDelay": 0,
        "hideDelay": 100,
        "enterable": false,
        "confine": false,
        "appendToBody": false,
        "transitionDuration": 0.4,
        "displayTransition": true,
        "textStyle": {
            "fontSize": 14,
            "richInheritPlainLabel": true
        },
        "borderWidth": 0,
        "padding": 5,
        "order": "seriesAsc"
    },
    "xAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0,
            "data": [
                "\u672a\u5a5a",
                "\u5df2\u5a5a"
            ]
        }
    ],
    "yAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0
        }
    ],
    "title": [
        {
            "show": true,
            "text": "\u5206\u6790\u4e0d\u540c\u6027\u522b\u5a5a\u5426\u4e0b\u5bf9\u5e94\u7684\u91c7\u8d2d\u989d",
            "target": "blank",
            "subtarget": "blank",
            "padding": 5,
            "itemGap": 10,
            "textAlign": "auto",
            "textVerticalAlign": "auto",
            "triggerEvent": false
        }
    ]
};
                chart_ce76430431c24cefbae4579f800c0572.setOption(option_ce76430431c24cefbae4579f800c0572);
        });
    </script>




#### 年龄对消费能力的影响


```python
# 统计每个年龄段的人数
# 性别女数据，年龄段
nv_dd=df_dd[df_dd['性别']=='F']
nv_result=nv_dd.groupby(by='年龄')['用户ID'].count()
nv_result
```




    年龄
    0-17      78
    18-25    287
    26-35    545
    36-45    333
    46-50    182
    51-55    142
    55+       99
    Name: 用户ID, dtype: int64




```python
# 性别男数据，年龄段
nan_dd=df_dd[df_dd['性别']=='M']
nan_result=nan_dd.groupby(by='年龄')['用户ID'].count()
nan_result
```




    年龄
    0-17      140
    18-25     782
    26-35    1508
    36-45     834
    46-50     349
    51-55     339
    55+       273
    Name: 用户ID, dtype: int64




```python
# 每个年龄段男女人数统计
from pyecharts import options as opts
from pyecharts.charts import Bar

c=(
    Bar()
    .add_xaxis(nan_result.index.tolist())
    .add_yaxis('女性',nv_result.values.tolist())
    .add_yaxis('男性',nan_result.values.tolist())
    .set_global_opts(title_opts=opts.TitleOpts(title='每个年龄段男女人数统计'))
)
c.render_notebook()
```





<script>
    require.config({
        paths: {
            'echarts':'https://assets.pyecharts.org/assets/v6/echarts.min'
        }
    });
</script>

        <div id="2902793f0a754c818d1da244c636eb81" style="width:900px; height:500px;"></div>

<script>
        require(['echarts'], function(echarts) {
                var chart_2902793f0a754c818d1da244c636eb81 = echarts.init(
                    document.getElementById('2902793f0a754c818d1da244c636eb81'), 'white', {renderer: 'canvas', locale: 'ZH'});
                var option_2902793f0a754c818d1da244c636eb81 = {
    "animation": true,
    "animationThreshold": 2000,
    "animationDuration": 1000,
    "animationEasing": "cubicOut",
    "animationDelay": 0,
    "animationDurationUpdate": 300,
    "animationEasingUpdate": "cubicOut",
    "animationDelayUpdate": 0,
    "aria": {
        "enabled": false
    },
    "series": [
        {
            "type": "bar",
            "name": "\u5973\u6027",
            "legendHoverLink": true,
            "data": [
                78,
                287,
                545,
                333,
                182,
                142,
                99
            ],
            "realtimeSort": false,
            "showBackground": false,
            "stackStrategy": "samesign",
            "cursor": "pointer",
            "barMinHeight": 0,
            "barCategoryGap": "20%",
            "barGap": "30%",
            "large": false,
            "largeThreshold": 400,
            "seriesLayoutBy": "column",
            "datasetIndex": 0,
            "clip": true,
            "zlevel": 0,
            "z": 2,
            "label": {
                "show": true,
                "margin": 8,
                "richInheritPlainLabel": true,
                "valueAnimation": false
            }
        },
        {
            "type": "bar",
            "name": "\u7537\u6027",
            "legendHoverLink": true,
            "data": [
                140,
                782,
                1508,
                834,
                349,
                339,
                273
            ],
            "realtimeSort": false,
            "showBackground": false,
            "stackStrategy": "samesign",
            "cursor": "pointer",
            "barMinHeight": 0,
            "barCategoryGap": "20%",
            "barGap": "30%",
            "large": false,
            "largeThreshold": 400,
            "seriesLayoutBy": "column",
            "datasetIndex": 0,
            "clip": true,
            "zlevel": 0,
            "z": 2,
            "label": {
                "show": true,
                "margin": 8,
                "richInheritPlainLabel": true,
                "valueAnimation": false
            }
        }
    ],
    "legend": [
        {
            "data": [
                "\u5973\u6027",
                "\u7537\u6027"
            ],
            "selected": {},
            "show": true,
            "padding": 5,
            "itemGap": 10,
            "itemWidth": 25,
            "itemHeight": 14,
            "backgroundColor": "transparent",
            "borderColor": "#ccc",
            "borderRadius": 0,
            "pageButtonItemGap": 5,
            "pageButtonPosition": "end",
            "pageFormatter": "{current}/{total}",
            "pageIconColor": "#2f4554",
            "pageIconInactiveColor": "#aaa",
            "pageIconSize": 15,
            "animationDurationUpdate": 800,
            "selector": false,
            "selectorPosition": "auto",
            "selectorItemGap": 7,
            "selectorButtonGap": 10,
            "triggerEvent": false
        }
    ],
    "tooltip": {
        "show": true,
        "trigger": "item",
        "triggerOn": "mousemove|click",
        "axisPointer": {
            "type": "line"
        },
        "showContent": true,
        "alwaysShowContent": false,
        "showDelay": 0,
        "hideDelay": 100,
        "enterable": false,
        "confine": false,
        "appendToBody": false,
        "transitionDuration": 0.4,
        "displayTransition": true,
        "textStyle": {
            "fontSize": 14,
            "richInheritPlainLabel": true
        },
        "borderWidth": 0,
        "padding": 5,
        "order": "seriesAsc"
    },
    "xAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0,
            "data": [
                "0-17",
                "18-25",
                "26-35",
                "36-45",
                "46-50",
                "51-55",
                "55+"
            ]
        }
    ],
    "yAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0
        }
    ],
    "title": [
        {
            "show": true,
            "text": "\u6bcf\u4e2a\u5e74\u9f84\u6bb5\u7537\u5973\u4eba\u6570\u7edf\u8ba1",
            "target": "blank",
            "subtarget": "blank",
            "padding": 5,
            "itemGap": 10,
            "textAlign": "auto",
            "textVerticalAlign": "auto",
            "triggerEvent": false
        }
    ]
};
                chart_2902793f0a754c818d1da244c636eb81.setOption(option_2902793f0a754c818d1da244c636eb81);
        });
    </script>





```python
# 每个年龄段的消费能力
cost=df_dd.groupby(by='年龄')['采购额'].sum()
cost
```




    年龄
    0-17      173133537
    18-25     850215584
    26-35    1864941491
    36-45     989914718
    46-50     466932856
    51-55     395769716
    55+       276760476
    Name: 采购额, dtype: int64




```python
# 每个年龄段消费能力
from pyecharts import options as opts
from pyecharts.charts import Bar

c=(
    Bar()
    .add_xaxis(cost.index.tolist())
    .add_yaxis('消费水平',cost.values.tolist())
    .set_global_opts(title_opts=opts.TitleOpts(title='每个年龄段消费能力统计'))
)
c.render_notebook()
```





<script>
    require.config({
        paths: {
            'echarts':'https://assets.pyecharts.org/assets/v6/echarts.min'
        }
    });
</script>

        <div id="a6b222ab07fe48e28c5a86b2bec9435b" style="width:900px; height:500px;"></div>

<script>
        require(['echarts'], function(echarts) {
                var chart_a6b222ab07fe48e28c5a86b2bec9435b = echarts.init(
                    document.getElementById('a6b222ab07fe48e28c5a86b2bec9435b'), 'white', {renderer: 'canvas', locale: 'ZH'});
                var option_a6b222ab07fe48e28c5a86b2bec9435b = {
    "animation": true,
    "animationThreshold": 2000,
    "animationDuration": 1000,
    "animationEasing": "cubicOut",
    "animationDelay": 0,
    "animationDurationUpdate": 300,
    "animationEasingUpdate": "cubicOut",
    "animationDelayUpdate": 0,
    "aria": {
        "enabled": false
    },
    "series": [
        {
            "type": "bar",
            "name": "\u6d88\u8d39\u6c34\u5e73",
            "legendHoverLink": true,
            "data": [
                173133537,
                850215584,
                1864941491,
                989914718,
                466932856,
                395769716,
                276760476
            ],
            "realtimeSort": false,
            "showBackground": false,
            "stackStrategy": "samesign",
            "cursor": "pointer",
            "barMinHeight": 0,
            "barCategoryGap": "20%",
            "barGap": "30%",
            "large": false,
            "largeThreshold": 400,
            "seriesLayoutBy": "column",
            "datasetIndex": 0,
            "clip": true,
            "zlevel": 0,
            "z": 2,
            "label": {
                "show": true,
                "margin": 8,
                "richInheritPlainLabel": true,
                "valueAnimation": false
            }
        }
    ],
    "legend": [
        {
            "data": [
                "\u6d88\u8d39\u6c34\u5e73"
            ],
            "selected": {},
            "show": true,
            "padding": 5,
            "itemGap": 10,
            "itemWidth": 25,
            "itemHeight": 14,
            "backgroundColor": "transparent",
            "borderColor": "#ccc",
            "borderRadius": 0,
            "pageButtonItemGap": 5,
            "pageButtonPosition": "end",
            "pageFormatter": "{current}/{total}",
            "pageIconColor": "#2f4554",
            "pageIconInactiveColor": "#aaa",
            "pageIconSize": 15,
            "animationDurationUpdate": 800,
            "selector": false,
            "selectorPosition": "auto",
            "selectorItemGap": 7,
            "selectorButtonGap": 10,
            "triggerEvent": false
        }
    ],
    "tooltip": {
        "show": true,
        "trigger": "item",
        "triggerOn": "mousemove|click",
        "axisPointer": {
            "type": "line"
        },
        "showContent": true,
        "alwaysShowContent": false,
        "showDelay": 0,
        "hideDelay": 100,
        "enterable": false,
        "confine": false,
        "appendToBody": false,
        "transitionDuration": 0.4,
        "displayTransition": true,
        "textStyle": {
            "fontSize": 14,
            "richInheritPlainLabel": true
        },
        "borderWidth": 0,
        "padding": 5,
        "order": "seriesAsc"
    },
    "xAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0,
            "data": [
                "0-17",
                "18-25",
                "26-35",
                "36-45",
                "46-50",
                "51-55",
                "55+"
            ]
        }
    ],
    "yAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0
        }
    ],
    "title": [
        {
            "show": true,
            "text": "\u6bcf\u4e2a\u5e74\u9f84\u6bb5\u6d88\u8d39\u80fd\u529b\u7edf\u8ba1",
            "target": "blank",
            "subtarget": "blank",
            "padding": 5,
            "itemGap": 10,
            "textAlign": "auto",
            "textVerticalAlign": "auto",
            "triggerEvent": false
        }
    ]
};
                chart_a6b222ab07fe48e28c5a86b2bec9435b.setOption(option_a6b222ab07fe48e28c5a86b2bec9435b);
        });
    </script>




#### 不同城市类别对消费能力的影响


```python
df_city=df_dd['城市类别'].value_counts()
df_city
```




    城市类别
    C    3139
    B    1707
    A    1045
    Name: count, dtype: int64




```python
# 不同城市人数占比
from pyecharts.globals import CurrentConfig,NotebookType
from pyecharts import options as opts
from pyecharts.charts import Pie

x=df_city.index.tolist()
y=df_city.values.tolist()
data_pair=[list(z) for z in zip(x,y)]

c = (
    Pie()
    .add("", data_pair)
    .set_global_opts(title_opts=opts.TitleOpts(title="不同城市人数比重"))
    .set_series_opts(label_opts=opts.LabelOpts(formatter="{b}: {c}-{d}%"))
)
c.render_notebook()
```





<script>
    require.config({
        paths: {
            'echarts':'https://assets.pyecharts.org/assets/v6/echarts.min'
        }
    });
</script>

        <div id="0c9eaf5e5d4e4a6889666675a28fdb49" style="width:900px; height:500px;"></div>

<script>
        require(['echarts'], function(echarts) {
                var chart_0c9eaf5e5d4e4a6889666675a28fdb49 = echarts.init(
                    document.getElementById('0c9eaf5e5d4e4a6889666675a28fdb49'), 'white', {renderer: 'canvas', locale: 'ZH'});
                var option_0c9eaf5e5d4e4a6889666675a28fdb49 = {
    "animation": true,
    "animationThreshold": 2000,
    "animationDuration": 1000,
    "animationEasing": "cubicOut",
    "animationDelay": 0,
    "animationDurationUpdate": 300,
    "animationEasingUpdate": "cubicOut",
    "animationDelayUpdate": 0,
    "aria": {
        "enabled": false
    },
    "series": [
        {
            "type": "pie",
            "colorBy": "data",
            "legendHoverLink": true,
            "selectedMode": false,
            "selectedOffset": 10,
            "clockwise": true,
            "startAngle": 90,
            "minAngle": 0,
            "minShowLabelAngle": 0,
            "avoidLabelOverlap": true,
            "stillShowZeroSum": true,
            "percentPrecision": 2,
            "showEmptyCircle": true,
            "emptyCircleStyle": {
                "color": "lightgray",
                "borderColor": "#000",
                "borderWidth": 0,
                "borderType": "solid",
                "borderDashOffset": 0,
                "borderCap": "butt",
                "borderJoin": "bevel",
                "borderMiterLimit": 10,
                "opacity": 1
            },
            "data": [
                {
                    "name": "C",
                    "value": 3139
                },
                {
                    "name": "B",
                    "value": 1707
                },
                {
                    "name": "A",
                    "value": 1045
                }
            ],
            "radius": [
                "0%",
                "75%"
            ],
            "center": [
                "50%",
                "50%"
            ],
            "label": {
                "show": true,
                "margin": 8,
                "formatter": "{b}: {c}-{d}%",
                "richInheritPlainLabel": true,
                "valueAnimation": false
            },
            "labelLine": {
                "show": true,
                "showAbove": false,
                "length": 15,
                "length2": 15,
                "smooth": false,
                "minTurnAngle": 90,
                "maxSurfaceAngle": 90
            },
            "rippleEffect": {
                "show": true,
                "brushType": "stroke",
                "scale": 2.5,
                "period": 4
            }
        }
    ],
    "legend": [
        {
            "data": [
                "C",
                "B",
                "A"
            ],
            "selected": {},
            "show": true,
            "padding": 5,
            "itemGap": 10,
            "itemWidth": 25,
            "itemHeight": 14,
            "backgroundColor": "transparent",
            "borderColor": "#ccc",
            "borderRadius": 0,
            "pageButtonItemGap": 5,
            "pageButtonPosition": "end",
            "pageFormatter": "{current}/{total}",
            "pageIconColor": "#2f4554",
            "pageIconInactiveColor": "#aaa",
            "pageIconSize": 15,
            "animationDurationUpdate": 800,
            "selector": false,
            "selectorPosition": "auto",
            "selectorItemGap": 7,
            "selectorButtonGap": 10,
            "triggerEvent": false
        }
    ],
    "tooltip": {
        "show": true,
        "trigger": "item",
        "triggerOn": "mousemove|click",
        "axisPointer": {
            "type": "line"
        },
        "showContent": true,
        "alwaysShowContent": false,
        "showDelay": 0,
        "hideDelay": 100,
        "enterable": false,
        "confine": false,
        "appendToBody": false,
        "transitionDuration": 0.4,
        "displayTransition": true,
        "textStyle": {
            "fontSize": 14,
            "richInheritPlainLabel": true
        },
        "borderWidth": 0,
        "padding": 5,
        "order": "seriesAsc"
    },
    "title": [
        {
            "show": true,
            "text": "\u4e0d\u540c\u57ce\u5e02\u4eba\u6570\u6bd4\u91cd",
            "target": "blank",
            "subtarget": "blank",
            "padding": 5,
            "itemGap": 10,
            "textAlign": "auto",
            "textVerticalAlign": "auto",
            "triggerEvent": false
        }
    ]
};
                chart_0c9eaf5e5d4e4a6889666675a28fdb49.setOption(option_0c9eaf5e5d4e4a6889666675a28fdb49);
        });
    </script>





```python
# 不同城市人数统计
from pyecharts import options as opts
from pyecharts.charts import Bar

c = (
    Bar()
    .add_xaxis(df_city.index.tolist())
    .add_yaxis('人数', df_city.values.tolist(),bar_width=69)
    .set_global_opts(title_opts=opts.TitleOpts(title='不同城市人数统计'))
)
c.render_notebook()
```





<script>
    require.config({
        paths: {
            'echarts':'https://assets.pyecharts.org/assets/v6/echarts.min'
        }
    });
</script>

        <div id="89bd1752d145404c9e006d937dd35d82" style="width:900px; height:500px;"></div>

<script>
        require(['echarts'], function(echarts) {
                var chart_89bd1752d145404c9e006d937dd35d82 = echarts.init(
                    document.getElementById('89bd1752d145404c9e006d937dd35d82'), 'white', {renderer: 'canvas', locale: 'ZH'});
                var option_89bd1752d145404c9e006d937dd35d82 = {
    "animation": true,
    "animationThreshold": 2000,
    "animationDuration": 1000,
    "animationEasing": "cubicOut",
    "animationDelay": 0,
    "animationDurationUpdate": 300,
    "animationEasingUpdate": "cubicOut",
    "animationDelayUpdate": 0,
    "aria": {
        "enabled": false
    },
    "series": [
        {
            "type": "bar",
            "name": "\u4eba\u6570",
            "legendHoverLink": true,
            "data": [
                3139,
                1707,
                1045
            ],
            "realtimeSort": false,
            "showBackground": false,
            "stackStrategy": "samesign",
            "cursor": "pointer",
            "barWidth": 69,
            "barMinHeight": 0,
            "barCategoryGap": "20%",
            "barGap": "30%",
            "large": false,
            "largeThreshold": 400,
            "seriesLayoutBy": "column",
            "datasetIndex": 0,
            "clip": true,
            "zlevel": 0,
            "z": 2,
            "label": {
                "show": true,
                "margin": 8,
                "richInheritPlainLabel": true,
                "valueAnimation": false
            }
        }
    ],
    "legend": [
        {
            "data": [
                "\u4eba\u6570"
            ],
            "selected": {},
            "show": true,
            "padding": 5,
            "itemGap": 10,
            "itemWidth": 25,
            "itemHeight": 14,
            "backgroundColor": "transparent",
            "borderColor": "#ccc",
            "borderRadius": 0,
            "pageButtonItemGap": 5,
            "pageButtonPosition": "end",
            "pageFormatter": "{current}/{total}",
            "pageIconColor": "#2f4554",
            "pageIconInactiveColor": "#aaa",
            "pageIconSize": 15,
            "animationDurationUpdate": 800,
            "selector": false,
            "selectorPosition": "auto",
            "selectorItemGap": 7,
            "selectorButtonGap": 10,
            "triggerEvent": false
        }
    ],
    "tooltip": {
        "show": true,
        "trigger": "item",
        "triggerOn": "mousemove|click",
        "axisPointer": {
            "type": "line"
        },
        "showContent": true,
        "alwaysShowContent": false,
        "showDelay": 0,
        "hideDelay": 100,
        "enterable": false,
        "confine": false,
        "appendToBody": false,
        "transitionDuration": 0.4,
        "displayTransition": true,
        "textStyle": {
            "fontSize": 14,
            "richInheritPlainLabel": true
        },
        "borderWidth": 0,
        "padding": 5,
        "order": "seriesAsc"
    },
    "xAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0,
            "data": [
                "C",
                "B",
                "A"
            ]
        }
    ],
    "yAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0
        }
    ],
    "title": [
        {
            "show": true,
            "text": "\u4e0d\u540c\u57ce\u5e02\u4eba\u6570\u7edf\u8ba1",
            "target": "blank",
            "subtarget": "blank",
            "padding": 5,
            "itemGap": 10,
            "textAlign": "auto",
            "textVerticalAlign": "auto",
            "triggerEvent": false
        }
    ]
};
                chart_89bd1752d145404c9e006d937dd35d82.setOption(option_89bd1752d145404c9e006d937dd35d82);
        });
    </script>





```python
# 不同城市的消费统计
city_sum=df_dd.groupby(by='城市类别')['采购额'].sum()
city_sum
```




    城市类别
    A     896457389
    B    1501213804
    C    2619997185
    Name: 采购额, dtype: int64




```python
from pyecharts.globals import CurrentConfig,NotebookType
from pyecharts import options as opts
from pyecharts.charts import Pie

x=city_sum.index.tolist()
y=city_sum.values.tolist()
data_pair=[list(z) for z in zip(x,y)]

c = (
    Pie()
    .add("", data_pair)
    .set_global_opts(title_opts=opts.TitleOpts(title="不同城市对消费能力的影响"))
    .set_series_opts(label_opts=opts.LabelOpts(formatter="{b}: {c}-{d}%"))
)
c.render_notebook()
```





<script>
    require.config({
        paths: {
            'echarts':'https://assets.pyecharts.org/assets/v6/echarts.min'
        }
    });
</script>

        <div id="ec1621a9bb9d4e6abcd5784e93dafbde" style="width:900px; height:500px;"></div>

<script>
        require(['echarts'], function(echarts) {
                var chart_ec1621a9bb9d4e6abcd5784e93dafbde = echarts.init(
                    document.getElementById('ec1621a9bb9d4e6abcd5784e93dafbde'), 'white', {renderer: 'canvas', locale: 'ZH'});
                var option_ec1621a9bb9d4e6abcd5784e93dafbde = {
    "animation": true,
    "animationThreshold": 2000,
    "animationDuration": 1000,
    "animationEasing": "cubicOut",
    "animationDelay": 0,
    "animationDurationUpdate": 300,
    "animationEasingUpdate": "cubicOut",
    "animationDelayUpdate": 0,
    "aria": {
        "enabled": false
    },
    "series": [
        {
            "type": "pie",
            "colorBy": "data",
            "legendHoverLink": true,
            "selectedMode": false,
            "selectedOffset": 10,
            "clockwise": true,
            "startAngle": 90,
            "minAngle": 0,
            "minShowLabelAngle": 0,
            "avoidLabelOverlap": true,
            "stillShowZeroSum": true,
            "percentPrecision": 2,
            "showEmptyCircle": true,
            "emptyCircleStyle": {
                "color": "lightgray",
                "borderColor": "#000",
                "borderWidth": 0,
                "borderType": "solid",
                "borderDashOffset": 0,
                "borderCap": "butt",
                "borderJoin": "bevel",
                "borderMiterLimit": 10,
                "opacity": 1
            },
            "data": [
                {
                    "name": "A",
                    "value": 896457389
                },
                {
                    "name": "B",
                    "value": 1501213804
                },
                {
                    "name": "C",
                    "value": 2619997185
                }
            ],
            "radius": [
                "0%",
                "75%"
            ],
            "center": [
                "50%",
                "50%"
            ],
            "label": {
                "show": true,
                "margin": 8,
                "formatter": "{b}: {c}-{d}%",
                "richInheritPlainLabel": true,
                "valueAnimation": false
            },
            "labelLine": {
                "show": true,
                "showAbove": false,
                "length": 15,
                "length2": 15,
                "smooth": false,
                "minTurnAngle": 90,
                "maxSurfaceAngle": 90
            },
            "rippleEffect": {
                "show": true,
                "brushType": "stroke",
                "scale": 2.5,
                "period": 4
            }
        }
    ],
    "legend": [
        {
            "data": [
                "A",
                "B",
                "C"
            ],
            "selected": {},
            "show": true,
            "padding": 5,
            "itemGap": 10,
            "itemWidth": 25,
            "itemHeight": 14,
            "backgroundColor": "transparent",
            "borderColor": "#ccc",
            "borderRadius": 0,
            "pageButtonItemGap": 5,
            "pageButtonPosition": "end",
            "pageFormatter": "{current}/{total}",
            "pageIconColor": "#2f4554",
            "pageIconInactiveColor": "#aaa",
            "pageIconSize": 15,
            "animationDurationUpdate": 800,
            "selector": false,
            "selectorPosition": "auto",
            "selectorItemGap": 7,
            "selectorButtonGap": 10,
            "triggerEvent": false
        }
    ],
    "tooltip": {
        "show": true,
        "trigger": "item",
        "triggerOn": "mousemove|click",
        "axisPointer": {
            "type": "line"
        },
        "showContent": true,
        "alwaysShowContent": false,
        "showDelay": 0,
        "hideDelay": 100,
        "enterable": false,
        "confine": false,
        "appendToBody": false,
        "transitionDuration": 0.4,
        "displayTransition": true,
        "textStyle": {
            "fontSize": 14,
            "richInheritPlainLabel": true
        },
        "borderWidth": 0,
        "padding": 5,
        "order": "seriesAsc"
    },
    "title": [
        {
            "show": true,
            "text": "\u4e0d\u540c\u57ce\u5e02\u5bf9\u6d88\u8d39\u80fd\u529b\u7684\u5f71\u54cd",
            "target": "blank",
            "subtarget": "blank",
            "padding": 5,
            "itemGap": 10,
            "textAlign": "auto",
            "textVerticalAlign": "auto",
            "triggerEvent": false
        }
    ]
};
                chart_ec1621a9bb9d4e6abcd5784e93dafbde.setOption(option_ec1621a9bb9d4e6abcd5784e93dafbde);
        });
    </script>





```python
# 不同城市人均消费
cost_pj=city_sum/df_city.sort_index()
cost_pj
```




    城市类别
    A    857853.960766
    B    879445.696544
    C    834659.823192
    dtype: float64




```python
# 不同城市人均消费统计
from pyecharts import options as opts
from pyecharts.charts import Bar

c = (
    Bar()
    .add_xaxis(cost_pj.index.tolist())
    .add_yaxis('消费额度', cost_pj.values.tolist(),bar_width=69)
    .set_global_opts(title_opts=opts.TitleOpts(title='不同城市人均消费统计'))
)
c.render_notebook()
```





<script>
    require.config({
        paths: {
            'echarts':'https://assets.pyecharts.org/assets/v6/echarts.min'
        }
    });
</script>

        <div id="ae1183f0fad84f4697a5b7a350452a91" style="width:900px; height:500px;"></div>

<script>
        require(['echarts'], function(echarts) {
                var chart_ae1183f0fad84f4697a5b7a350452a91 = echarts.init(
                    document.getElementById('ae1183f0fad84f4697a5b7a350452a91'), 'white', {renderer: 'canvas', locale: 'ZH'});
                var option_ae1183f0fad84f4697a5b7a350452a91 = {
    "animation": true,
    "animationThreshold": 2000,
    "animationDuration": 1000,
    "animationEasing": "cubicOut",
    "animationDelay": 0,
    "animationDurationUpdate": 300,
    "animationEasingUpdate": "cubicOut",
    "animationDelayUpdate": 0,
    "aria": {
        "enabled": false
    },
    "series": [
        {
            "type": "bar",
            "name": "\u6d88\u8d39\u989d\u5ea6",
            "legendHoverLink": true,
            "data": [
                857853.9607655503,
                879445.6965436438,
                834659.8231920993
            ],
            "realtimeSort": false,
            "showBackground": false,
            "stackStrategy": "samesign",
            "cursor": "pointer",
            "barWidth": 69,
            "barMinHeight": 0,
            "barCategoryGap": "20%",
            "barGap": "30%",
            "large": false,
            "largeThreshold": 400,
            "seriesLayoutBy": "column",
            "datasetIndex": 0,
            "clip": true,
            "zlevel": 0,
            "z": 2,
            "label": {
                "show": true,
                "margin": 8,
                "richInheritPlainLabel": true,
                "valueAnimation": false
            }
        }
    ],
    "legend": [
        {
            "data": [
                "\u6d88\u8d39\u989d\u5ea6"
            ],
            "selected": {},
            "show": true,
            "padding": 5,
            "itemGap": 10,
            "itemWidth": 25,
            "itemHeight": 14,
            "backgroundColor": "transparent",
            "borderColor": "#ccc",
            "borderRadius": 0,
            "pageButtonItemGap": 5,
            "pageButtonPosition": "end",
            "pageFormatter": "{current}/{total}",
            "pageIconColor": "#2f4554",
            "pageIconInactiveColor": "#aaa",
            "pageIconSize": 15,
            "animationDurationUpdate": 800,
            "selector": false,
            "selectorPosition": "auto",
            "selectorItemGap": 7,
            "selectorButtonGap": 10,
            "triggerEvent": false
        }
    ],
    "tooltip": {
        "show": true,
        "trigger": "item",
        "triggerOn": "mousemove|click",
        "axisPointer": {
            "type": "line"
        },
        "showContent": true,
        "alwaysShowContent": false,
        "showDelay": 0,
        "hideDelay": 100,
        "enterable": false,
        "confine": false,
        "appendToBody": false,
        "transitionDuration": 0.4,
        "displayTransition": true,
        "textStyle": {
            "fontSize": 14,
            "richInheritPlainLabel": true
        },
        "borderWidth": 0,
        "padding": 5,
        "order": "seriesAsc"
    },
    "xAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0,
            "data": [
                "A",
                "B",
                "C"
            ]
        }
    ],
    "yAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0
        }
    ],
    "title": [
        {
            "show": true,
            "text": "\u4e0d\u540c\u57ce\u5e02\u4eba\u5747\u6d88\u8d39\u7edf\u8ba1",
            "target": "blank",
            "subtarget": "blank",
            "padding": 5,
            "itemGap": 10,
            "textAlign": "auto",
            "textVerticalAlign": "auto",
            "triggerEvent": false
        }
    ]
};
                chart_ae1183f0fad84f4697a5b7a350452a91.setOption(option_ae1183f0fad84f4697a5b7a350452a91);
        });
    </script>




#### 居住年数对消费的影响


```python
city_live=df_dd.groupby(by='居住城市年数')['用户ID'].count()
city_live
```




    居住城市年数
    0      772
    1     2086
    2     1145
    3      979
    4+     909
    Name: 用户ID, dtype: int64




```python
from pyecharts.globals import CurrentConfig,NotebookType
from pyecharts import options as opts
from pyecharts.charts import Pie

x=['游客','一年','两年','三年','四年及以上']
y=city_live.values.tolist()
data_pair=[list(z) for z in zip(x,y)]

c = (
    Pie()
    .add("", data_pair)
    .set_global_opts(title_opts=opts.TitleOpts(title="城市居住年份数人数占比"))
    .set_series_opts(label_opts=opts.LabelOpts(formatter="{b}: {c}-{d}%"))
)
c.render_notebook()
```





<script>
    require.config({
        paths: {
            'echarts':'https://assets.pyecharts.org/assets/v6/echarts.min'
        }
    });
</script>

        <div id="faa15c149deb470fa5ecddab439e7db5" style="width:900px; height:500px;"></div>

<script>
        require(['echarts'], function(echarts) {
                var chart_faa15c149deb470fa5ecddab439e7db5 = echarts.init(
                    document.getElementById('faa15c149deb470fa5ecddab439e7db5'), 'white', {renderer: 'canvas', locale: 'ZH'});
                var option_faa15c149deb470fa5ecddab439e7db5 = {
    "animation": true,
    "animationThreshold": 2000,
    "animationDuration": 1000,
    "animationEasing": "cubicOut",
    "animationDelay": 0,
    "animationDurationUpdate": 300,
    "animationEasingUpdate": "cubicOut",
    "animationDelayUpdate": 0,
    "aria": {
        "enabled": false
    },
    "series": [
        {
            "type": "pie",
            "colorBy": "data",
            "legendHoverLink": true,
            "selectedMode": false,
            "selectedOffset": 10,
            "clockwise": true,
            "startAngle": 90,
            "minAngle": 0,
            "minShowLabelAngle": 0,
            "avoidLabelOverlap": true,
            "stillShowZeroSum": true,
            "percentPrecision": 2,
            "showEmptyCircle": true,
            "emptyCircleStyle": {
                "color": "lightgray",
                "borderColor": "#000",
                "borderWidth": 0,
                "borderType": "solid",
                "borderDashOffset": 0,
                "borderCap": "butt",
                "borderJoin": "bevel",
                "borderMiterLimit": 10,
                "opacity": 1
            },
            "data": [
                {
                    "name": "\u6e38\u5ba2",
                    "value": 772
                },
                {
                    "name": "\u4e00\u5e74",
                    "value": 2086
                },
                {
                    "name": "\u4e24\u5e74",
                    "value": 1145
                },
                {
                    "name": "\u4e09\u5e74",
                    "value": 979
                },
                {
                    "name": "\u56db\u5e74\u53ca\u4ee5\u4e0a",
                    "value": 909
                }
            ],
            "radius": [
                "0%",
                "75%"
            ],
            "center": [
                "50%",
                "50%"
            ],
            "label": {
                "show": true,
                "margin": 8,
                "formatter": "{b}: {c}-{d}%",
                "richInheritPlainLabel": true,
                "valueAnimation": false
            },
            "labelLine": {
                "show": true,
                "showAbove": false,
                "length": 15,
                "length2": 15,
                "smooth": false,
                "minTurnAngle": 90,
                "maxSurfaceAngle": 90
            },
            "rippleEffect": {
                "show": true,
                "brushType": "stroke",
                "scale": 2.5,
                "period": 4
            }
        }
    ],
    "legend": [
        {
            "data": [
                "\u6e38\u5ba2",
                "\u4e00\u5e74",
                "\u4e24\u5e74",
                "\u4e09\u5e74",
                "\u56db\u5e74\u53ca\u4ee5\u4e0a"
            ],
            "selected": {},
            "show": true,
            "padding": 5,
            "itemGap": 10,
            "itemWidth": 25,
            "itemHeight": 14,
            "backgroundColor": "transparent",
            "borderColor": "#ccc",
            "borderRadius": 0,
            "pageButtonItemGap": 5,
            "pageButtonPosition": "end",
            "pageFormatter": "{current}/{total}",
            "pageIconColor": "#2f4554",
            "pageIconInactiveColor": "#aaa",
            "pageIconSize": 15,
            "animationDurationUpdate": 800,
            "selector": false,
            "selectorPosition": "auto",
            "selectorItemGap": 7,
            "selectorButtonGap": 10,
            "triggerEvent": false
        }
    ],
    "tooltip": {
        "show": true,
        "trigger": "item",
        "triggerOn": "mousemove|click",
        "axisPointer": {
            "type": "line"
        },
        "showContent": true,
        "alwaysShowContent": false,
        "showDelay": 0,
        "hideDelay": 100,
        "enterable": false,
        "confine": false,
        "appendToBody": false,
        "transitionDuration": 0.4,
        "displayTransition": true,
        "textStyle": {
            "fontSize": 14,
            "richInheritPlainLabel": true
        },
        "borderWidth": 0,
        "padding": 5,
        "order": "seriesAsc"
    },
    "title": [
        {
            "show": true,
            "text": "\u57ce\u5e02\u5c45\u4f4f\u5e74\u4efd\u6570\u4eba\u6570\u5360\u6bd4",
            "target": "blank",
            "subtarget": "blank",
            "padding": 5,
            "itemGap": 10,
            "textAlign": "auto",
            "textVerticalAlign": "auto",
            "triggerEvent": false
        }
    ]
};
                chart_faa15c149deb470fa5ecddab439e7db5.setOption(option_faa15c149deb470fa5ecddab439e7db5);
        });
    </script>





```python
# 城市居住年数的消费能力
years_cost=df_dd.groupby(by='居住城市年数')['采购额'].count()
years_cost
```




    居住城市年数
    0      772
    1     2086
    2     1145
    3      979
    4+     909
    Name: 采购额, dtype: int64




```python
from pyecharts.globals import CurrentConfig,NotebookType
from pyecharts import options as opts
from pyecharts.charts import Pie

x=['游客','一年','两年','三年','四年及以上']
y=years_cost.values.tolist()
data_pair=[list(z) for z in zip(x,y)]

c = (
    Pie()
    .add("", data_pair)
    .set_global_opts(title_opts=opts.TitleOpts(title="城市居住年数的消费水平占比"))
    .set_series_opts(label_opts=opts.LabelOpts(formatter="{b}: {c}-{d}%"))
)
c.render_notebook()
```





<script>
    require.config({
        paths: {
            'echarts':'https://assets.pyecharts.org/assets/v6/echarts.min'
        }
    });
</script>

        <div id="2e2ff71a0d0d41f3b6d4415ec762d953" style="width:900px; height:500px;"></div>

<script>
        require(['echarts'], function(echarts) {
                var chart_2e2ff71a0d0d41f3b6d4415ec762d953 = echarts.init(
                    document.getElementById('2e2ff71a0d0d41f3b6d4415ec762d953'), 'white', {renderer: 'canvas', locale: 'ZH'});
                var option_2e2ff71a0d0d41f3b6d4415ec762d953 = {
    "animation": true,
    "animationThreshold": 2000,
    "animationDuration": 1000,
    "animationEasing": "cubicOut",
    "animationDelay": 0,
    "animationDurationUpdate": 300,
    "animationEasingUpdate": "cubicOut",
    "animationDelayUpdate": 0,
    "aria": {
        "enabled": false
    },
    "series": [
        {
            "type": "pie",
            "colorBy": "data",
            "legendHoverLink": true,
            "selectedMode": false,
            "selectedOffset": 10,
            "clockwise": true,
            "startAngle": 90,
            "minAngle": 0,
            "minShowLabelAngle": 0,
            "avoidLabelOverlap": true,
            "stillShowZeroSum": true,
            "percentPrecision": 2,
            "showEmptyCircle": true,
            "emptyCircleStyle": {
                "color": "lightgray",
                "borderColor": "#000",
                "borderWidth": 0,
                "borderType": "solid",
                "borderDashOffset": 0,
                "borderCap": "butt",
                "borderJoin": "bevel",
                "borderMiterLimit": 10,
                "opacity": 1
            },
            "data": [
                {
                    "name": "\u6e38\u5ba2",
                    "value": 772
                },
                {
                    "name": "\u4e00\u5e74",
                    "value": 2086
                },
                {
                    "name": "\u4e24\u5e74",
                    "value": 1145
                },
                {
                    "name": "\u4e09\u5e74",
                    "value": 979
                },
                {
                    "name": "\u56db\u5e74\u53ca\u4ee5\u4e0a",
                    "value": 909
                }
            ],
            "radius": [
                "0%",
                "75%"
            ],
            "center": [
                "50%",
                "50%"
            ],
            "label": {
                "show": true,
                "margin": 8,
                "formatter": "{b}: {c}-{d}%",
                "richInheritPlainLabel": true,
                "valueAnimation": false
            },
            "labelLine": {
                "show": true,
                "showAbove": false,
                "length": 15,
                "length2": 15,
                "smooth": false,
                "minTurnAngle": 90,
                "maxSurfaceAngle": 90
            },
            "rippleEffect": {
                "show": true,
                "brushType": "stroke",
                "scale": 2.5,
                "period": 4
            }
        }
    ],
    "legend": [
        {
            "data": [
                "\u6e38\u5ba2",
                "\u4e00\u5e74",
                "\u4e24\u5e74",
                "\u4e09\u5e74",
                "\u56db\u5e74\u53ca\u4ee5\u4e0a"
            ],
            "selected": {},
            "show": true,
            "padding": 5,
            "itemGap": 10,
            "itemWidth": 25,
            "itemHeight": 14,
            "backgroundColor": "transparent",
            "borderColor": "#ccc",
            "borderRadius": 0,
            "pageButtonItemGap": 5,
            "pageButtonPosition": "end",
            "pageFormatter": "{current}/{total}",
            "pageIconColor": "#2f4554",
            "pageIconInactiveColor": "#aaa",
            "pageIconSize": 15,
            "animationDurationUpdate": 800,
            "selector": false,
            "selectorPosition": "auto",
            "selectorItemGap": 7,
            "selectorButtonGap": 10,
            "triggerEvent": false
        }
    ],
    "tooltip": {
        "show": true,
        "trigger": "item",
        "triggerOn": "mousemove|click",
        "axisPointer": {
            "type": "line"
        },
        "showContent": true,
        "alwaysShowContent": false,
        "showDelay": 0,
        "hideDelay": 100,
        "enterable": false,
        "confine": false,
        "appendToBody": false,
        "transitionDuration": 0.4,
        "displayTransition": true,
        "textStyle": {
            "fontSize": 14,
            "richInheritPlainLabel": true
        },
        "borderWidth": 0,
        "padding": 5,
        "order": "seriesAsc"
    },
    "title": [
        {
            "show": true,
            "text": "\u57ce\u5e02\u5c45\u4f4f\u5e74\u6570\u7684\u6d88\u8d39\u6c34\u5e73\u5360\u6bd4",
            "target": "blank",
            "subtarget": "blank",
            "padding": 5,
            "itemGap": 10,
            "textAlign": "auto",
            "textVerticalAlign": "auto",
            "triggerEvent": false
        }
    ]
};
                chart_2e2ff71a0d0d41f3b6d4415ec762d953.setOption(option_2e2ff71a0d0d41f3b6d4415ec762d953);
        });
    </script>





```python
import pyecharts.options as opts
from pyecharts.charts import Line
from pyecharts.faker import Faker

x=['游客','一年','两年','三年','四年及以上']
y=years_cost.values.tolist()

c = (
    Line()
    .add_xaxis(x)
    .add_yaxis("消费水平", y)
    .set_global_opts(title_opts=opts.TitleOpts(title="城市居住年数的消费水平趋势"))

)
c.render_notebook()
```





<script>
    require.config({
        paths: {
            'echarts':'https://assets.pyecharts.org/assets/v6/echarts.min'
        }
    });
</script>

        <div id="44ddfcfe896e45809a380dc30dab20a2" style="width:900px; height:500px;"></div>

<script>
        require(['echarts'], function(echarts) {
                var chart_44ddfcfe896e45809a380dc30dab20a2 = echarts.init(
                    document.getElementById('44ddfcfe896e45809a380dc30dab20a2'), 'white', {renderer: 'canvas', locale: 'ZH'});
                var option_44ddfcfe896e45809a380dc30dab20a2 = {
    "animation": true,
    "animationThreshold": 2000,
    "animationDuration": 1000,
    "animationEasing": "cubicOut",
    "animationDelay": 0,
    "animationDurationUpdate": 300,
    "animationEasingUpdate": "cubicOut",
    "animationDelayUpdate": 0,
    "aria": {
        "enabled": false
    },
    "series": [
        {
            "type": "line",
            "name": "\u6d88\u8d39\u6c34\u5e73",
            "connectNulls": false,
            "xAxisIndex": 0,
            "symbolSize": 4,
            "showSymbol": true,
            "smooth": false,
            "clip": true,
            "step": false,
            "stackStrategy": "samesign",
            "data": [
                [
                    "\u6e38\u5ba2",
                    772
                ],
                [
                    "\u4e00\u5e74",
                    2086
                ],
                [
                    "\u4e24\u5e74",
                    1145
                ],
                [
                    "\u4e09\u5e74",
                    979
                ],
                [
                    "\u56db\u5e74\u53ca\u4ee5\u4e0a",
                    909
                ]
            ],
            "hoverAnimation": true,
            "label": {
                "show": true,
                "margin": 8,
                "richInheritPlainLabel": true,
                "valueAnimation": false
            },
            "logBase": 10,
            "seriesLayoutBy": "column",
            "lineStyle": {
                "show": false
            },
            "areaStyle": {
                "opacity": 0
            },
            "zlevel": 0,
            "z": 0
        }
    ],
    "legend": [
        {
            "data": [
                "\u6d88\u8d39\u6c34\u5e73"
            ],
            "selected": {},
            "show": true,
            "padding": 5,
            "itemGap": 10,
            "itemWidth": 25,
            "itemHeight": 14,
            "backgroundColor": "transparent",
            "borderColor": "#ccc",
            "borderRadius": 0,
            "pageButtonItemGap": 5,
            "pageButtonPosition": "end",
            "pageFormatter": "{current}/{total}",
            "pageIconColor": "#2f4554",
            "pageIconInactiveColor": "#aaa",
            "pageIconSize": 15,
            "animationDurationUpdate": 800,
            "selector": false,
            "selectorPosition": "auto",
            "selectorItemGap": 7,
            "selectorButtonGap": 10,
            "triggerEvent": false
        }
    ],
    "tooltip": {
        "show": true,
        "trigger": "item",
        "triggerOn": "mousemove|click",
        "axisPointer": {
            "type": "line"
        },
        "showContent": true,
        "alwaysShowContent": false,
        "showDelay": 0,
        "hideDelay": 100,
        "enterable": false,
        "confine": false,
        "appendToBody": false,
        "transitionDuration": 0.4,
        "displayTransition": true,
        "textStyle": {
            "fontSize": 14,
            "richInheritPlainLabel": true
        },
        "borderWidth": 0,
        "padding": 5,
        "order": "seriesAsc"
    },
    "xAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0,
            "data": [
                "\u6e38\u5ba2",
                "\u4e00\u5e74",
                "\u4e24\u5e74",
                "\u4e09\u5e74",
                "\u56db\u5e74\u53ca\u4ee5\u4e0a"
            ]
        }
    ],
    "yAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0
        }
    ],
    "title": [
        {
            "show": true,
            "text": "\u57ce\u5e02\u5c45\u4f4f\u5e74\u6570\u7684\u6d88\u8d39\u6c34\u5e73\u8d8b\u52bf",
            "target": "blank",
            "subtarget": "blank",
            "padding": 5,
            "itemGap": 10,
            "textAlign": "auto",
            "textVerticalAlign": "auto",
            "triggerEvent": false
        }
    ]
};
                chart_44ddfcfe896e45809a380dc30dab20a2.setOption(option_44ddfcfe896e45809a380dc30dab20a2);
        });
    </script>





```python
from pyecharts import options as opts
from pyecharts.charts import Bar

c = (
    Bar()
    .add_xaxis(['游客','一年','两年','三年','四年及以上'])
    .add_yaxis('消费水平', years_cost.values.tolist(),bar_width=69)
    .set_global_opts(title_opts=opts.TitleOpts(title='城市居住年份消费统计'))
)
c.render_notebook()
```





<script>
    require.config({
        paths: {
            'echarts':'https://assets.pyecharts.org/assets/v6/echarts.min'
        }
    });
</script>

        <div id="56f4da0f6bf2447b998ac3adf15cac1f" style="width:900px; height:500px;"></div>

<script>
        require(['echarts'], function(echarts) {
                var chart_56f4da0f6bf2447b998ac3adf15cac1f = echarts.init(
                    document.getElementById('56f4da0f6bf2447b998ac3adf15cac1f'), 'white', {renderer: 'canvas', locale: 'ZH'});
                var option_56f4da0f6bf2447b998ac3adf15cac1f = {
    "animation": true,
    "animationThreshold": 2000,
    "animationDuration": 1000,
    "animationEasing": "cubicOut",
    "animationDelay": 0,
    "animationDurationUpdate": 300,
    "animationEasingUpdate": "cubicOut",
    "animationDelayUpdate": 0,
    "aria": {
        "enabled": false
    },
    "series": [
        {
            "type": "bar",
            "name": "\u6d88\u8d39\u6c34\u5e73",
            "legendHoverLink": true,
            "data": [
                772,
                2086,
                1145,
                979,
                909
            ],
            "realtimeSort": false,
            "showBackground": false,
            "stackStrategy": "samesign",
            "cursor": "pointer",
            "barWidth": 69,
            "barMinHeight": 0,
            "barCategoryGap": "20%",
            "barGap": "30%",
            "large": false,
            "largeThreshold": 400,
            "seriesLayoutBy": "column",
            "datasetIndex": 0,
            "clip": true,
            "zlevel": 0,
            "z": 2,
            "label": {
                "show": true,
                "margin": 8,
                "richInheritPlainLabel": true,
                "valueAnimation": false
            }
        }
    ],
    "legend": [
        {
            "data": [
                "\u6d88\u8d39\u6c34\u5e73"
            ],
            "selected": {},
            "show": true,
            "padding": 5,
            "itemGap": 10,
            "itemWidth": 25,
            "itemHeight": 14,
            "backgroundColor": "transparent",
            "borderColor": "#ccc",
            "borderRadius": 0,
            "pageButtonItemGap": 5,
            "pageButtonPosition": "end",
            "pageFormatter": "{current}/{total}",
            "pageIconColor": "#2f4554",
            "pageIconInactiveColor": "#aaa",
            "pageIconSize": 15,
            "animationDurationUpdate": 800,
            "selector": false,
            "selectorPosition": "auto",
            "selectorItemGap": 7,
            "selectorButtonGap": 10,
            "triggerEvent": false
        }
    ],
    "tooltip": {
        "show": true,
        "trigger": "item",
        "triggerOn": "mousemove|click",
        "axisPointer": {
            "type": "line"
        },
        "showContent": true,
        "alwaysShowContent": false,
        "showDelay": 0,
        "hideDelay": 100,
        "enterable": false,
        "confine": false,
        "appendToBody": false,
        "transitionDuration": 0.4,
        "displayTransition": true,
        "textStyle": {
            "fontSize": 14,
            "richInheritPlainLabel": true
        },
        "borderWidth": 0,
        "padding": 5,
        "order": "seriesAsc"
    },
    "xAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0,
            "data": [
                "\u6e38\u5ba2",
                "\u4e00\u5e74",
                "\u4e24\u5e74",
                "\u4e09\u5e74",
                "\u56db\u5e74\u53ca\u4ee5\u4e0a"
            ]
        }
    ],
    "yAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0
        }
    ],
    "title": [
        {
            "show": true,
            "text": "\u57ce\u5e02\u5c45\u4f4f\u5e74\u4efd\u6d88\u8d39\u7edf\u8ba1",
            "target": "blank",
            "subtarget": "blank",
            "padding": 5,
            "itemGap": 10,
            "textAlign": "auto",
            "textVerticalAlign": "auto",
            "triggerEvent": false
        }
    ]
};
                chart_56f4da0f6bf2447b998ac3adf15cac1f.setOption(option_56f4da0f6bf2447b998ac3adf15cac1f);
        });
    </script>




#### 不同职业对消费的影响


```python
df_dd.head()
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
      <th>用户ID</th>
      <th>商品ID</th>
      <th>性别</th>
      <th>年龄</th>
      <th>职业</th>
      <th>城市类别</th>
      <th>居住城市年数</th>
      <th>婚姻状况</th>
      <th>采购额</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000001</td>
      <td>P00069042</td>
      <td>F</td>
      <td>0-17</td>
      <td>10</td>
      <td>A</td>
      <td>2</td>
      <td>0</td>
      <td>44108</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1000002</td>
      <td>P00285442</td>
      <td>M</td>
      <td>55+</td>
      <td>16</td>
      <td>C</td>
      <td>4+</td>
      <td>0</td>
      <td>44432</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1000003</td>
      <td>P00193542</td>
      <td>M</td>
      <td>26-35</td>
      <td>15</td>
      <td>A</td>
      <td>3</td>
      <td>0</td>
      <td>45551</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1000004</td>
      <td>P00184942</td>
      <td>M</td>
      <td>46-50</td>
      <td>7</td>
      <td>B</td>
      <td>2</td>
      <td>1</td>
      <td>46070</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1000005</td>
      <td>P00274942</td>
      <td>M</td>
      <td>26-35</td>
      <td>20</td>
      <td>A</td>
      <td>1</td>
      <td>1</td>
      <td>46091</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 各职业人数统计
work_count=df_dd['职业'].value_counts().sort_values()
work_count
```




    职业
    8      17
    18     67
    19     71
    9      88
    5     111
    11    128
    13    140
    15    140
    3     170
    10    192
    6     228
    16    235
    2     256
    20    273
    14    294
    12    376
    17    491
    1     517
    7     669
    0     688
    4     740
    Name: count, dtype: int64




```python
from pyecharts import options as opts
from pyecharts.charts import Bar

c = (
    Bar()
    .add_xaxis(work_count.index.tolist())
    .add_yaxis('消费水平', work_count.values.tolist())
    .set_global_opts(title_opts=opts.TitleOpts(title='不同职业人数统计'))
)
c.render_notebook()
```





<script>
    require.config({
        paths: {
            'echarts':'https://assets.pyecharts.org/assets/v6/echarts.min'
        }
    });
</script>

        <div id="d07248b69030408babba93bf44fcb919" style="width:900px; height:500px;"></div>

<script>
        require(['echarts'], function(echarts) {
                var chart_d07248b69030408babba93bf44fcb919 = echarts.init(
                    document.getElementById('d07248b69030408babba93bf44fcb919'), 'white', {renderer: 'canvas', locale: 'ZH'});
                var option_d07248b69030408babba93bf44fcb919 = {
    "animation": true,
    "animationThreshold": 2000,
    "animationDuration": 1000,
    "animationEasing": "cubicOut",
    "animationDelay": 0,
    "animationDurationUpdate": 300,
    "animationEasingUpdate": "cubicOut",
    "animationDelayUpdate": 0,
    "aria": {
        "enabled": false
    },
    "series": [
        {
            "type": "bar",
            "name": "\u6d88\u8d39\u6c34\u5e73",
            "legendHoverLink": true,
            "data": [
                17,
                67,
                71,
                88,
                111,
                128,
                140,
                140,
                170,
                192,
                228,
                235,
                256,
                273,
                294,
                376,
                491,
                517,
                669,
                688,
                740
            ],
            "realtimeSort": false,
            "showBackground": false,
            "stackStrategy": "samesign",
            "cursor": "pointer",
            "barMinHeight": 0,
            "barCategoryGap": "20%",
            "barGap": "30%",
            "large": false,
            "largeThreshold": 400,
            "seriesLayoutBy": "column",
            "datasetIndex": 0,
            "clip": true,
            "zlevel": 0,
            "z": 2,
            "label": {
                "show": true,
                "margin": 8,
                "richInheritPlainLabel": true,
                "valueAnimation": false
            }
        }
    ],
    "legend": [
        {
            "data": [
                "\u6d88\u8d39\u6c34\u5e73"
            ],
            "selected": {},
            "show": true,
            "padding": 5,
            "itemGap": 10,
            "itemWidth": 25,
            "itemHeight": 14,
            "backgroundColor": "transparent",
            "borderColor": "#ccc",
            "borderRadius": 0,
            "pageButtonItemGap": 5,
            "pageButtonPosition": "end",
            "pageFormatter": "{current}/{total}",
            "pageIconColor": "#2f4554",
            "pageIconInactiveColor": "#aaa",
            "pageIconSize": 15,
            "animationDurationUpdate": 800,
            "selector": false,
            "selectorPosition": "auto",
            "selectorItemGap": 7,
            "selectorButtonGap": 10,
            "triggerEvent": false
        }
    ],
    "tooltip": {
        "show": true,
        "trigger": "item",
        "triggerOn": "mousemove|click",
        "axisPointer": {
            "type": "line"
        },
        "showContent": true,
        "alwaysShowContent": false,
        "showDelay": 0,
        "hideDelay": 100,
        "enterable": false,
        "confine": false,
        "appendToBody": false,
        "transitionDuration": 0.4,
        "displayTransition": true,
        "textStyle": {
            "fontSize": 14,
            "richInheritPlainLabel": true
        },
        "borderWidth": 0,
        "padding": 5,
        "order": "seriesAsc"
    },
    "xAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0,
            "data": [
                8,
                18,
                19,
                9,
                5,
                11,
                13,
                15,
                3,
                10,
                6,
                16,
                2,
                20,
                14,
                12,
                17,
                1,
                7,
                0,
                4
            ]
        }
    ],
    "yAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0
        }
    ],
    "title": [
        {
            "show": true,
            "text": "\u4e0d\u540c\u804c\u4e1a\u4eba\u6570\u7edf\u8ba1",
            "target": "blank",
            "subtarget": "blank",
            "padding": 5,
            "itemGap": 10,
            "textAlign": "auto",
            "textVerticalAlign": "auto",
            "triggerEvent": false
        }
    ]
};
                chart_d07248b69030408babba93bf44fcb919.setOption(option_d07248b69030408babba93bf44fcb919);
        });
    </script>





```python
work_cost=df_dd.groupby(by='职业')['采购额'].count()
work_cost
```




    职业
    0     688
    1     517
    2     256
    3     170
    4     740
    5     111
    6     228
    7     669
    8      17
    9      88
    10    192
    11    128
    12    376
    13    140
    14    294
    15    140
    16    235
    17    491
    18     67
    19     71
    20    273
    Name: 采购额, dtype: int64




```python
from pyecharts import options as opts
from pyecharts.charts import Bar

c = (
    Bar()
    .add_xaxis(work_cost.index.tolist())
    .add_yaxis('消费水平', work_cost.values.tolist())
    .set_global_opts(title_opts=opts.TitleOpts(title='不同职业消费水平统计'))
)
c.render_notebook()
```





<script>
    require.config({
        paths: {
            'echarts':'https://assets.pyecharts.org/assets/v6/echarts.min'
        }
    });
</script>

        <div id="07f7e6eac7f44636b05689bb5f0e9e03" style="width:900px; height:500px;"></div>

<script>
        require(['echarts'], function(echarts) {
                var chart_07f7e6eac7f44636b05689bb5f0e9e03 = echarts.init(
                    document.getElementById('07f7e6eac7f44636b05689bb5f0e9e03'), 'white', {renderer: 'canvas', locale: 'ZH'});
                var option_07f7e6eac7f44636b05689bb5f0e9e03 = {
    "animation": true,
    "animationThreshold": 2000,
    "animationDuration": 1000,
    "animationEasing": "cubicOut",
    "animationDelay": 0,
    "animationDurationUpdate": 300,
    "animationEasingUpdate": "cubicOut",
    "animationDelayUpdate": 0,
    "aria": {
        "enabled": false
    },
    "series": [
        {
            "type": "bar",
            "name": "\u6d88\u8d39\u6c34\u5e73",
            "legendHoverLink": true,
            "data": [
                688,
                517,
                256,
                170,
                740,
                111,
                228,
                669,
                17,
                88,
                192,
                128,
                376,
                140,
                294,
                140,
                235,
                491,
                67,
                71,
                273
            ],
            "realtimeSort": false,
            "showBackground": false,
            "stackStrategy": "samesign",
            "cursor": "pointer",
            "barMinHeight": 0,
            "barCategoryGap": "20%",
            "barGap": "30%",
            "large": false,
            "largeThreshold": 400,
            "seriesLayoutBy": "column",
            "datasetIndex": 0,
            "clip": true,
            "zlevel": 0,
            "z": 2,
            "label": {
                "show": true,
                "margin": 8,
                "richInheritPlainLabel": true,
                "valueAnimation": false
            }
        }
    ],
    "legend": [
        {
            "data": [
                "\u6d88\u8d39\u6c34\u5e73"
            ],
            "selected": {},
            "show": true,
            "padding": 5,
            "itemGap": 10,
            "itemWidth": 25,
            "itemHeight": 14,
            "backgroundColor": "transparent",
            "borderColor": "#ccc",
            "borderRadius": 0,
            "pageButtonItemGap": 5,
            "pageButtonPosition": "end",
            "pageFormatter": "{current}/{total}",
            "pageIconColor": "#2f4554",
            "pageIconInactiveColor": "#aaa",
            "pageIconSize": 15,
            "animationDurationUpdate": 800,
            "selector": false,
            "selectorPosition": "auto",
            "selectorItemGap": 7,
            "selectorButtonGap": 10,
            "triggerEvent": false
        }
    ],
    "tooltip": {
        "show": true,
        "trigger": "item",
        "triggerOn": "mousemove|click",
        "axisPointer": {
            "type": "line"
        },
        "showContent": true,
        "alwaysShowContent": false,
        "showDelay": 0,
        "hideDelay": 100,
        "enterable": false,
        "confine": false,
        "appendToBody": false,
        "transitionDuration": 0.4,
        "displayTransition": true,
        "textStyle": {
            "fontSize": 14,
            "richInheritPlainLabel": true
        },
        "borderWidth": 0,
        "padding": 5,
        "order": "seriesAsc"
    },
    "xAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0,
            "data": [
                0,
                1,
                2,
                3,
                4,
                5,
                6,
                7,
                8,
                9,
                10,
                11,
                12,
                13,
                14,
                15,
                16,
                17,
                18,
                19,
                20
            ]
        }
    ],
    "yAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "nameTruncate": {},
            "nameMoveOverlap": true,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "silent": false,
            "triggerEvent": false,
            "splitLine": {
                "show": true,
                "lineStyle": {
                    "show": false
                }
            },
            "animation": true,
            "animationThreshold": 2000,
            "animationDuration": 1000,
            "animationEasing": "cubicOut",
            "animationDelay": 0,
            "animationDurationUpdate": 300,
            "animationEasingUpdate": "cubicOut",
            "animationDelayUpdate": 0
        }
    ],
    "title": [
        {
            "show": true,
            "text": "\u4e0d\u540c\u804c\u4e1a\u6d88\u8d39\u6c34\u5e73\u7edf\u8ba1",
            "target": "blank",
            "subtarget": "blank",
            "padding": 5,
            "itemGap": 10,
            "textAlign": "auto",
            "textVerticalAlign": "auto",
            "triggerEvent": false
        }
    ]
};
                chart_07f7e6eac7f44636b05689bb5f0e9e03.setOption(option_07f7e6eac7f44636b05689bb5f0e9e03);
        });
    </script>




## 总结

- 性别方面: 男性的消费能力比女性要高
- 婚否: 消费人数上,未婚比已婚的消费人数要多;
      已婚的人群不管是男性还是女性, 比未婚的人群消费能力要低
      总体上从未婚到已婚消费的趋势会下降, 男性下降的幅度比女性下降的幅度要大
- 年龄: 18 - 45 年龄范围的人, 消费能力要强
- 城市: BC 两城市人均消费高, 猜测可能是中大型城市, 购买力要强
- 居住年份: 随着居住年份的增加, 消费能力会降低
- 职业: 不同职业消费人数和消费能力差异化比较大, 重点可以吧营销放在人数多切消费能力高的职业上[12 17 1 7 0 4]
