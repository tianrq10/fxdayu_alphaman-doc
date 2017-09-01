#####**Intersection_Strategy**
- ` fxdayu_alphaman.selector.admin.Admin.Intersection_Strategy(*args, **kwargs) `

**简要描述：**

- 对若干选股方案取交集

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|selectors_result_dict|是  |dict|  若干选股器结果组成的字典(dict),形式为:<br>{"selector_name_1":selector_1,"selector_name_2":selector_2} <br> 每个选股器结果(selector_result)格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列结果值。(1:选出,0:不选,-1:做空)|
|rank|否|int|选出得分排名前rank的股票(个数排名) 该参数在交集方案下默认为空|
|rank_pct|否|float|选出得分排名前rank_pct的股票(百分位排名) 该参数在交集方案下默认为空。|
|weight_dict|否|dict|各选股器权重所组成的dict。该参数在交集方案下默认为空。|

**参数示例:**

- selectors_result_list:

```
{"test001":
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
               -----------------------,
"test002":
-----------------------------------
  date         |    asset   |
  -----------------------------------
               |   AAPL     |   0
               -----------------------
               |   BA       |   0
               -----------------------
  2014-01-01   |   CMG      |  -1
               -----------------------
               |   DAL      |   1
               -----------------------
               |   LULU     |   0
               -----------------------
,......}
```

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|strategy_result|Strategy 对象|取交集的结果。Strategy 对象包含"strategy_name", "strategy_result", "weight_dict"三个属性。<br>"strategy_name":<br>组合的选股结果名称(str); <br>"strategy_result":<br>组合的选股结果(格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列结果值。(>0:选出,0:不选,<0:做空)); <br>"weight_dict":<br>各选股器权重所组成的dict(dict/None)。|

#####**Union_Strategy**
- ` fxdayu_alphaman.selector.admin.Admin.Union_Strategy(*args, **kwargs) `

**简要描述：**

- 对若干选股方案取并集

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|selectors_result_dict|是  |dict|  若干选股器结果组成的字典(dict),形式为:<br>{"selector_name_1":selector_1,"selector_name_2":selector_2} <br> 每个选股器结果(selector_result)格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列结果值。(1:选出,0:不选,-1:做空)|
|rank|否|int|选出得分排名前rank的股票(个数排名) 该参数在并集方案下默认为空|
|rank_pct|否|float|选出得分排名前rank_pct的股票(百分位排名) 该参数在并集方案下默认为空。|
|weight_dict|否|dict|各选股器权重所组成的dict。该参数在并集方案下默认为空。|

**参数示例:**

- selectors_result_list:

```
{"test001":
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
               -----------------------,
"test002":
-----------------------------------
  date         |    asset   |
  -----------------------------------
               |   AAPL     |   0
               -----------------------
               |   BA       |   0
               -----------------------
  2014-01-01   |   CMG      |  -1
               -----------------------
               |   DAL      |   1
               -----------------------
               |   LULU     |   0
               -----------------------
,......}
```

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|strategy_result|Strategy 对象|取并集的结果。Strategy 对象包含"strategy_name", "strategy_result", "weight_dict"三个属性。<br>"strategy_name":<br>组合的选股结果名称(str); <br>"strategy_result":<br>组合的选股结果(格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列结果值。(>0:选出,0:不选,<0:做空)); <br>"weight_dict":<br>各选股器权重所组成的dict(dict/None)。|

#####**Rank_Strategy**
- ` fxdayu_alphaman.selector.admin.Admin.Rank_Strategy(*args, **kwargs) `

**简要描述：**

- 各选股结果加权汇总后,取排名前rank/rank_pct且至少被某一个选股器选出过一次的股票。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|selectors_result_dict|是  |dict|  若干选股器结果组成的字典(dict),形式为:<br>{"selector_name_1":selector_1,"selector_name_2":selector_2} <br> 每个选股器结果(selector_result)格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列结果值。(1:选出,0:不选,-1:做空)|
|rank|否|int|选出得分排名前rank的股票(个数排名) 默认值为10|
|rank_pct|否|float|选出得分排名前rank_pct的股票(百分位排名) (float) ,与rank二选一。该参数有值的时候,rank参数失效。|
|weight_dict|否|dict|各选股器权重所组成的dict。默认等权重。字典键为选股器名称(str),包含了selectors_result_dict中的所有选股器;字典值为float,代表对应选股器的给分权重。形如:{'selector_name_1':1.0,'selector_name_2':2.0,...}|

**参数示例:**

- selectors_result_list:

```
{"test001":
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
               -----------------------,
"test002":
-----------------------------------
  date         |    asset   |
  -----------------------------------
               |   AAPL     |   0
               -----------------------
               |   BA       |   0
               -----------------------
  2014-01-01   |   CMG      |  -1
               -----------------------
               |   DAL      |   1
               -----------------------
               |   LULU     |   0
               -----------------------
,......}
```

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|strategy_result|Strategy 对象|Strategy 对象包含"strategy_name", "strategy_result", "weight_dict"三个属性。<br>"strategy_name":<br>组合的选股结果名称(str); <br>"strategy_result":<br>组合的选股结果(格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列结果值。(>0:选出,0:不选,<0:做空)); <br>"weight_dict":<br>各选股器权重所组成的dict(dict/None)。|

#####**calculate_performance**
- ` fxdayu_alphaman.selector.admin.Admin.calculate_performance(*args, **kwargs) `

**简要描述：**

- 计算选股(含多策略组合)策略的绩效表现。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|strategy_name|是|string |策略名称|
|strategy_result|是|MultiIndex Series|策略结果(选股结果 或组合策略结果)格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列结果值。(>0:选出,0:不选,<0:做空)|
|start|是|datetime|回测起始时间|
|end|是|datetime|回测结束时间|
|periods|是|tuple|持有时间|
|benchmark_return|否|pandas.MultiIndex|基准收益 mulitiIndex.索引(index)为factor_quantile(level 0)和date(level 1),columns 为持有时间(与periods一一对应)。|
|price|否|pandas.Dataframe|计算绩效时用到的的个股每日价格,通常为收盘价(close)。索引(index)为datetime,columns为各股票代码。|
|price_high|否|pandas.Dataframe|计算绩效时用到的的个股每日最高价格,pandas dataframe类型,形同price|
|price_low|否|pandas.Dataframe|计算绩效时用到的的个股每日最低价格,pandas dataframe类型,形同price|


**参数示例:**

- strategy_name:

```
"test"
```

- strategy_result:

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

- start:

```
datetime.datetime(2010,1,1)
```

- end:

```
datetime.datetime(2014,1,1)
```

- period:

```
(1, 5, 10)
```

- benchmark_return:

```
                                         1         5         10
factor_quantile date
HS300           2013-01-01 15:00:00  0.000000  0.000000  0.000000
                2013-01-02 15:00:00  0.000000  0.000000  0.000000
                2013-01-03 15:00:00  0.000000  0.000000  0.000000
                2013-01-04 15:00:00  0.004587 -0.016313  0.028137
                2013-01-05 15:00:00  0.000000  0.000000  0.000000
                2013-01-06 15:00:00  0.000000  0.000000  0.000000
                2013-01-07 15:00:00 -0.004203  0.016459  0.029539
                2013-01-08 15:00:00  0.000317  0.027929  0.028341
                2013-01-09 15:00:00  0.001758  0.020173  0.032195
                2013-01-10 15:00:00 -0.018707  0.008769  0.020620
                .................................................
```

- price：

```
                   600011.XSHG 600015.XSHG 600018.XSHG 600021.XSHG 00028.XSHE
datetime
2014-10-08 15:00:00    18.743    17.639       NaN     7.463     9.872
2014-10-09 15:00:00    18.834    17.556       NaN     7.536     9.909
2014-10-10 15:00:00    18.410    17.597       NaN     7.580     9.835
2014-10-13 15:00:00    18.047    17.515       NaN     7.536     9.685
2014-10-14 15:00:00    18.773    17.494       NaN     7.433     9.704
2014-10-15 15:00:00    18.561    17.597       NaN     7.477     9.704
2014-10-16 15:00:00    18.501    17.659       NaN     7.448     9.685
2014-10-17 15:00:00    18.349    17.535       NaN     7.272     9.611
2014-10-20 15:00:00    18.319    17.618       NaN     7.360     9.629
.....................................................................
```

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|performance|Performance object|该策略的绩效。包含"strategy_name","mean_return","key_performance_indicator","holding_return", "holding_distribution_features","upside_return","upside_distribution_features","downside_return","downside_distribution_features" 这些属性|

#####**rank_performance**
- ` fxdayu_alphaman.selector.admin.Admin.rank_performance(*args, **kwargs) `

**简要描述：**

- 将若干Performance对象所组成的列表(strategies_performance)按指定持有期(target_period)下的指定指标(target_indicator)排序,默认为降序。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|strategies_performance|是|list|若干Performance对象所组成的列表(list)。Performance object包含"strategy_name","mean_return","key_performance_indicator","holding_return", "holding_distribution_features","upside_return","upside_distribution_features","downside_return","downside_distribution_features" 这些属性|
|target_period|是|int|指定持有期|
|target_indicator|否|"Annual return";"Cumulative returns";"Annual volatility";"Sharpe ratio";"Calmar ratio";"Stability";"Max drawdown";"Omega ratio";"Sortino ratio";"Skew";"Kurtosis";"Tail ratio";"Daily value at risk";"Alpha";"Beta"|指定用于排序的绩效指标,默认为"Sharpe ratio"|
|ascending|否|bool|是否升序。默认False(降序)|

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|ranked_performance_list|list of Performance object|排序后的Performance对象所组成的列表|

#####**show_strategies_performance**
- ` fxdayu_alphaman.selector.admin.Admin.show_strategies_performance(*args, **kwargs) `

**简要描述：**

-  批量计算strategies_result_dict中所有选股方案(含组合方案)的表现,并汇总成列表——list。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|strategies_result_dict|是  |dict|  若干选股策略结果组成的字典(dict),形式为:<br> {"strategy_name_1":strategy_1,"strategy_name_2:strategy_2}。<br>每个选股策略结果(选股结果 或组合策略结果)格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level1),包含一列结果值。(>0:选出,0:不选,<0:做空) |
|start|是|datetime|回测起始时间|
|end|是|datetime|回测结束时间|
|periods|否|tuple|持有时间 ,默认(1,5,10)|
|benchmark_return|否|pandas.MultiIndex|基准收益 mulitiIndex.索引(index)为factor_quantile(level 0)和date(level 1),columns 为持有时间(与periods一一对应)。|
|price|否|pandas.Dataframe|计算绩效时用到的的个股每日价格,通常为收盘价(close)。索引(index)为datetime,columns为各股票代码。|
|price_high|否|pandas.Dataframe|计算绩效时用到的的个股每日最高价格,pandas dataframe类型,形同price|
|price_low|否|pandas.Dataframe|计算绩效时用到的的个股每日最低价格,pandas dataframe类型,形同price|
|parallel|否|bool|是否执行并行计算(bool) 默认不执行。 如需并行计算需要在jupyter notebook下启动工作脚本|


 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|performance_list|list of Performance object|选股方案的表现 (Performance object)所组成的列表(list),列表里每个元素为选股方案的表现 (Performance object)。包含"strategy_name","mean_return","key_performance_indicator", "holding_return", "holding_distribution_features","upside_return","upside_distribution_features","downside_return","downside_distribution_features" 这些属性|

#####**enumerate_selectors_weight**
- ` fxdayu_alphaman.selector.admin.Admin.enumerate_selectors_weight(*args, **kwargs) `

**简要描述：**

-  按指定的组合方法,枚举不同权重(不同打分),对若干选股器进行组合打分。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|func|是|Admin.Intersection_Strategy；Admin.Union_Strategy；Admin.Rank_Strategy|指定选股器的组合策略|
|weight_range_dict|是|dict|描述selectors_result_dict当中每个选股器的权重优化空间。键为选股器名称,值为range对象,表示优化空间的起始、终止、步长。如weight_range_dict ={"selector1"：range(0,10,1),"selector2":range(0,10,1)}。|
|selectors_result_dict|否|dict|若干选股器结果组成的字典(dict),形式为:{"selector_name_1":selector_1,"selector_name_2":selector_2}|
|rank|否|int|选出得分排名前rank的股票(个数排名) |
|rank_pct |否|float|选出得分排名前rank_pct的股票(百分位排名) (float) ,与rank二选一。该参数有值的时候,rank参数失效。|
|parallel|否|bool|是否执行并行计算(bool) 默认不执行。 如需并行计算需要在jupyter notebook下启动工作脚本。|


 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|strategy_list|list of Strategy object|不同权重下的组合选股结果。由Strategy 对象所组成的列表(list),每个由Strategy 对象包含"strategy_name", "strategy_result", "weight_dict"三个属性。<br>"strategy_name":<br>组合的选股结果名称(str)；<br>"strategy_result":<br>组合的选股结果(格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),    包含一列结果值。(>0:选出,0:不选,<0:做空))； <br>"weight_dict":<br>各选股器权重所组成的dict(dict/None)|

#####**instantiate_selector_and_get_selector_result**
- ` fxdayu_alphaman.selector.admin.Admin.instantiate_selector_and_get_selector_result(*args, **kwargs) `

**简要描述：**

-  计算某个选股器指定时间段的选股结果。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|selector_name|是|str|选股器名称(str) 需确保传入的selector_name、选股器的类名、对应的module文件名一致(不含.后缀),选股器才能正确加载|
|pool|是|list|股票池范围(list),如：["000001.XSHE","600300.XSHG",......]|
|start|是|datetime|起始时间|
|end|是|datetime|结束时间|
|Selector|否|Selector|选股器(selector.selector.Selector object),可选。可以输入一个设计好的Selector类来执行计算。|
|data|否|自定义|计算选股结果需用到的数据,根据计算需求自行指定。(可选)|
|data_config|否|dict|在data参数为None的情况下(不传入自定义数据),可通过该参数调用fxdayu_data api 访问到数据 (dict),与data参数二选一。例如：{"freq": "D", "api": "candle", "adjust": "after"}|
|para_dict|否|dict|外部指定选股器里所用到的参数集(dict),为空则不修改原有参数。 形如:{"fast":5,"slow":10}|


 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|selector_result|pandas.MultiIndex|选股器结果　格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列结果值。(1:选出,0:不选,-1:做空) |

#####**enumerate_parameter**
- ` fxdayu_alphaman.selector.admin.Admin.enumerate_parameter(*args, **kwargs) `

**简要描述：**

-  枚举选股器的不同参数。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|selector_name|是|str|选股器名称(str) 需确保传入的selector_name、选股器的类名、对应的module文件名一致(不含.后缀),选股器才能正确加载|
|para_range_dict|是|dict|描述了selector当中待优化参数的选择空间(dict)。键为参数名称,值为range对象,表示优化空间的起始、终止、步长。如：para_range_dict = {"fast"：range(0,10,1),"slow":range(0,10,1)}|
|pool|是|list|股票池范围(list),如：["000001.XSHE","600300.XSHG",......]|
|start|是|datetime|起始时间|
|end|是|datetime|结束时间|
|Selector|否|Selector|选股器(selector.selector.Selector object),可选。可以输入一个设计好的Selector类来执行计算。|
|data|否|自定义|计算选股结果需用到的数据,根据计算需求自行指定。(可选)|
|data_config|否|dict|在data参数为None的情况下(不传入自定义数据),可通过该参数调用fxdayu_data api 访问到数据 (dict),与data参数二选一。例如：{"freq": "D", "api": "candle", "adjust": "after"}|
|parallel|否|bool|是否执行并行计算(bool) 默认不执行。 如需并行计算需要在jupyter notebook下启动工作脚本。|


 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|----- |
|selector_result_by_para_list,<br> para_dict_list|(list,list)|selector_result_by_para_list：<br>不同参数下得到的选股结果所组成的list(list)。<br>para_dict_list：<br>不同参数集所组成的list(list),与selector_result_by_para_list一一对应。每个参数集格式为dict,形如:{"fast":5,"slow":10}|

#####**get_all_selectors_result**
- ` fxdayu_alphaman.selector.admin.Admin.get_all_selectors_result(*args, **kwargs) `

**简要描述：**

-  计算admin下加载的所有选股器的选股器结果。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|pool|是|list|股票池范围(list),如：["000001.XSHE","600300.XSHG",......]|
|start|是|datetime|起始时间|
|end|是|datetime|结束时间|
|all_Selectors_dict|否|dict|加载到admin下的所有Selector类(selector.selector.Selector object)构成的字典, 可以输入一系列设计好的选股器类(与Admin._all_selectors_name一一对应)直接执行计算。形如:{"selector_name_1":Selector_1,"selector_name_2":Selector_2,...}。(可选)|
|all_selectors_data_dict|否|dict|计算选股器需用到的自定义数据组成的字典(dict),根据计算需求自行指定。字典键名为所有载入的选股器的选股器名(admin._all_selectors_name),值为对应选股器所需的数据。形如：{"selector_name_1":data_1,"selector_name_2":data_2,...}。|
|all_selectors_data_config_dict|否|dict|在all_selectors_data_dict参数为None的情况下(不传入自定义数据),可通过该参数调用fxdayu_data api 访问到数据 (dict)。二选一(未指定数据通过fxdayu_data api获取)。字典键名为所有载入的选股器的选股器名(admin._all_selectors_name),值为对应选股器所需的数据api访问参数设置dict(data_config)。形如：{"selector_name_1":data_config_1,"selector_name_2":data_config_2,...}|
|all_selectors_para_dict|否|dict|所有选股器外部指定参数集(dict)所构成的字典(dict),可选。为空则不修改选股器原有参数。字典键名为所有载入的选股器的选股器名(admin._all_selectors_name),值为对应选股器的指定参数集(dict)。形如: {"selector_name_1":{"fast":5,"slow":10},"selector_name_2":{"fast":4,"slow":7},...}|
|parallel|否|bool|是否执行并行计算(bool) 默认不执行。 如需并行计算需要在jupyter notebook下启动工作脚本。|
|update|否|bool|是否更新已有记录值(bool)。默认为False——如果admin曾经计算过所有选股器结果,则不再重复计算。 True 则更新计算所加载的选股器结果。|


 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|----- |
|all_selectors_result|dict|admin下加载的所有选股器的选股器结果(dict)。字典键名为所有载入的选股器的选股器名(admin._all_selectors_name)。值为 选股器结果(selector_result)　格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列selector结果。|