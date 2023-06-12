# The Requirement Document of PDPM portal

PDPM portal is a proteomics data centered, a priori knowledge driven, biology and clinical researcher oriented data portal, which enables integrated analysis of multi-omics data and towards an development ecosystem.

This is the Requirement document for the first version of PDPM portal, which contains two diemensions of omics data, proteomics and phosphoproteomincs, with a build-in data analyzing toolkit, "PDPM toolkit", to enable users make biology insights from clinical and multi-omics data.

## Pages

* `Home` - The homepage of PDPM  portal, which enables the operation on datasets and  provides the original navigation for users to begin their analyzing process.
* `Customized selection` - The pages that enables users to select data randomly or with some filter criterias.
* `Projects` - The page for users to choose projects(or Datasets) and display basic statistics to represents clinical data.
* `Annotations` - The page for users to view relationships between clinical and molecular data, which is based on the data annotation.
* `Proteins` - The page that presents the expression data in serveral way.
* `Login and Data Submission` - The page that allows data providers and database administrator uploading and managing data.

## Overview
整体设计部分，这部分已经涉及到一些技术的实现方案，因此不使用英语表述。以下涉及到技术与实现的部分，也不使用英语表述。
### 整体思路
自从生物学发现了自己的微观基础，生物学家对于某种宏观现象的解释就必须建立在某种微观机制的基础上，尤其在分子生物学诞生以来，各类生物分子进一步拥有了更为准确的名称，从而形成了另一套成体系的“语言”，与先前描述宏观生物学现象的那种语言相独立。因此，“阐明某个生物学现象的分子机理”，不妨认为是一个翻译的过程，或者用符号学术语，“指号过程”，即在不同的“语言”下指认同一个事物，从而在两种语言之间建立联系。

当前的各类生物学教材，已经提供了对于“宏观生命现象”的语言的较为完备的知识体系，而以UniprotKB为代表的各类生物信息学数据库与知识库也已经构建了分子层面的“微观生命现象”的语言系统。当前迫切需要一种能够使得两种体系进行对话的方法。这种“对话”是以归纳的逻辑为基础的，在技术层面上，一般以统计学的方法实现。因此，PDPM portal的基本构成逻辑如下图所示：

<body>
<div style="text-align:center">
<img src="img/logic_structure.png" width="60%">
</div>
</body>

临床的因素与分子的因素在注释数据当中交汇。使用统计学在数据注释结果当中寻找某种结构，这种结构就蕴含着某种“归纳的”生物学知识，即“某种生物学现象背后的分子机理”。PDPM portal当前的任务就在于利用预先整理并注释的数据，引导用户恰当的使用统计学工具，从这些数据当中挖掘这些结构。因此应当对于PDPM portal的操作逻辑进行设计，便于用户从“宏观现象”与“分子机理”两个层面切入，以最为高效、最接近没有编程基础的生物学家操作习惯的方式设计网站的操作逻辑。

### 参照系评述
PDPM portal的主要参照系有：

* cBioPortal - [cBioPortal](https://www.cbioportal.org/)
* ICGC Data portal - [ICGC](https://dcc.icgc.org/)
* GDC Data portal - [GDC](https://portal.gdc.cancer.gov/)

cBioPortal主要面向没有编程经验的生物学家，其操作逻辑为Dataset-centric，用户选择一个或多个Dataset进行浏览、分析，cBioPortal利用一些预先得到的数据注释结果进行展示，以“研究项目->集合选取->比较分析->基因特性”的操作逻辑引导用户逐步对于数据集当中的数据进行分析，并较为便捷的得到其需要的分析结果；但其浏览界面当中各种元素混杂，整体上给人一种不知如何下手的杂乱感，并且其中的“自定义选取”功能并不成熟，对于有数据分析经验的人员而言，使用体验总体上较为蹩脚。

ICGC Data portal与GDC Data portal则主要面向数据分析人员提供数据选取与下载服务，用户根据一定的规则选择一系列数据并保存其ID，利用一些基本的分析工具概览这些数据的基本性质，确定这些数据是否为需要的数据，最终下载数据，在本地进行进一步的分析。这二者主要是为某个Data Commons提供一个数据浏览与下载的门户，其数据分析功能相当薄弱。二者的操作逻辑非常适合有编程与数据分析经验的用户，但没有数据分析经验的用户（PDPM portal主要面向的用户群体）会感到相当难以上手。

### 操作逻辑
PDPM portal将主要以cBioPortal作为参照系，相应的，其操作逻辑也将是“Dataset-Centric”；我们同时需要考虑到从蛋白质入手进行分析的需求。综合考虑以上诸参照系的表现，PDPM portal的整体架构将被设计为一种与ICGC与GDC Data portal相近的结构，而“Dataset-centric”的操作逻辑将在UI的设计当中实现，即通过一些链接、控件引导用户在不同的分析或浏览工具当中切换，从而同时照顾两类用户的使用体验，并且能够更加方便的对于分析功能进行扩展。

因此首先要对于PDPM的各类逻辑与结构进行概览。