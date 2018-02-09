---
title: "NuGet 包名称争议的解决 | Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "此过程用于解决 NuGet 包发布服务器之间有关品牌、商标和其他冲突情况的争议。"
keywords: "NuGet 包争议, NuGet 争议解决, 争议解决过程"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 589fe4e7d2b05f3d589dcc70e78e7199d7e717c8
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2018
---
# <a name="resolving-disputes-over-nuget-package-names"></a>解决对 NuGet 包名称的争议

本文推荐的解决过程，适用于社区成员解决与其他 NuGet 发布服务器之间的争议。

例如，假设 Northwind Traders 生成 CRM 系统，且他们将客户端驱动程序作为其网站中可下载的 MSI 提供给该系统。 独立开发人员 Nancy 想要将 Northwind 客户端库的使用方法变得更简便，因此将其转换成名为 `NorthwindTraders.Client` 的 NuGet 包。 随后，Northwind 想要为其客户端库生成自己的官方 NuGet 包，因此想要对 Nancy 对该包名称的所有权提出异议。

在此情况中，Nancy 的行为似乎没有恶意，只是通过贡献自己的时间和代码支持 Northwind 的工具和客户。 同时，Northwind 是 Northwind 名称的合法所有者。

通过遵照以下流程，Northwind 和 Nancy 可以共同协作，商讨出合适的解决方案，因为双方都希望为开发人员社区提供服务。 通常不需要 NuGet 团队进行干涉；协作通常是最佳解决方案。 事实上，引起 NuGet 团队注意的每个争议均得到了解决，无需团队做出裁决。

## <a name="process"></a>进程

1. 使用包详细信息页上的“联系所有者”链接，联系与其有争议的包的所有者。 以友好和直接的方式说明问题。
1. 将邮件副本发送到 [support@nuget.org](mailto:support@nuget.org)，以便 NuGet 和 .NET Foundation 了解此争议。
1. 最长需等待 30 天才能解决，之后请再次通知 [support@nuget.org](mailto:support@nuget.org)。 nuget.org 支持团队将参与商讨，与双方共同解决争议。
