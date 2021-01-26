---
title: NuGet 2.8 发行说明
description: NuGet 2.8 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cb77cf0f049b5b3cfe1039d83ab58e33457674bf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776719"
---
# <a name="nuget-28-release-notes"></a>NuGet 2.8 发行说明

[NuGet 2.7.2 发行说明](../release-notes/nuget-2.7.2.md)  | [NuGet 2.8.1 发行说明](../release-notes/nuget-2.8.1.md)

NuGet 2.8 于2014年1月29日发布。

## <a name="acknowledgements"></a>致谢

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie)) 
    - [#3466](https://nuget.codeplex.com/workitem/3466) -打包包时，验证依赖项包的 Id。
2. [圣马丁 Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw)) 
    - [#2379](https://nuget.codeplex.com/workitem/2379) -删除 persistening 源凭据时 $metadata 后缀。
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks)) 
    - [#3538](http://nuget.codeplex.com/workitem/3538) -支持指定 nuget.exe update 命令的项目文件。
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - 不通过-IncludeReferencedProjects 传递[#3536](http://nuget.codeplex.com/workitem/3536)替换标记。
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave)) 
    - [#3677](http://nuget.codeplex.com/workitem/3677) 修复了推送大包时的 OutOfMemoryException 引发。
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -在项目引用另一个 CLI/c + + 项目时修复不正确的目标路径。
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph)) 
    - [#3639](https://nuget.codeplex.com/workitem/3639) -默认情况下，允许将包安装为开发依赖项
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl)) 
    - [#3717](https://nuget.codeplex.com/workitem/3717) -删除到最新修补程序版本的隐式升级
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - NuGet. Server、nuget.exe mirror 命令及其他程序的几个 bug 修复和改进。
    - 这项工作是在数个月内完成的，Gregory 与我们一起使用，以将其集成到2.8 的主节点。

## <a name="patch-resolution-for-dependencies"></a>依赖项的修补程序解析

解析包依赖关系时，NuGet 一直实现了一个策略，该策略选择满足包的依赖项的最低主要和次要包版本。 但与主要和次要版本不同的是，修补程序版本总是解析为最高版本。 尽管此行为是善意的，但它却缺乏了安装具有依赖项的包的确定性。 请看下面的示例：

```
PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

PackageB@1.0.1 is published

Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1
```

在此示例中，即使安装了 Developer1 和 Developer2 PackageA@1.0.0 ，每个都最终使用不同版本的 PackageB。 NuGet 2.8 更改此默认行为，以便修补程序版本的依赖关系解析行为与主版本和次要版本的行为一致。 在上面的示例中，将在 PackageB@1.0.0 安装时安装 PackageA@1.0.0 ，而不考虑较新的修补程序版本。

## <a name="-dependencyversion-switch"></a>-DependencyVersion 开关

尽管 NuGet 2.8 更改了用于解决依赖项的 _默认_ 行为，但它还在包管理器控制台中通过-DependencyVersion 开关更精确地控制依赖项解析过程。 开关允许将依赖项解析 (默认行为) 、可能的最高版本或最高的次要版本或修补程序版本。  此开关仅适用于 powershell 命令中的安装包。

![DependencyVersion 开关](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>DependencyVersion 特性

除了上面详细说明的-DependencyVersion 开关以外，还允许 NuGet 在定义默认值的情况下设置新 Nuget.Config 属性的功能，如果未在的调用中指定-DependencyVersion 开关。 任何安装包操作的 "NuGet 包管理器" 对话框也会遵守此值。 若要设置此值，请将以下属性添加到 Nuget.Config 文件：

```xml
<config>
    <add key="dependencyversion" value="Highest" />
</config>
```

## <a name="preview-nuget-operations-with--whatif"></a>预览具有-whatif 的 NuGet 操作

某些 NuGet 包可能具有深层依赖项关系图，因此，在安装、卸载或更新操作过程中，它可帮助您首先了解将发生的情况。 NuGet 2.8 将标准 PowerShell whatif 交换机添加到安装包、卸载包和更新包命令中，以使将应用该命令的包的整个关闭可视化。 例如， `install-package Microsoft.AspNet.WebApi -whatif` 在空的 ASP.NET Web 应用程序中运行将生成以下项。

```
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
```

## <a name="downgrade-package"></a>降级包

安装包的预发行版本是为了调查新功能，然后决定回滚到最后一个稳定的版本，这种情况并不常见。 在 NuGet 2.8 之前，这是卸载预发行包及其依赖项，然后安装早期版本的多步骤过程。 不过，对于 NuGet 2.8，更新包现在将回滚整个包关闭 (例如，包的依赖关系树) 到以前的版本。

## <a name="development-dependencies"></a>开发依赖项

许多不同类型的功能可作为 NuGet 包提供-包括用于优化开发过程的工具。 这些组件虽然可以有助于开发新包，但在以后发布时，不应将其视为新包的依赖项。 使用 NuGet 2.8，包可以将文件中的自身标识 `.nuspec` 为 developmentDependency。 安装后，还会将此元数据添加到 `packages.config` 安装包的项目的文件中。 稍后在 `packages.config` 中为 NuGet 依赖关系分析该文件时 `nuget.exe pack` ，它将排除标记为开发依赖项的这些依赖项。

## <a name="individual-packagesconfig-files-for-different-platforms"></a>不同平台的单个 packages.config 文件

为多个目标平台开发应用程序时，通常会为各自的每个生成环境使用不同的项目文件。 在不同的项目文件中使用不同的 NuGet 包也很常见，因为包具有不同平台的不同级别的支持。 NuGet 2.8 通过 `packages.config` 为不同平台特定的项目文件创建不同的文件，为此方案提供了改进的支持。

![多个 package.config 文件](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>回退到本地缓存

尽管 NuGet 包通常是从使用网络连接 [的](http://www.nuget.org/) 远程库使用，但在很多情况下客户端未连接。 如果没有网络连接，NuGet 客户端将无法成功安装包-即使这些包已在本地 NuGet 缓存中的客户端计算机上。 NuGet 2.8 将自动缓存回退添加到程序包管理器控制台。 例如，断开网络适配器和安装 jQuery 时，控制台将显示以下内容：

```
PM> Install-Package jquery
The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
Installing 'jQuery 2.0.3'.
Successfully installed 'jQuery 2.0.3'.
Adding 'jQuery 2.0.3' to WebApplication18.
Successfully added 'jQuery 2.0.3' to WebApplication18.
```

缓存回退功能不需要任何特定的命令参数。 此外，缓存回退当前仅在包管理器控制台中运行-"包管理器" 对话框中当前未使用该行为。

## <a name="webmatrix-nuget-client-updates"></a>WebMatrix NuGet 客户端更新

除了 NuGet 2.8，还更新了 WebMatrix 的 NuGet 扩展，以包含 [nuget 2.5](../release-notes/nuget-2.5.md)提供的很多主要功能。 新功能包括 "全部更新"、"最低 NuGet 版本" 等，并允许覆盖内容文件。

在 WebMatrix 3 中更新 NuGet 包管理器扩展：

1. 打开 WebMatrix 3
1. 单击功能区中的扩展图标
1. 选择 "更新" 选项卡
1. 单击以将 NuGet 包管理器更新到2.5。0
1. 关闭并重新启动 WebMatrix 3

这是 NuGet 团队发布的 NuGet 包管理器扩展的第一个版本。  Microsoft 最近向开源 NuGet 项目提供了该代码。 以前，NuGet 集成内置于 WebMatrix 中，无法在 WebMatrix 中进行带外更新。  现在，我们可以将其与 NuGet 的客户端工具的其余部分进行进一步更新。

## <a name="bug-fixes"></a>Bug 修复

在更新包-重新安装命令中，所做的一个主要 bug 修复是性能改进。

除了这些功能和前面提到的性能修复外，此版本的 NuGet 还包括许多其他 bug 修复。 此版本中解决了181的总问题。 有关 NuGet 2.8 中已修复工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)。
