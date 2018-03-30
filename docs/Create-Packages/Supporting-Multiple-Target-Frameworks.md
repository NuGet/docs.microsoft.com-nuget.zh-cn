---
title: NuGet 包的多目标 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 09/27/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 介绍从一个 NuGet 包中以多个 .NET Framework 版本为目标的各种方法。
keywords: NuGet 包目标, .NET Framework 版本, NuGet 和 .NET, 面向多个框架, NuGet 包创建
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4349fed276b1a1f46845c990718f9202b356072c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="supporting-multiple-net-framework-versions"></a>支持多个 .NET Framework 版本

有关使用 NuGet 4.0+ 的 .NET Core 项目，请参阅 [NuGet 包和作为 MSBuild 目标还原](../reference/msbuild-targets.md)以获取有关跨目标的详细信息。

许多库以 .NET Framework 的特定版本为目标。 例如，你可能拥有特定于 UWP 的一个库版本，而拥有的另一版本利用 .NET Framework 4.6 中的功能。

为了适应此情况，NuGet 支持在使用[创建包](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)中所述的基于约定的工作目录方法时，将同一库的多个版本放入一个包中。

## <a name="framework-version-folder-structure"></a>框架版本的文件夹结构

生成仅包含一个库版本或面向多个框架的包时，始终根据以下约定使用区分大小写的不同框架名称在 `lib` 下创建子文件夹：

    lib\{framework name}[{version}]

有关支持的名称的完整列表，请参阅[目标框架引用](../reference/target-frameworks.md#supported-frameworks)。

所具有的库版本必须特定于某框架，且不应直接放置在根 `lib` 文件夹中。 （此功能仅受 `packages.config` 支持。） 此操作会导致与任何目标框架兼容，并允许在任何位置上进行安装，很可能造成意外的运行时错误。 已弃用在根文件夹（如 `lib\abc.dll`）或子文件夹（如 `lib\abc\abc.dll`）中添加程序集的操作，且在使用 PackagesReference 格式时忽略了此操作。

例如，以下文件夹结构支持特定于框架的程序集的四种版本：

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

若要在生成包时轻松包括所有这些文件，请在 `.nuspec` 的 `<files>` 部分中使用递归 `**` 通配符：

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>特定于体系结构的文件夹

如果具有特定于体系结构的程序集，即面向 ARM、x86 和 x64 的单独程序集，必须将它们放置在名为 `{platform}-{architecture}\lib\{framework}` 或 `{platform}-{architecture}\native` 的子文件夹内名为 `runtimes` 的文件夹中。 例如，以下文件夹结构可以容纳面向 Windows 10 的本机和托管 DLL 以及 `uap10.0` 框架：

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

有关在 `.nuspec` 清单中引用这些文件的示例，请参阅[创建 UWP 包](../guides/create-uwp-packages.md)。

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>将程序集版本与项目中的目标框架匹配

NuGet 在安装具有多个程序集版本的包时，会尝试将程序集的框架名称与项目的目标框架匹配。

如果未找到匹配项，NuGet 将复制小于或等于项目的目标框架的最高版本的程序集（如果可用）。 如果未找到任何兼容的程序集，NuGet 将返回相应的错误消息。

例如，假设包中具有以下文件夹结构：

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

当在面向 .NET Framework 4.6 的项目中安装此包时，NuGet 将在 `net45` 文件夹中安装程序集，因为它是小于或等于 4.6 的最高可用版本。

但是，如果项目面向 .NET Framework 4.6.1，NuGet 将在 `net461` 文件夹中安装程序集。

如果项目面向 .NET Framework 4.0 和更早版本，NuGet 会发出相应的错误消息，因为找不到兼容的程序集。

## <a name="grouping-assemblies-by-framework-version"></a>通过框架版本对程序集进行分组

NuGet 仅从包中的单个库文件夹中复制程序集。 例如，假设包具有以下文件夹结构：

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

当在面向 .NET Framework 4.5 的项目中安装包时，将仅安装 `MyAssembly.dll` (v2.0) 程序集。 不会安装 `MyAssembly.Core.dll` (v1.0)，因为它未在 `net45` 文件夹中列出。 NuGet 执行此操作的原因是 `MyAssembly.Core.dll` 可能已合并到 `MyAssembly.dll` 的 2.0 版本中。

如果要为 .NET Framework 4.5 安装 `MyAssembly.Core.dll`，请在 `net45` 文件夹中放置副本。

## <a name="grouping-assemblies-by-framework-profile"></a>通过框架配置文件对程序集进行分组

NuGet 还通过向文件夹末尾追加短划线和配置文件名称，支持以特定的框架配置文件为目标。

    lib\{framework name}-{profile}

以下是支持的配置文件：

- `client`：客户端配置文件
- `full`：完整配置文件
- `wp`：Windows Phone
- `cf`：Compact Framework

## <a name="determining-which-nuget-target-to-use"></a>确定要使用的 NuGet 目标

当打包面向可移植类库的库时，不容易确定应在文件夹名称和 `.nuspec` 文件中使用的 NuGet 目标，尤其当仅面向 PCL 的子集时。 以下外部资源有助于解决此问题：

- [Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html)（.NET 中的框架配置文件）(stephenclearly.com)
- [可移植类库的配置文件](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co)：枚举 PCL 配置文件及其等效 NuGet 目标的表
- [可移植类库的配置文件工具](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com)：用于确定系统上可用的 PCL 配置文件的命令行工具

## <a name="content-files-and-powershell-scripts"></a>内容文件和 PowerShell 脚本

> [!Warning]
> 仅可通过 `packages.config` 格式使用可变的内容文件和脚本执行；这些内容在使用所有其他格式时已弃用，且不应用于任何新的包。

对于 `packages.config`，可以使用 `content` 和 `tools` 文件夹中的相同文件夹约定，通过目标框架对内容文件和 PowerShell 脚本进行分组。 例如:

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

如果框架文件夹保留为空，NuGet 不会添加程序集引用或内容文件，也不会运行该框架的 PowerShell 脚本。

> [!Note]
> 因为 `init.ps1` 在解决方案级别执行，且它不依赖于项目，所以必须将其直接放置在 `tools` 文件夹下。 如果将其放置在框架文件夹下，它会被忽略。
