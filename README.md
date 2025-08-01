# AIOps 手册

英文版见 <README_en.md>。

AIOps 的论文、演讲、开源库的汇总手册。按照[《企业AIOps实施建议白皮书》](https://pic.huodongjia.com/ganhuodocs/2018-04-16/1523873064.74.pdf)中的场景分类进行收集和展示。

对于同一个场景，尽量提供比较新的链接。因为新论文里一般会引用和对比旧论文。

## 异常检测

### 指标

#### 单指标

* 清华裴丹团队举办的 KPI 异常检测比赛用数据(需注册登录) <http://iops.ai/competition_detail/?competition_id=5&flag=1>
    * 比赛前 5 名的分享：<http://workshop.aiops.org/>
    * 某博士生发的程序(未在参赛的 40 支队伍上看到名字哈)：<https://github.com/chengqianghuang/exp-anomaly-detector-AIOps>
    * 北邮某硕士论文(KPI 部分考虑标记异常区间，并加异常过滤)：<https://kns.cnki.net/kcms/detail/detail.aspx?dbcode=CMFD&dbname=CMFD202101&filename=1021025248.nh&v=4bo62xCRybUZ6jmdkuL2wRQvfR0LRDN2TNkCZ1Og3VbUglRzjmact7Ot3k2Yf2vT>
* 清华/阿里巴巴开源的 Donut(基于 VAE 算法)：<https://github.com/haowen-xu/donut>
    * 清华开源的 Bagel(Donut改进型，基于 CVAE 算法)：<https://github.com/lizeyan/Bagel>
    * 基于 Donut 封装的开源项目 LoudML(支持从不同数据源自动获取数据做异常检测，RESTful 接口配置)：<https://github.com/regel/loudml>
* 清华/百度的 opprentice 系统(14 个检测器，平均取参数值，随机森林)：<http://netman.cs.tsinghua.edu.cn/wp-content/uploads/2015/11/liu_imc15_Opprentice.pdf>
* 清华/南开/腾讯的 ADS 系统(ROCKA+opprentice+CPLE)，论文：<https://netman.aiops.org/wp-content/uploads/2018/12/bujiahao.pdf>
    * github上一个开源的CPLE实现：<https://github.com/tmadl/semisup-learn>
* 腾讯开源的 metis 系统(参考了 opprentice 实现)：<https://github.com/tencent/metis>
* 阿里巴巴开源的Time2Graph(基于序列片段的图迁移路径做异常检测)：<https://github.com/petecheng/Time2Graph>
* skyline
    * etsy 开源版(9 个检测器，简单投票)：<https://github.com/etsy/skyline>
    * etsy 未开源版的介绍(小波分解后分别过 KS 和广义 ESD 检验)：<https://vimeo.com/131581331>
    * lytics 公司用 golang 重写的：<https://github.com/lytics/anomalyzer>
    * 社区版(加入 Ionosphere 模块做反馈修正，使用 tsfresh 库)：<https://github.com/earthgecko/skyline>
    * 360 公司开源的异常检测，和skyline一样简单投票，不过自己另写了几个EWMA、iForest、同环比等检测器：<https://github.com/jixinpu/aiopstools/tree/master/aiopstools/anomaly_detection>
* 开源的时序特征值提取库 tsfresh：<http://tsfresh.readthedocs.io/en/latest/>
* facebook 开源的时序数据处理库 kats，包括时序特征提取、模式检测、预测等功能：<https://github.com/facebookresearch/Kats>
* arundo 开源的 adtk 时序异常检测 python 库：<https://github.com/arundo/adtk>
* netflix基于 PCA 算法的异常检测，跑在 Pig 上：<https://github.com/netflix/surus>
* twitter 的异常检测库，R 语言：<https://github.com/twitter/anomalydetection>
* numenta 公司，HTM 算法：<https://github.com/numenta/nupic>
    * 顺带还做了一个项目专门用来比较效果(和裴丹比赛的评价标准不太一样，裴的标准是异常点往后 7 个都算；NAB 标准是异常区间内前一半算满分，后一半衰减)：<https://github.com/numenta/NAB>
    * 南京大学一位硕士论文的 windowKDE 实现(文中还实现了另外两个叫 RDE 和 TEDA 的检测器)，代码很简陋：<https://github.com/lyzhang0614/windowKDEdetector>
* 微软开源的 anomalydetector 项目(基于Spectral Residual算法，辅以 CNN，不过验证评估是对整个数据集所有指标训练一个大模型)：<https://github.com/microsoft/anomalydetector>
* 雅虎开源的时序预测和异常检测项目 EGADS：<https://github.com/yahoo/egads>
    * 对应解释论文的中文翻译版：<http://www.infoq.com/cn/articles/automated-time-series-anomaly-detection>
* 亿客行Expedia开源的异常检测项目 adaptive-alerting：<https://github.com/ExpediaDotCom/adaptive-alerting>
* RedHat公司CTO办公室开源的prometheus anomaly detector项目(基于傅里叶变换和Facebook的prophet预测算法)：<https://github.com/AICoE/prometheus-anomaly-detector>
* AWS 开源的 gluon-ts 项目，基于 MXNet 进行时序指标的概率模型训练，以此做预测和异常检测：<https://github.com/awslabs/gluon-ts/>
    * 以及 AWS 自己用 gluon-ts 实现云资源性能指标异常检测的论文：<http://export.arxiv.org/pdf/2007.15541>
* 华为爱尔兰研究中心发的 SLMAD 论文(对周期性数据直接做 Robust BoxPlot，非周期性的做 Matrix Profile，但文中没说 MP 的 window size 如何定)：<https://www.researchgate.net/publication/344378625_SLMAD_Statistical_Learning-Based_Metric_Anomaly_Detection>
    * Matrix Profile 本身也是一个比较新的时序分析算法，支持流式更新，国内介绍较少，对应的开源项目 STUMPY 官方文档见：<https://stumpy.readthedocs.io/en/latest/Tutorial_The_Matrix_Profile.html> 
* 北航/快手的 CutAddPaste 论文，进行指标数据的数据增强：<https://dl.acm.org/doi/pdf/10.1145/3637528.3671739>。思路比较简单，从指标自己的历史数据里随机切片段下来，然后附加一些随机斜率啥的，再替换进另一个位置，就变成“含有指标自己知识的”异常样本了。

#### 多指标

* CMU 做多指标模式提取和异常检测的 SPIRIT 系统，论文：<https://bitquill.net/pdf/spirit_vldb05.pdf>
* 清华裴丹团队做的多指标聚类 ROCKA 系统，论文：<https://netman.aiops.org/~peidan/ANM2018/8.DependencyDiscovery/LectureCoverage/2018IWQOS_ROCKA.pdf>
* 清华裴丹团队做的多指标异常检测 OmniAnomaly 开源实现，主要是对同一对象的多个指标，采用和单指标Donut类似的方法：<https://github.com/NetManAIOps/OmniAnomaly>
* 微软亚研做的多指标聚类 YADING 系统，论文：<https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/p457-ding.pdf>
* 北卡顾晓晖团队做云主机异常检测和根因定位的 UBL 系统(基于 SOM 算法)，论文：<http://dance.csc.ncsu.edu/papers/UBL.pdf> 
* 新加坡国立大学做传感器多变量指标异常检测的开源项目(基于 GAN 算法)：<https://github.com/LiDan456/MAD-GANs>
* 德国波斯坦大学做的多/单指标在71 种不同算法下的对比测试(RUC 最差情况几乎都不咋样)：<https://hpi-information-systems.github.io/timeeval-evaluation-paper/>

#### 大模型方法

* 清华大学基于 GPT2 做的[GPT4TS大模型](https://github.com/DAMO-DI-ML/NeurIPS2023-One-Fits-All)。本领域的开山之作，后续进展的基准。
   * 浙江大学 anomalyLLM：<https://arxiv.org/html/2401.15123v1>，将 GPT4TS 大模型蒸馏成小模型。
   * 港中文/同济 aLLM4TS：<https://arxiv.org/pdf/2402.04852.pdf>，在 GPT4TS 的结构上做修改。
* 卡内基梅隆大学 MOMENT 模型和 Time-Series Pile 数据集：<https://arxiv.org/pdf/2402.03885.pdf>。对标大语言模型的 Pile 数据集，收集了目前最常用的 5 个指标数据集，同时覆盖了单维度和多维度指标的分类、长短期预测、异常检测等任务。然后类似 T5 的方式预训练了 moment-base、large、small 三个规格的指标大模型。论文主要对比的基线是 TimesNet 和 GPT4TS。
* 谷歌开源的时序指标预测基础模型：<https://github.com/google-research/timesfm>
* 微软/清华发表的[MonitorAssistant](https://netman.aiops.org/wp-content/uploads/2024/05/MonitorAssistant_CameraReady-v1.4_submitted.pdf): 主要是在指标监控和标注的流程里，引入 LLM 助手。比如新指标上线时的配置参数推荐，和指标告警时的历史告警推荐，除了指标时序相似度加上指标描述的文本相似度；还有在工单对话中，通过文本问答来反馈哪些时段的异常类型是误报或不关心。
* datadog 的 Toto 指标大模型技术报告：<https://arxiv.org/pdf/2407.07874>，预训练数据包含一万亿个指标数据点，其中 75% 来自 datadog 云平台上的匿名数据。
* 清华裴丹团队开源的 ChatTS 指标问答大模型：<https://github.com/NetManAIOps/ChatTS>。基于 qwen2.5-14B 做的增量预训练和微调对齐。预训练数据的合成，参照 evol-instruct 设计了一套 TS-Evol 方案。指标数据入大模型之前，先有一个自训练的 5 层 MLP encoder。
    * MCQ2 reasoning 指标问答推理数据集：<https://aclanthology.org/2024.findings-emnlp.201.pdf>。数据集不限于运维场景，ChatTS 中只是抽取里这个数据集的一小部分。该数据集也是合成数据，不过是由 GPT4o 根据不同场景设定生成 python 代码再运行合成的。
    * 北邮/中国联通发表的 [ChatTime 论文](https://arxiv.org/pdf/2412.11376)：在 llama2-7B 基础上做的增量预训练和微调对齐。直接将指标数据做归一化再分桶，然后当 token 处理，扩展词表。和 ChatTS 都有指标分类场景的评估，按 GPT4 为共同基准的话，ChatTime 效果差一些。
* 阿里/复旦发表的 [PromAssistant 论文](https://arxiv.org/pdf/2503.03114)：通过类 GraphRAG 方案实现针对 k8s 监控指标的 NL2PromQL。根据测试，直接调用 LLM 的语法准确率就有96%，因此主要解决的是怎么写对指标和标签名称的问题。

### 日志

#### 传统方法

* 国防科大的日志领域研究综述(日志监测部分比我前面列的老，但还提了基于源码的静态分析和基于虚拟机增强的日志内容改进两个方向，基本都是袁丁教授团队做的)：<http://www.jos.org.cn/1000-9825/4936.htm>
    * morningpaper 博客关于静态分析的 lprof 论文解析：<https://blog.acolyer.org/2015/10/08/lprof-a-non-intrusive-request-flow-profiler-for-distributed-systems/>
    * morningpaper 博客关于日志增强的 log20 论文解析：<https://blog.acolyer.org/2017/11/03/log20-fully-automated-optimal-placement-of-log-printing-statements-under-specified-overhead-threshold/>
* 香港中文大学的日志领域研究综述(比国防科大的新，加入了关于日志压缩、人机交互、语义等新方向)：<https://arxiv.org/pdf/2009.07237.pdf>
* 荷兰代尔夫特理工大学的日志领域研究综述(2021 年，统计了不同方向的研究趋势)：<https://pdfs.semanticscholar.org/b3c1/e91f3f73ff1d63504fb8d522558baa7334d4.pdf?_ga=2.256964171.1591127296.1641452870-511869175.1640757218>
* 加拿大滑铁卢大学的日志领域研究综述(2022 年，总结了各方向各算法的优劣)：<https://arxiv.org/pdf/2110.12489.pdf>
* 香港中文大学团队收集的多篇日志异常检测相关论文和数据集(共87GB)：<https://github.com/logpai/loghub>
    * 他们也做了各种现有算法的开源实现和自己的 Drain 算法进行横向测试对比，报告见：<https://arxiv.org/pdf/1811.03509.pdf>
    * 针对多行日志，尤其是一些应用中间件输出的表格式、KV 式的多行日志，升级了一版数据集和新算法，对应项目见：<https://github.com/logpai/hybridlog>
    * 华为开源的 [NuLog](https://jorge-cardoso.github.io/publications/Papers/CP-2020-094-ICDM_Self_Attentive_Classification_Based_Anomaly_Detection.pdf) 项目(采用MLM掩码语言模型，并复现了上一篇论文一样的对比)：<https://github.com/nulog/nulog>
    * 华为德研开源的 [ADLILog](https://arxiv.org/pdf/2207.03206.pdf)，爬了 github 上最活跃的1000 个开源项目，把其中输出日志的源码里的静态文本抽取出来做语料库辅助：<https://github.com/ADLILog/ADLILog>
    * IBM云数据中心团队改进和开源的 Drain3 包，加强了持久化，自定义参数替换等：<https://github.com/IBM/Drain3>
    * IBM 在 Drain3 基础上，通过公开文档爬虫获取事件 ID 的关键字描述，然后走语义分析相似度，来提取复杂变量类型(即除了常量、变量以外，新定义了sequential、optional 和 single-select 类型)：<https://arxiv.org/pdf/2202.07169.pdf>
    * 上海交通大学采用日志中的 punct 部分作为日志模式学习的来源，实现了一个 logpunk 系统，在 loghub 下对比，效果居然也好过其他算法：<https://www.mdpi.com/2076-3417/11/24/11974/pdf>
    * concordia 大学发表[针对日志模式特征的研究](https://users.encs.concordia.ca/~abdelw/papers/ICPC2025_LECs.pdf)，提出了 30 种 LEC(log event characteristics)，其中 multi-level nested token 等变量类型，几乎所有算法提前效果都不好。
* 香港中文大学团队更新版的日志异常检测数据集和相关实现评测：<https://github.com/logpai/LogPub>。和 loghub 不同的地方是：loghub 里每种日志只有 2k 条打了 label，而 logpub 这次全部人工打 label 了。此外，因为时隔多年，对比时也连带上 UniParser、LogPPT 这两个依赖 GPU 的方案。评测标准也考虑了模板和日志量的频次偏差、训练耗时等方面的问题。
* 北大开源的 MultiLog 数据集:<https://github.com/AIOps-LogDB/MultiLog-Dataset>，在分布式数据库 Apache IoTDB 上进行了单节点单类型、单节点多类型、多节点单类型、多节点多类型等不同的故障注入方式。此外，也通过 drain+fasttext+autoencoder+lstm 方案实现了自己的异常检测：<https://arxiv.org/pdf/2406.07976>
* 微软的 UniParser 论文，通过语义分析，识别训练集中某些常量为变量：<https://arxiv.org/pdf/2202.06569.pdf>
* 香港中文大学的 SemParser 论文，尝试用语义分析来命名模式中的参数位：<https://arxiv.org/pdf/2112.12636.pdf>
* 南京大学的 PosParser 论文，尝试用词性标注生成 token 序列，然后生成日志模式：<https://www.computer.org/csdl/journal/bd/5555/01/10663950/1ZW74ddAxAQ>
* elasticsearch 的 categorize_text aggregation 开源实现，利用开源词库 SCOWL 做词性分析，给动词加权：<https://github.com/elastic/elasticsearch/pull/80867>
* 斯里兰卡莫拉图瓦大学/WSO2 公司的 vue4logs-parser 开源实现，直接利用倒排索引搜索相关性来完成模式过滤：<https://github.com/IsuruBoyagane15/vue4logs-parser>
* IBM 研究院基于语言模型做的日志异常检测模型，对比了 fasttext 和 BERT 的效果：<https://www.researchgate.net/publication/344693315_Using_Language_Models_to_Pre-train_Features_for_Optimizing_Information_Technology_Operations_Management_Tasks>
* IBM 发表的 LogMId 论文：<https://www.semanticscholar.org/paper/Decoding-Logs-for-Automatic-Metric-Identification-Gupta-Mohapatra/a7c70da522ec868df0e3bc30fb3f943ae1037fee>。提出一个新颖的改进想法：对日志模式和参数，都做一下分类，属于 golden signals 相关的，才需要关注，可以提升异常检测效果。
* 爱立信研究院做的 LoganMeta，采用 meta learning 算法，不过是监督式：<https://arxiv.org/pdf/2212.10992.pdf>
* 多伦多大学的 CLP 开源实现：<https://github.com/y-scope/clp>，uber 已经利用该技术处理其 spark 平台日志，官博文章见：<https://www.uber.com/en-US/blog/reducing-logging-cost-by-two-orders-of-magnitude-using-clp>
    * 同期也提供了一份测试数据集，包括 hadoop,hive 这种 text 类和 clickhouse,es 这种 JSON 类日志数据：<https://docs.yscope.com/clp/main/user-guide/resources-datasets.html>
* 香港中文大学的 LogZip 开源实现：<https://github.com/logpai/logzip>
    * 清华/阿里的 LogReducer 系统(用 C/C++ 重写了 logzip，并加上对特定数值型参数值的差分、关联和变长压缩优化)，论文：<https://www.usenix.org/system/files/fast21-wei.pdf>
    * 清华/阿里的 [LogGrep 开源实现](https://github.com/THUBear-wjy/LogGrep)，在上面 LogReducer 基础上，参考 CLP，重新设计了参数值的压缩方式，实现了不解压查询。总结来说还是牺牲一些写入 CPU，换磁盘空间和查询 CPU。论文：<https://web.cse.ohio-state.edu/~wang.7564/papers/eurosys23-final39.pdf>
    * 匈牙利罗兰大学的改进，主要在内存消耗上领先，论文：<https://www.mdpi.com/2076-3417/12/4/2044/pdf>
    * 北大/港中深的 DeNum 项目：<https://github.com/gaiusyu/Denum>。抓住了一个很有趣的点“日志里数值占比很高，且不会太长”，并对数值设计了一套`(长度、首位)`编码标记，同一个标记的数值序列压缩率超高。剩余部分直接复用 logzip。
* DeepLog 论文(包含模式检测、参数检测、工作流检测三部分)：<https://acmccs.github.io/papers/p1285-duA.pdf>
    * 开源实现：<https://github.com/wuyifan18/DeepLog>
    * 另一个开源实现，还实现了另外两种算法[LogAnomaly](https://www.ijcai.org/Proceedings/2019/658)和[RobustLog](https://dl.acm.org/doi/10.1145/3338906.3338931)，可切换：<https://github.com/donglee-afar/logdeep>
* 中山大学的 SwissLog 论文，和 RobustLog 一样关注模型的鲁棒性问题：<https://www.researchgate.net/publication/346867203_SwissLog_Robust_and_Unified_Deep_Learning_Based_Log_Anomaly_Detection_for_Diverse_Faults>
* 中山大学/腾讯微信的 LogReducer 开源实现，通过离线分析低效日志，反馈给在线的eBPF过滤器：<https://github.com/IntelligentDDS/LogReducer>，其实论文中有关微信现状的分析解读更有趣。比如写错日志和忘删测试日志，占了无效日志的一半，一天几个PB。而且微信目前日志是promtail+loki+clickhouse。
* 清华/南开/腾讯的 FT-tree 开源实现：<https://github.com/WeibinMeng/ft-tree>
* 清华/南开/百度的 LogClass 开源实现：<https://github.com/NetManAIOps/LogClass>
* 北卡顾晓晖团队做日志异常检测的 ELT 系统(拆分为粗粒度的 MAV 和细粒度的 MFG 两层)：<http://dance.csc.ncsu.edu/papers/srds11.pdf>
* NEC 美国实验室/北卡做云系统工作流监控的 CloudSeer 系统：<https://people.engr.ncsu.edu/gjin2/Classes/591/Spring2017/case-cloudseer.pdf>
* NEC 美国实验室 LogMine 系统：<http://www.cs.unm.edu/~mueen/Papers/LogMine.pdf>
   * 开源实现：<https://github.com/trungdq88/logmine>
* NEC 美国实验室/蚂蚁金服做的 LogLens 系统(在 LogMine 基础上，和 ELK 的 Grok 设计结合；并加上了对 traceid 的判断处理，支持序列异常检测)，论文：<http://120.52.51.14/www.cs.ucsb.edu/~bzong/doc/icdcs-18.pdf>
* 香港中文大学/华为的 POP 系统(和 LogMine 思路比较类似，在 Spark 上运行)：<http://www.cse.cuhk.edu.hk/lyu/_media/journal/pjhe_tdsc18.pdf>
* 康考迪亚大学发表的 logram 论文(用 n-gram 来做日志解析)：<https://petertsehsun.github.io/papers/HetongTSE2020.pdf>
* 康考迪亚大学发表的 LogAssist 论文，用 n-gram 对已提取的日志模板序列做二次压缩，并用案例研究法对比效果：<https://petertsehsun.github.io/papers/TSE2021_LogAssist.pdf>
* 加拿大麦克马斯特大学的日志序列异常检测开源实现，加上序列每一步 duration 子序列做神经网络特征：<https://github.com/hfyxin/Ts-models-log-data-analysis>
* RedHat公司CTO办公室开源的Log Anomaly Detector项目(基于word2vec和SOM算法)：<https://github.com/AICoE/log-anomaly-detector>
* 其他商业公司：
    * Loomsystems(已被 serviceNow 收购，其对参数类型的 meter/gauge/timeless-gauge/histogram/invalid/root-cause 分类值得借鉴)：<https://www.loomsystems.com/hubfs/SophieTechnicalOverview.pdf>
    * coralogix(有基础的无关顺序的关联模式检测，对 XML/JSON 类型进行对象参数检测)：<https://coralogix.com/tutorials/what-is-coralogix-pattern-anomaly/>
    * zebrium(存 newsql，参数名称的自动识别值得借鉴，最后用 GPT-3 生成告警描述也很有趣)：<https://www.zebrium.com/blog/using-ml-to-auto-learn-changing-log-structures>
    * ludexAI(用向量微调来做日志模式解析，附加向量相似度搜索做模式缓存，对比 LILAC 稍慢。但作为商业公司，宣称在自己生产环境上对 unseen log 更稳定，并给了生产环境上的 p90 延迟监控图)：<https://arxiv.org/pdf/2408.08300>

#### 大模型方法

* 北航发表的 LogQA 论文，利用 [T5 大模型](https://huggingface.co/iarfmoose/t5-base-question-generator)，和手工标记生成的[训练数据](https://github.com/LogQA-dataset/LogQA/tree/main/data)，实现了对日志的自然语言问答：<https://arxiv.org/pdf/2303.11715.pdf>
* 澳大利亚纽卡斯尔大学开源的 LogPPT 项目，利用 RoBERTa 大模型和 loghub 数据集。最有趣的点是 loghub 数据集中虽然 80G 日志但每类只有 2k 条有标签的。本论文思路正好就反向用 2k 有标签的做 prompt：<https://github.com/LogIntelligence/LogPPT>
* 香港中文大学发表的 DivLog 论文，利用 GPT3 大模型，全面超过 LogPPT 的效果。并探讨了 ICL 方法用 5-shot 可能效果最佳：<https://arxiv.org/pdf/2307.09950v3.pdf>
   * 后续的 LILAC 开源项目，通过设计的 sampling 方法和 cache，在日志模板推理速率上逼近 Drain 效果！此外，和 LogPPT/LogDiv 的对比中，也验证了基础模型从 110MB 的 RoBerta 到 13B 的 Curie 到 176B 的 ChatGPT，似乎提升不太高。在模板识别任务上，可能中型 LM 的语言理解力就不错了？<https://github.com/logpai/LILAC>
   * 后续的 ULog 论文：<https://arxiv.org/pdf/2406.07174>。最前面先加一个简单的日志长度分桶，让任务可以并行起来。单任务的速度其实比 LILAC 慢，并行以后就更快了。
* IBM 开源的 BERTOps 项目，利用 BERT 大模型，和一部分人工标记数据，尝试了日志领域的三个分类任务，日志格式分类、黄金信号分类，故障分类(不过这个库就是纯展示，跑不起来，train.sh 里的 pretrain.txt不存在，只给了清洗前的 annotation Excel 文件)：<https://github.com/BertOps/bertops>
    * IBM 发表的 InstantOps 论文，利用 BERTOps 提取的日志特征，加上指标、k8s event、trace 等，进一步构建了图谱，做根因分析：<https://dl.acm.org/doi/pdf/10.1145/3629526.3645047>。在复旦开源的 [train-ticket](https://github.com/FudanSELab/train-ticket/)、[云智慧开源的 micross](https://github.com/CloudWise-OpenSource/GAIA-DataSet/tree/main/MicroSS) 和 [gitlab 开源的 quota-of-the-day](https://gitlab.com/quote-of-the-day/quote-of-the-day) 三个测试床上，准确度召回度都接近 1 了。
* 浙大/华为开源的 KTeleBERT 项目，综合知识图谱和 BERT 大模型，同时利用产品手册、设备告警日志和 KPI 异常进行通讯领域故障分析：<https://github.com/hackerchenzhuo/KTeleBERT>
* 华为/中科大开源的 Biglog 大模型，基于 Bert 利用 16 个项目的4 亿 5 千万日志做无监督预训练：<https://github.com/BiglogOpenSource/PretrainedModel>。对应论文见：<https://ieeexplore.ieee.org/document/10188759/>
* 华为/北邮发布的 LogPrompt 论文，利用 ChatGPT 和 Vicuna-13B 验证 zero-shot、CoT、ICL 几种不同 prompt 方案下的日志模板提取和异常检测效果：<https://arxiv.org/pdf/2308.07610.pdf>。对比基准就是上面的 LogPPT，结论是 ChatGPT 即使 zero-shot 也比 LogPPT 强一点。而开源的 Vicuna-13B 在 zero-shot 情况下差很多，但 ICL 方案下效果提升很大，接近可用水准。
* 北航/云智慧开源的 Owl 运维大模型数据集，包括问答题和多选题两类：<https://github.com/HC-Guo/Owl>。对应论文中还评测了 MoA 微调、NBCE 长上下文支持、在 loghub 日志模式识别上的差异，不过优势都很微弱。
* 华为开源的 [SuperLog 数据集](https://github.com/J-York/SuperLog/blob/main/data/NLPLog.json)：在 loghub 数据集的基础上，进行模式比例调整重构，然后针对每个模板，分 5 个维度(Grok 正则、日志解读、根因分析、组件关联分析、潜在故障预测) 10 个模板，生成25 万条问答。
* 北航/云智慧发表的 ECLIPSE 论文，重点解决实际日志模式过多问题（除了 logpub 以外还自己做了一个 ECLIPSE-Bench 数据集）：<https://arxiv.org/pdf/2405.13548>。大致思路是在日志模式提取后，再用 LLM 提取模板对应的核心单词和punct标点，然后构建`{关键词:标点模板}`词典存入 faiss 向量数据库。然后新日志先通过faiss 做 kNN 搜索，只在搜索结果内做 LCS 最长子串匹配逻辑来考虑是否合并更新模式。
    * 北大/港中深的 AdaParser 论文：<https://arxiv.org/pdf/2406.03376>。类似思路上，加了一个 corrector 模块，包括对匹配失败的“错误”模式的更正、“正确”模式里一些不恰当变量(关键信息保留为常量)的更正。
    * 重庆大学的 LogBatcher 项目：<https://anonymous.4open.science/r/LogBatcher/README.md>。类似思路，而且就用了基础的 TF-IDF 和 DBSCAN 来实现聚类，DPP 实现采样。一个额外改进就是模板缓存里会记录频率并重排序。最后评估结果里还对比了 tokens 消耗，比 LILAC 省钱～
    * 阿里巴巴美国的 LogParser-LLM 论文：<https://dl.acm.org/doi/pdf/10.1145/3637528.3671810>。类似思路，额外改进时候区分了“松散匹配”，对松散匹配的模式可以让 LLM 更新。最后评估结果里还对比了 LLM 调用次数，但是如果换算成 tokens 消耗的话，应该不如 LogBatcher 省钱～
* 清华/必示发表的 OpsEval 论文，场景和 Owl 类似，不过仅对比开源模型的表现，并区分中英文差异。实践发现中文问答质量差很多：<https://arxiv.org/pdf/2310.07637.pdf>。
    * 后续还有 LogEval: <https://github.com/LinDuoming/LogEval>。总的来说不同任务，不同模型表现不一样，甚至 few-shot 都不一定领先 zero-shot。
* 北大/蚂蚁金服开源的 CodeFuse-DevOpsEval 评测数据集，包括 DevOps 和 AIOps 两大块12类场景的选择器：<https://github.com/codefuse-ai/codefuse-devops-eval/blob/main/README_zh.md>，不过 AIOps 里根因分析场景 qwen 的分数异常的高，我个人怀疑是不是 qwen 预训练用到了阿里巴巴内部资料。
* 香港中文大学/微软发表的 UniLog 论文，把 LLM 的 ICL 方法用在日志增强领域：<https://www.computer.org/csdl/proceedings-article/icse/2024/021700a129/1RLIWpCelqg>
* 复旦大学开源的 KnowLog 项目，爬取了思科、新华三、华为三家网络设备的公开文档里关于日志模板的描述内容，基于 Bert 和 RoBerta 做预训练模型：<https://github.com/LeaperOvO/KnowLog>
    * 后续更新的 LUK 项目，改用 ChatGPT 来生成日志解读数据，用于 Bert 预训练：<https://github.com/LeaperOvO/LUK>

## 标注

### 指标异常标注

* 百度开源的指标异常标注工具：<https://github.com/baidu/Curve>
* 微软开源的指标异常工具：<https://github.com/Microsoft/TagAnomaly>
* 清华/建行做的指标批量标注 Label-less 项目(基于 iForest 异常检测和 DTW 相似度学习)：<https://netman.aiops.org/wp-content/uploads/2019/10/Label-less-v2.pdf>

## 预测

### 单指标

* 脸书开源，时序预测：<https://github.com/facebook/prophet>
* 红帽开源，是 hawkular(已被 jaeger 取代)项目的一部分，在 ARIMA 基础上做了自动调参：<https://github.com/hawkular/hawkular-datamining>
* 360 开源，封装了LR、ARIMA、LSTM等通用算法做预测：<https://github.com/jixinpu/aiopstools/tree/master/aiopstools/timeseries_predict>
* 北卡顾晓晖团队做监控系统数据传输压缩的论文(先聚类并下发预测模型，agent上预测无偏差就不上报了)：<http://dance.csc.ncsu.edu/papers/ICAC09.pdf>
* 蚂蚁金服开源的 Pyraformer 项目，其中还额外开源了公司内部的 AppFlow 数据集：<https://github.com/ant-research/Pyraformer>

### 容量规划

* 谷歌 某 12.5k 规模集群的任务资源和机器数据：<https://github.com/google/cluster-data>
* 微软 Azure 云某区的云主机启停、 CPU 和内存时序数据：<https://github.com/Azure/AzurePublicDataset>
* 阿里云某 1.3k 规模集群的云主机、容器和后台任务的时序数据：<https://github.com/alibaba/clusterdata>
   * 使用该数据集做的天池调度算法大赛第6名"地球漫步"的开源版本：<https://github.com/NeuronEmpire/aliyun_schedule_semi>
* Trulia 开源，根据查询语句预测 Solr 集群的查询性能并调度：<https://github.com/trulia/thoth>
* CMU 开源的关系型数据库自动调参工具 ottertune：<https://github.com/cmu-db/ottertune>
* PingCAP 仿作的 TiKV 自动调参工具：<https://github.com/tikv/auto-tikv>
* 中山大学发的 Elasticsearch 自动调参研究：<https://ieeexplore.ieee.org/ielx7/6287639/8948470/09079492.pdf>
* 康考迪亚大学发的 Kafka 容量预测研究(前半段过程和自动调参类似，但是目的是得到模型后做参数变化下的预测，所以主要对比的是 XGBoost、LR、RF、MLP 的区别)：<https://github.com/SPEAR-SE/mlasp>
* 南加州大学开源的 unicorn 项目，采用因果推理算法发现最佳最重要的参数，最有趣的是还在 wiki 上贴了历次投稿驳回和修改意见：<https://github.com/softsys4ai/unicorn>
* AT&T和得克萨斯大学奥斯丁分校发的 Chroma 论文，通过网络 KPI 和网络拓扑、属性等数据，推荐最佳的 4G/5G 蜂窝网络配置：<https://dl.acm.org/doi/pdf/10.1145/3570361.3613256>

### 网络

* 南开张圣林，交换机 syslog 故障预测：<http://workshop.aiops.org/files/shenglinzhang2018prefix.pdf>

### 事件关联挖掘

* 微软亚研的 Log3C，日志和 KPI 的关联挖掘：<https://github.com/logpai/Log3C>
* 微软和吉林大学的论文：<http://www.microsoft.com/en-us/research/wp-content/uploads/2016/07/SIGKDD-2014-Correlating-Events-with-Time-Series-for-Incident-Diagnosis.pdf>
    * 360 公司按照该论文的开源实现：<https://github.com/jixinpu/aiopstools/tree/master/aiopstools/association_analysis>
* IBM研究院的论文，利用微服务错误指标和错误日志，采用因果推理算法和个性化 PageRank 算法，进行故障定位(文章主要目的是引入个性化 PR，因果推理这方面没区分 PC 和回归有什么差异)：<https://www.researchgate.net/publication/344435606_Localization_of_Operational_Faults_in_Cloud_Applications_by_Mining_Causal_Dependencies_in_Logs_using_Golden_Signals>

## 根因分析

### 调用链

* 开源 APM/tracing 实现：
   * zipkin/brave：<https://github.com/openzipkin/brave>
   * springcloud/sleuth：<https://github.com/spring-cloud/spring-cloud-sleuth>
   * skywalking：<https://skywalking.apache.org/>
   * jaeger：<https://github.com/jaegertracing/jaeger>
   * pinpoint：<https://github.com/pinpoint-apm/pinpoint>
   * elastic apm：<https://github.com/elastic/apm>
   * datadog apm：<https://github.com/DataDog/dd-trace-java>
   * opencensus/opentelemetry：<https://opentelemetry.io/>
   * cilium/hubble：<https://github.com/cilium/hubble>
   * pixie/stirling：<https://github.com/pixie-labs/pixie/tree/main/src/stirling>
* 萨尔布吕肯大学Jonathan Mace，利用层次聚类尽量避免采样时丢失罕见个例：<https://people.mpi-sws.org/~jcmace/papers/lascasas2018weighted.pdf>
* 谷歌开源的微服务测试床：<https://github.com/GoogleCloudPlatform/microservices-demo>
* 复旦大学开源的大规模微服务测试床：<https://github.com/FudanSELab/train-ticket/>
* 清华裴丹团队举办的调用链根因定位比赛：<http://iops.ai/competition_detail/?competition_id=15&flag=1>
    * 华南理工针对该比赛发的论文：<https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9293310>
* 意大利比萨大学关于微服务环境下异常检测和根因分析的综述论文：<https://arxiv.org/pdf/2105.12378.pdf>
* Uber开源的调用链关键路径分析工具，还包括时钟偏移补偿和异常检测等：<https://github.com/uber-research/CRISP>

### 多维定位

* 清华/百度的HotSpot论文，有多维属性的 KPI 故障范围分析：<http://netman.ai/wp-content/uploads/2018/03/sunyq_IEEEAccess_HotSpot.pdf>
* 清华/建行的FluxRank论文，在服务级故障时，快速定位到小范围的主机层问题并重启：<https://netman.aiops.org/wp-content/uploads/2019/08/liuping-camera-ready.pdf>
* 里昂国立应用科学学院的论文，采用子群发现算法，综合 SQL 解析、环境版本、告警、指标进行 SQL 慢查询定位：<https://www.researchgate.net/publication/353776691_What_makes_my_queries_slow_Subgroup_Discovery_for_SQL_Workload_Analysis>
* NEC 实验室开源的 LEMMA-RCA 数据集：<https://lemma-rca.github.io/>，包括 product review 和内部一个 openshift 微服务上收集的日志和指标两类原始数据、以及对应的故障标注。并在这个数据集上，评估了包括 REASON、NEZHA 和 MULAN 在内的 sota 多模态根因定位方案的效果。

### 时序相关性分析

* etsy 开源版，基于 elasticsearch 实现的 fastDTW 时序相关性排序：<https://github.com/etsy/oculus>
* linkedin 开源的基于 SAX 的异常检测和相关性计算库：<https://github.com/linkedin/luminol>
    * 此外，还有一个完整系统的介绍分享：<https://docs.google.com/presentation/d/1DWMNgoAtxuK8ZbFJOpq5vt3dEz5_4ptMuLtoTUjQ_ro/pub?start=false&loop=false&delayms=3000&slide=id.p>
* Uber 公司的 Argos 系统，只有介绍文章：<https://eng.uber.com/argos/>
* IBM 发表的 [KIMetrix 论文](https://arxiv.org/pdf/2501.03547)：服务内基于指标数据熵排序，熵最大的就是基准指标，然后其他指标根据互信息量过滤，保留最终集合；服务间以 root service 的指标集合为初始化集合，重复互信息量过滤流程，并根据 trace 路径的请求量动态调整过滤阈值。最终得到整个微服务应用的核心指标集合。

### 解决方案相关性推荐

* 佛罗里达国际大学/IBM的论文，基于 CNN 做工单的关联和推荐，重点在如何过滤和提取工单文本的有效特征值：<https://www.researchgate.net/publication/318373831_STAR_A_System_for_Ticket_Analysis_and_Resolution>

### 大模型方法

* 北大发表的故障管理领域大模型研究综述：<https://arxiv.org/pdf/2406.11213>
* 东南大学发表的根因分析领域算法研究综述，3.5 小节是大模型部分：<https://arxiv.org/pdf/2408.00803>。比较有意思是开篇总结了一个表格，列出来了最近 3 年国内外有名的 14 次互联网厂商大型故障影响和原因。
* 微软发表的 Xpert 论文，从告警工单入口，依赖告警消息内容作为上下文，生成微软Azure自有的 Kusto Query Language：<https://arxiv.org/pdf/2312.11988.pdf>。论文提出了一个 Xcore 评价方法，从文本、符号、字段名匹配度多方面综合评估。不过文中举的错误示例，告警上线文和正确输出之间一个字都对不上，实在是不可能写对——本文给我的另一个提示：纯粹通过 Chat 形式让人提问生成查询语句，上下文信息太少，太难。当前阶段合适的策略还是找一些特定入口。
* google 开源的 NL2LogQL 问答数据集：<https://huggingface.co/datasets/nl-to-logql/natural-logql>。数据集主要针对 loghub 里 openstack、hdfs 和 openssh 三种源日志，对应的 grafana dashboard 的趋势图，然后按照 LogQL 语句的复杂度做了比例调整。
* 微软发表的《Recommending Root-Cause and Mitigation Steps for Cloud Incidents using Large Language Models》论文，通过对微软内部4万个故障数据复盘，研究 GPT 模型对比 BERT 模型是否在故障诊断方面更有优势。大概的结论可以认为是：有优势，但依然没啥用。：<https://arxiv.org/pdf/2301.03797.pdf>
* 微软亚研/南开发表的《Assess and Summarize: Improve Outage Understanding with Large Language Models》论文，对比 GPT2(本地单卡微调)，GPT3(6.7b)和 GPT3.5(175b) 的告警概要水平。3 到 2 确实差异非常明显，但 6.7b 到 175b 倒没有提升特别多：<https://arxiv.org/pdf/2305.18084.pdf>
* 微软发表的 RCACopilot 论文：<https://yinfangchen.github.io/assets/pdf/rcacopilot_paper.pdf>。先对告警信息做摘要，然后用预训练的 fasttext 嵌入模型来做历史故障的向量搜索，在最终的 prompt 里同时提供摘要和历史故障的分类和描述，让 LLM 判断是不是老故障，是的话用 CoT 推理怎么处理。论文中提供了较多的评估数据，但本身对实验运用的团队和业务环境有强依赖，很难判断适用性。
* 微软发表的另一篇 ReAct 框架做 RCA 的技术报告：<https://arxiv.org/pdf/2403.04123.pdf>。大概结论是：不开发特定 Tool，靠通用的文档召回 tool，ReAct 效果还不如直接 RAG 或 CoT。即使开发特定 Tool，知识库里的分析计划写的如何，也才是影响最大的。一旦涉及多个知识库文档，ReAct 差不多到第二三轮就会一直失败下去了。
* 清华/微软开源的 AIOpsLab 项目：<https://microsoft.github.io/AIOpsLab/>。提供了一套 AIOps 从检测到定位到修复的评估框架。首批对比了直接使用 GPT 和 ReAct 方案、以及微软之前发表的[FLUSH智能体方案](https://www.microsoft.com/en-us/research/uploads/prod/2024/10/FLASH_Paper.pdf)的差异。结果分析里最有趣的是：成功 case 里其实调用 get_metric 和 get_trace tools 的比例很低！也就是说直接 kubectl 工具分析不出来的故障，就算再加指标和调用链，成功概率也不高了。
* IBM 开源的 [KubePlaybook 数据集](https://github.com/K8sPlayBook/KubePlaybook/tree/main)，包括 130 份自然语言查询生成 ansible playbook 的语料，分为配置查询和故障分析操作等场景。该团队同时基于这个数据集验证了 few-shot learning 对生成 ansible playbook 的重要性（GPT4 和 llama2-70B 下测试，成功率从个位数提升到百分之七八十。另一个有趣的结论是温度设置最好为 0.6）：<https://dl.acm.org/doi/pdf/10.1145/3663529.3663855>
* 阿里云 Flink 团队发表的 RCAgent 论文: <https://arxiv.org/pdf/2310.16340v1>。其中为了对 flink 错误日志做概要，设计了一大段巨复杂的流程（向量转换，滚动构建矩阵，Louvain贪婪去重聚类，RGA 生成解释和证据，计算证据和原始日志的LEVENSHTEIN距离做过滤，最后二次概要）。
* 港中深开源的 [OpenRCA 数据集](https://github.com/microsoft/OpenRCA)：将之前三届 AIOps 挑战赛的数据集整理过滤，方便进行 RCA 智能体评测。论文自己也实现了一个简单的 Agent 但是效果很一般。注意数据集中有一些号称故障但其实对业务指标毫无影响的场景，我个人认为并无 RCA 必要。
* Flip.AI 公司，自研的 DevOps 大模型，发表了技术报告。采用了 1 encoder -> N decoder 的 MoE 架构，在 80B token 上增量预训练；微调训练部分主要数据来源是基于 RAG 的 evol-instruct 仿真数据再辅以 18 个月的人工双盲过滤；强化学习阶段是 RLHAIF，构建一个故障注入环境，让模型生成 RCA 报告：<https://assets-global.website-files.com/65379657a6e8b5a6ad9463ed/65a6ec298f8b53c8ddb87408_System%20of%20Intelligent%20Actors_FlipAI.pdf>

## 告警归并

* 360 开源，基于 Apriori 算法：<https://github.com/jixinpu/aiopstools/blob/master/examples/alarm_convergence.py>
* 里昂国立应用科学学院的 SplitSD4X，采用子群发现算法，配合 NLP 解析事故报告文本，生成同类故障描述：<https://github.com/RemilYoucef/split-sd4x>
* anodot 公司论文，第三部分，利用 SAE 和 LDA 做 KPI 和告警的拓扑：<http://proceedings.mlr.press/v71/toledano18a/toledano18a.pdf>
* 其他商业公司：
    * [moogsoft](https://docs.moogsoft.com/) 公司(专门做告警处理的AIOps创业公司)有关技术实现的演讲：<https://docs.google.com/presentation/d/1F-8eop-9ffCpX4trOJS28FXATAFlQkgkfnDV_Zqnkuo/edit?pref=2&pli=1#slide=id.g990524d96_0_0>

## 图谱

* 清华大学徐葳团队，状态图谱解决 OpenStack 问题：<http://iiis.tsinghua.edu.cn/~weixu/files/apsys-yong-slides.pdf>
* 徐葳早年论文，用状态图来辅助开源项目更好的修改 logging 代码：<http://iiis.tsinghua.edu.cn/~weixu/files/slaml10-rabkin.pdf>
* 华为开源的 [OpenStack 可观测性数据](https://jorge-cardoso.github.io/publications/Papers/CP-2020-093-Multi-source_Distributed_System_Data.pdf)样本集，trace 部分用的osprofiler 采集：<https://zenodo.org/record/3549604#.YE8Q-eHithE>
* 宜信张真的演讲：[WOT2018 -张真-运维机器人之任务决策系统演讲](https://pan.baidu.com/s/1gSjJZIXswOPoeQzZ6cJT1g?errno=0&errmsg=Auth%20Login%20Sucess&&bduss=&ssnerror=0&traceid=)
* CA/加泰罗尼亚理工大学，用日志和指标构建的基于图谱的微服务根因分析系统：<https://www.researchgate.net/publication/336585890_Graph-based_Root_Cause_Analysis_for_Service-Oriented_and_Microservice_Architectures>
* 微众银行的智能运维系列分享第八篇(给了非常详细的节点属性和边属性设计，比 CA 的更细节)：[事件指纹库：构建异常案例的“博物馆”](https://mp.weixin.qq.com/s/M8tcS8q6sPPRRebAJkrb7Q)
* 中山大学融合了拓扑的指标异常检测系统 TopoMAD，开源的数据样本：<https://github.com/QAZASDEDC/TopoMAD>
    * 网络另一篇针对 TopoMAD 论文的解析和评论文章，比较犀利：<https://dreamhomes.top/posts/202103111131.html>
* 中山大学融合可观测性三大数据的根因定位系统“哪吒”，将指标、日志、调用链都转换成事件后，构建拓扑图，并根据业务告警触发异常拓扑和正常拓扑的对比，给出根因事件(调用变化或指标、日志异常等)。开源地址：<https://github.com/IntelligentDDS/Nezha>。文章在电商和火车票两个开源微服务 demo 上(比原始版本做了 otel 插码的升级改造，日志里也加 traceid 和 spanid 了)都验证了效果，同时分别验证了缺少某类数据的影响，发现两个 demo 上一个偏重指标一个偏重日志。不过评估上一堆 95+还是有点让人不敢相信。
    * NEC美国实验室发表的“木兰”，用指标和日志构建GraphSage图神经网络，在电商、火车票和产品打分三个应用上评测，并对比了“哪吒”：<https://dl.acm.org/doi/pdf/10.1145/3589334.3645442>。论文引入的 KPI 感知注意力机制能较好的避免指标数据质量问题。但是我不太理解为啥日志部分还要自己单独训练一个双向 transformer 语言模型来做日志向量化？
* 维也纳工业大学的[VloGraph](https://www.mdpi.com/2504-4990/4/2/16)项目，利用 NLP 和图谱分析技术，做安全场景的日志解析、存储和查询可视化框架：<https://github.com/sepses>
* 清华大学/ebay的 AlertRCA，算是之前北大/ebay 的 [Groot](https://arxiv.org/pdf/2108.00344) 的加强版。利用 Bert 向量化告警、图注意力来学习因果，不用手动配置规则：<https://netman.aiops.org/wp-content/uploads/2024/03/AlertRCA_CCGRID2024_CameraReady.pdf>
* 清华大学/蚂蚁金服的 SparseRCA 论文：<https://netman.aiops.org/wp-content/uploads/2024/09/SparseRCA__Unsupervised_Root_Cause_Analysis_in_Sparse_Microservice_Testing_Traces__ISSRE24_Camera_Ready_.pdf>。论文通过案例研究提出一个观点：有一部分 span 的自身耗时，也跟 child 的数量有关，所以能用 EM 算法构建一个对未知 trace pattern 的耗时的拟合函数，用于 RCA 异常检测和排序。
* IBM 发表的 Astraea 论文，针对的是 trace 采样问题，思路比较另类，span 级采样，根据耗时分布，丢掉对排障没意义的 span。每种 span 的采样率就是在自身耗时拟合的 beta 分布下，蒙特卡洛方法筛选的 P90 概率：<https://arxiv.org/pdf/2405.15645>。论文背景里还提到，阿里曾经发过论文，说只有 10% 的 span 在 trace 排障中有用。
* 中大/阿里云发表的 Mint 论文：<https://arxiv.org/pdf/2411.04605>。提出了“近似 trace”的概念。按 trace 模式(分 trace 调用路径模式和 span 属性模式两层)聚类采样，未被挑中的数据只保留traceid、spanname、starttime、duration、模式和参数分桶。这样既大幅降低了传输流量和存储空间，还保留了正常请求的全部 traceid和 duration，可以更准地进行根因定位。

## 行为异常

* 北卡顾晓晖团队做程序行为异常分析的 PerfScope 系统(利用 LTTng 在线采集系统调用，配合 Apriori 算法)，论文：<http://dance.csc.ncsu.edu/papers/socc14.pdf>
* ee-outliers 开源项目，利用 word2vec 做 osquery 输出的事件异常检测：<https://github.com/NVISO-BE/ee-outliers>
* ubad 开源项目，利用 LSTM 和 OCSVM 做 osquery 输出的用户行为事件异常检测：<https://github.com/morrigan/user-behavior-anomaly-detector>
* 阿里云天池算法大赛扫描爆破部分，第10名的开源介绍：<https://github.com/wufanyou/aliyun_safety>
* Security Repo数据集，Mike Sconzo收集的各种和安全运维有关的数据：<https://www.secrepo.com/>
* 奥地利 AIT 的安全日志数据集：<https://zenodo.org/record/5789064#.YkFnZWJBxhE> 及其数据生成的测试床项目：<https://github.com/ait-aecid/kyoushi-environment>
* 其他商业公司：
    * ExtraHop：<https://docs.extrahop.com/current/>

## 扩展阅读

* salesforce AI实验室的 AIOps 综述论文：<https://arxiv.org/pdf/2304.04661.pdf>，覆盖了指标、日志、调用链、根因分析、故障预测、自愈策略等各领域 237 篇论文。
* @linjinjin123 的 [awesome-AIOps](https://github.com/linjinjin123/awesome-AIOps) 库，但我认为运维人员可能更需要的是一个从实用场景出发的归类。
* @Jun-jie-Huang 的 [awesome-LLM-AIOps]https://github.com/Jun-jie-Huang/awesome-LLM-AIOps) 库，专精在大模型领域的智能运维论文收集。
* @zhuyiche 的 [awesome-anomaly-detection](https://github.com/zhuyiche/awesome-anomaly-detection) 库，专精在异常检测领域的论文收集。
* @logpai 的 [log-survey](https://github.com/logpai/log-survey) 库，专精在日志领域的论文和研究者收集，不光包括分析，还包括生成增强、压缩等。
* @jorge-cardoso 对 AIOps 领域的系统映射研究：<https://jorge-cardoso.github.io/publications/Papers/WP-2020-079-AIOPS2020_A_Systematic_Mapping_Study_in_AIOps.pdf>
* @jorge-cardoso 对 AIOps 故障大类别的研究综述：<https://jorge-cardoso.github.io/publications/Papers/JA-2021-025-Survey_AIOps_Methods_for_Failure_Management.pdf>
* 中国移动信息技术有限公司关于自动化运维和智能运维的成熟度评估模型介绍：<https://kns.cnki.net/kcms/detail/detail.aspx?dbcode=CJFD&dbname=CJFDLAST2021&filename=DGJB202101009&v=4TGdKbAr7slYCfXAgxJfw2rHqvDI%25mmd2FLQ8iARm627FUgNvt7c9lvfHVIbYjAz8eR2x>
