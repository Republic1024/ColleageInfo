```python
import pandas as pd
```


```python
df = pd.read_excel("../浙江工业大学/计算机学院各专业2022年硕士研究生复试考生名单.xlsx")
```


```python
df[:5]
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
      <th>序号</th>
      <th>考生类型</th>
      <th>学生代码</th>
      <th>姓名</th>
      <th>第一志愿</th>
      <th>大类专业</th>
      <th>录取专业</th>
      <th>专业类型</th>
      <th>外语</th>
      <th>政治</th>
      <th>业务课一</th>
      <th>业务课二</th>
      <th>总分</th>
      <th>录取代码</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>第一批一志愿考生</td>
      <td>103372210006660</td>
      <td>陈天涯</td>
      <td>浙江工业大学</td>
      <td>081200计算机科学与技术</td>
      <td>081200计算机科学与技术</td>
      <td>全日制</td>
      <td>80</td>
      <td>73</td>
      <td>110</td>
      <td>120</td>
      <td>383</td>
      <td>ZG0812-001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>第一批一志愿考生</td>
      <td>103372210009385</td>
      <td>伊秋华</td>
      <td>浙江工业大学</td>
      <td>081200计算机科学与技术</td>
      <td>081200计算机科学与技术</td>
      <td>全日制</td>
      <td>74</td>
      <td>66</td>
      <td>111</td>
      <td>130</td>
      <td>381</td>
      <td>ZG0812-002</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>第一批一志愿考生</td>
      <td>103372210006633</td>
      <td>吴康惠</td>
      <td>浙江工业大学</td>
      <td>081200计算机科学与技术</td>
      <td>081200计算机科学与技术</td>
      <td>全日制</td>
      <td>78</td>
      <td>66</td>
      <td>117</td>
      <td>120</td>
      <td>381</td>
      <td>ZG0812-003</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>第一批一志愿考生</td>
      <td>103372210009382</td>
      <td>严涵婷</td>
      <td>浙江工业大学</td>
      <td>081200计算机科学与技术</td>
      <td>081200计算机科学与技术</td>
      <td>全日制</td>
      <td>77</td>
      <td>77</td>
      <td>99</td>
      <td>121</td>
      <td>374</td>
      <td>ZG0812-004</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>第一批一志愿考生</td>
      <td>103372210006653</td>
      <td>沈哲辉</td>
      <td>浙江工业大学</td>
      <td>081200计算机科学与技术</td>
      <td>081200计算机科学与技术</td>
      <td>全日制</td>
      <td>69</td>
      <td>73</td>
      <td>128</td>
      <td>104</td>
      <td>374</td>
      <td>ZG0812-005</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.columns
```




    Index(['序号', '考生类型', '学生代码', '姓名', '第一志愿', '大类专业', '录取专业', '专业类型', '外语', '政治',
           '业务课一', '业务课二', '总分', '录取代码'],
          dtype='object')




```python

# pattern=r'^((?!士兵专项).)*$'
# df[df['录取代码'].str.extract(pattern)]
df = df[~df['录取代码'].str.contains('士兵')]
```


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 390 entries, 0 to 389
    Data columns (total 14 columns):
     #   Column  Non-Null Count  Dtype 
    ---  ------  --------------  ----- 
     0   序号      390 non-null    int64 
     1   考生类型    390 non-null    object
     2   学生代码    390 non-null    int64 
     3   姓名      390 non-null    object
     4   第一志愿    390 non-null    object
     5   大类专业    390 non-null    object
     6   录取专业    390 non-null    object
     7   专业类型    390 non-null    object
     8   外语      390 non-null    int64 
     9   政治      390 non-null    int64 
     10  业务课一    390 non-null    int64 
     11  业务课二    390 non-null    int64 
     12  总分      390 non-null    int64 
     13  录取代码    390 non-null    object
    dtypes: int64(7), object(7)
    memory usage: 45.7+ KB



```python
df_1 = df.groupby(by=['录取专业'])['总分'].describe()
df_1.to_excel("各专业分数情况.xlsx")
df_1
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
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
    <tr>
      <th>录取专业</th>
      <th></th>
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
      <th>081200计算机科学与技术</th>
      <td>97.0</td>
      <td>330.185567</td>
      <td>21.762128</td>
      <td>300.0</td>
      <td>313.0</td>
      <td>327.0</td>
      <td>345.0</td>
      <td>383.0</td>
    </tr>
    <tr>
      <th>083500软件工程</th>
      <td>41.0</td>
      <td>317.365854</td>
      <td>19.852904</td>
      <td>284.0</td>
      <td>302.0</td>
      <td>320.0</td>
      <td>329.0</td>
      <td>360.0</td>
    </tr>
    <tr>
      <th>085400电子信息</th>
      <td>252.0</td>
      <td>360.456349</td>
      <td>18.752797</td>
      <td>318.0</td>
      <td>350.0</td>
      <td>360.0</td>
      <td>372.0</td>
      <td>407.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
!jupyter nbconvert --to markdown process_data.ipynb 
```

    [NbConvertApp] Converting notebook process_data.ipynb to markdown
    [NbConvertApp] Writing 5391 bytes to process_data.md

