#####**read_benchmark**
- ` fxdayu_alphaman.selector.utility.read_benchmark(*args, **kwargs)`

**简要描述：**

- 获取指数行情数据。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|start|是|datetime|起始时间|
|end|是|datetime|结束时间|
|index_code|否|str|指数代码 默认为"000300.XSHG"(沪深300指数)|
|freq|否|str|数据频率 默认为"D"|

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|benchmark|benchmark object|指数行情 返回一个benchmark对象 包含五个属性。"index", "close", "open", "high", "low"。<br>"index":<br>一个MultiIndex Series的序列。索引为date (level 0) 和 asset (level 1),包含一列factor值。其中asset的值固定是index_code,factor值固定是1。用于fxdayu_alphaman.selector.selector_analysis.get_stocklist_mean_return中作为stock_list参数来计算指数收益。<br>"close":<br>收盘价。(pandas.Dateframe ),index为datetime,column.name为index_code,值为对应指数的收盘价。<br>"open":<br>开盘价。(pandas.Dateframe ),index为datetime,column.name为index_code,值为对应指数的开盘价。<br>"high":<br>最高价。(pandas.Dateframe ),index为datetime,column.name 为index_code,值为对应指数的最高价。<br>"low":<br>最低价。(pandas.Dateframe ),index为datetime,column.name 为index_code,值为对应指数的最低价。|