---
title: ID 前缀保留引用
description: 包 ID 前缀保留功能说明和作者指南。
author: diverdan92
ms.author: diverdan92
ms.date: 10/09/2017
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: e8b902c89427333afb7a27ee9de0eeb99a92f391
ms.sourcegitcommit: 571644118e3c5a2fd818891d305b4b8de8ef21de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2019
ms.locfileid: "57225870"
---
# <a name="package-id-prefix-reservation"></a>包 ID 前缀保留

包所有者可保留，并通过保留 ID 前缀来保护其标识。 包使用者都是提供的其他信息时使用包，它们使用的包不是欺骗其标识的属性中。 

[nuget.org](https://www.nuget.org/)和 Visual Studio 2017 版本 15.4 或更高版本的包所有者具有保留的包 ID 前缀，前提是保留的 ID 相匹配的包提交前缀的命名模式显示可视的指示器。 参考以下说明 ID 前缀保留的需要，以及如何将所有者可以应用 ID 前缀。

## <a name="id-prefix-reservation-details"></a>ID 前缀保留详细信息

保留包 ID 前缀后上, 会发生以下情况[nuget.org](https://www.nuget.org/)库，如 Visual Studio 中所示。 此外，一些高级的方案支持的 ID 前缀保留项，例如，设置为 public，将前缀子集委派给多个所有者的前缀。

### <a name="id-prefix-reservation-on-nugetorg"></a>在 nuget.org 上的 ID 前缀保留

当上保留前缀[nuget.org](https://www.nuget.org/)，将发生以下情况：

1. 前缀保留相关联的所有者或组的所有者与上[nuget.org](https://www.nuget.org/)。

1. 每当包提交给[nuget.org](https://www.nuget.org/) id 相匹配的保留的 ID 前缀，包被拒绝，除非它来自保留 ID 前缀的所有者。

1. 匹配保留的 ID 前缀和源自所有者的 ID 前缀保留的任何包将在 Visual Studio 2017 版本 15.4 或更高版本，以及具有可视的指示器[nuget.org](https://www.nuget.org/) ，该值指示包正在保留的 ID 前缀。 这适用于新的包提交以及在所有者下的现有包。 **注意：** 仅当单个源选择作为数据包来源，将显示 Visual Studio 中的指示符。

1. 所有先前存在的包相匹配的保留的 ID 前缀，但都*不*的保留所有者所拥有的前缀将保持不变 （它们将不会取消列出，但它们还将不具有可视的指示器）。 此外，这些包的所有者将仍能够提交到包的新版本。

这些更改基于以下条件，并且有多个附加限制：

- 只有一个所有者的包需要具有可视的指示器显示 （适用于具有多个所有者的包） 的保留的前缀。

- 如果有多个包，一个或多个所有者具有保留的前缀，而一个或多个所有者不具有保留的前缀的所有者，仅保留的前缀与所有者可以删除其他所有者使用保留的前缀。 所有者不具有保留的前缀不能删除以保留前缀的所有者。 他们仍可以删除其他所有者也不具有保留的前缀。

- 后一个包具有可视的指示器，它应*始终*具有可视的指示器 （保证与保留的前缀，至少一个所有者始终将保持所有者）

### <a name="advanced-prefix-reservation-scenarios"></a>高级的前缀保留方案

有更高级的多个前缀保留方案如下所述包括 subprefix 委派和为公共的标记前缀。 以下是可以进行更高级的前缀保留项。 

- 在前缀保留命令可以委派前缀子集 （或前缀） 到其他所有者请求所有者。 例如，如果 '[Microsoft](https://www.nuget.org/profiles/microsoft)拥有 Microsoft。\*，但[aspnet](https://www.nuget.org/profiles/aspnet)想要保留 Microsoft.AspNet。\*'，'[Microsoft](https://www.nuget.org/profiles/microsoft)可以选择委派 Microsoft.AspNet。\*到[aspnet](https://www.nuget.org/profiles/aspnet)帐户。

- 在前缀保留所有者可以选择公开一个前缀。 这将仍为其提供包源自保留的前缀，但它将显示可视的指示器**不**阻止未来的程序包提交前缀上的任何所有者。 这是可用于对开放源代码项目具有很多参与者-顶部或核心参与者可以具有前缀保留，但它仍可能会受到所有 contributors （参与者）。 

### <a name="prefix-reservation-visual-indicator"></a>前缀保留可视的指示器

当包从保留的前缀，您可以看到如下上的可视指示符[nuget.org](https://www.nuget.org/)库和 Visual Studio 2017 版本 15.4 或更高版本中：

**nuget.org 库**
![nuget.org 库](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>ID 前缀保留应用程序进程

1. 查看验收[为前缀 ID 预订条件](#id-prefix-reservation-criteria)。

2. 确定你想要保留，以及任何的前缀[高级前缀保留方案](#advanced-prefix-reservation-scenarios)，你可能需要。

3. 发送到邮件[ account@nuget.org ](mailto:account@nuget.org)与所有者上显示名称[nuget.org](https://www.nuget.org/)，以及正在请求任何保留前缀。 如果您前缀子集委派到多个所有者，请确保提及所有所有者显示名称和前缀子集。

提交应用程序后，会接受或拒绝 （具有导致拒绝的条件） 的通知你。 我们可能需要询问其他标识问题，以确认所有者身份。

### <a name="id-prefix-reservation-criteria"></a>ID 前缀保留标准

评审 ID 前缀保留任何应用程序时[nuget.org](https://www.nuget.org/)团队会评估将应用程序与以下条件。 不是所有条件都需要满足的前缀保留，但如果不存在大量证据的条件得到满足 （以及给定的说明），可能会拒绝应用程序：

1. 没有包 ID 前缀正确并清楚地标识包所有者？

1. 大量的已提交的包的包 ID 前缀下的所有者？

1. 包 ID 前缀是很常见，不应属于的任何单个所有者或组织？

1. 将*不*保留包 ID 前缀导致二义性和社区的困惑吗？

1. 是与匹配的包 ID 前缀清晰、 一致 （尤其是包的作者） 的程序包的标识属性？

1. 执行包具有的许可证 (使用[许可证](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license)元数据元素，并不将被弃用的 licenseUrl)？

## <a name="third-party-feed-provider-scenarios"></a>第三方源提供程序方案

如果第三方源提供程序是有意实施其自己的服务来提供前缀保留项，可以执行以便 NuGet V3 中的搜索服务通过修改源提供程序。 源的搜索服务中的功能是将添加*验证*属性，并提供 V3 源下面的示例。 NuGet 客户端将不支持在源 V2 中添加的属性。

有关详细信息，请参阅[有关 API 的搜索服务的文档](../api/search-query-service-resource.md)。

## <a name="package-id-prefix-reservation-dispute-policy"></a>包 ID 前缀保留争议策略
如果你在认为所有者[NuGet.org](https://www.nuget.org)分配就不符合上述列出的条件，或侵犯任何商标或版权请电子邮件的包 ID 前缀保留[ support@nuget.org ](mailto:support@nuget.org)与有问题的 ID 前缀，所有者 ID 前缀，以及已分配的前缀保留争议的原因。

