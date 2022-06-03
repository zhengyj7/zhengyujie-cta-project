## 甲醇期货基本面单因子趋势策略
### 1. 择时因子
- 1.1 基差（日频）
- 1.2 现货价格（日频）
- 1.3 仓单（日频）（表现不好 舍弃）
- 1.4 甲醇制烯烃利润（日频）（表现不好 舍弃）
- 数据来源：同花顺、rqdata
### 2. 择时模型
- 直接择时（arima） 
- OLS滚动回归择时
### 3. 回测
- 以T+1日开盘价开仓、T+2日开盘价平仓，日频调仓
- 为避免主力合约价格的跳空，甲醇期货主力选择的是开盘价前复权
- 警惕期货的交易时间与股票有所不同，回测时要将因子shift(1)，收益率shift(-1)
### 4. 代码说明
- utils.py：对基本面指标原时间序列进行一系列分析，确定ARIMA(p,d,q)最优参数
- model.py：训练模型（arima、ols滚动回归）
- backtest.py：基于交易信号的回测
- spread_factor_analysis：基于基差数据的单因子趋势策略
- actuals_factor_analysis：基于主流现货价格的单因子趋势策略
- warehouse_factor_analysis：基于仓单数据的单因子趋势策略
- profit_factor_analysis：基于甲醇制烯烃利润的单因子趋势策略
### 5. 反思
- 期货基本面量化的核心是对该品种的供求关系、上下游产业链的情况及品种的内在属性要非常熟悉，这之于数据预处理非常的重要
- 策略优化空间：
- 一、参数优化
 1. 直接择时中，arima参数可以写一个遍历函数
 2. 直接择时中，arima样本内数据长度需要根据不同因子的特征进行调整
 3. 直接择时中，开平仓阈值大小的选择
- 二、模型优化
 1. LSTM模型可能可以更好地预测时间序列
 2. 多因子模型


