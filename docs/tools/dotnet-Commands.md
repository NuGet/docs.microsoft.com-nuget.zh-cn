---
title: dotnet CLI NuGet 命令
description: 短 NuGet 相关的命令，使用 dotnet 命令行接口的引用。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496471"
---
# <a name="dotnet-cli-commands"></a>dotnet CLI 命令

`dotnet`命令行接口 (CLI)，在 Windows、 Mac OS X 和 Linux 运行，提供了许多基本命令，例如安装、 还原和发布包。 如果 dotnet 满足你的需求，不需要使用`nuget.exe`。

有关使用这些命令来使用包的示例，请参阅[安装和管理包使用 dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md)。 使用以下命令以创建包的示例，请参阅[创建和发布包使用 dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)。

有关完整的命令参考`dotnet`CLI，请参阅[.NET Core 命令行接口 (CLI) 工具](/dotnet/core/tools/?tabs=netcore2x)。

## <a name="package-consumption"></a>包使用

- [**dotnet 添加包**](/dotnet/core/tools/dotnet-add-package):添加包引用的项目文件，则会运行`dotnet restore`安装该包。
- [**dotnet 中删除程序包**](/dotnet/core/tools/dotnet-remove-package):从项目文件中删除的包引用。
- [**dotnet 还原**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x):还原依赖项和项目的工具。 截至 NuGet 4.0 中，这将运行的相同代码`nuget restore`。
- [**dotnet nuget 局部变量**](/dotnet/core/tools/dotnet-nuget-locals):列出的位置*全局包*， *http 缓存*，并*temp*文件夹和清除这些文件夹的内容。
- [**dotnet 新 nugetconfig**](/dotnet/core/tools/dotnet-new):创建[ `nuget.config` ](../reference/nuget-config-file.md)文件来配置 NuGet 的行为。

## <a name="package-creation"></a>创建包

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x):将代码打包到 NuGet 包。
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push):将包发布到 NuGet 服务器。 适用于 nuget.org 中，Azure 项目，并[第三方 NuGet 服务器](../hosting-packages/overview.md)。
- [**dotnet nuget 删除**](/dotnet/core/tools/dotnet-nuget-delete):删除或取消列出包从 NuGet 服务器。 适用于 nuget.org 中，Azure 项目，并[第三方 NuGet 服务器](../hosting-packages/overview.md)。
