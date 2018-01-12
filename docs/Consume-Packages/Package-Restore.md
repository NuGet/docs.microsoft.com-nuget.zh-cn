---
title: "NuGet 程序包还原 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "描述 NuGet 如何还原项目依赖的包，包括如何禁用还原和约束版本。"
keywords: "NuGet 包还原, NuGet 包安装, 安装包, 还原包, 依赖项版本, 禁用自动还原, 约束包版本"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4e819a2bb34bbe70f0f11d5adeed82b976a8cb65
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="package-restore"></a>包还原

为了提升为更干净的开发环境并减少存储库大小，NuGet“包还原”在生成项目前会安装所有引用的包。 这种广泛使用的功能确保了所有依赖项在项目中均可用，无需那些包存储在源代码管理中（有关如何配置存储库排除包二进制文件的信息，请参阅[包与源代码管理](../consume-packages/packages-and-source-control.md)。

本主题内容：
- [包还原快速指南](#quick-guide-to-package-restore)
- [包还原概述](#package-restore-overview)
- [启用和禁用包还原](#enabling-and-disabling-package-restore)
- [使用还原约束包版本](#constraining-package-versions-with-restore)
- [命令行还原](#command-line-restore)，适用于 NuGet 的所有版本
- [Visual Studio 中的自动还原](#automatic-restore-in-visual-studio)，适用于 NuGet 2.7 和更高版本。
- [Visual Studio 中集成 MSBuild 的存储](#msbuild-integrated-restore)，适用于 NuGet 2.6 和更早版本。
- [使用 Team Foundation Build 还原包](#package-restore-with-team-foundation-build)

还原行为会随着版本变化，若要检查 NuGet 版本，只需在命令行上运行 `nuget.exe` 并查看输出的第一行。

有关生成服务器上的包还原的其他详细信息，请参阅[使用 TFBuild 还原包](../consume-packages/team-foundation-build.md)。

> [!Note]
> 为包还原配置的项目同样使用 Mono 上的 xbuild。

## <a name="quick-guide-to-package-restore"></a>包还原快速指南

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> 如果看到错误“此项目引用此计算机上缺少的 NuGet 包”或者“一个或更多 NuGet 包需要还原但无法还原，因为未授予许可”，则按照[启用和禁用包还原](#enabling-and-disabling-package-restore)中的以下说明打开自动还原。

## <a name="package-restore-overview"></a>包还原概述

首先，包引用按以下其中一种包管理格式保留，具体取决于项目类型和 NuGet 版本。 （注意 NuGet 4 和 MSBuild 15.1 是使用 Visual Studio 2017 安装的。）

| 方法 | NuGet 版本 | 描述 | 
| --- | --- | --- |
| `packages.config` | 2.x+ | 列出依赖项的完整深层集。 添加到 `packages.config` 的包还必须添加到项目文件，“目标”和“属性”也必须添加到项目文件。 这是适用于所有版本的 NuGet 的基线法，但是与其他选项相比性能较低。 （请参阅 [packages.config 架构](../schema/packages-config.md)。） | 
| `project.json` | 3.x+ | 默认情况下仅与 UWP 项目共同使用，但是可以从 `packages.config` 转换项目。 `project.json` 仅列出顶级依赖项。 生成期间，将“引用”、“目标”和“属性”动态添加到项目，获得比 `packages.config` 更好的性能。 （请参阅 [project.json 架构](../schema/project-json.md)。）|
| PackageReference | 4.x+ | 在 `<Reference>` 和 `<ProjectReference>` 旁的 `<PackageReference>` 节点的项目文件中直接列出依赖项。 工作原理类似 `project.json`请参阅[项目文件中的包引用](../Consume-Packages/Package-References-in-Project-Files.md)。 |

其次，使用引用列表通过多种方法开始还原：

从命令行或者[包管理器控制台](../tools/Package-Manager-Console.md)：

| 命令 | 适用方案 |
| --- | --- | 
| `nuget restore` | NuGet 所有版本和所有引用类型。 请参阅以下[命令行还原](#command-line-restore)。 | 
| `dotnet restore` | 与 .NET Core 项目的 `nuget restore` 相同。 请参阅 [dotnet restore](/dotnet/articles/core/tools/dotnet-restore)。 |
| `msbuild /t:restore` | 仅有[项目文件中的包引用](../Consume-Packages/Package-References-in-Project-Files.md)的 Nuget 4.x+ 和 MSBuild 15.1+。 `nuget restore` 和 `dotnet restore` 均对适用项目使用此命令。 请参阅[NuGet 打包和还原为 MSBuild 目标 - 还原目标](../schema/msbuild-targets.md#restore-target)。|

Visual Studio 自身同样在不同时间还原包：

| 类型 | 还原发生时 |
| --- | --- |
| 模板还原 | 创建新项目期间，某些模板依赖外部包。 |
| 生成还原 | 作为生成第一步。 |
| 解决方案还原 | 用户右键单击解决方案并选择“还原 NuGet 包”时。 |
| 项目更改上的还原 | （仅 NuGet 4.x）使用基于 .NET Core SDK 的项目时，包括项目状态的更改时间。 |

## <a name="enabling-and-disabling-package-restore"></a>启用和禁用包还原

包还原主要通过 Visual Studio 中的“工具”>“选项”>“NuGet 包管理器”启用：

![通过NuGet 包管理器选项控制包还原行为](media/Restore-01-AutoRestoreOptions.png)

- 允许 NuGet 下载缺失的包：如下所示，通过更改 `%AppData%\NuGet\NuGet.Config` 文件中的 `packageRestore/enabled` 设置控制包还原的所有窗体。

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  可以通过在启动 Visual Studio 或启动生成前将名为 EnableNuGetPackageRestore 的环境变量设为 TRUE 或 FALSE 值，全局重写 `packageRestore/enabled` 设置。
    

- **生成期间在 Visual Studio 中自动检查缺失的包**：如下所示，通过更改 `%AppData%\NuGet\NuGet.Config` 文件中的 `packageRestore/automatic` 设置，控制适用于 NuGet 2.7 和更改版本的自动还原。
            
    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

有关引用，请参阅 [NuGet 配置文件 - packageRestore 部分](../Schema/nuget-config-file.md#packagerestore-section)。

在某些情况下，开发人员或公司可能希望默认情况下对所有用户在计算机上启用或禁用包还原。 这可以通过将与以上相同的设置添加到位于 `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]` 中的全局 NuGet 配置文件完成。 然后，各个用户可以按照项目级别的要求有选择地启用还原。 有关 NuGet 如何设置多个配置文件优先级的准确详细信息，请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。

## <a name="constraining-package-versions-with-restore"></a>使用还原约束包版本

NuGet 通过任意方法还原包时，它将遵守 `packages.config`、`project.json` 或项目文件中指定的任何约束：

- `packages.config`：在依赖项的 `allowedVersion` 属性中指定版本范围。 请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)。 例如:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- `project.json` 使用依赖项的版本号直接指定版本范围。 例如:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- 项目文件中的包引用：使用依赖项的版本号直接指定版本范围。 例如:
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

在所有情况下，都使用[包版本控制](../reference/package-versioning.md)中介绍的表示法。

## <a name="command-line-restore"></a>命令行还原

对于 NuGet 2.7 和更高版本，使用 [Restore](../tools/cli-ref-restore.md) 命令还原解决方案的所有包（无论它使用 `packages.config`、`project.json` 还是项目文件中的包引用）。 对于 `c:\proj\app` 之类的给定项目文件夹，以下每个常见变体都会还原包：

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

对于 NuGet 4.0+ 和 MSBuild 15.1+，还可以使用 `MSBuild /t:restore`，如 [NuGet 打包和还原为 MSBuild 目标](../schema/msbuild-targets.md)中所述。

## <a name="build-time-restore-in-visual-studio"></a>Visual Studio 中的生成时还原

Visual Studio 默认在生成开始时自动还原缺失的包。 此行为可以通过清除“工具”>“选项”>“NuGet 包管理器”>“常规”>“生成期间在 Visual Studio 中自动检查缺失的包”进行更改。

启用时，自动还原的工作原理如下所示：

1. 生成开始时，Visual Studio 指示 NuGet 还原包。
1. NuGet 以递归的方式在解决方案中查找所有 `packages.config` 文件、查找 `project.json` 文件或在项目文件中查找。
1. 对于引用文件中列出的每个包，NuGet 都会检查它是否已存在于解决方案中（`packages` 文件夹、`project.lock.json` 或 `project.assets.json`，具体取决于项目是否使用 `packages.config`、`project.json` 或项目文件中的包引用）。
1. 如果未找到包，则 NuGet 尝试先从缓存中检索包（请参阅[管理 NuGet 缓存](../consume-packages/managing-the-nuget-cache.md)。 如果在缓存中未找到包，则 NuGet 尝试从“工具”>“选项”>“NuGet 包管理器”>“包源”中列出的已启用源中，按照源出现的顺序下载包。 在这种情况下，NuGet 不指示查找包失败，除非检查完所有源，才报告列表中仅最后源出现失败。 此类错误还暗示着 包已不在其他任意源上，尽管那些源没有单独显示错误。
1. 如果下载成功，则 NuGet 会缓存包并将其安装到解决方案（同样也会安装到 `packages` 文件夹 `project.lock.json` 或 `project.assets.json`）；否则，NuGet 和生成均失败。

在此过程中，会出现含有取消包还原选项的进度对话框。

## <a name="package-restore-with-team-foundation-build"></a>使用 Team Foundation Build 还原包

在生成服务器上生成项目时通常会用到包还原，正如 Team Foundation Server (TFS) 和 Visual Studio Team Services（以及其他此处未涉及的生成系统）。

### <a name="visual-studio-team-services"></a>Visual Studio Team Services

在 Team Services 上创建生成定义时，只需在任意生成任务前将“还原 NuGet 包”任务包括在定义中。 大量生成模板中默认包括了此任务。

![Visual Studio Team Service 生成定义中的 NuGet 包还原任务](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a>Team Foundation Server

使用 TFS 2013 和更高版本时，在生成期间会默认自动还原包，前提是使用适用于 Team Foundation Server 2013 或更高版本的 Team Build Template。

如果使用更早版本的生成模板（例如在从更早版本的 TFS 中迁移的项目中），则还需要将这些生成模板迁移到 TFS 2013。 这在本质上相当于使用适合源控件（TFVC 或 Git）的模板重新创建生成模板的自定义部分。

对于更早版本的 TFS，只需按照前面所述的方法，包括一个调用[命令行还原](#command-line-restore)的生成步骤。

有关详细信息，请参阅[使用 Team Foundation Build 还原包的演练](../consume-packages/team-foundation-build.md)。    
