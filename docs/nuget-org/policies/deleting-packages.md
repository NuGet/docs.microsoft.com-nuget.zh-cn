---
title: 删除 nuget.org 的 NuGet 包
description: 用于取消列出 nuget.org 的包的策略；除非包违反其他策略，否则不支持永久删除。
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 3abe809d76e75801c2f936aba129d27ba7b64913
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "80581269"
---
# <a name="deleting-packages"></a>删除包

nuget.org 不支持永久删除包。 此操作会破坏依赖该包可用性的每个项目，尤其是涉及包还原的生成工作流。

nuget.org 支持[取消列出包](#unlisting-a-package)，此操作可在网站上的包管理页中执行。 取消列出的包不会显示在 nuget.org、Visual Studio UI 或搜索结果中。 但是，仍可使用支持包还原的确切版本号下载和安装取消列出的包。 此外，仍可能在以下特定方案中发现取消列出的包：

- 如果与版本或依赖项约束匹配的最新可用包是取消列出的包，使用浮动版本（如 `1.0.0-*`）进行包还原。
- 通过目录复制包（因为该目录也包含取消列出的包）。

## <a name="exceptions"></a>异常

在侵犯版权和可能包含有害内容等例外情况下，NuGet 团队可以手动删除包。 可使用 NuGet.org 包详细信息页上的“报告滥用情况”按钮报告相关包。 如果你是包所有者，请登录 NuGet.org 帐户，使用 NuGet.org 包详细信息页上的“联系支持人员”按钮联系 NuGet 支持人员。

## <a name="prohibited-use"></a>禁止使用

公共 NuGet 库中不允许存在满足以下任一条件的包，且将在不经过讨论的情况下立即删除这些包。 但是，包的所有者会获得删除包的通知。

- 包含恶意软件、广告程序或任何类型的间谍软件。
- 企图危害开发人员的工作站或组织。
- 侵犯版权或违反许可证。
- 包含非法内容。
- 用于制止包标识符，包括包含零工作效率内容的包。 包必须包含代码，或所有者必须将标识符让与实际具有要运送的产品的某个人员。
- 尝试让库执行设计明确意图以外的操作。

如果发现违反以上任一项的包，请单击包详细信息页上的“报告滥用行为”链接并提交报告  。

请注意，NuGet 团队和 .NET Foundation 保留随时更改这些条件的权利。

## <a name="unlisting-a-package"></a>取消列出包
取消列出包版本，会在搜索和 nuget.org 包详细信息页中隐藏该包。 这样做，允许包的现有用户继续使用它，而减少新的采用，因为包在搜索中不可见。

取消列出包的步骤：

1. 选择 `Your account name`（右上角），然后选择 `Manage packages` > `Published packages`
1. 选择“管理包”图标
1. 展开“列表”部分，然后选择包版本
1. 取消选中“在搜索结果中列出”，然后选择“保存”

该包版本现在已取消列出。 若要进行验证，请从你的帐户注销，并导航到包页面（不包含版本部分），例如： https://www.nuget.org/packages/YOUR-PACKAGE-NAME/ 。 你将看到该程序包的所有版本都未列出  。 但是，包所有者登录时，可以看到所有版本及其列出状态。

还可以弃用包版本（如果无法删除包版本）。 有关弃用包版本的详细信息，请参阅[弃用包](../deprecate-packages.md)。
