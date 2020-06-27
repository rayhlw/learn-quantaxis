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
- 处理「基本面」数据最容易（人人可做），但剩余可发掘的价值也不太高
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
    - 每个bar含tick数 = tick总数 / bar数
    - tick bar和time bar的图基本一致，就是在几个暴涨和暴跌点更加极端
    - 优点
        - 一些研究发现按tick bar来取样得到的数据更接近独立正态同分布（IID），而IID在统计上的均值和方差都有非常好的性质。
    - 缺点
        - 不过tick bar也有自身的问题，假设你下单买1000股阿里巴巴，一次性的话就记录1个tick，但是分10单每单100股来买的话，就记录成10个tick，这样明显不太合理

- 等量抽样
    - 是将tick数据转化为volume bars，以每段时间含（固定成交量）的前提下抽样得到
    - 每个bar含的成交量 = 总成交量 / bar数
    - 优点
        - 一些研究发现按volume bar来取样得到的数据比tick bar更接近独立正态同分布（IID），此外不少关于市场微观理论都是基于价格和成交量来研究的，因此用volume bar能更好的结合那些研究
    - 缺点
        - 假设迅雷股票6个月从6美元涨了400%到24美元，一开始你买了1000股迅雷花了6000美元，那么在终止点只需要卖250股票（6000美元）就能回本
        - 如果按volume bar来看，1000股到250股波动很大，但实际成交额都是6000美元
        - 此外，股票的量在分割（split）和反向分割（reverse split）都会变化很大，但股票的额并没有变

- 等额抽样
    - 是将tick数据转换为dollar bars，以每段时间含「固定成交额」的前提下中抽样得到（比如固定每10000美元）
    - dollar泛指交易产品的计价货币（denominated currency），也可以是欧元、英镑、日元或人民币
    - 每个bar含的成家额 = 总成交额 / bar数
    - 优点
        - 假设一只股票在一定时间区间内股价翻倍，期初10000元可以购买的股票将会是期末10000元可购买股票手数的两倍
        - 在股价有巨大波动的情况下，tick bars和volume bars每天的数量都会随之有较大的波动
        - 此外，增发、配股、回购等时间也会导致tick bars和volume bars每天数量的波动
        - 一般来说，等额抽样相比较而言是一个更加稳健的抽样方法

### 信息驱动Bar

- 构建信息驱动bar在更多信息进入市场时进行更频繁的抽样。当买卖不均衡时，市场参与者之间的信息差也变大，市场会出现知情交易者（informed trader）。在抽样时考虑买卖不均衡，我们可以在价格大道新的均衡水平之前做出决定
    - Imbalance Bars（IB）系列：TIB、VIB、DIB
    - Runs Bars（RB）系列：TRB、VRB、DRB
    - 上面缩写里的T、V、D代表的是tick、volume、dollar
    - 可使用金融机器学习包mlfinlab的API来抽样信息驱动bar（可获取dollar bar、volume bar、tick bar）

- IB（inbalance bars）用mlfinlab来实现
    - Imbalance Bar - 不等笔抽样（Tick Imbalance Bars）
        - 可类比等笔抽样（tick bar）
        - 不等笔抽样是按「不固定笔数」的前提下抽样得到
        - 等笔抽样是按「固定笔数」的前提下抽样得到
    - Imbalance Bar - 不等量抽样（Volume Imbalance Bars）
        - 可类比等量抽样（volume bar）
        - 不等量抽样是在「不固定成交量」的前提下抽样得到
        - 等量抽样是在「固定成交量」的前提下抽样得到
    - Imbalance Bar - 不等额抽样（Dollar Imbalance Bars）
        - 可类比等额抽样（dollar bar）
        - 不等额抽样是在「不固定成交额」的前提下抽样得到
        - 等额抽样是在「固定成交额」的前提下抽样得到
    
- RB（runs bars）用mlfinlab来实现
    - 区别：IB和RB都是以不固定笔数、不固定成交量、不固定成交额的方式来抽样，但它们的区别在于
        - IB统计了bt的总和
        - RB统计了bt = 1和bt = -1数量的最大值
    - 通过类比TIB、VIB和DIB来定义TRB、VRB和DRB

### 总结

- 从tick数据抽样到bar数据，大方向上有两种方法
    - 标准法：等时抽样、等笔抽样、等量抽样、等额抽样
    - 信息驱动法：
        - Imbalance抽样，满足条件 *|Imbalance| ≥ Expected Imbalance*
        - Runs抽样，满足条件 *|Run| ≥ Expected Run*
    - 道理不难，但实际操作有很多难点
        - 数据量太大，运行时间太长
        - 画出来的图和Prado书上不太一样（看不出dollar bar最稳定），光看图不行，还需要用具体的统计指标来证明dollar bar最稳定
        - 抽样IB和RB需要超参数，这些参数怎么改没有一个明确的规则，需要慢慢试出来，而且发现每次抽样的结果对超参数非常敏感


# 3.基于事件采样

### 前言

- 「从Tick到Bar」里，从「异质」的tick数据采样出「同质」的bar数据。当数据太多时，传统（非深度）机器学习算法的表现会有上限，从低到高分别为：传统机器学习 --> 浅层神经网络 --> 中层神经网络 --> 深层神经网络。这时减少数据量并发掘出更好特征的数据才能使机器学习取得好效果，通常有两种方法：
    - 无脑型下采样（downsampling）
        - 可细分为*线性分采样（linspace sampling）和均匀采样（uniform sampling）*
        - 虽然可以做到减少数据量，但是采样数据的方法都没有金融含义支撑，线性等分采样过于简单，均匀采样过于随机
    - 基于事件采样（event-based sampling）「背后有金融含义支撑的采样方法」
        - 投资组合经历买卖通常发生在特定事件发生后，如：
            - 结构性突破（structural break）：均值回归模式 --> 动量模式
            - 市场微观结构（market microstructure）：FIX信息
        - 以上事件通常伴随着下面三种场景
            - 宏观统计数据公布
            - 波动率急剧增加
            - 价格大幅偏离均衡水平

### 数据处理

- 源数据「当用标普500价值股ETF的高频tick数据时候，做了数据处理工作，过程麻烦又非常重要，因此将这个处理数据的完整过程记录下来」
    - 源数据
        - 使用标普500价值股ETF（IVE）tick级别的数据来自一下链接
        - http://www.kibot.com/free_historical_data.aspx
    - 知识点：指数ETF
        - ETF是EXchange Traded Fund的缩写，交易型开放式指数基金，是一种追踪「标的指数」的基金
        - 比如我看好美国股票市场，又不想投资个股，那么可以投资标普500指数，用的金融工具就是其ETF，代号为IVE

- 处理数据「数据清洗」
    - 读取数据
        - 根据介绍文档，找出数据对应的名称标题栏
    - 处理数据
        - 使用pandas读取将数据转换成DataFrame，并做一些处理

### 基于事件采样

- Tick数据
    - 那出一段数据，首先不做任何采样，画出tick数据的价格折线图
    - 为了快，从pandas的DataFrame上直接用里面的plot函数，而没有用matplotlib.pyplot
    - 在量化中，很多时候并不需要每条tick的高频信息，我们需要的是从中进行有效的采样，最常见的是dollar bar（等成交额采样）

- Dollar Bar数据
    - 如关注分钟级别的数据，从一定的时间内采样Time Bar数据
    - 接着使用mlfinlab里面的内置函数get_dollar_bars来做等交易额采样，函数生成dollar bar
    - 画出doller bar的折线图
    - Dollar bar折线图比起tick折线图波动与噪音都少了

- 基于事实采样
    - 进行之前，AFML书中的第40页又这样一句话，CUSUM filter决定什么样的时间被触发（方法很多，书中这一章给出一个方法）。作者拿CUSUM filter和Bollinger bands相比，发现后者没有像前者触发很多‘有价值’的事件（multiple events are not triggered）
    - 知识点：布林线（Bollinger Line）
        - 价格总是围绕某个中轴在一定的范围内波动，这个范围就形成了一个带状区间（band）
        - 价格就在这个区间的上限和下限之间进行波动。而这条带状区间的宽窄也会随着价格波动幅度的大小而变化
            - 价格涨跌幅度加大时，带状区变宽
            - 价格涨跌幅度变小时，带状区变窄
        - 三条曲线组成，上轨线（upper band）、中轨线（mid band）和下轨线（lower band），一般下轨对价格有支撑作用，上轨对价格有阻力作用
            - 当股价穿越上轨（突破阻力了），卖点信号
            - 当股价穿越下轨（冲破支撑了），买点信号
            - 当股价由下向上穿越中界限，加码信号
            - 当股价有上向下穿越中界限，卖出信号
        - 根据布林带可以找出一些触发事件（用来买卖），首先根据其定义求出上轨、下轨和中轨
        - CUSUM Filter中，CUSUM就是cumulative sum的缩写，就是某个变量的累加，而filter是过滤器，两个词放在一起，实际上就是一种「当一个变量累加到某个程度，触发事件」的检测方法

### 总结

处理数据永远是最花精力和事件的，机器学习是，量化金融也是，数据科学更是。获取的源数据格式和你想用的格式总是差别很远，务必在数据上下功夫，要不然胡乱使用一通模型只会Garbage In Garbage Out。

- 明白了如何从「非结构性」的杂乱金融数据转换成同质的「结构性」的数据，但是直接把它们丢进机器学习（ML）模型中还是会出问题的，原因是：
    - 一些ML模型，比如支持向量机（Support Vector Machine，SVM），随着本量变化的表现不稳定
    - ML模型在输入好特征后，得到的精度才最佳