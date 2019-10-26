---
layout: cnpost
title: 你所理解的程序员与我所理解的·上
date: 2019-10-24 23:00:00
categories: cn
tags: 程序员入门指南
--- 

__Contents__

* content
{:toc}

### 前言

从 2018 年 08 月到现在(2019.10)，我一直在从事 golang 方向的软件研发工作，算下来，14 个月有余了。我想把这期间的经历和感想总结下来，希望对你有所帮助。

### 槽点

我的朋友中（哦对,也包括你）从事软件开发的人不多，他们对这个行业里的人往往有很多“自己的理解”。比如：程序员是修电脑好手、盗号天才，可以肆意的对某某网站发起致命的攻击等等，包括秃顶 ：）

我们开发人员私下聊天里有不少这样的抱怨：

- 谁谁谁又让我修电脑
- 谁谁找我要外挂
- 某网站总给我推送植发广告

生活中有不少类似上面的这些例子，我们队伍里颇有些人埋怨：我招谁惹谁了？

不过我本人倒不太在意，不就是些标签嘛，娱乐一下大家也蛮好的。况且，通过这样的噱头，我们工程技术人员能从幕后走到台前，走进大众的视野，不挺好吗？你看，我们的职业在社会的曝光度越来越高，我们这个群体在全社会的存在感也越来越强，那么不难想到，整个社会对我们这个群体发出的声音，只会越来越重视。

这对我们来说，当然是一件大好事。我们仅仅付出被人无缘无故问候发量这样芝麻绿豆点儿的代价，就收获这么一大堆回报，是一件多么经济的事情啊。远的不说，前些日子一位开发人员仅仅做了一个 [996.icu](https://996.icu) 静态网页，就引起全社会对加班的大讨论，这还不能说明我们的价值吗？

### 正名

有一次碰到一个法国人，我跟他聊天。他问我做什么工作的，我想了一下，竟然不太晓得该用哪个单词来描述我的职业。最后我说我是一名 software engineer，然后你看到他瞪大了眼睛，露出一份不可思议的表情，连说很棒很棒之类的话。

我一直不清楚为什么那个外国人如此大惊小怪，后来我猜啊，有可能是“software engineer”的表述问题。

在中文世界中，我们对*从事软件撰写、程序开发及维护的专业人员*就有不同的称谓。正式一点你可以说**软件工程师**，你也可以说**开发人员**，非正式一点就是**程序员**，再土一点就是**码农**了。

每个名字所代表的**情感**是不一样的。

我最不喜欢称自己或者别的同事为“码农”了。这个词并不是什么好词儿，虽然“代码”和“农民”都是两个中性的名词。我不否认我们是写代码的一群人，也没有看不起农民伯伯的意思，但是“码”和“农”组合在一起，就是有一种明显的自卑感啊。我们用作自嘲时还可以，如果认为自己的工作是“码农”，总有种你心不甘情不愿、被别人逼迫着、不得已才选择这一岗位的感觉，一点不自信，一点不热爱。那你未免有些太小看自己所在的行业，未免也太看不起自己了。你请门口的保安人员帮忙时，你会称呼人家“看大门的”吗？

程序员这个名字也不太好，都被大家娱乐化了。评价中性也是我最喜欢的名字就是“开发”或者“软件研发”，它其实是“开发者/软件研发人员”的简称。你称自己是“一个开发”，在业内一点儿问题都没有；碰到外人就称“我是一个软件研发人员”，特别好，倍儿自信，精神面貌倍儿好。你不用非得显摆英语足够好说自己“搞 IT”，搞的你像被挨踢了一样，“开发者” 的含义已经够用了。

软件工程师就又不太一样了。就像咱吃大蒜，人家喝咖啡一样，就又显得高端了。严格意义上讲，每一个软件研发人员都是“软件工程师”，但中文意境里，没两把刷子的也能叫 “xxx师”？的确是这样，反正我不好意思称自己为“软件工程师”，我心目中也是，只有那些基础扎实，技术过硬，能攻坚克难的软件开发人员，我才认可他为“软件工程师”。

说回到那个法国人，我用英文表达的“software engineer”可能就暗示了我 “基础扎实、技术过硬、能攻坚克难”，所以他才啧啧赞叹，其实此处最合适的单词应该是“developer”或者“programmer”。嘿嘿，不小心沾了个便宜。

### 黑客

软件开发人员跟黑客有联系吗？

有。

这就好像拿我的篮球水平跟姚明的水平进行比较一样。当然了，姚明的水平肯定经历过我这个阶段，但现阶段的情况是，我根本够不到姚明的脚后跟。

黑客首先是个软件开发人员，而软件开发人员只有经历过一番寒彻骨的技术的磨练，才能成为黑客。

> 然后就能盗号，就能破解软件，就能攻击美国白宫网站了吗？

对不起，不支持。

黑客不是你想象的那样…龌龊。关于黑客是什么，我建议你去阅读一下《黑客与画家》_--Paul Graham著·阮一峰译_

>黑客代表那些具备高度的革新、独树一帜的风格、精湛的技艺、第一流的能力、最能干的一群人。
>
>—黑客与画家·page2

### 日常

人们很容易想到销售人员的日常，不停的说话、说话、说话，说到客户掏腰包为止。

人们很容易想到作家的日常，不停的写，写了改，改了写，写了扔，扔了重写，直到满意。

这两种职业因为历史过于悠久，所以没有什么神秘的，你想到的，就是从事该职业的人每天经历的。但你很难知道一个金融分析师的日常，一个职业经理人的日常。这些职业比较新鲜，你没有机会亲身经历，甚至身边都很少有这样的人，而听来的小道消息往往不准，才导致你对这群人的印象模糊。

俗话说：距离产生美。人们往往对印象模糊的东西好奇心更大，更觉得有意思，因为神秘，神秘才会觉得高级。

软件研发行业也大概如此。如果你没接触过代码，没接触过写代码的人，很容易被小道消息带偏。你会想当然的认为研发工作中会有多少多少的奇思妙想，软件研发人员手指在键盘上飞快的舞蹈，脑袋则在飞快的旋转、跳跃，不知疲倦，每天都在改变世界。

你这样想，我也理解，这不能怪你。

首先，你在生活中接触不到失败的软件项目。能被大众列举出来的项目往往都是这个时代最出色、最成功的产品，比如苹果、微软、Google、腾讯等公司各种各样的软件产品，撑起了几乎大半个互联网世界。这些软件当然少不了软件工程师的功劳。不过同时，还有很多的项目最终无疾而终，很多的软件成了这个时代的陪葬品、炮灰，那也同样凝聚了不少软件工程师（甚至是同样顶尖的工程师）的心血，但，很遗憾，他们失败了，并没有改变世界，甚至浪费了大量资源。

其次，很多创业神剧的夸张渲染。为了迎合观众，那些根本没有技术背景的编剧胡编乱造。这些编造的桥段往往违背常识，包括技术行业里的常识，也包括职场的常识，甚至有的地方明显不符合“人”的常识，但，没办法啊，为了挣钱，为了迎合大众看热闹不嫌事大的口味，就编下去了。

再次，人们对未知心甘情愿的臆想。人们不了解这个行业，但小道消息可不少：所谓的工资高、工作充实、能力提升快，还能顺便改变世界。这样的岗位该是怎样的呢？他们想当然的认为从事这个行业的人个个精神抖擞、有梦想、有活力、聪明绝顶、老实本分而又才华横溢，个个都像比尔盖茨。总之，人们最缺什么品德，就把这些品德往陌生人上贴就对了，就像“别人家的孩子”永远是最好的、完美的、无敌的。

事实情况是：

>开发人员首先是人，其次是职场人，再次是软件研发人。

是人就有喜怒哀乐，有精神饱满的时候，就有颓废沮丧的时候。碰到简单问题可能会不屑一顾，复杂问题开始怀疑智商。

职场有职场的规则，不管哪个行业，领导具有决策权、一票否决权，软件行业依旧如此，依旧遵循基本的职场规则。你需要尊重你的上级，不胡言乱语、不恶意中伤；你需要勤勤恳恳、兢兢业业的工作，向其他人证明你的能力，你才能收获更多的尊重、更多的支持。

就像建筑行业、制造业，软件研发行业工作的开展，也非常依赖一套成熟的工作流程。比如建筑行业需要设计、成本预估、掉配资源、干活；软件研发行业需要首先项目立项，需求收集，再技术选型，分模块派发任务，约定任务截止日期，干活。

销售人员的业绩非常容易考核- -订单量，但对软件研发人员的考核却不太容易。虽然都是写代码，代码行数却并不是一个可靠的衡量指标，优秀的工程师代码量少而精，效率高，初级工程师往往是臭而长，效率低；难度也不太容易分辨，哪个功能实现比哪个功能难几个百分点，并不方便核算。

什么是优秀的软件工程师呢？或者俗气一点，如何做一个挣钱多的软件工程师呢？

软件研发行业因为其技术导向有一个优势：

> 不太容易滥竽充数。

故障如何修复，功能如何实现，服务器性能如何提高，这些都是板上定钉的指标，来不了一丁点儿的弄虚作假，能解决就是能解决，不能解决说破大天也解决不了。一个优秀的软件工程师有以下几个考核要素：

1. 计算机基础是否扎实
2. 解决问题的效率如何
3. 解决问题的质量如何
4. 遇到难题的解决态度和思路

有了上面这四个实打实的指标，你现在可以猜了，我们的日常都会干些什么呢？假如你是老板，你会给什么样的员工升职加薪呢？会给那些未来将要改变世界的还是解决了你当下难题的员工？是口号喊的震天响的员工，还是俯首甘为孺子牛的员工？是磨磨蹭蹭拖延到deadline的员工，还是日行千里的员工？

软件研发人员的日常是紧紧围绕公司的业务线展开，你的技术储备、接触的数据甚至是你的薪水，都直接依赖于你维护的业务。你要知道，你的代码并不值钱，只有你的代码被卖出去了，你付出的努力才算是有了价值回报。业务需求丰富，用户数量多，业务价值就大，开发难度也大，当然了，挣的也多；如果业务需求仨瓜俩枣，没几个人使用，一次开发，无需升级、维护，那业务价值就可想而知了，开发难度也就小了，你不需要加班，当然，挣的不会多，这不是你技术水平的原因，而是市场导向。

你应该明白，开发人员也只是一个生活在市场经济中的角色，一个角色能在社会中生存下去，靠的不是理想和情怀，是带给其他人多大的价值。这个给别人带来的价值会按一个不太严格的比例折现给你的。一个初级程序员更是这样，没有太多精彩、刺激可言，相反，每天面临的可能尽是困难、困难，你总得经历一段煎熬、挣扎、枯燥、无聊、困顿还缺钱的技术学习岁月，才能有所成长。

这样也好。据我观察来看，没有多少人大学毕业后还能保持旺盛的学习精力的，因为大多数的职业多靠有经验的人传授或者自己摸索，对书本的学习需求没有了，读书的人就少了，刷剧的、关注花边新闻的人就多了。软件研发行业秉承了黑客开源、共享的精神，随着它五六十年的发展，积淀下来一大批资深、经典的“内功型”书籍，还有散落在各个网站的文档。毫不夸张的说，软件研发人员的成长史就是一部阅读史。

处在这个行业中的人，即研发小伙伴们，他们没有应酬，不需要出差，生活可谓是安静、恬淡，可以心无旁骛的琢磨计算机技术问题。我很喜欢这群人，他们单纯、善良、真诚、淳朴，他们开放、包容、共享、人人平等。我爱这氛围。

未完待续...