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
### 基于jupyterNotebool以及QADataStruct / QAAnalysis / QAIndicator / QAutil模块

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
！[image](https://github.com/rayhlw/learn-quantaxis/blob/master/image/QAMarket:Broker示意图.png)



























