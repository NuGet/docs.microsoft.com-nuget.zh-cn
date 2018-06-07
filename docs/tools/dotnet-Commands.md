---
title: dotnet NuGet 命令
description: 使用 dotnet 命令行界面的 NuGet 相关命令短引用。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: dd30c5d5e29ff7ef7c6622a9b93c32b908198d52
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817002"
---
# <a name="dotnet-commands"></a>dotnet 命令

`dotnet`命令行界面，在 Windows、 Mac OS X 和 Linux 运行，提供了大量基本 nuget.exe 命令，如下所示。 如果 dotnet 满足你的需求，不需要使用`nuget.exe`。

有关完整信息`dotnet`，请参阅[.NET 核心命令行界面 (CLI) 工具](/dotnet/core/tools/?tabs=netcore2x)。

## <a name="package-consumption"></a>包消耗

- [**dotnet 添加包**](/dotnet/core/tools/dotnet-add-package): 包将引用添加到项目文件中，然后运行`dotnet restore`安装该包。
- [**dotnet 删除包**](/dotnet/core/tools/dotnet-remove-package)： 从项目文件中删除的包引用。
- [**dotnet 还原**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x)： 还原的依赖关系和项目的工具。 截至 NuGet 4.0 中，这将运行的相同代码`nuget restore`。
- [**dotnet nuget 局部变量**](/dotnet/core/tools/dotnet-nuget-locals)： 列出的位置*全局包*， *http 缓存*，和*temp*文件夹和清除的内容这些文件夹。

## <a name="package-creation"></a>创建包

- [**dotnet 包**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x)： 包代码放在一个 NuGet 程序包。 截至 NuGet 4.0 中，这将运行的相同代码`nuget pack`。
- [**dotnet nuget 推送**](/dotnet/core/tools/dotnet-nuget-push)： 将包推送到服务器并发布它适用于 nuget.org、 Visual Studio Team Services 和第三方 NuGet 服务器。
- [**dotnet nuget 删除**](/dotnet/core/tools/dotnet-nuget-delete)： 删除或 unlists 从一台主机，适用于 nuget.org、 Visual Studio Team Services 和第三方 NuGet 服务器包。
