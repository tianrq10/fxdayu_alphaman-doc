#####**execute**
- ` fxdayu_alphaman.selector.selector.Selector.execute(*args, **kwargs) `

**简要描述：**

- 继承自Selector的自定义选股器需在在此方法下实现执行选股的逻辑

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|pool|是  |list |股票池范围(list),如：["000001.XSHE","600300.XSHG",......]|
|start|是|datetime|起始时间|
|end|是|datetime|结束时间|
|data|否|自定义|计算选股结果需用到的数据,根据计算需求自行指定。|
|data_config|否|dict|在data参数为None的情况下(不传入自定义数据),可通过该参数调用fxdayu_data api 访问到数据 (dict),与data参数二选一。|

**参数示例:**

- pool:

```
["000001.XSHE","600300.XSHG",......]
```

- start:

```
datetime(2010,1,1)
```

- end:

```
datetime(2011,1,1)
```

- data:

```
<class 'pandas.core.panel.Panel'>
Dimensions: 196 (items) x 335 (major_axis) x 5 (minor_axis)
Items axis: sh600011 to sz300450
Major_axis axis: 2015-12-02 15:00:00 to 2017-04-18 15:00:00
Minor_axis axis: close to volume
```

- data_config:

```
取K线数据config —— {"freq": "D", "api": "candle", "adjust": "after"}
取factor数据config —— {"api": "candle",fields=("PE","PB")}
```

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|selector_result|pandas.MultiIndex   |选股器结果。格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列结果值。(1:选出,0:不选,-1:做空)|

**返回示例:**
```
  -----------------------------------
  date         |    asset   |
  -----------------------------------
               |   AAPL     |   1
               -----------------------
               |   BA       |   1
               -----------------------
  2014-01-01   |   CMG      |   0
               -----------------------
               |   DAL      |   1
               -----------------------
               |   LULU     |   0
               -----------------------
```

#####**selector_result**
- ` fxdayu_alphaman.selector.selector.Selector.selector_result(*args, **kwargs) `

**简要描述：**

- 获得选股结果

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|pool|是  |list |股票池范围(list),如：["000001.XSHE","600300.XSHG",......]|
|start|是|datetime|起始时间|
|end|是|datetime|结束时间|
|data|否|自定义|计算选股结果需用到的数据,根据计算需求自行指定。|
|data_config|否|dict|在data参数为None的情况下(不传入自定义数据),可通过该参数调用fxdayu_data api 访问到数据 (dict),与data参数二选一。|
|update|否|bool|是否更新计算(bool)。默认为False(当该选股器实例曾经做过选股运算时,再次调用该方法将不会重新计算,而直接返回上次计算的结果)。|

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|selector_result|pandas.MultiIndex   |选股器结果。格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列结果值。(1:选出,0:不选,-1:做空)|