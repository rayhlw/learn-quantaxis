# 金融数据结构

基于量化投资与机器学习的金融数据结构基础学习


# 1.金融数据类型（financial data type）

### 介绍「数据越原始其含有的价值越高」

| 基本面数据 | 市场数据 | 分析数据 | 另类数据 |
| :---- | :---- | :---- | :---- |
| 资产 | 价格 / 收益率 / 隐含波动率 | 分析师推荐 | 卫星数据 |
| 负债 | 成交量 | 信用评级 | 图像 |
| 销量 | 股息 / 债息 | 盈利预期 | 视屏 |
| 成本 | 未平仓量 | 新闻情感 | 网页搜索 |
| 盈利 | 报价 | | 社交网络 |
| 宏观变量 | | | 元数据 |

### 基本面数据（Fundamental Data）

- 会计数据（accounting data）
    - 资产（assets）
    - 负债（liabilities）
    - 销量（sales）
    - 盈利（earnings）

- 基本面数据
    - 数据发布日期（release date）「定期报告披露日期」
    - 季度报告截止日期（quarter-end reporting period）「使用此日期易引起：视偏差（look-ahead bias）」
    - 回填偏见（backfill bias）「历史偏见，在计算体系中，包含了其新成分的过去表现时往往倾向于添加过去表现优良的成分，会造成该指数曲解」
    - PIT（point-in-time）「使用PIT数据可以避免前视偏差，国内：万矿，国外：Quantopian
    - 使用原则「基本面数据频率低，监管严，易获得，价值可挖掘的差不多，通常是把基本面数据和其它类数据一起使用」

### 市场数据（Market Data）

- 包含交易所有类型产品时收集到的数据
    - 现货价格（spot price）
    - 期货价格（futures price）
    - 利率（interest rate）
    - 汇率（exchange rate）
    - 波动率（volatility）
    - 成交量（volume）

- 在交易中，市场数据以「限价定单簿（limitorder book，LOB）的形式，市场参与者可看：定单信息（order information）」
    - 买家（buyer） / 卖家（seller）
    - 买价（bid price）：卖家可以卖到的最高价（XXX美元）
    - 买量（bid quantity）：卖家可以卖的数量（XXX股）
    - 卖价（ask price）：买家可以买到的最低价（XXX美元）
    - 卖量（ask quantity）：买家可以买的数量（XXX股）

- 在每个时点LOB可以显示三种不同层次的信息
    - L1信息（Level 1）一维数据（price）
        - 最佳买卖价格（Best Bid and Offer，BBO）
            - 最佳买价（hitting the bid）
            - 最佳卖价（lifting the offer）
    - L2信息（Level 2）二维数据（price + depth）
        - 最佳买卖价格（Best Bid and Offer，BBO）
            - 最佳买价（hitting the bid）
            - 最佳卖价（lifting the offer）
        - 非最佳买卖价（Not Best Bid and Offer，NBBO）
    - L3信息（Level 3）三维数据（price + depth + size）
        - 最佳买卖价格（Best Bid and Offer，BBO）
            - 最佳买价（hitting the bid）
            - 最佳卖价（lifting the offer）
        - 非最佳买卖价（Not Best Bid and Offer，NBBO）
        - 不同人下单的量

### 分析数据

- 分析数据（Analytics Data）是原始数据的衍生品
    - 基本面数据「销量、成本、运营费用等来评估一个公司的盈利能力和运营质量，并推荐买卖其股票」
    - 市场数据「限价定单簿和交易信息等来预测冰山单（iceberg order）的大小和概率」
    - 另类数据「新闻舆情、财报公告、卫星图像等来做情感分析（sentiment analysis）和经营预测」
    - 使用分析数据的利弊
        - 优点是特征和信号已经从原始数据中提取出来，使用起来方便
        - 缺点是价格昂贵，而且处理方法不透明（opaque）也可能存有偏差（bias）

### 另类数据

- 另类数据
    - 个人数据（Individual Data）是由个人网上行为产生
        - 社交网络数据（social media data）：Twitter、Linkedln、微信
        - 新闻舆论数据（nwes & reviews data）：新闻、产品舆论
        - 网页搜索数据（web search data）：谷歌搜索、百度搜索、邮件
        - 案例：
            - iSentium 提供交易股票时用到的Twitter上的情绪数据指标
            - RavenPack 提供交易债券、外汇和股票时用到的新闻情绪数据指标
    - 商业数据（Business Process Data）是由商业流程产生
        - 交易数据（transcation data）：主要是消费者交易数据（Square、Intuit、Xero等）
        - 公司数据（corporate data）：主要是行业数据（AROQ、Edmunds、SNL Financial、Smith Travel等）
        - 政府机构数据（government agency data）：国际级别（IMF、WTO、World Bank）、国家级别（美联储、人民央行）
        - 案例：
            - Eagle Alpha 提供交易个股时用到的用户电子邮件收据
    - 传感数据（Sensor Data）是由手机、无人机、卫星上的传感器产生
        - 卫星图像数据（satellites images data）：卫星、无人机
        - 地理定位数据（geolocation data）：GPS、手机APP
        - 天气数据（weather data）
        - 案例：
            - Advan Research 提供交易个股时用手机记录的地理位置数据（根据人流量预测零售）
            - RSMetrics 提供交易个股时用无人机拍的停车场和仓库图像数据（根据车位占满率预测员工）

### 总结

金融市场数据可分为四类，基本面数据、交易数据、分析数据和另类数据。
前三类属于结构性数据（structured data），即可以用二维数据表（excel、DataFrame等）储存的；
而最后的另类数据属于非结构性数据（unstructured data），在使用前需要转换成结构性数据。
- 处理「基本面」数据最容易（人人可做），但剩余可发掘的价值也不太高来
- 处理「另类数据」最困难（鲜有人做），一旦你做了对你的价值是唯一的


# 2.数据采样（bar sampling）「从Tick到Bar」

### 前言

- 量化金融数据（bar）一般包含6个属性
    - 日期时间（date_time）是2013年9月1日19时32分23秒387毫秒
    - 起始价（open）是1640.25
    - 最高价（high）是1642.00
    - 最低价（low）是1639.00
    - 结束价（close）是1642.00
    - 成交量（volume）为28031

- OHLC代表（open、high、low、close）在一段时间内的多个tick数据的价格决定的，这段时间可以表达为
    - 一天
    - 一小时
    - 一分钟
    - 一秒
    - 包含1000笔交易的那段时间
    - 包含成交100个合约的那段时间
    - 包含成交10000美元的那段时间

- 收集tick数据而生成某些统计量的操作叫抽样（sample），这些统计量可以是这些tick数据
    - 起始值、最大值、最小值、终止值
    - 简单平均值（下面要介绍的TWAP）
    - 成交量加权平均值（下面要介绍的VWAP）

*抽样就是从大量的「tick级别」的高频数据，选出有代表性「bar类型」的样本*

### Tick和Bar

- Tick「某金融产品交易时的逐笔数据」
    - Tick数据也是交易所对定单簿（order book）中进行增加、删除、更新和成交四个操作产生的数据
    - 只要在定单簿中买价、买量、卖价和卖量发生变化，就产生一个tick
    - 国内交易所发送的是切片信息，不是真正意义的tick信息「切片方式可能因信息丢失而无法获得」

- Bar数据
    - 为了高频的tick数据从中提取有价值的信息，并以合适的形式储存它们，这种数据储存形式叫做Bar
    - python中万物皆对象，bar也是对象，除了OHLC和volume属性，还有时间戳（timestamp）、代号（symbol）、ID等等
    - 把bar里每一条属性当成Column，那么*每一条记录（observation）或者一个样例（instance）就是一个bar*
    - *DataFrame就是储存多个bar的数据结构*

### 标准Bar

- 构建标准bar通过标准抽样（regular sampling），将非均匀序列的「原始数据」转化为均匀序列的「加工数据」
    - 读取、概览、处理、可视化数据
    - 选取最重要的特征，如比特币：
        - side：买卖方向
        - price：价格
        - tickDirection：每笔的价格走向
            - minusTick是价格向下
            - zeroMinusTick都是价格不变但前一个tick价格向下
            - plusTick是价格向上
            - zeroPlusTick都是价格不变但前一个tick价格向上
        - homeNotional：合约数，即volume
        - foerignNotional：成交额，以美元为单位
    - 在量化中，我们很多时候并不需要每条tick的高频信息，我们需要从中进行有效的取样

*抽样是指从目标总体（population）中抽取一部分个体作为样本（sample），也可以对抽取的部分个体进行比如取平均来作为样本*

- 等时抽样
    - 是将tick数据转换为time bars，在「固定段时间」中抽样得到（固定从1，15，30，60分钟进行一次抽样）
    - 有了每个time bar里的一组tick数据，我们
        - 可以找出OHLC四类价格（K线图）
        - 也可以计算（加权）平均价格（线状图），业界普遍用VWAP
            - 时间加权平均价（Time-weighted Average Price，TWAP）
            - 成交量加权平均价（Volume-weighted Average Price，VWAP） 
    - 缺点
        - 信息从来都不会均速在市场流动，比如股市开盘交易比临近中午交易要活跃的多
        - 等时抽样得到的序列通常呈现自相关（serial correlation），异方差（heteroscedasticity）和收益非正态（non-normal return）等不好的性质

- 等笔抽样
    - 是将tick数据转换为tick bars，以每段时间含「固定笔数」的前提下中抽样得到（比较固定每1000，2000，3000笔进行一次抽样）
    

### 信息驱动Bar