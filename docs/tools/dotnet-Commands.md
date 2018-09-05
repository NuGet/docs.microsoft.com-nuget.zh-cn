---
title: dotnet NuGet 命令
description: 短 NuGet 相关的命令，使用 dotnet 命令行接口的引用。
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: 88e058be674ecddc500665bfa3517f19acde0cd7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546311"
---
# <a name="dotnet-commands"></a>dotnet 命令

`dotnet`命令行接口，在 Windows、 Mac OS X 和 Linux 运行，提供了许多重要的 nuget.exe 命令，如下所示。 如果 dotnet 满足你的需求，不需要使用`nuget.exe`。

有关完整信息`dotnet`，请参阅[.NET Core 命令行接口 (CLI) 工具](/dotnet/core/tools/?tabs=netcore2x)。

## <a name="package-consumption"></a>包使用

- [**dotnet 添加包**](/dotnet/core/tools/dotnet-add-package)： 添加包引用的项目文件，则会运行`dotnet restore`安装该包。
- [**dotnet 中删除程序包**](/dotnet/core/tools/dotnet-remove-package)： 从项目文件中删除的包引用。
- [**dotnet 还原**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x)： 恢复依赖项和项目的工具。 截至 NuGet 4.0 中，这将运行的相同代码`nuget restore`。
- [**dotnet nuget 局部变量**](/dotnet/core/tools/dotnet-nuget-locals)： 列出的位置*全局包*， *http 缓存*，以及*temp*文件夹和清除的内容这些文件夹。

## <a name="package-creation"></a>创建包

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x)： 将代码打包到 NuGet 包。 截至 NuGet 4.0 中，这将运行的相同代码`nuget pack`。
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push)： 将包推送到服务器，并将它适用于 nuget.org、 Visual Studio Team Services 和第三方 NuGet 服务器发布。
- [**dotnet nuget 删除**](/dotnet/core/tools/dotnet-nuget-delete)： 删除或取消列出包从一台主机，适用于 nuget.org、 Visual Studio Team Services 和第三方 NuGet 服务器。
