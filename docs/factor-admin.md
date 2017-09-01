#####**equal_weighted_factor**
- ` fxdayu_alphaman.factor.admin.Admin.equal_weighted_factor(factors_dict) `

**简要描述：**

- 将若干个因子等权重合成新因子

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----  |
|factors_dict|是  |dict|  若干因子组成的字典(dict),形式为: <br> {"factor_name_1":factor_1,"factor_name_2":factor_2} <br> 每个因子值格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列factor值。|

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|----- |
| weighted_factor  | MultiFactor object |合成后的因子。该对象包含三个属性：<br>(1)"name"：合成的因子名称(str)<br>(2)"multifactor_value":合成因子值(MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列factor值)<br>(3)"weight": 加权方式 (str) |

#####**ic_cov_weighted_factor**
- ` fxdayu_alphaman.factor.admin.Admin.ic_cov_weighted_factor(*args, **kwargs) `

**简要描述：**

- 根据Sample协方差矩阵估算方法得到的因子权重,将若干个因子按该权重加权合成新因子

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|factors_dict|是  |dict|  若干因子组成的字典(dict),形式为: <br> {"factor_name_1":factor_1,"factor_name_2":factor_2} <br> 每个因子值格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列factor值。|
|ic_weight_df|是|pandas.Dataframe|使用Sample 协方差矩阵估算方法得到的因子权重(pd.Dataframe),可通过[Admin.get_ic_weight_df](#get_ic_weight_df) 获取。<br>索引(index)为datetime,columns为待合成的因子名称,与factors_dict一致。|

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
| weighted_factor  | MultiFactor object |合成后的因子。该对象包含三个属性：<br>(1)"name"：合成的因子名称(str)<br>(2)"multifactor_value":合成因子值(MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列factor值)<br>(3)"weight": 加权方式 (str) |

#####**ic_shrink_cov_weighted_factor**
- ` fxdayu_alphaman.factor.admin.Admin.ic_shrink_cov_weighted_factor(*args, **kwargs) `

**简要描述：**

- 根据 Ledoit-Wolf压缩的协方差矩阵估算方法得到的因子权重,将若干个因子按该权重加权合成新因子

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|factors_dict|是  |dict|  若干因子组成的字典(dict),形式为: <br> {"factor_name_1":factor_1,"factor_name_2":factor_2} <br> 每个因子值格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列factor值。|
|ic_weight_shrink_df|是|pandas.Dataframe|使用Ledoit-Wolf 压缩的协方差矩阵估算方法得到的因子权重(pd.Dataframe),可通过 [Admin.get_ic_weight_shrink_df](#get_ic_weight_shrink_df)获取。<br>索引(index)为datetime,columns为待合成的因子名称,与factors_dict一致。|


 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
| weighted_factor  | MultiFactor object |合成后的因子。该对象包含三个属性：<br>(1)"name"：合成的因子名称(str)<br>(2)"multifactor_value":合成因子值(MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列factor值)<br>(3)"weight": 加权方式 (str) |

#####**get_factors_ic_df**
- ` fxdayu_alphaman.factor.admin.Admin.get_factors_ic_df(*args, **kwargs) `

**简要描述：**

- 获取指定周期下的多个因子ic值序列矩阵

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|factors_dict|是  |dict|  若干因子组成的字典(dict),形式为: <br> {"factor_name_1":factor_1,"factor_name_2":factor_2} <br> 每个因子值格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列factor值。|
|pool|是|list|股票池范围,如：["000001.XSHE","600300.XSHG",......]|
|start|是|datetime|起始时间|
|end|是|datetime|结束时间 |
|periods|否|tuple|指定持有周期,周期值类型为(int)|
|quantiles|否|int|根据因子大小将股票池划分的分位数量|
|price|否|pandas.Dataframe|包含了pool中所有股票的价格时间序列,索引(index)为datetime,columns为各股票代码,与pool对应。|

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
| ic_df_dict|dict of pd.DataFrame|指定的不同周期下的多个因子ic值序列矩阵所组成的字典(dict), 键为周期(int),值为因子ic值序列矩阵(ic_df)。如：｛１:ic_df_1,5:ic_df_5,10:ic_df_10｝<br> ic_df(ic值序列矩阵) 类型pd.DataFrame,索引(index)为datetime,columns为各因子名称,与factors_dict中的对应|

**返回参数示例:**

- ic_df:

```
date　        BP	     　CFP	　　    EP	　 ILLIQUIDITY	  REVS20	　SRMI	　　　VOL20
2016-06-24	0.165260	0.002198	0.085632	-0.078074	0.173832	0.214377	0.068445
2016-06-27	0.165537	0.003583	0.063299	-0.048674	0.180890	0.202724	0.081748
2016-06-28	0.135215	0.010403	0.059038	-0.034879	0.111691	0.122554	0.042489
2016-06-29	0.068774	0.019848	0.058476	-0.049971	0.042805	0.053339	0.079592
2016-06-30	0.039431	0.012271	0.037432	-0.027272	0.010902	0.077293   -0.050667
```

#####**<span id="get_ic_weight_df">get_ic_weight_df</span>**
- ` fxdayu_alphaman.factor.admin.Admin.get_ic_weight_df(*args, **kwargs)`

**简要描述：**

-  输入ic_df(ic值序列矩阵),指定持有期和滚动窗口,给出相应的多因子组合权重(样本协方差估计)

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|ic_df |是  |pandas.Dataframe|ic值序列矩阵,索引(index)为datetime,columns为各因子名称。|
|holding_period|是|int |持有周期|
|rollback_period|否|int|滚动窗口,即计算每一天的因子权重时,使用了之前rollback_period下的IC时间序列来计算IC均值向量和IC协方差矩阵。|


 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
| ic_weight_df   |pandas.Dataframe |使用Sample协方差矩阵估算方法得到的因子权重,索引(index)为datetime,columns为待合成的因子名称。|


#####**<span id="get_ic_weight_shrink_df">get_ic_weight_shrink_df</span>**
- ` fxdayu_alphaman.factor.admin.Admin.get_ic_weight_shrink_df(*args, **kwargs) `

**简要描述：**

-  输入ic_df(ic值序列矩阵),指定持有期和滚动窗口,给出相应的多因子组合权重( Ledoit-Wolf压缩的协方差估计)

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|ic_df |是|pandas.Dataframe|ic值序列矩阵,索引(index)为datetime,columns为各因子名称。|
|holding_period|是|int |持有周期|
|rollback_period|否|int|滚动窗口,即计算每一天的因子权重时,使用了之前rollback_period下的IC时间序列来计算IC均值向量和IC协方差矩阵。|


 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
| ic_weight_shrink_df   |pandas.Dataframe |使用Ledoit-Wolf压缩方法得到的因子权重,索引(index)为datetime,columns为待合成的因子名称。|


#####**orthogonalize**
- ` fxdayu_alphaman.factor.admin.Admin.orthogonalize(*args, **kwargs) `

**简要描述：**

-  因子间存在较强同质性时,使用施密特正交化方法对因子做正交化处理,用得到的正交化残差作为因子,默认对Admin里加载的所有因子做调整

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|factors_dict|是  |dict|  若干因子组成的字典(dict),形式为: <br> {"factor_name_1":factor_1,"factor_name_2":factor_2} <br> 每个因子值格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列factor值。|
|standardize_type|否|"rank"/"z_score"|标准化方法,有"rank"(排序标准化),"z_score"(z-score标准化)两种。|


 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
| factors_dict(new)|dict|正交化处理后所得的一系列新因子|


#####**calculate_performance**
- ` fxdayu_alphaman.factor.admin.Admin.calculate_performance(*args, **kwargs) `

**简要描述：**

-  计算因子(含组合因子)的表现

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|factor_name |是|string|因子名称|
|factor_value|是|MultiIndex Series |因子值,格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列factor值。|
|start|是|datetime|回测起始时间|
|end|是|datetime|回测结束时间|
|periods|否|tuple|持有时间|
|quantiles|否|int|划分分位数|
|price|否|pandas.Dataframe|计算绩效时用到的的个股每日价格,通常为收盘价(close)。索引(index)为datetime,columns为各股票代码。|

**参数示例:**

- price:

```
   datetime          sh600011  sh600015  sh600018  sh600021  sh600028
2014-10-08 15:00:00   18.743    17.639     NaN      7.463     9.872
2014-10-09 15:00:00   18.834    17.556     NaN      7.536     9.909
2014-10-10 15:00:00   18.410    17.597     NaN      7.580     9.835
2014-10-13 15:00:00   18.047    17.515     NaN      7.536     9.685
2014-10-14 15:00:00   18.773    17.494     NaN      7.433     9.704
2014-10-15 15:00:00   18.561    17.597     NaN      7.477     9.704
2014-10-16 15:00:00   18.501    17.659     NaN      7.448     9.685
2014-10-17 15:00:00   18.349    17.535     NaN      7.272     9.611
2014-10-20 15:00:00   18.319    17.618     NaN      7.360     9.629
```

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
| performance| Performance object |该因子的表现,包含"factor_name", "holding_return", "mean_return_by_q", "ic", "mean_ic_by_M", "mean_ic"这些属性。|

#####**rank_performance**
- ` fxdayu_alphaman.factor.admin.Admin.rank_performance(*args, **kwargs) `

**简要描述：**

-  将若干Performance对象所组成的列表(factors_performance)按指定持有期(target_period)下的"mean_ic"排序,默认为降序

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|factors_performance |是|list|若干Performance object 所组成的列表。<br>Performance object 包含"factor_name", "holding_return", "mean_return_by_q", "ic", "mean_ic_by_M", "mean_ic"这些属性。|
|target_period|否|int |指定持有期|
|ascending|否|bool|是否升序。默认False(降序)|


 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
| ranked_factors_performance|list |排序后的Performance object所组成的列表。|

#####**show_factors_performance**
- ` fxdayu_alphaman.factor.admin.Admin.show_factors_performance(*args, **kwargs) `

**简要描述：**

-  批量计算factors_dict中所有因子的表现。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|factors_dict|是  |dict|  若干因子组成的字典(dict),形式为: <br> {"factor_name_1":factor_1,"factor_name_2":factor_2} <br> 每个因子值格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列factor值。|
|start|是|datetime|回测起始时间|
|end|是|datetime|回测结束时间|
|periods|否|tuple|持有时间|
|quantiles|否|int|划分分位数|
|price|否|pandas.Dataframe|计算绩效时用到的的个股每日价格,通常为收盘价(close)。索引(index)为datetime,columns为各股票代码。|
|parallel|否|boolean|是否执行并行计算,默认不执行。 如需并行计算需要在jupyter notebook下启动工作脚本。|

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
| factors_performance|list |因子的表现 (Performance object)所组成的列表(list),列表里每个元素为因子的表现 (Performance object),包含"factor_name", "holding_return", "mean_return_by_q", "ic", "mean_ic_by_M", "mean_ic"这些属性。|

#####**instantiate_factor_and_get_factor_value**
- ` fxdayu_alphaman.factor.admin.Admin.instantiate_factor_and_get_factor_value(*args, **kwargs)`

**简要描述：**

-  计算某个因子指定时间段的因子值。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|factor_name|是|string| 因子名称|
|pool|是|list |股票池范围,如：["000001.XSHE","600300.XSHG",......]。|
|start|是|datetime|起始时间|
|end|是|datetime|结束时间|
|Factor|否|object|因子。可以输入一个设计好的Factor类来执行计算|
|data|否|不定|计算因子需用到的数据,根据计算需求自行指定。|
|data_config|否|不定|在data参数为None的情况下(不传入自定义数据),可通过该参数调用fxdayu_data api 访问到数据 (dict),与data参数二选一。|
|para_dict|否|不定|外部指定因子里所用到的参数集(dict),为空则不修改原有参数。 形如:{"fast":5,"slow":10}。|

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
| factor_value|MultiIndex Series |因子值,格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列factor值。|


**返回参数示例:**
```
------------------------------------
   date     |    asset   |
------------------------------------
            |   AAPL     |   0.5
            -------------------------
            |   BA       |  -1.1
            ------------------------
2014-01-01  |   CMG      |   1.7
            ------------------------
            |   DAL      |  -0.1
            ------------------------
            |   LULU     |   2.7
------------------------------------
```

#####**enumerate_parameter**
- ` fxdayu_alphaman.factor.admin.Admin.enumerate_parameter(*args, **kwargs)`

**简要描述：**

-  枚举不同参数下的所得到的不同因子值。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|factor_name|是|string| 因子名称|
|para_range_dict|是|list |描述了factor当中待优化参数的选择空间(dict)。<br>键为参数名称,值为range对象,表示优化空间的起始、终止、步长。如：para_range_dict = {"fast"：range(0,10,1),"slow":range(0,10,1)}。|
|pool|是|list |股票池范围,如：["000001.XSHE","600300.XSHG",......]。|
|start|是|datetime|起始时间|
|end|是|datetime|结束时间|
|Factor|否|object|因子。可以输入一个设计好的Factor类来执行计算|
|data|否|不定|计算因子需用到的数据,根据计算需求自行指定。|
|data_config|否|不定|在data参数为None的情况下(不传入自定义数据),可通过该参数调用fxdayu_data api 访问到数据 (dict),与data参数二选一。|
|parallel|否|boolean|是否执行并行计算(bool) 默认不执行。 如需并行计算需要在jupyter notebook下启动工作脚本。|

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|factor_value_by_para_list|list |不同参数下得到的因子值所组成的list。|
|para_dict_list|list|不同参数集所组成的list(list),与factor_value_by_para_list一一对应。<br>每个参数集格式为dict,形如:{"fast":5,"slow":10}|


#####**get_all_factors_value**
- ` fxdayu_alphaman.factor.admin.Admin.get_all_factors_value(*args, **kwargs) `

**简要描述：**

-  计算admin下加载的所有因子的因子值。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|pool|是|list |股票池范围,如：["000001.XSHE","600300.XSHG",......]。|
|start|是|datetime|起始时间|
|end|是|datetime|结束时间|
|all_Factors_dict|否|object|加载到admin下的所有因子类构成的字典,可以输入一系列设计好的Factor类(与Admin._all_factors_name一一对应)直接执行计算。<br>形如:{"factor_name_1":Factor_1,"factor_name_2":Factor_2,...}|
|all_factors_data_dict|否|dict|计算因子需用到的自定义数据组成的字典(dict),根据计算需求自行指定。<br>字典键名为所有载入的因子的因子名(admin._all_factors_name),值为对应因子所需的数据。                     形如：{"factor_name_1":data_1,"factor_name_2":data_2,...}|
|all_factors_data_config_dict|否|不定|在all_factors_data_dict参数为None的情况下(不传入自定义数据),可通过该参数调用fxdayu_data api 访问到数据 (dict)。 与all_factors_data_dict二选一(未指定数据通过fxdayu_data api获取)。   <br>字典键名为所有载入的因子的因子名(admin._all_factors_name),值为对应因子所需的数据api访问参数设置dict(data_config)。形如：{"factor_name_1":data_config_1,"factor_name_2":data_config_2,...}。|
|all_factors_para_dict|否|boolean|所有因子外部指定参数集(dict)所构成的字典(dict)。为空则不修改因子原有参数。<br>字典键名为所有载入的因子的因子名(admin._all_factors_name),值为对应因子的指定参数集(dict)。形如:{"factor_name_1":{"fast":5,"slow":10},"factor_name_2":{"fast":4,"slow":7},...}。|
|parallel|否|boolean|是否执行并行计算(bool) 默认不执行。 如需并行计算需要在jupyter notebook下启动工作脚本。|
|update|否|boolean|是否更新已有记录值。默认为False——如果admin曾经计算过所有因子值,则不再重复计算。 True 则更新计算所加载的因子值。|

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|----- |
|all_factors_dict|dict| admin下加载的所有因子的因子值。字典键名为所有载入的因子的因子名,值为因子值,格式为一个MultiIndex Series,索引(index)为date(level 0)和asset(level 1),包含一列factor值。|
