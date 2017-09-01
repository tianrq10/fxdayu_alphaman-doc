#####**factor_calculator**
- ` fxdayu_alphaman.factor.factor.Factor.factor_calculator(pn_data) `

**简要描述：**

- 继承自Factor的自定义因子需在此方法下实现因子的计算逻辑

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|pn_data |是  |pandas.Panel |时间为索引,按资产分类的一张时间序列数据表,用于计算因子的初始所需数据 pandas.Panel类型 一共三个维度。items axis 为股票代码,包含所有该因子跟踪的股票;在这之下,每只股票对应一个pandas.Dataframe,对应这只股票需要被访问到的数据,index为时间,columns为数据字段名称。|

**参数示例:**

```
<class 'pandas.core.panel.Panel'>
Dimensions: 196 (items) x 335 (major_axis) x 5 (minor_axis)
Items axis: 600011.XSHG to 300450.XSHG
Major_axis axis: 2015-12-02 15:00:00 to 2017-04-18 15:00:00
Minor_axis axis: close to volume
```


 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|factor_value |pandas.MultiIndex   |A MultiIndex Series indexed by date (level 0) and asset (level 1), containing the values for a single alpha factor |

**返回示例:**
```
  -----------------------------------
  date         |    asset   |
  -----------------------------------
               |   AAPL     |   0.5
               -----------------------
               |   BA       |  -1.1
               -----------------------
  2014-01-01   |   CMG      |   1.7
               -----------------------
               |   DAL      |  -0.1
               -----------------------
               |   LULU     |   2.7
               -----------------------
```

#####**get_factor**
- ` fxdayu_alphaman.factor.factor.Factor.get_factor(pn_data, update=False)`

**简要描述：**

- 获得因子值

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|pn_data |是  |pandas.Panel |时间为索引,按资产分类的一张时间序列数据表,用于计算因子的初始所需数据 pandas.Panel类型 一共三个维度。items axis 为股票代码,包含所有该因子跟踪的股票;在这之下,每只股票对应一个pandas.Dataframe,对应这只股票需要被访问到的数据,index为时间,columns为数据字段名称。|
|update   |否|bool |是否更新因子值(bool),默认为False,即在该factor实例被销毁前,因子值以第一次计算为准。否则每次取因子值都会重新计算。  |


**参数示例:**

- pn_data:

```
<class 'pandas.core.panel.Panel'>
Dimensions: 196 (items) x 335 (major_axis) x 5 (minor_axis)
Items axis: 600011.XSHG to 300450.XSHG
Major_axis axis: 2015-12-02 15:00:00 to 2017-04-18 15:00:00
Minor_axis axis: close to volume
```

- update:

```
False
```

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|factor_value |pandas.MultiIndex   |A MultiIndex Series indexed by date (level 0) and asset (level 1), containing the values for a single alpha factor |

**返回示例:**
```
  -----------------------------------
  date         |    asset   |
  -----------------------------------
               |   AAPL     |   0.5
               -----------------------
               |   BA       |  -1.1
               -----------------------
  2014-01-01   |   CMG      |   1.7
               -----------------------
               |   DAL      |  -0.1
               -----------------------
               |   LULU     |   2.7
               -----------------------
```

#####**factor_df_to_factor_mi**
- ` fxdayu_alphaman.factor.factor.Factor.factor_df_to_factor_mi(factor_df) `

**简要描述：**

- 将pandas.Dataframe格式的因子值调整为以date(level0),asset(level1)为索引的MultiIndex格式

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|factor_df |是  |pandas.Dataframe|因子值 (pandas.Dataframe类型),index为datetime, colunms为股票代码(asset)。|

**参数示例:**
```
                AAPL	　　　BA	　　　CMG	　　   DAL	     LULU	　　
 date
 2016-06-24	0.165260	0.002198	0.085632	-0.078074	0.173832
 2016-06-27	0.165537	0.003583	0.063299	-0.048674	0.180890
 2016-06-28	0.135215	0.010403	0.059038	-0.034879	0.111691
 2016-06-29	0.068774	0.019848	0.058476	-0.049971	0.042805
 2016-06-30	0.039431	0.012271	0.037432	-0.027272	0.010902
```

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|factor_value |pandas.MultiIndex   |A MultiIndex Series indexed by date (level 0) and asset (level 1), containing the values for a single alpha factor |

**返回示例:**
```
  -----------------------------------
  date         |    asset   |
  -----------------------------------
               |   AAPL     |   0.5
               -----------------------
               |   BA       |  -1.1
               -----------------------
  2014-01-01   |   CMG      |   1.7
               -----------------------
               |   DAL      |  -0.1
               -----------------------
               |   LULU     |   2.7
               -----------------------
```

#####**get_factor_by_rankScore**
- ` fxdayu_alphaman.factor.factor.Factor.get_factor_by_rankScore(factor, ascending = True) `

**简要描述：**

-  输入multiIndex格式的因子值, 将因子用排序分值重构,并处理到0-1之间(默认为升序——因子越大 排序分值越大(越好)

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|factor |是  |pandas.MultiIndex|A MultiIndex Series indexed by date (level 0) and asset (level 1), containing the values for a single alpha factor.|
|ascending|否|bool |因子值按升序法排序对应还是降序法排序对应。具体根据因子对收益的相关关系而定,为正则应用升序,为负用降序|

**参数示例:**

-  factor:

```
  -----------------------------------
  date         |    asset   |
  -----------------------------------
               |   AAPL     |   0.5
               -----------------------
               |   BA       |  -1.1
               -----------------------
  2014-01-01   |   CMG      |   1.7
               -----------------------
               |   DAL      |  -0.1
               -----------------------
               |   LULU     |   2.7
               -----------------------
```

-  ascending:

```
 True
```

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|factor_value |pandas.MultiIndex   |重构后的因子值。A MultiIndex Series indexed by date (level 0) and asset (level 1), containing the values for a single alpha factor. 取值范围在0-1之间 |

**返回示例:**
```
  -----------------------------------
  date         |    asset   |
  -----------------------------------
               |   AAPL     |   0.5
               -----------------------
               |   BA       |   0.1
               -----------------------
  2014-01-01   |   CMG      |   0.7
               -----------------------
               |   DAL      |   0.1
               -----------------------
               |   LULU     |   0.9
               -----------------------
```

#####**get_disturbed_factor**
- ` fxdayu_alphaman.factor.factor.Factor.get_disturbed_factor(factor) `

**简要描述：**

-  输入multiIndex格式的因子值, 将因子值加一个极小的扰动项,用于做quantile区分

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|factor |是  |pandas.MultiIndex|A MultiIndex Series indexed by date (level 0) and asset (level 1), containing the values for a single alpha factor.|

**参数示例:**

```
  -----------------------------------
  date         |    asset   |
  -----------------------------------
               |   AAPL     |   0.5
               -----------------------
               |   BA       |  -1.1
               -----------------------
  2014-01-01   |   CMG      |   1.7
               -----------------------
               |   DAL      |  -0.1
               -----------------------
               |   LULU     |   2.7
               -----------------------
```

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|factor_value |pandas.MultiIndex   |重构后的因子值,每个值加了一个极小的扰动项。A MultiIndex Series indexed by date (level 0) and asset (level 1), containing the values for a single alpha factor. 取值范围在0-1之间 |

**返回示例:**
```
  -----------------------------------
  date         |    asset   |
  -----------------------------------
               |   AAPL     |   0.5
               -----------------------
               |   BA       |  -1.1
               -----------------------
  2014-01-01   |   CMG      |   1.7
               -----------------------
               |   DAL      |  -0.1
               -----------------------
               |   LULU     |   2.7
               -----------------------
```


#####**winsorize**
- ` fxdayu_alphaman.factor.factor.Factor.winsorize(factor_df) `

**简要描述：**

-  横截面去极值 - 对Dataframe类型的因子值

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|factor_df |是  |pandas.Dataframe|因子值 (pandas.Dataframe类型),index为datetime, colunms为股票代码(asset)。|

**参数示例:**
```
                AAPL	　　　BA	　　　CMG	　　   DAL	     LULU	　　
 date
 2016-06-24	0.165260	0.002198	0.085632	-0.078074	0.173832
 2016-06-27	0.165537	0.003583	0.063299	-0.048674	0.180890
 2016-06-28	0.135215	0.010403	0.059038	-0.034879	0.111691
 2016-06-29	0.068774	0.019848	0.058476	-0.049971	0.042805
 2016-06-30	0.039431	0.012271	0.037432	-0.027272	0.010902
```

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
| factor_df   |pandas.Dataframe  |去极值后的因子值(pandas.Dataframe类型),index为datetime, colunms为股票代码。 |

#####**standardize**
- ` fxdayu_alphaman.factor.factor.Factor.standardize(factor_df) `

**简要描述：**

-  横截面z-score标准化 - 对Dataframe类型的因子值

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|factor_df |是  |pandas.Dataframe|因子值 (pandas.Dataframe类型),index为datetime, colunms为股票代码(asset)。|

**参数示例:**
```
                AAPL	　　　BA	　　　CMG	　　   DAL	     LULU	　　
 date
 2016-06-24	0.165260	0.002198	0.085632	-0.078074	0.173832
 2016-06-27	0.165537	0.003583	0.063299	-0.048674	0.180890
 2016-06-28	0.135215	0.010403	0.059038	-0.034879	0.111691
 2016-06-29	0.068774	0.019848	0.058476	-0.049971	0.042805
 2016-06-30	0.039431	0.012271	0.037432	-0.027272	0.010902
```

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
| factor_df   |pandas.Dataframe  |z-score标准化后的因子值(pandas.Dataframe类型),index为datetime, colunms为股票代码。 |

#####**neutralize**
- ` fxdayu_alphaman.factor.factor.Factor.neutralize(factor_df,factorIsMV = False) `

**简要描述：**

-  行业、市值中性化 - 对Dataframe类型的因子值

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|factor_df |是  |pandas.Dataframe|因子值 (pandas.Dataframe类型),index为datetime, colunms为股票代码(asset)。|
|factorIsMV    |否|bool |待中性化的因子是否是市值类因子(bool)。是则为True,默认为False|

**参数示例:**
```
                AAPL	　　　BA	　　　CMG	　　   DAL	     LULU	　　
 date
 2016-06-24	0.165260	0.002198	0.085632	-0.078074	0.173832
 2016-06-27	0.165537	0.003583	0.063299	-0.048674	0.180890
 2016-06-28	0.135215	0.010403	0.059038	-0.034879	0.111691
 2016-06-29	0.068774	0.019848	0.058476	-0.049971	0.042805
 2016-06-30	0.039431	0.012271	0.037432	-0.027272	0.010902


factorIsMV:
False
```

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
| factor_df   |pandas.Dataframe  |中性化后的因子值(pandas.Dataframe类型),index为datetime, colunms为股票代码。 |