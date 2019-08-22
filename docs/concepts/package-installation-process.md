---
title: 安装包时会发生什么情况？
description: 有关包安装过程的详细信息
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 69ef02e3c935287759b4012aadcfb1cb9811367c
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488446"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>安装 NuGet 包时会发生什么情况？

简而言之，不同的 NuGet 工具通常会对项目文件或 `packages.config` 中的包创建引用，然后执行包还原，从而有效安装包。 `nuget install` 除外，它仅将包展开到 `packages` 文件夹，而不修改任何其他文件。

一般流程如下：

1. （除 `nuget.exe` 之外的所有工具）将包标识符和版本记录到项目文件或 `packages.config`中。

   如果安装工具是 Visual Studio 或 dotnet CLI，则该工具首先尝试安装包。 如果不兼容，则不会将包添加到项目文件或 `packages.config` 中。

2. 获取包：
   - 检查包是否（通过标识符和版本号）已安装在 global-packages  文件夹中，如[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)中所述。

   - 如果包不在 global-packages  文件夹中，请尝试从[配置文件](../consume-packages/Configuring-NuGet-Behavior.md)中列出的源检索包。 对于在线源，请首先尝试从 HTTP 缓存中检索包，除非通过 `nuget.exe` 命令指定 `-NoCache` 或通过 `dotnet restore` 指定 `--no-cache`。 （Visual Studio 和 `dotnet add package` 始终使用缓存。）如果从缓存中使用包，“缓存”将出现在输出中。 缓存有 30 分钟的到期时间。

   - 如果包不在 HTTP 缓存中，请尝试从配置中列出的源下载包。 如果下载包，则会在输出中出现“GET”和“OK”。 NuGet 以常规详细级别记录 http 流量。

   - 如果无法从任何源成功获取包，安装将失败，并显示诸如 [NU1103](../reference/errors-and-warnings/NU1103.md) 之类的错误。 注意，来自 `nuget.exe` 命令的错误仅显示最后检查的源，但意味着无法从任何源获取包。

   获取包时，NuGet 配置中的源顺序可能适用：

   - NuGet 将首先检查源本地文件夹和网络共享，然后再检查 HTTP 源。

3. 保存包副本和 http-cache  文件夹中的其他信息，如[管理全局包和缓存文件夹中所述](../consume-packages/managing-the-global-packages-and-cache-folders.md)。

4. 如下载，请将包安装到每个用户的 global-packages  文件夹中。 NuGet 创建每个包标识符的子文件夹，然后创建每个已安装包版本的子文件夹。

5. NuGet 安装所需的包依赖项。 此过程可能会更新过程中的包版本，如[依赖项解析](../concepts/dependency-resolution.md)中所述。

6. 更新其他项目文件和文件夹：

    - 对于使用 PackageReference 的项目，更新存储在 `obj/project.assets.json` 中的包依赖项关系图。 包内容本身不会复制到任何项目文件夹中。
    - 如果包使用[源和配置文件转换](../create-packages/source-and-config-file-transformations.md)，则更新 `app.config` 和/或 `web.config`。

7. （仅适用于 Visual Studio）如果可用，请在 Visual Studio 窗口中显示包的自述文件。

享受利用 NuGet 包高效处理代码的体验！
