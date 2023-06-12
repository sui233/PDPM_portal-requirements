# 操作逻辑设计
PDPM portal的操作逻辑为Dataset-centric，在这个意义上，其参照系为cBioPortal。但cBioPortal本身的架构，使得该网站在客观上强制要求用户按照其规定的操作规程来进行分析操作，某种意义上降低了用户操作的自由程度，并且限制了该网站自身分析功能的可扩展性。

GDC与ICGC的Data portal的分析功能则显示出高度的可扩展性，这种可扩展性是建立在“用户有一定的数据分析经验”的基础之上的，用户必须对于数据分析流程较为熟悉，并且能够较为清楚的知晓每种数据分析方法的意义，这个假设对于PDPM portal需要面向的用户群体在很大程度上是不现实的。考虑到本小组先前设计、上线的ExpressVis网站是面向这类用户的，并且ExpressVis更倾向于*引导用户推进数据分析*而非*强制要求用户根据某个操作流程进行数据分析*（这一点使得我在一开始对于cBioPortal产生了“分析功能匮乏”的错觉），因此，我们可以考虑将ICGC、GDC的Data portal的架构与ExpressVis的操作逻辑设计思路结合起来，通过引导与“代劳”的方式，帮助用户完成数据分析任务。

## 操作逻辑概览
在一般用户视角下，PDPM portal主要有“Project viewing and selecting”、“Gene searching and overviewing”、“Express Overview”、“Comprehensive Analyze”、“Customized selection”与“Set managing & manipulation”六个界面，用到“Patient”与“Protein”两类实体集合，其各类关系如下图所示：

<body>
<div style="text-align:center">
<img src="img/operation_logic.png" width="60%">
<p> 其中，蓝色折线代表操作流程，橙色折线代表数据流，绿色折线代表控制流 </p>
</div>
</body>

在这个分析过程当中，用户选择一个或多个基因或数据集，此后转到分析工具页面，利用分析工具给出的结果，在用户界面的引导下依次利用多种分析工具进行数据分析并浏览分析结果，最终完成分析，得出结论。这样就将cBioPortal与GDC、ICGC Data portal的优势有机的结合起来了。

## 页面功能概述
根据以上表述，要把操作逻辑落到实处，最重要的是UI功能的设计。这里的各个页面当中都包含了一些重要的元素，因此有必要在这里进行概述：

* **Project viewing and selecting**：该页面为主页的一部分。主要用于展示各个研究项目并辅助用户选取研究项目，以便用户针对其感兴趣的研究项目开展分析；
* **Gene searching and overviewing**：该“页面”在主页上显示为一个搜索框，用户可以在这个搜索框根据蛋白质的各种ID或相应基因的各类ID来对于蛋白质或基因进行检索；
* **Express Overview**：该页面为数据分析页面的一部分，用于对于单个数据集进行概览，并且能够引导用户根据各种不同的标准对于患者的集合进行划分，从而进入对比分析等页面进行进一步的分析；
* **Comprehensive Analyze**：除“Express Overview”以外的所有数据分析相关页面，用于对数据进行进一步的分析处理并展示其结果；
* **Customized selection**：对于Patient、Protein与Proteoform等实体进行筛选与选取的页面。用户可以在这个页面当中选取多个数据条目并保存为集合，以用于进一步的分析；
* **Set managing & manipulation**：数据集合的管理界面，用户在此管理自己所保存的各类集合。用户在跟随UI的引导进行分析的过程当中产生的“集合”，如果用户不单独点击“保存”，则不会在这里体现。

由以上叙述可知，数据库主要有“数据集与基因的选取”、“用户自定义选取”与“数据分析”三种主要功能，这3类功能要在以上6类页面当中实现，这6类页面稍作归结，可以表述为“Home Page”、“Customized selection”、“PDPM toolkit”与“Set Managing”四类页面；此外，数据库当中的所有主要的实体，都要有一个概览界面。这些页面相应的设计与需求将在后面的几个页面当中分别展示。