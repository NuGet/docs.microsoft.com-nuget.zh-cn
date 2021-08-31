---
title: 弃用 nuget.org 上的包
description: 详细介绍包弃用过程以及客户端如何显示此信息
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 4a6dbd645cb72b0085fd0347def58ade134fc5ee
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726959"
---
# <a name="deprecating-packages"></a>弃用包

如果不再维护某个包，或者希望鼓励该包的使用者移到其他包，可将此包弃用。 

如下所示，包弃用与取消列出包不同：
* 取消列出包会阻止它的发现，因为包会在搜索列表中隐藏。 
* 而弃用包可让包的现有使用者了解其是否已在其项目中安装或使用此包。 它还让使用者了解弃用原因以及你（包发布者）指定的备用推荐包。 弃用包后，包仍会列出。 

作为包发布者，你可选择同时弃用和取消列出包。

## <a name="deprecation-workflow"></a>弃用工作流
1. 要弃用包，请转到“管理包”，然后选择“弃用”：

    ![转到“弃用包”选项](media/deprecation-select-option.png)

2. 选择要弃用的版本。 要弃用所有版本，请选中“选择所有版本”选项。

    ![选择要弃用的包版本](media/deprecation-select-version.png)

3. 选择弃用原因。 如果不再维护包，请选择“旧版”选项。 如果特定版本有关键 bug，请选择“存在关键 bug”选项。 对于其他任何原因，请选择“其他”。 始终可为所有者指定备用推荐包（及版本）和自定义消息。 

    ![选择备用包推荐和自定义消息的原因](media/deprecation-save.png)

> [!Note]
> 自定义消息仅在 nuget.org 上显示，而不显示在客户端上。 目前，`dotnet.exe` 和 NuGet 包管理器等客户端不会显示自定义消息。

## <a name="client-experience-for-deprecated-packages"></a>有关已弃用包的客户端体验
某个包一旦被弃用，其使用者就会（根据使用的客户端）通过以下方式收到通知。

### <a name="visual-studio"></a>Visual Studio 
*自 Visual Studio 2019 版本16.3 起可用*

Visual Studio 警告称 `Installed` 选项卡上使用了已弃用的包。它将显示包的警告及其弃用信息，包括弃用的原因和要改用的备用包（若有）。

   ![包管理器的 Visual Studio installed 选项卡上的已弃用的包](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*自 .NET SDK 3.0 起可用*

如果使用 dotnet.exe，则可在解决方案或项目文件夹上运行 `dotnet list package --deprecated` 命令，以获取列表了解已弃用的包及相关弃用信息：

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```

## <a name="transfer-popularity-to-a-newer-package"></a>将热门度转移到新包

已弃用旧包的包作者可选择将旧包的“热门度”转移到新包，以提高新包的搜索排名。 这有助于客户发现较新的包，而不是已弃用的包。

例如，假设我有两个包：

* 已弃用的旧包 `Contoso.Legacy`，下载量 300 万次
* 最新包 `Contoso.Latest`，下载量 5 次

NuGet.org 更偏向下载量/热门度更高的搜索结果。 就搜索查询“Contoso”而言，在搜索结果中，已弃用的包 `Contoso.Legacy` 可能会排在我的最新包 `Contoso.Latest` 之上。

若要解决此问题，可申请将已弃用的旧包的热门度转移到最新包。 这将使 `Contoso.Latest` 在搜索结果中排名较高，而 `Contoso.Legacy` 排名较低。 只有包的内部热门度分数会受到影响，每个包的实际下载计数不会受到影响。

> [!Note]
> 热门度转移会让使用者更难找到旧包。

请参阅下表，具体了解热门度转移可能会如何影响查询“Contoso”的搜索排名：

| 搜索排名    | 热门度转移之前        | 热门度转移之后         |
|----------------   |--------------------------------   |--------------------------------   |
| 1                 | Contoso.Legacy，300 万次下载    | Contoso.Latest，5 次下载     |
| 2                 | Contoso.Scanner，200 万次下载     | Contoso.Scanner，200 万次下载     |
| 3                 | Contoso.Core，150 万次下载     | Contoso.Core，150 万次下载     |
| 4                 | Contoso.UI，100 万次下载          | Contoso.UI，100 万次下载          |
| ...               | ...                               | ...                               |
| 20                | Contoso.Latest，5 次下载     | Contoso.Legacy，300 万次下载    |

### <a name="popularity-transfer-application-process"></a>热门度转移申请流程

1. 查看[热门度转移要求](#popularity-transfer-requirements)。
2. 向 [account@nuget.org](mailto:account@nuget.org) 发送电子邮件，告知应转移其热门度的已弃用包，以及应接收热门度转移的稳定包列表。

提交申请后，你将收到申请是得到接受还是被拒绝（以及导致拒绝的标准）的通知。 我们可能需要提出其他标识问题以确认所有者身份。

#### <a name="popularity-transfer-requirements"></a>热门度转移要求

* 旧包和新包必须共有全部的所有者。
* 新包必须在命名和功能上与旧包明确相关（即新包是旧包的演化或下一代）。
* 旧包的所有版本必须弃用，并指向接收转移的新包。
* 热门度转移不得给 NuGet 用户造成困惑，也不能恶化 NuGet 搜索体验。
* 新包必须具有稳定的版本。
* 旧包不能接收来自另一个已弃用包的热门度转移。

### <a name="advanced-popularity-transfer-scenarios"></a>高级热门度转移场景

#### <a name="package-consolidations"></a>包合并

可转移多个已弃用包的热门度，以支持单个新包。 例如，假设我有三个包：

* 第一个已弃用的旧包 `Contoso.Legacy1`
* 第二个已弃用的旧包 `Contoso.Legacy2`
* 新的合并包 `Contoso.Latest`

在弃用 `Contoso.Legacy1` 和 `Contoso.Legacy2` 后，可申请将它们的热门度转移到 `Contoso.Latest`。

#### <a name="package-splits"></a>包拆分

已弃用的包的热门度可转移到最多 5 个新软件包，并在它们之间进行拆分。 如果已在多个新包之间拆分了已弃用的包的功能，这会很有用。 例如，假设我有三个包：

* 已弃用的旧包 `Contoso.Legacy`
* 第一个新包 `Contoso.Web`
* 第二个新包 `Contoso.Cloud`

`Contoso.Legacy` 包含 Web 和云功能，但我决定将这些功能分成不同的包以供下一代使用。 在弃用 `Contoso.Legacy` 后，可申请将其热门度转移到 `Contoso.Web` 和 `Contoso.Cloud`。

> [!Warning]
> 转移的热门度将在所有新包之间平均拆分。 因此，建议将已弃用的包的热门度转移到尽可能少的包。

#### <a name="popularity-transfer-chains"></a>热门度转移链

如果一个已弃用的包已从另一个已弃用的包获得了热门度，它就不能转移它的热门度。 例如，假设我有三个包：

* 已弃用的旧包 `Contoso.First`
* 已弃用的旧包 `Contoso.Second`
* 新包 `Contoso.Latest`

如果将 `Contoso.First` 其热门度转移到 `Contoso.Second,`，则 `Contoso.Second` 无法将其热门度转移到 `Contoso.Latest`。 建议根据[包合并](#package-consolidations)场景，将 `Contoso.First` 和 `Contoso.Second` 的热门度转移到 `Contoso.Latest`。
