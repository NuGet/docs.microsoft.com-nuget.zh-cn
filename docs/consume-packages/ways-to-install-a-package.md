---
title: "安装 NuGet 包的方式 | Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "介绍将 NuGet 包安装到项目中的过程，包括磁盘上和适用的项目文件会发生的情况。"
keywords: "安装 NuGet, NuGet 包使用, 安装 NuGet 包, NuGet 包引用"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3bae03e148a366388c10d08e83c89dac6ff56d06
ms.sourcegitcommit: 33436d122873249dbb20616556cd8c6783f38909
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>安装 NuGet 包的不同方式

使用以下任一方法下载和安装 NuGet 包（如果尚未安装，请参阅[安装 NuGet 客户端工具](../install-nuget-client-tools.md)）：

| 方法 | 描述 |
| --- | --- |
| dotnet.exe CLI<br/>`dotnet install <package_name>` | （所有平台）下载用 \<package_name\> 识别的包，将其内容展开到当前目录下的文件夹中，然后添加对项目文件的引用。 同时还要下载和安装依赖项。<ul><li>[安装并使用包 (dotnet CLI)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[dotnet 命令](../tools/dotnet-commands.md)</li></ul> |
| 包管理器 UI (Visual Studio) | （Windows 和 Mac）提供 UI，你可以通过此 UI 浏览、选择包，并将包及其依赖项安装到项目中。 将对已安装的程序包引用添加到项目文件。<ul><li>[安装并使用包 (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[程序包管理器 UI 引用 (Windows)](../tools/package-manager-ui.md)</li><li>[在项目中包括 NuGet 包 (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| 程序包管理器控制台 (Visual Studio)<br/>`Install-Package <package_name>` | （仅限 Windows）下载并将用 \<package_name\> 识别的包安装到解决方案的指定项目中，然后添加对项目文件的引用。 同时还要下载和安装依赖项。<ul><li>[安装并使用包 (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[程序包管理器控制台指南](../tools/package-manager-console.md)</li></ul> |
| nuget.exe CLI<br/>`nuget install <package_name>` | （所有平台）下载用 \<package_name\> 识别的包，将其内容展开到当前目录下的文件夹中；还可以下载 `packages.config` 文件中列出的所有包。 同时还要下载和安装依赖项，但对项目文件未进行任何更改。<ul><li>[安装命令](../tools/cli-ref-install.md)</li></ul> |

## <a name="general-install-process"></a>常规安装过程

一般情况下，NuGet 会执行以下操作，然后要求安装一个包：

1. 获取包：
    - 检查请求的包是否已存在于缓存中（请参阅[管理 NuGet 缓存](managing-the-nuget-cache.md)）。
    - 如果包不在缓存中，请尝试从[配置文件](Configuring-NuGet-Behavior.md)中列出的源下载包。
      - 对于使用 `packages.config` 引用格式的项目，NuGet 会使用配置中的源顺序。
      - 对于使用 PackageReference 格式的项目，NuGet 会先检查本地文件夹的源，再检查网络共享中的源，最后检查 HTTP (Internet) 源。
      - 一般情况下，NuGet 检查源的顺序不具有特别意义，因为具有特定标识符和版本号的任意给定包在找到的源方面完全相同。
    - 如果该包是从其中一个源成功获取的，NuGet 会将其添加到缓存中。 否则，安装将失败。

1. 将该包扩展到项目中。
    - 展开意味着将包的内容解压缩到适当的子文件夹中。 子文件夹中还放置了 `.nupkg` 本身的副本。
    - 如果将包安装到 Visual Studio 或 .NET Core 项目中，则只展开与项目目标框架相关的文件。 使用 nuget.exe 命令行进行安装时，所有程序集都将展开。

1. 如果将包安装在 Visual Studio 或 dotnet CLI 中，则将引用添加到相应的项目文件（或者对于 Visual Studio 中的某些项目类型为 `packages.config`）。

## <a name="related-topics"></a>相关主题

- [包使用的概述和工作流](../consume-packages/overview-and-workflow.md)
- [查找和选择包](../consume-packages/finding-and-choosing-packages.md)
- [配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)
- [管理 NuGet 缓存](managing-the-nuget-cache.md)
