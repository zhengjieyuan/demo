## [说明地址](https://mp.weixin.qq.com/s?__biz=MzIzOTU0NTQ0MA==&mid=2247504353&idx=1&sn=e2e91db76cdcdb8ce015ec10e107b749&chksm=e92aeceede5d65f8603919d22f92623bdbd5ae12d671f33f118e7b035fb4c70f3e245e95b5e2&scene=178&cur_album_id=1391790902901014528#rd)


本文的重点在于说明工作中所使用的设计模式，为了能够更好的理解设计模式，首先简单介绍一下业务场景。使用设计模式，可以简化代码、提高扩展性、可维护性和复用性。有哪些设计模式，这里就不再介绍了，网上很多，本文只介绍所用到设计模式。

一  线路检查工具

1  意义

为什么需要线路检查工具呢，有以下几个方面的原因：

    每逢大促都需要进行各网络和各行业的线路调整，调整完成之后，是否得到期望状态，需要检查确认。


    上下游应用之间数据的一致性检查，如果存在不一致，可能会在订单履行时造成卡单。


    有些问题发生后，业务同学需要全面检查一遍线路数据，判断是否符合预期。


    各领域之间的数据变更缺乏联动性，导致资源和线路出现不一致。


为什么要把线路检查工具产品化呢，考虑如下：

    以前每次大促，都是技术同学现场编写代码捞数据给到业务同学，而且因为人员流动性较大，代码可复用性较低，导致重复劳动。产品化后，可以方便地传承下去，避免不必要的重复劳动。


    每次因为时间紧急，现场写的代码都比较简单，经常是直接将数据打印到标准输出，然后复制出来，人工拆分转成Excel格式；这样的过程要进行多次，占用太多技术同学的时间。产品化后，解放了技术同学，业务同学可以自己在页面操作。


    很多数据检查，是每次大促都会进行的，业务同学与技术同学之间来回沟通的成本较高。产品化后，可以避免这些耗时耗力的沟通，大家可以把更多的时间放在其他的大促保障工作上。


2  检查项

根据2020年D11进行的数据检查，本次共实现8项，下面列举了4项，如下：

    时效对齐检查：确保履行分单正常。


    弱控线路与表达网络一致性：确保履行和路由不会因为线路缺失而卡单。


    资源映射和编码映射一致：前者是表达线路时所用，后者是订单履约时所用，确保表达和履约能够一致。


    检查线路数量：统计现存线路的情况。


好了，了解了背景知识，下面开始介绍所用到的设计模式，以及为什么要用、怎么用。


1  模板方法模式+泛型

2  策略模式

3  工厂模式

4  “代理模式”

![Image text](https://mmbiz.qpic.cn/mmbiz_png/Z6bicxIx5naJBBvNVIibvdkZ4CtMJQvBEEXDFicHOgV2b7V3pj71TnoRJthDHvuavMajUbOpfKxwq3c5L4HT52C7A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

针对不同的检查工具，只有“线路数据检查”这一步是不一样的逻辑，其他步骤都是相同的，如果每个检查工具都实现这么一套逻辑，必定造成大量的重复代码，维护性较差。
