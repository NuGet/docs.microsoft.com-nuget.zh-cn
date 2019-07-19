---
title: dotnet CLI NuGet 命令
description: 使用 dotnet 命令行界面的 NuGet 相关命令的简短参考。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327484"
---
# <a name="dotnet-cli-commands"></a>dotnet CLI 命令

`dotnet`命令行接口 (CLI) 在 Windows、Mac OS X 和 Linux 上运行, 它提供了许多必要的命令, 例如安装、还原和发布包。 如果 dotnet 满足你的需求, 则无需使用`nuget.exe`。

有关使用这些命令来使用包的示例, 请参阅[使用 DOTNET CLI 安装和管理包](../consume-packages/install-use-packages-dotnet-cli.md)。 有关使用这些命令创建包的示例, 请参阅[使用 DOTNET CLI 创建和发布包](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)。

有关`dotnet` CLI 的完整命令参考, 请参阅[.net Core 命令行接口 (CLI) 工具](/dotnet/core/tools/?tabs=netcore2x)。

## <a name="package-consumption"></a>包消耗

- [**dotnet 添加包**](/dotnet/core/tools/dotnet-add-package):向项目文件添加包引用, 然后运行`dotnet restore`以安装包。
- [**删除包 dotnet**](/dotnet/core/tools/dotnet-remove-package):从项目文件中删除包引用。
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x):还原项目的依赖项和工具。 从 NuGet 4.0 开始，它运行与 `nuget restore` 相同的代码。
- [**dotnet nuget 局部变量**](/dotnet/core/tools/dotnet-nuget-locals):列出*全局包*、 *http 缓存*和*临时*文件夹的位置, 并清除这些文件夹的内容。
- [**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new):[`nuget.config`](../reference/nuget-config-file.md)创建文件以配置 NuGet 的行为。

## <a name="package-creation"></a>包创建

- [**dotnet 包**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x):将代码打包到 NuGet 包中。
- [**dotnet nuget 推送**](/dotnet/core/tools/dotnet-nuget-push):将包发布到 NuGet 服务器。 适用于 nuget.org、Azure Artifacts 和[第三方 nuget 服务器](../hosting-packages/overview.md)。
- [**dotnet nuget 删除**](/dotnet/core/tools/dotnet-nuget-delete):从 NuGet 服务器删除或取消列出包。 适用于 nuget.org、Azure Artifacts 和[第三方 nuget 服务器](../hosting-packages/overview.md)。
