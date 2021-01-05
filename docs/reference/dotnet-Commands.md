---
title: dotnet CLI NuGet 命令
description: 使用 dotnet 命令行界面的 NuGet 相关命令的简短参考。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 87cb3c8153931a0917338de9f7001406b5e12dfc
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699817"
---
# <a name="dotnet-cli-commands"></a>.NET CLI 命令

`dotnet`命令行界面 (CLI) ，在 Windows、Mac OS X 和 Linux 上运行，它提供了许多必要的命令，例如安装、还原和发布程序包。 如果 dotnet 满足你的需求，则无需使用 `nuget.exe` 。

有关使用这些命令来使用包的示例，请参阅 [使用 DOTNET CLI 安装和管理包](../consume-packages/install-use-packages-dotnet-cli.md)。 有关使用这些命令创建包的示例，请参阅 [使用 DOTNET CLI 创建和发布包](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)。

有关 cli 的完整命令参考 `dotnet` ，请参阅 [.net Core 命令行界面 (cli) 工具](/dotnet/core/tools/?tabs=netcore2x)。

## <a name="package-consumption"></a>包消耗

- [**dotnet 添加包**](/dotnet/core/tools/dotnet-add-package)：向项目文件添加包引用，然后运行 `dotnet restore` 以安装包。
- [**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package)：从项目文件中删除包引用。
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x)：还原项目的依赖项和工具。 从 NuGet 4.0 开始，它运行与 `nuget restore` 相同的代码。
- [**dotnet nuget 局部变量**](/dotnet/core/tools/dotnet-nuget-locals)：列出 *全局包*、 *http 缓存* 和 *临时* 文件夹的位置，并清除这些文件夹的内容。
- [**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new)：创建 [`nuget.config`](../reference/nuget-config-file.md) 文件以配置 NuGet 的行为。

## <a name="package-creation"></a>包创建

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x)：将代码打包到 NuGet 包中。
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push)：将包发布到 nuget 服务器。 适用于 nuget.org、Azure Artifacts 和 [第三方 nuget 服务器](../hosting-packages/overview.md)。
- [**dotnet nuget 删除**](/dotnet/core/tools/dotnet-nuget-delete)：从 nuget 服务器中删除或取消列出包。 适用于 nuget.org、Azure Artifacts 和 [第三方 nuget 服务器](../hosting-packages/overview.md)。
- [**dotnet nuget 验证**](/dotnet/core/tools/dotnet-nuget-verify)：验证已签名的 nuget 包。
