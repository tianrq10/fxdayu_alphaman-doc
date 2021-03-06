#####**get_stocks_holding_return**
- ` fxdayu_alphaman.selector.selector_analysis.get_stocks_holding_return(*args, **kwargs) `

**简要描述：**

- 计算持股方案的股票持有期(periods)收益。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|stock_strategy|是|pandas.MultiIndex|一个MultiIndex Series的序列。索引为date (level 0) 和 asset (level 1),包含一列持有股票相对权重(目前在计算总体收益时并未生效)。其中asset的值为指定日期待持有的股票代码。|
|prices|是|pandas.Dataframe|计算绩效时用到的的个股每日价格,通常为收盘价(close)。索引(index)为datetime,columns为各股票代码。|
|strategy_name|是|str|该持股方案的名称,可任意命名(str)|
|periods|否|tuple|持有周期。默认(1,5,10)|


**参数示例:**

- stock_strategy:

```
-----------------------------------
    date    |    asset   |
-----------------------------------
            |   AAPL     |   1
            -----------------------
            |   BA       |   1
            -----------------------
2014-01-01  |   CMG      |   1
            -----------------------
            |   DAL      |   3
            -----------------------
            |   LULU     |   2
            -----------------------
```

- prices:

```
                      sh600011  sh600015  sh600018  sh600021  sh600028
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
```

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|stocks_holding_return|pandas.Dataframe|该持股方案对应每一只股票的持有期收益。|

#####**get_stocks_downside_return**
- ` fxdayu_alphaman.selector.selector_analysis.get_stocks_downside_return(*args, **kwargs) `

**简要描述：**

- 计算持股方案的股票下行(periods)收益。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|stock_strategy|是|pandas.MultiIndex|一个MultiIndex Series的序列。索引为date (level 0) 和 asset (level 1),包含一列持有股票相对权重(目前在计算总体收益时并未生效)。其中asset的值为指定日期待持有的股票代码。|
|prices|是|pandas.Dataframe|计算绩效时用到的的个股每日价格,通常为收盘价(close)。索引(index)为datetime,columns为各股票代码。|
|prices_low|是|pandas.Dataframe|计算绩效时用到的的个股每日最低价格,pandas dataframe类型,形同prices。|
|strategy_name|是|str|该持股方案的名称,可任意命名(str)|
|periods|否|tuple|持有周期。默认(1,5,10)|


**参数示例:**

- stock_strategy:

```
-----------------------------------
    date    |    asset   |
-----------------------------------
            |   AAPL     |   1
            -----------------------
            |   BA       |   1
            -----------------------
2014-01-01  |   CMG      |   1
            -----------------------
            |   DAL      |   3
            -----------------------
            |   LULU     |   2
            -----------------------
```

- prices:

```
                      sh600011  sh600015  sh600018  sh600021  sh600028
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

```

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|stocks_downside_return|pandas.Dataframe|该持股方案对应每一只股票的下行收益。|


#####**get_stocks_upside_return**
- ` fxdayu_alphaman.selector.selector_analysis.get_stocks_upside_return(*args, **kwargs) `

**简要描述：**

- 计算持股方案的股票上行(periods)收益。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|stock_strategy|是|pandas.MultiIndex|一个MultiIndex Series的序列。索引为date (level 0) 和 asset (level 1),包含一列持有股票相对权重(目前在计算总体收益时并未生效)。其中asset的值为指定日期待持有的股票代码。|
|prices|是|pandas.Dataframe|计算绩效时用到的的个股每日价格,通常为收盘价(close)。索引(index)为datetime,columns为各股票代码。|
|prices_high|是|pandas.Dataframe|计算绩效时用到的的个股每日最高价格,pandas dataframe类型,形同prices。|
|strategy_name|是|str|该持股方案的名称,可任意命名(str)|
|periods|否|tuple|持有周期。默认(1,5,10)|


**参数示例:**

- stock_strategy:

```
-----------------------------------
    date    |    asset   |
-----------------------------------
            |   AAPL     |   1
            -----------------------
            |   BA       |   1
            -----------------------
2014-01-01  |   CMG      |   1
            -----------------------
            |   DAL      |   3
            -----------------------
            |   LULU     |   2
            -----------------------
```

- prices:

```
                      sh600011  sh600015  sh600018  sh600021  sh600028
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

```

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|stocks_upside_return|pandas.Dataframe|该持股方案对应每一只股票的上行收益。|


#####**get_stocklist_mean_return**
- ` fxdayu_alphaman.selector.selector_analysis.get_stocklist_mean_return(*args, **kwargs) `

**简要描述：**

- 计算某持股方案的平均日持有收益。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|stock_strategy|是|pandas.MultiIndex|一个MultiIndex Series的序列。索引为date (level 0) 和 asset (level 1),包含一列持有股票相对权重(目前在计算总体收益时并未生效)。其中asset的值为指定日期待持有的股票代码。|
|start|是|datetime|起始时间|
|end|是|datetime|终止时间|
|strategy_name|是|str|该持股方案的名称,可任意命名(str)|
|prices|是|pandas.Dataframe|计算绩效时用到的的个股每日价格,通常为收盘价(close)。索引(index)为datetime,columns为各股票代码。|
|periods|否|tuple|持有周期。默认(1,5,10)|


**参数示例:**

- stock_strategy:

```
-----------------------------------
    date    |    asset   |
-----------------------------------
            |   AAPL     |   1
            -----------------------
            |   BA       |   1
            -----------------------
2014-01-01  |   CMG      |   1
            -----------------------
            |   DAL      |   3
            -----------------------
            |   LULU     |   2
            -----------------------
```

- prices:

```
                      sh600011  sh600015  sh600018  sh600021  sh600028
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

```

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|stocklist_mean_return|pandas.MultiIndex|日平均收益的时序数据(pandas.multiIndex类型)。index 为factor_quantile——用以表示该收益序列的名称/标记 (level 0),和 date (level 1),colunms为不同持有期。|

**返回参数示例:**
```
                                         1         5         10
factor_quantile date
hs300           2016-01-04 15:00:00  0.002412 -0.080094 -0.097879
                2016-01-05 15:00:00  0.017544 -0.075621 -0.073491
                2016-01-06 15:00:00 -0.069334 -0.108461 -0.103234
                2016-01-07 15:00:00  0.020392 -0.022101 -0.064665
                2016-01-08 15:00:00 -0.050307 -0.072237 -0.073805
                2016-01-11 15:00:00  0.007286 -0.019333 -0.019909
                2016-01-12 15:00:00 -0.018606  0.002304 -0.085580
                2016-01-13 15:00:00  0.020815  0.005862 -0.071463
                2016-01-14 15:00:00 -0.031922 -0.043525 -0.114171
                2016-01-15 15:00:00  0.003848 -0.001690 -0.055356
                2016-01-18 15:00:00  0.029511 -0.000588 -0.073363
                2016-01-19 15:00:00 -0.015122 -0.087682 -0.081223
                2016-01-20 15:00:00 -0.029307 -0.076875 -0.071113
                2016-01-21 15:00:00  0.010421 -0.073860 -0.031347
                2016-01-22 15:00:00  0.004956 -0.053757 -0.048072
```


#####**plot_distribution_features_table**
- ` fxdayu_alphaman.selector.selector_analysis.plot_distribution_features_table(stocks_return,periods) `

**简要描述：**

- 根据指定持有周期下的收益序列(含持有收益、上行收益、下行收益等),计算该收益序列的分布特征。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|stocks_return|是|pandas.Dataframe|选股方案收益, columns包含"factor_quantile"——收益序列名称/标记和periods当中存在的持有期。|
|periods|是|tuple|持有周期。|


**参数示例:**

- stocks_return:

```
                date        asset         1         5        10       factor_quantile
0   2016-01-04 15:00:00  600600.XSHG  0.002412 -0.080094 -0.097879       test
1   2016-01-04 15:00:00  601600.XSHG  0.017544 -0.075621 -0.073491       test
2   2016-01-04 15:00:00  603600.XSHG -0.069334 -0.108461 -0.103234       test
3   2016-01-04 15:00:00  600131.XSHG  0.020392 -0.022101 -0.064665       test
4   2016-01-05 15:00:00  600600.XSHG -0.050307 -0.072237 -0.073805       test
5   2016-01-15 15:00:00  000030.XSHE  0.007286 -0.019333 -0.019909       test
6   2016-01-15 15:00:00  000031.XSHE -0.018606  0.002304 -0.085580       test
7   2016-01-15 15:00:00  000032.XSHE  0.020815  0.005862 -0.071463       test
8   2016-01-15 15:00:00  000034.XSHE -0.031922 -0.043525 -0.114171       test
9   2016-01-15 15:00:00  000035.XSHE  0.003848 -0.001690 -0.055356       test
10  2016-01-18 15:00:00  600600.XSHG  0.029511 -0.000588 -0.073363       test
11  2016-01-18 15:00:00  601600.XSHG -0.015122 -0.087682 -0.081223       test
12  2016-01-20 15:00:00  000030.XSHE -0.029307 -0.076875 -0.071113       test
13  2016-01-20 15:00:00  000031.XSHE  0.010421 -0.073860 -0.031347       test
14  2016-01-20 15:00:00  000032.XSHE  0.004956 -0.053757 -0.048072       test
15  2016-01-20 15:00:00  000034.XSHE -0.060207 -0.072818 -0.058225       test
16  2016-01-20 15:00:00  000035.XSHE -0.003455  0.007080  0.032828       test
```

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|distribution_features_table|pandas.Dataframe|不同持有周期下的收益分布特征。|

**返回参数示例:**
```
                                      std      q0.5      q0.25      min       max      mean
holding period factor_quantile
1              test              0.026118 -0.000401 -0.011203 -0.100128   0.100398  0.000648
5              test              0.060400  0.001621 -0.024587 -0.285132   0.480710  0.004665
10             test              0.075704  0.008019 -0.032575 -0.358760   0.673005  0.010801
```

#####**plot_cumulative_returns**
- ` fxdayu_alphaman.selector.selector_analysis.plot_cumulative_returns(stocklist_mean_return, period=1, ax=None) `

**简要描述：**

- 画出选股方案累积收益曲线。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|stocklist_mean_return|是|pandas.MultiIndex|日平均收益的时序数据(pandas.multiIndex类型)。index 为factor_quantile——用以表示该收益序列的名称/标记 (level 0 ) 和 date (level 1),colunms为不同持有期。|
|period|是|int|指定按何种持有期画图|
|ax|否|matplotlib.Axes|Axes upon which to plot|

**参数示例:**

- stocklist_mean_return:

```
                                        1         5         10
factor_quantile date
hs300           2016-01-04 15:00:00  0.002412 -0.080094 -0.097879
                2016-01-05 15:00:00  0.017544 -0.075621 -0.073491
                2016-01-06 15:00:00 -0.069334 -0.108461 -0.103234
                2016-01-07 15:00:00  0.020392 -0.022101 -0.064665
                2016-01-08 15:00:00 -0.050307 -0.072237 -0.073805
                2016-01-11 15:00:00  0.007286 -0.019333 -0.019909
                2016-01-12 15:00:00 -0.018606  0.002304 -0.085580
                2016-01-13 15:00:00  0.020815  0.005862 -0.071463
                2016-01-14 15:00:00 -0.031922 -0.043525 -0.114171
                2016-01-15 15:00:00  0.003848 -0.001690 -0.055356
                2016-01-18 15:00:00  0.029511 -0.000588 -0.073363
                2016-01-19 15:00:00 -0.015122 -0.087682 -0.081223
                2016-01-20 15:00:00 -0.029307 -0.076875 -0.071113
                2016-01-21 15:00:00  0.010421 -0.073860 -0.031347
                2016-01-22 15:00:00  0.004956 -0.053757 -0.048072
```

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|ax|matplotlib.Axes| |

#####**plot_distribution_of_returns**
- ` fxdayu_alphaman.selector.selector_analysis.plot_distribution_of_returns(*args, **kwargs)`

**简要描述：**

- 画出选股方案所选出的股票的收益分布特征(含持有收益、上行收益、下行收益等)。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|returns|是|pandas.Dataframe|选股方案收益, columns包含"factor_quantile"——收益序列名称/标记和periods当中存在的持有期。|
|period|是|int|指定按何种持有期画图|
|return_type|是|str|收益类型(upside、downside、holding)|
|ax|否|matplotlib.Axes|Axes upon which to plot|

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|ax|matplotlib.Axes| |

#####**plot_stock_returns_violin**
- ` fxdayu_alphaman.selector.selector_analysis.plot_stock_returns_violin(*args, **kwargs)`

**简要描述：**

- 画出选股方案所选出的股票的收益分布特征——提琴图(含持有收益、上行收益、下行收益等)。

**参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|returns|是|pandas.Dataframe|选股方案收益, columns包含"factor_quantile"——收益序列名称/标记和periods当中存在的持有期。|
|return_type|是|str|收益类型(upside、downside、holding)|
|ax|否|matplotlib.Axes|Axes upon which to plot|

 **返回参数说明:**

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|ax|matplotlib.Axes| |