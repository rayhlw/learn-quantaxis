# learn-quantaxis

基于QUANTAXIS量化金融策略框架的学习延展笔记


# BASE REVIEW | 基本观点

- 开源框架众多，形成闭环解决方法的较少
    - 闭环解决方案；无需过多中间件开发
    - 重复单解决一些简答问题
    - 尚未进入生产力领域
    
- 针对特定场景的实现能力缺乏
    - 主观想法的理想状态和最终实现产物相差过大
    - 实现能力的严重不足
    
- 需要一套基于业务的标准化解决方案
    - 标准化决绝方案
    - 给予场景定制的解决方案


# BASIC SOLUTION ｜ 基础的研发流程
### 基于jupyterNotebook以及QADataStruct / QAAnalysis / QAIndicator / QAutil模块

- 概念/想法产生
    - 一个新的想法依赖于实盘观察/理论推导/交易员经验
    
- 策略编写/调试 「快速对于想法进行实现」
    - 使用python快速测试想法
    - 完成一个策略初步代码
 
- 回测/分析 「基于QAbacktest / QAAccount / QAPortfolio / QARisk / QAPerformance」
    - 进行不同周期的回测 
    - 基于绩效/风险/收益进行分析
    
- 策略优化 「基于QA_AutoGeneration快速分析大量相似的策略」
    - 基于策略的表现和风险暴露
    - 优化策略的参数以及出入场条件
    
- 模拟测试 「基于QA_REALTIME / QA_BROKER / QAWEBSERVER / QADESKPRO」
    - 在模拟盘上进行真实行情模拟资金策略
    - 跟踪一段周期
    
- 实盘 「基于QA_UNICCORN / QUANTAXIS_RUN」
    - 上线实盘资金
    - 每日跟踪汇报
    
    
- QUANTAXIS实盘/模拟盘 & QAMarket/Broker示意图
![image](https://github.com/rayhlw/learn-quantaxis/blob/master/image/QAMarket:Broker示意图.png)

- QUANTAXIS实盘流程
![image](https://github.com/rayhlw/learn-quantaxis/blob/master/image/QUANTAXIS实盘流程.png)

- QUANTAXIS RELTIME 实盘
![image](https://github.com/rayhlw/learn-quantaxis/blob/master/image/QUANTAXIS%20RELTIME%20实盘.png)

- QUANTAXIS 实盘运行架构
![image](https://github.com/rayhlw/learn-quantaxis/blob/master/image/QUANTAXIS%20实盘运行架构.png)

- QUANTAXIS 实盘运行整体框架
![image](https://github.com/rayhlw/learn-quantaxis/blob/master/image/QUANTAXIS%20结构框架.png)

- QAREALTIMECollecer / QAStrategy(行情分发与订阅)
    - 原始状态下的实时策略
        - For：
        - （get_XXXX） --> handle（data） --> sangal --> sendorder
        - time.sleep（5min）
        - threading
    - 订阅模式 / 主推模式策略
        - on_bar/tick
        - Handle（data） --> signal --> sendorder
        - qa-eventmq（QUANTAXIS Message IO）<--> MarketData Handler「tick的数据实时分发与二次分发」
        - ![image](https://github.com/rayhlw/learn-quantaxis/blob/master/image/QAREALTIMECollecer:QAStrategy流程.png)
    - 优势
        - 如有100个策略「其中：20 全市场选股 股票策略、20 CTA策略、30 t0策略、30 模拟盘策略」
        - 每个策略都需要行情驱动
            - 旧，100个策略同时for循环获取行情
                - 1.如果API --> 限速
                - 2.如果是爬虫 --> tps过高 --> 封ip
            - 新，Mq --> 分发行情
                - 一次获取 --> 无限个订阅者
        - 以新的方式可以稳定行情 / 解决在大规模情况下的数据需求问题

- qatrader 模拟盘命令
    - `pip install qatrader`
    - `qatrader --acc admin --pwd admin --broker QUANTAXIS`
    - `qatraderserver`

















