---
title: 安装 NuGet 包的方式
description: 介绍将 NuGet 包安装到项目中的过程，包括磁盘上和适用的项目文件会发生的情况。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 02/12/2018
ms.topic: overview
ms.openlocfilehash: 028fb9710e808974348d9cca3c56103c087d5390
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>安装 NuGet 包的不同方式

使用下表中的任一方法下载和安装 NuGet 包（如果尚未安装，请参阅[安装 NuGet 客户端工具](../install-nuget-client-tools.md)）。 可能从缓存中检索包而不是下载包。

| 方法 | 描述 |
| --- | --- |
| dotnet.exe CLI<br/>`dotnet add package <package_name>` | （所有平台）检索用 \<package_name\> 识别的包，将其内容展开到当前目录下的文件夹中，然后添加对项目文件的引用。 同时还要检索和安装依赖项。<ul><li>[安装并使用包 (dotnet CLI)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[dotnet add package 命令](/dotnet/core/tools/dotnet-add-package)</li></ul> |
| 包管理器 UI (Visual Studio) | （Windows 和 Mac）提供 UI，用户可以通过此 UI 浏览、选择包，并从指定包源将包及其依赖项安装到项目中。 将对已安装的程序包引用添加到项目文件。<ul><li>[安装并使用包 (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[程序包管理器 UI 引用 (Windows)](../tools/package-manager-ui.md)</li><li>[在项目中包括 NuGet 包 (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| 程序包管理器控制台 (Visual Studio)<br/>`Install-Package <package_name>` | （仅限 Windows）检索并将用 \<package_name\> 识别的包从所选源安装到解决方案的指定项目中，然后添加对项目文件的引用。 同时还要检索和安装依赖项。<ul><li>[安装并使用包 (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[程序包管理器控制台指南](../tools/package-manager-console.md)</li></ul> |
| nuget.exe CLI<br/>`nuget install <package_name>` | （所有平台）检索用 \<package_name\> 识别的包，将其内容展开到当前目录下的文件夹中；还可以检索 `packages.config` 文件中列出的所有包。 同时还要检索和安装依赖项，但对项目文件或 `packages.config` 不作任何更改。<ul><li>[安装命令](../tools/cli-ref-install.md)</li></ul> |

## <a name="what-happens-when-a-package-is-installed"></a>安装包时会发生什么情况

简而言之，不同的 NuGet 工具通常会对项目文件或 `packages.config` 中的包创建引用，然后执行包还原，从而有效安装包。 `nuget install` 除外，它仅将包展开到 `packages` 文件夹，而不修改任何其他文件。

一般流程如下：

1. （除 `nuget.exe` 之外的所有工具）将包标识符和版本记录到项目文件或 `packages.config`中。

2. 获取包：
   - 检查包是否（通过标识符和版本号）已安装在 global-packages 文件夹中，如[管理全局包和缓存文件夹](managing-the-global-packages-and-cache-folders.md)中所述。

   - 如果包不在 global-packages 文件夹中，请尝试从[配置文件](Configuring-NuGet-Behavior.md)中列出的源检索包。 对于在线源，请首先尝试从缓存中检索包，除非通过 `nuget.exe` 命令指定 `-NoCache` 或通过 `dotnet restore` 指定 `--no-cache`。 （Visual Studio 和 `dotnet add package` 始终使用缓存。）如果从缓存中使用包，“缓存”将出现在输出中。 缓存有 30 分钟的到期时间。

   - 如果包不在缓存中，请尝试从配置中列出的源下载包。 如果下载包，则会在输出中出现“GET”和“OK”。

   - 如果无法从任何源成功获取包，安装将失败，并显示诸如 [NU1103](../reference/errors-and-warnings.md#nu1103) 之类的错误。 注意，来自 `nuget.exe` 命令的错误仅显示最后检查的源，但意味着无法从任何源获取包。

   获取包时，NuGet 配置中的源顺序可能适用：

   - 对于使用 PackageReference 格式的项目，NuGet 将首先检查源本地文件夹和网络共享，然后再检查 HTTP 源。

   - 对于使用 `packages.config` 管理格式的项目，NuGet 会使用配置中的源顺序。 还原操作除外，这种情况下将忽略源排序，NuGet 会使用任何最先响应的源中的包。

   - 一般情况下，NuGet 检查源的顺序不具有特别意义，因为具有特定标识符和版本号的任意给定包在找到的源方面完全相同。

3. （除 `nuget.exe` 之外的所有工具）保存包副本和 http-cache 文件夹中的其他信息，如[管理全局包和缓存文件夹](managing-the-global-packages-and-cache-folders.md)中所述。

4. 如下载，请将包安装到每个用户的 global-packages 文件夹中。 NuGet 创建每个包标识符的子文件夹，然后创建每个已安装包版本的子文件夹。

5. 更新其他项目文件和文件夹：

    - 对于使用 PackageReference 的项目，更新存储在 `obj/project.assets.json` 中的包依赖项关系图。 包内容本身不会复制到任何项目文件夹中。
    - 对于使用 `packages.config` 的项目，将展开包中与项目目标框架匹配的那些部分复制到项目的 `packages` 文件夹。 （在使用 `nuget install` 时，将复制整个展开包，因为 `nuget.exe` 不检查项目文件来标识目标框架。）
    - 如果包使用[源和配置文件转换](../create-packages/source-and-config-file-transformations.md)，则更新 `app.config` 和/或 `web.config`。

6. 安装任何低级别的依赖项（如果项目中尚不存在）。 此过程可能会更新过程中的包版本，如[依赖项解析](../consume-packages/dependency-resolution.md)中所述。

7. （仅适用于 Visual Studio）如果可用，请在 Visual Studio 窗口中显示包的自述文件。

## <a name="related-articles"></a>相关文章

- [包使用的概述和工作流](../consume-packages/overview-and-workflow.md)
- [查找和选择包](../consume-packages/finding-and-choosing-packages.md)
- [管理 NuGet 缓存和 global-packages 文件夹](managing-the-global-packages-and-cache-folders.md)
- [配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)
