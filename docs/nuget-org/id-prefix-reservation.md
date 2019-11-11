---
title: ID 前缀预留
description: 包 ID 前缀预留功能说明和作者指南。
author: karann-msft
ms.author: karann
ms.date: 09/07/2019
ms.topic: reference
ms.reviewer: karann
ms.openlocfilehash: da464cc44d8c874e13c0cdfab871f31e643b577f
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610494"
---
# <a name="package-id-prefix-reservation"></a>包 ID 前缀预留

包所有者可以通过保留 ID 前缀来保留和保护其标识。 当使用者使用的包在其标识属性中不具有欺骗性时，他们将收到附加信息。 

[nuget.org](https://www.nuget.org/) 和 Visual Studio 2017 15.4 或更高版本只要包与保留的 ID 前缀命名模式匹配，就会显示所有者提交的具有保留的包 ID 前缀的包的视觉提示。 以下参考资料说明了 ID 前缀预留需要的内容，以及所有者如何申请 ID 前缀。

## <a name="id-prefix-reservation-details"></a>ID 前缀预留详细信息

保留包 ID 前缀时，在 [nuget.org](https://www.nuget.org/) 库和 Visual Studio 中会发生一些情况。 此外，ID 前缀预留还支持一些高级方案，比如将前缀设置为“public”，将前缀子集委托给多个所有者。

### <a name="id-prefix-reservation-on-nugetorg"></a>nuget.org 上的 ID 前缀预留

在 [nuget.org](https://www.nuget.org/) 上保留前缀时，将发生以下情况：

1. 前缀预留与 [nuget.org](https://www.nuget.org/) 上的所有者或所有者组相关。

1. 每当包提交到 ID 与保留的 ID 前缀匹配的 [nuget.org](https://www.nuget.org/) 时，都会拒绝该包，除非它来自已保留 ID 前缀的所有者。

1. 任何与保留 ID 前缀匹配并来自已保留 ID 前缀的所有者的包将在 Visual Studio 2017 15.4 或更高版本中和在 [nuget.org](https://www.nuget.org/) 上具有视觉提示，指示该包位于保留 ID 前缀下。 提交的新包和所有者名下的现有包都是如此。 **注意：** 仅当选择单个订阅源作为包来源时，Visual Studio 中才会出现标志。

1. 所有先前存在的包如果与保留 ID 前缀匹配，但不属于保留前缀所有者，则将保持不变（它们依然会被列出，但没有视觉提示）  。 此外，这些包的所有者仍然可以向包提交新版本。

这些更改基于以下条件，并附加了一些限制：

- 为了显示视觉提示，只有一个包所有者需要保留前缀（适用于具有多个所有者的包）。

- 如果一个包有多个所有者，其中一个或多个所有者具有保留前缀，而一个或多个所有者没有保留前缀，那么只有具有保留前缀的所有者才能移除具有保留前缀的其他所有者。 没有保留前缀的所有者无法移除保留了前缀的所有者。 他们仍然可以移除其他没有保留前缀的所有者。

- 一旦包具有视觉提示，它应该始终具有视觉提示（确保至少有一个具有保留前缀的所有者始终保持所有者身份） 

### <a name="advanced-prefix-reservation-scenarios"></a>高级前缀预留方案

下面描述了几种更高级的前缀预留方案，包括子前缀委托和将前缀标记为公用。 以下是可以进行的更高级的前缀预留。 

- 在前缀预留期间，所有者可以请求将前缀子集（或前缀）委托给其他所有者。 例如，如果“[Microsoft](https://www.nuget.org/profiles/microsoft)”具有“Microsoft.\*”，但“[aspnet](https://www.nuget.org/profiles/aspnet)”希望保留“Microsoft.AspNet.\*”，则“[Microsoft](https://www.nuget.org/profiles/microsoft)”可以选择将“Microsoft.AspNet.\*”委托给 [aspnet](https://www.nuget.org/profiles/aspnet) 帐户。

- 在前缀预留期间，所有者可以选择设置公用前缀。 这仍将为他们提供视觉提示，显示包源自保留的前缀，但它以后不会对任何所有者的前缀阻止提交包  。 这对于有许多贡献者的开源项目很有用，顶级或核心贡献者可以保留前缀，但它仍然可以向所有贡献者开放。 

### <a name="prefix-reservation-visual-indicator"></a>前缀预留视觉提示

当包来自保留前缀时，在 [nuget.org](https://www.nuget.org/) 库和 Visual Studio 2017 15.4 或更高版本中将看到以下视觉提示：

**nuget.org 库**
![nuget.org Gallery](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>ID 前缀预留申请过程

1. 查看[前缀 ID 预留的验收条件](#id-prefix-reservation-criteria)。

2. 确定你想预留的前缀，以及可能需要的任何[高级前缀预留方案](#advanced-prefix-reservation-scenarios)。

3. 使用 [nuget.org](https://www.nuget.org/) 上的所有者显示名称以及你请求的任何保留前缀向 [account@nuget.org](mailto:account@nuget.org) 发送邮件。 如果要将前缀子集委托给多个所有者，请确保提及所有的所有者显示名称和前缀子集。

提交申请后，你会收到接受或拒绝通知（以及拒绝标准）。 我们可能需要提出其他标识问题以确认所有者身份。

### <a name="id-prefix-reservation-criteria"></a>ID 前缀预留标准

在审核任何 ID 前缀预留申请时，[nuget.org](https://www.nuget.org/) 团队将根据以下标准评估申请。 并非所有标准均需满足才可保留前缀，但如没有确实证据证明满足标准（并给出解释），申请可能会被拒绝：

1. 包 ID 前缀是否会正确且清楚地标识包所有者？

1. 是否让包所有者[启用了其 NuGet.org 帐户的 2FA](individual-accounts.md#enable-two-factor-authentication-2fa)？

1. 所有者已提交的大量包是否已在包 ID 前缀下？

1. 包 ID 前缀是否为不应属于任何个人所有者或组织的常见内容？

1. 不保留包 ID 前缀是否会给社区带来歧义和混淆  ？

1. 与包 ID 前缀匹配的包的标识属性是否清晰且一致（尤其是包作者）？

1. 包是否具有许可证（使用[许可证](../reference/nuspec.md#license)元数据元素而不是弃用的 licenseUrl？

1. 如果包具有图标（使用 iconUrl 元数据元素），则这些包是否也使用该[图标](../reference/nuspec.md#icon) 元数据元素（不需要删除 iconUrl）？

## <a name="third-party-feed-provider-scenarios"></a>第三方源提供程序方案

如果第三方源提供程序有兴趣实现自己的服务以提供前缀预留，则可以通过修改 NuGet V3 源提供程序中的搜索服务来实现。 源搜索服务中的更改是添加 `verified` 属性。 NuGet 客户端不支持 V2 源中添加的属性。

有关详细信息，请参阅[有关 API 搜索服务的文档](../api/search-query-service-resource.md)。

## <a name="package-id-prefix-reservation-dispute-policy"></a>包 ID 前缀预留争议策略
如果你认为 [NuGet.org](https://www.nuget.org) 上的所有者被分配了违反上述标准或侵犯任何商标或版权的包 ID 前缀预留，请通过电子邮件发送相关的 ID 前缀、ID 前缀的所有者以及质疑分配的前缀预留的原因至 [support@nuget.org](mailto:support@nuget.org)。

