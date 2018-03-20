---
title: "NuGet 程序包还原 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "概述 NuGet 如何还原项目依赖的包，包括如何禁用还原和约束版本。"
keywords: "NuGet 包还原, NuGet 包安装, 安装包, 还原包, 依赖项版本, 禁用自动还原, 约束包版本"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 761ef86a70e0a681449dc9fe86d6a52ac2b19bb1
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="package-restore"></a>包还原

为了提升为更干净的开发环境并减少存储库大小，NuGet“包还原”在生成项目前会安装所有引用的包。 这种广泛使用的功能&mdash;是在 Visual Studio、.NET Core 2.0+ 和 Mono 上的 xbuild 中提供的&mdash;确保了所有依赖项在项目中均可用，无需那些包存储在源代码管理中（有关如何配置存储库排除包二进制文件的信息，请参阅[包与源代码管理](../consume-packages/packages-and-source-control.md)）。 另外，还可以随时手动还原包。

有关生成服务器上的包还原的其他详细信息，请参阅[使用 TFBuild 还原包](../consume-packages/team-foundation-build.md)。

## <a name="package-restore-overview"></a>包还原概述

要还原包，首先根据需要安装项目的直接依赖项，然后在整个依赖项关系图中安装这些包的所有依赖项。

如果尚未安装程序包，NuGet 首先尝试从[缓存](../consume-packages/managing-the-nuget-cache.md)中检索它。 如果在缓存中未找到包，则 NuGet 将尝试从所有已启用的源下载（和缓存）该包（请参阅[配置 NuGet 行为](Configuring-NuGet-Behavior.md)）；源也会出现在 Visual Studio 的“工具”>“选项”>“NuGet 包管理器”>“包源”列表中。 NuGet 会忽略包源的顺序，使用来自任何首先响应请求的源的包。

> [!Note]
> 在检查完所有源之前，NuGet 不会指示包还原失败。 届时，NuGet 仅会报告列表中最后一个源的失败。 该错误说明包已不在其他任意源上，尽管那些源中的任何一个都没有单独显示错误。

包还原是通过以下方式触发的：

- **dotnet CLI**：使用 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 命令还原项目文件中列出的包（请参阅 [PackageReference](../consume-packages/package-references-in-project-files.md)）。 使用 .NET Core 2.0 和更高版本，通过 `dotnet build` 和 `dotnet run` 自动完成还原。

- **程序包管理器 UI（Windows 上的 Visual Studio）**：从模板创建项目以及构建项目时自动还原包（根据[启用和禁用包还原](#enabling-and-disabling-package-restore)中所述的选项）。 此外，在 NuGet 4.0+ 中，对基于 .NET Core SDK 的项目进行更改时还会自动进行还原。

    要手动还原，请右键单击“解决方案资源管理器”中的解决方案，选择“还原 NuGet 包”。 如果一个或多个独立包仍未正确安装（即“解决方案资源管理器”显示错误图标），请使用程序包管理器 UI 卸载受影响的包并重新安装。 请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md)

    如果看到错误“此项目引用此计算机上缺少的 NuGet 包”或者“一个或更多 NuGet 包需要还原但无法还原，因为未授予许可”，则按照[启用和禁用包还原](#enabling-and-disabling-package-restore)中的以下说明打开自动还原。

- **NuGet CLI**：使用 [nuget restore](../tools/cli-ref-restore.md) 命令还原项目文件（请参阅 [PackageReference](../consume-packages/package-references-in-project-files.md)）或 [packages.config](../reference/packages-config.md) 文件中列出的包。 此外，你还可以指定解决方案文件。

- **MSBuild**：使用 [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) 命令还原项目文件中列出的包（请参阅 [PackageReference](../consume-packages/package-references-in-project-files.md)）。 仅适用于 Visual Studio 2017 附带的 NuGet 4.x+ 和 MSBuild 15.1+。 `nuget restore` 和 `dotnet restore` 均对适用项目使用此命令。

- **Visual Studio Team Services**：在 Team Services 上创建生成定义时，只需在任意生成任务前将 [“NuGet 还原”](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) 或 [“.NET Core 还原”](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) 任务包括在定义中。 大量生成模板中默认包括了此任务。

- **Team Foundation Server**：TFS 2013 和更高版本在生成期间会自动还原包，前提是使用适用于 TFS 2013 或更高版本的 Team Build Template。 对于更早版本的 TFS，可以包括一个生成步骤以调用上面其中一个命令行还原选项。 你可以选择将生成模板迁移到 TFS 2013。 有关详细信息，请参阅[使用 Team Foundation Build 还原包的演练](../consume-packages/team-foundation-build.md)。

## <a name="enabling-and-disabling-package-restore"></a>启用和禁用包还原

包还原主要通过 Visual Studio 中的“工具”>“选项”>“NuGet 包管理器”启用：

![通过NuGet 包管理器选项控制包还原行为](media/Restore-01-AutoRestoreOptions.png)

- **允许 NuGet 下载缺失的包**：如下所示，通过更改 `NuGet.Config` 文件中的 `packageRestore/enabled` 设置控制包还原的所有窗体（Windows 上为 `%AppData%\NuGet\NuGet.Config`，Mac/Linux 上为 `~/.nuget/NuGet/NuGet.Config`）。 在 Visual Studio 中，此设置可使解决方案上下文菜单中的 Restore NuGet Packages 命令正常工作。

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

- **生成期间在 Visual Studio 中自动检查缺失的包**：如下所示，通过更改 `NuGet.Config` 文件中的 `packageRestore/automatic` 设置控制自动还原（Windows 上为 `%AppData%\NuGet\NuGet.Config`，Mac/Linux 上为 `~/.nuget/NuGet/NuGet.Config`）。 设置此选项后，从 Visual Studio 运行生成会自动还原任何缺失的包。 该选项不影响使用 MSBuild 从命令行运行的生成。

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

有关引用，请参阅 [NuGet 配置文件 - packageRestore 部分](../reference/nuget-config-file.md#packagerestore-section)。

在某些情况下，开发人员或公司可能希望对计算机上的所有用户启用或禁用包还原。 这可以通过将与以上相同的设置添加到位于 `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]` 中的全局 NuGet 配置文件来完成。 然后，各个用户可以按照项目级别的要求有选择地启用还原。 有关 NuGet 如何设置多个配置文件优先级的确切详细信息，请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。

## <a name="constraining-package-versions-with-restore"></a>使用还原约束包版本

NuGet 通过任意方法还原包时，它将遵守 `packages.config` 或项目文件中指定的任何约束：

- `packages.config`：在依赖项的 `allowedVersion` 属性中指定版本范围。 请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)。 例如:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- PackageReference：使用依赖项的版本号直接指定版本范围。 例如:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

在所有情况下，都使用[包版本控制](../reference/package-versioning.md)中介绍的表示法。

## <a name="troubleshooting"></a>疑难解答

请参阅[包还原疑难解答](package-restore-troubleshooting.md)。