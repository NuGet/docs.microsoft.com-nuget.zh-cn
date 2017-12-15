---
title: "ID 前缀保留引用 |Microsoft 文档"
author: diverdan92
ms.author: diverdan92
manager: unniravindranathan
ms.date: 10/9/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 76c0bb7f-9aaf-4c09-b3fd-f6802f9dd602
description: "包 ID 前缀保留功能说明和作者指南。"
keywords: "NuGet 包 ID、 前缀、 保留"
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.openlocfilehash: e94d1431667ec17347165ac0a3993c0b552e6a60
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="package-id-prefix-reservation"></a>包 ID 前缀保留
[nuget.org](https://www.nuget.org/)和 Visual Studio 2017 15.4 或更高版本的包，只要包与匹配的保留的 ID 提交由所有者具有保留的包 ID 前缀，前缀的命名模式显示可视的指示器。 下引用介绍 ID 前缀保留的需要，以及如何所有者可以将应用 ID 前缀。

## <a name="what-is-package-id-prefix-reservation"></a>包 ID 前缀保留是什么？
包所有者是能够保留并通过保留 ID 前缀来保护其标识。 包使用者会提供其他信息时使用包，它们使用的包不在其标识属性欺骗性。 阅读下文，看 ID 前缀保留详细信息中的工作方式。

## <a name="id-prefix-reservation-details"></a>ID 前缀保留详细信息 
保留包 ID 前缀后，将在发生下列情况[nuget.org](https://www.nuget.org/)库，以及如 Visual Studio 中所示。 此外，一些高级支持由 ID 前缀保留项，如设置为 'public' 前缀将前缀子集委托给多个所有者的方案。

以下部分介绍中的详细信息，以及更多高级的功能的功能。

### <a name="id-prefix-reservation-on-nugetorg"></a>在 nuget.org 上的 ID 前缀保留
当前缀会保留在[nuget.org](https://www.nuget.org/)，将发生以下情况：
1. 前缀保留关联的所有者或所有者的组上[nuget.org](https://www.nuget.org/)。 
2. 每当包提交到[nuget.org](https://www.nuget.org/) id 相匹配的保留的 ID 前缀，包被拒绝，除非它来自所有者保留 ID 前缀。
3. 与匹配的保留的 ID 前缀，并源自保留 ID 前缀所有者的任何包将具有的可视指示器，在 Visual Studio 2017 版本 15.4 或更高版本，和上[nuget.org](https://www.nuget.org/) ，该值指示包正在保留的 ID 前缀。 这适用于新的包提交以及在所有者下的现有包。 **注意：**单个源选择作为包源才会显示在 Visual Studio 中的指示器。 
4. 所有先前存在的包与匹配的保留的 ID 前缀，但都*不*拥有保留的所有者的前缀将保持不变 （它们不会未列出，但它们还将不具有可视的指示器）。 此外，这些包的所有者将仍能够提交到包的新版本。

这些更改基于以下条件，并且有多个附加限制：
* 只有一个所有者的包需要具有可视的指示器，显示 （对于与多个所有者的包） 的保留的前缀。
* 如果没有的包其中一个或多个所有者具有保留的前缀和一个或多个所有者不具有保留的前缀的多个所有者，仅保留前缀与所有者可以删除以保留前缀其他所有者。 而在不具有保留的前缀的所有者不能删除以保留前缀的所有者。 他们仍可以删除还没有保留的前缀其他所有者。
  * 可视的指示器包后，它应*始终*具有可视的指示器 （保留前缀与该至少一个所有者，从而保证始终将保留所有者）

### <a name="advanced-prefix-reservation-scenarios"></a>高级的前缀保留方案
有更高级的几种前缀保留方案下面所述，包括 subprefix 委派，并为公共的标记前缀。 以下是可以进行更高级的前缀保留。 

* 在前缀保留过程所有者可以请求的前缀子集委派 （或前缀） 到其他所有者。 例如，如果[Microsoft](https://www.nuget.org/profiles/microsoft)拥有 Microsoft。\*，但[aspnet](https://www.nuget.org/profiles/aspnet)想要保留 Microsoft.AspNet。\*'，'[Microsoft](https://www.nuget.org/profiles/microsoft)可以选择委派 Microsoft.AspNet。\*到[aspnet](https://www.nuget.org/profiles/aspnet)帐户。
*  在前缀保留所有者可以选择公开一个前缀。 这将仍为它们可视的指示器显示包源自保留前缀，但它将**不**阻止任何所有者提交的将来的软件包时根据的前缀。 这可用于具有很多参与者的开放源代码项目-顶部或核心参与者都可以具有前缀保留，但它仍可以打开到所有 contributors （参与者）。 

### <a name="prefix-reservation-visual-indicator"></a>前缀保留可视的指示器
如果包来自保留前缀，你将看到下面直观的指示器上, [nuget.org](https://www.nuget.org/)库和 Visual Studio 2017 15.4 或更高版本中：

**nuget.org 库**
![nuget.org 库](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>ID 前缀保留应用程序进程
若要应用前缀保留项，请按照以下步骤。 
1. 查看验收[前缀 ID 保留条件](#id-prefix-reservation-criteria)。
2. 确定你想要保留，除了任何命名的空间[高级前缀保留方案](#advanced-prefix-reservation-scenarios)可能需要。
3. 发送到邮件[ account@nuget.org ](mailto:account@nuget.org)与所有者显示名称上[nuget.org](https://www.nuget.org/)，以及任何您请求的保留前缀。 如果你的多个所有者分配前缀子集，请确保涉及所有所有者显示名称和前缀子集。

提交应用程序后，你将接受或拒绝 （与导致拒绝的条件） 的通知。 我们可能需要询问其他标识的一些问题，以确认所有者身份。 

### <a name="id-prefix-reservation-criteria"></a>ID 前缀保留条件
查看有关 ID 前缀保留任何应用程序时[nuget.org](https://www.nuget.org/)团队将 evalaute 针对对应用程序下面条件。 并非所有条件都需要满足的前缀以保留，但如果不满足 （的给定说明） 的条件的大量证据，应用程序可能会被拒绝：
1. 没有包 ID 前缀正确并清楚地标识包所有者？
2. 按下的包 ID 前缀所有者大量的已提交的包？
3. 是很常见应不属于任何单个所有者或组织的包 ID 前缀？
4. 将*不*保留的包 ID 前缀导致多义性和社区的困惑？
5. 是匹配的包 ID 前缀清晰且一致 （尤其是程序包作者） 的包的标识属性？

## <a name="3rd-party-feed-provider-scenarios"></a>第三方源提供程序方案
如果第三方源提供程序有兴趣实现其自己的服务提供前缀保留项，你可以执行以便 NuGet V3 中的搜索服务通过修改源提供程序。 源的搜索服务中添加是添加*验证*属性，并提供 V3 源下面的示例。 NuGet 客户端将不支持在 V2 中源添加的属性。

有关详细信息，请参阅[有关 API 的搜索服务的文档](../api/search-query-service-resource.md)。
