---
title: NuGet 2.8 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 2.8 发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547454"
---
# <a name="nuget-28-release-notes"></a>NuGet 2.8 发行说明

[NuGet 2.7.2 发行说明](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 发行说明](../release-notes/nuget-2.8.1.md)

NuGet 2.8 已于 2014 年 1 月 29 日发布。

## <a name="acknowledgements"></a>致谢

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) -打包验证 Id 的依赖项包的包时。
2. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [# 2379年](https://nuget.codeplex.com/workitem/2379)-persistening 源的凭据时删除 $metadata 后缀。
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) -指定用于 nuget.exe 更新命令的项目文件的支持。
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -不使用-IncludeReferencedProjects 传递的替换令牌。
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -修复 nuget.push 推送大型包时引发 OutOfMemoryException。
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -项目引用另一个 CLI/c + + 项目时修复不正确的目标路径。
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -允许用于默认情况下为开发依赖项安装的包
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -删除隐式升级到最新的修补程序版本
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - 了几个 bug 修复和改进 NuGet.Server、 nuget.exe 镜像命令和其他人。
    - 这项工作在几个月，已完成，Gregory 使用正确的计时我们要将集成到为 2.8 母版。

## <a name="patch-resolution-for-dependencies"></a>修补程序解析依赖项

在解析包依赖项，NuGet 已从历史上看实现选择满足对包依赖项的最小主版本号和次包版本的策略。 与不同的主版本号和次版本，但是，修补程序版本是始终解析为的最高版本。 该行为是善意的但缺乏安装具有依赖项包的确定性创建它。 请看下面的示例：

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

在此示例中，即使 Developer1 和 Developer2 安装PackageA@1.0.0、 每个使用不同版本的 PackageB 向上结束。 这样，修补程序版本的依赖关系解析行为与主要和次要版本的行为保持一致，NuGet 2.8 会更改此默认行为。 在上面的示例中，然后PackageB@1.0.0由于安装将安装PackageA@1.0.0，而不考虑的较新的修补程序版本。

## <a name="-dependencyversion-switch"></a>-DependencyVersion 开关

尽管 NuGet 2.8 更改_默认_行为对于解析的依赖关系，它还将添加更加精确地控制通过-DependencyVersion 开关的依赖关系解析过程中包管理器控制台。 开关可以启用对可能的最低版本 （默认行为）、 可能的最高版本，或最高次要或修补程序版本的解析依赖项。  此开关仅适用于在 powershell 命令中的安装包。

![DependencyVersion 开关](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>DependencyVersion 属性

除了上面详细说明的功能还允许 NuGet 在 Nuget.Config 文件中设置新属性-DependencyVersion 开关定义默认值什么，如果在调用中未指定-DependencyVersion 开关安装包。 NuGet 包管理器对话框中的任何安装包操作还会遵循此值。 若要设置此值，请将以下属性添加到在 Nuget.Config 文件：

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>使用-whatif 预览 NuGet 操作

一些 NuGet 包可以有深入的依赖项关系图，并且在这种情况下，它可以在安装过程中会有所帮助、 卸载或更新操作，以首先查看会发生什么情况。 NuGet 2.8 将标准 PowerShell-whatif 开关添加到安装包、 卸载包和更新包命令来启用可视化命令将应用于包的完整闭包。 例如，运行`install-package Microsoft.AspNet.WebApi -whatif`中一个空的 ASP.NET Web 应用程序会产生以下结果。

    PM> install-package Microsoft.AspNet.WebApi -whatif
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.WebHost (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Core (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Client (≥ 5.0.0)'.
    Attempting to resolve dependency 'Newtonsoft.Json (≥ 4.5.11)'.
    Install Newtonsoft.Json 4.5.11
    Install Microsoft.AspNet.WebApi.Client 5.0.0
    Install Microsoft.AspNet.WebApi.Core 5.0.0
    Install Microsoft.AspNet.WebApi.WebHost 5.0.0
    Install Microsoft.AspNet.WebApi 5.0.0

## <a name="downgrade-package"></a>降级包

不常见安装包的预发布版本，以便调查的新功能，然后决定要回滚到上次的稳定版本。 之前 NuGet 2.8，这是一个多步骤过程，以及卸载预发行包和其依赖项，然后安装较早版本。 使用 NuGet 2.8，但是，更新包将现在回滚整个包闭包 （例如包的依赖项树） 到以前的版本。

## <a name="development-dependencies"></a>开发依赖项

作为 NuGet 包-包括用于优化开发过程的工具，可以提供许多不同类型的功能。 这些组件，它们可有助于开发新的包，而不应将新包的依赖项更高版本发布时。 NuGet 2.8 使包来标识自身中`.nuspec`为 developmentDependency 文件。 安装时，此元数据也将添加到`packages.config`已在其中安装了包的项目文件。 时，`packages.config`文件更高版本的 NuGet 依赖项期间分析`nuget.exe pack`，它将排除这些依赖项标记为开发依赖项。

## <a name="individual-packagesconfig-files-for-different-platforms"></a>针对不同平台的单独的 packages.config 文件

开发针对多个目标平台的应用程序，时，通常会为每个相应的生成环境中有不同的项目文件。 也很常见使用不同的 NuGet 包在不同的项目文件中，如包具有不同级别的不同平台的支持。 NuGet 2.8 提供改进的支持实现此方案创建不同`packages.config`不同的特定于平台的项目文件的文件。

![多个 package.config 文件](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>回退到本地缓存

尽管 NuGet 包会通常占用从远程库等[NuGet 库](http://www.nuget.org/)使用的网络连接，有许多方案，客户端未连接。 无网络连接，NuGet 客户端无法成功安装包的即使这些包已在本地 NuGet 缓存中的客户端的计算机上。 NuGet 2.8 将自动缓存回退添加到包管理器控制台。 例如，当断开连接的网络适配器并安装 jQuery，在控制台显示如下信息：

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

缓存回退功能不需要任何特定的命令参数。 此外，只能在包管理器控制台中当前运行缓存回退-行为目前不能在包管理器对话框。

## <a name="webmatrix-nuget-client-updates"></a>WebMatrix NuGet 客户端的更新

NuGet 2.8 以及适用于 WebMatrix 的 NuGet 扩展也已更新为包括的许多主要功能附带[NuGet 2.5](../release-notes/nuget-2.5.md)。 新功能包括如更新全部、 最小值 NuGet 版本和允许的内容文件的覆盖。

若要更新你在 WebMatrix 3 中的 NuGet 包管理器扩展：

1. 打开 WebMatrix 3
1. 单击功能区中的扩展图标
1. 选择更新选项卡
1. 单击此项可为 2.5.0 更新 NuGet 包管理器
1. 关闭并重新启动 WebMatrix 3

这是 NuGet 团队的 NuGet 包管理器扩展的 WebMatrix 的第一个版本。  代码最近已由 Microsoft 的开源 NuGet 项目到提供。 以前，NuGet 集成已内置到 WebMatrix 中，并且带外从 WebMatrix 无法更新。  现在，我们能够进行进一步与 NuGet 的客户端工具的其余部分一起更新。

## <a name="bug-fixes"></a>Bug 修复

所做的主要 bug 修复之一就是更新包中的性能改进的重新安装命令。

除了这些功能和前面提到的性能修复程序，此版本的 NuGet 还包括许多其他 bug 修复。 出现的版本中解决的 181 总问题。 有关完整列表的工作项中已修复 NuGet 2.8，请查看[对于此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)。
