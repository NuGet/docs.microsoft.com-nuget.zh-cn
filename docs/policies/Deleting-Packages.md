---
title: 删除 nuget.org 的 NuGet 包
description: 用于取消列出 nuget.org 的包的策略；除非包违反其他策略，否则不支持永久删除。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: bea4f1589f184d38da27e5d82c3ce17a183fbdd1
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="deleting-packages"></a>删除包

nuget.org 不支持永久删除包。 此操作会破坏依赖该包可用性的每个项目，尤其是涉及包还原的生成工作流。

nuget.org 支持取消列出包，此操作可在网站上的包管理页中执行。 取消列出的包不会显示在 nuget.org、Visual Studio UI 或搜索结果中。 但是，仍可使用支持包还原的确切版本号下载和安装取消列出的包。 此外，仍可能在以下特定方案中发现取消列出的包：

- 如果与版本或依赖项约束匹配的最新可用包是取消列出的包，使用浮动版本（如 `1.0.0-*`）进行包还原。
- 通过目录复制包（因为该目录也包含取消列出的包）。

## <a name="exceptions"></a>异常

在侵犯版权和可能包含有害内容等例外情况下，NuGet 团队可以手动删除包。 通过 [NuGet 库](http://www.nuget.org)提交支持请求以启动该进程。

## <a name="prohibited-use"></a>禁止使用

公共 NuGet 库中不允许存在满足以下任一条件的包，且将在不经过讨论的情况下立即删除这些包。 但是，包的所有者会获得删除包的通知。

- 包含恶意软件、广告程序或任何类型的间谍软件。
- 企图危害开发人员的工作站或组织。
- 侵犯版权或违反许可证。
- 包含非法内容。
- 用于制止包标识符，包括包含零工作效率内容的包。 包必须包含代码，或所有者必须将标识符让与实际具有要运送的产品的某个人员。
- 尝试让库执行设计明确意图以外的操作。

如果发现违反以上任一项的包，请单击包详细信息页上的“报告滥用行为”链接并提交报告。

请注意，NuGet 团队和 .NET Foundation 保留随时更改这些条件的权利。
