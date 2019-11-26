---
title: 弃用 nuget.org 上的包
description: 详细介绍包弃用过程以及客户端如何显示此信息
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096885"
---
# <a name="deprecating-packages"></a>弃用包

如果不再维护某个包，或者希望鼓励该包的使用者移到其他包，可将此包弃用。 

如下所示，包弃用与取消列出包不同  ：
* 取消列出包会阻止它的发现，因为包会在搜索列表中隐藏  。 
* 而弃用包可让包的现有使用者了解其是否已在其项目中安装或使用此包  。 它还让使用者了解弃用原因以及你（包发布者）指定的备用推荐包。 弃用包后，包仍会列出。 

作为包发布者，你可选择同时弃用和取消列出包。

## <a name="deprecation-workflow"></a>弃用工作流
1. 要弃用包，请转到“管理包”，然后选择“弃用”   ：

    ![转到“弃用包”选项](media/deprecation-select-option.png)

2. 选择要弃用的版本。 要弃用所有版本，请选中“选择所有版本”选项  。

    ![选择要弃用的包版本](media/deprecation-select-version.png)

3. 选择弃用原因。 如果不再维护包，请选择“旧版”选项  。 如果特定版本有关键 bug，请选择“存在关键 bug”选项  。 对于其他任何原因，请选择“其他”  。 始终可为所有者指定备用推荐包（及版本）和自定义消息。 

    ![选择备用包推荐和自定义消息的原因](media/deprecation-save.png)

> [!Note]
> 自定义消息仅在 nuget.org 上显示，而不显示在客户端上。 目前，`dotnet.exe` 和 NuGet 包管理器等客户端不会显示自定义消息。

## <a name="client-experience-for-deprecated-packages"></a>有关已弃用包的客户端体验
某个包一旦被弃用，其使用者就会（根据使用的客户端）通过以下方式收到通知。

### <a name="visual-studio"></a>Visual Studio 
*自 Visual Studio 2019 版本16.3 起可用*

Visual Studio 警告称 `Installed` 选项卡上使用了已弃用的包。它将显示有关此包的警告及其弃用信息（内附弃用原因和改用的备用包（若有））。

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
