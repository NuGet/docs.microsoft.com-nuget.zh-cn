---
title: 使用 Team Foundation 生成还原 NuGet 包的演练
description: 演练如何使用 Team Foundation Build（TFS 和 Visual Studio Team Services）还原 NuGet 包。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 5eb8e68b800f623ef41a164f18efff2281e7c7cc
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>使用 Team Foundation Build 设置包还原

本文提供详细的演练：演示如何将包作为 [Team Services 生成](/vsts/build-release/index) 的一部分还原包，以实现 Git 和 Team Services 版本控制。

虽然此演练针对使用 Visual Studio Team Services 的方案，但这些概念也适用于其他版本控制和生成系统。

适用于：

- 在 TFS 任意版本上运行的自定义 MSBuild 项目
- Team Foundation Server 2012 或更早版本
- 迁移到 TFS 2013 或更高版本的自定义 Team Foundation Build 过程模板
- 删除了 Nuget 还原功能的生成过程模板

如果使用 Visual Studio Team Services 或 Team Foundation Server 2013 及其生成过程模板，则将在生成过程中进行自动包还原。

## <a name="the-general-approach"></a>常规方法

使用 NuGet 的优点是可以用它来避免将二进制文件签入到版本控制系统。

如果使用[分布式版本控制](http://en.wikipedia.org/wiki/Distributed_revision_control)系统（例如 git），这会变得特别有趣，因为开发人员需要先克隆整个存储库（包括完整历史记录），才能在本地开始工作。 签入二进制文件可能导致明显的存储库膨胀，因为二进制文件的存储通常不需要增量压缩。

NuGet 支持在生成过程中[还原包](../consume-packages/package-restore.md)，这种状态已经持续了一段较长的时间。 以前的实现对于想要扩展生成过程的包而言存在难分先后的问题，因为 NuGet 在生成项目的同时还原包。 但是，MSBuild 不允许在生成期间扩展生成；有人可能会说这是 MSBuild 的问题，但我认为这是一个固有问题。 根据需要扩展的特性，在还原包时才注册可能已经太迟。

解决此问题的方法是确保在生成过程中的第一步还原包：

```cli
nuget restore path\to\solution.sln
```

当你的生成过程在生成代码前还原包时，不再需要签入 `.targets` 文件

> [!Note]
> 包必须创作为允许在 Visual Studio 中加载。 否则，可能还是需要签入 `.targets` 文件，以便其他开发人员直接打开解决方案，而无需先还原包。

以下演示项目演示如何在不需要签入 `packages` 文件夹和 `.targets` 文件的情况下设置生成。 它还演示如何在 Team Foundation Service 上为此示例项目设置自动化生成。

## <a name="repository-structure"></a>存储库结构

演示项目是一个使用命令行参数来查询必应的简单命令行工具。 它面向 .NET Framework 4 并使用多种 [BCL 包](http://www.nuget.org/profiles/dotnetframework/)（[Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http)、[Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl)、[Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async) 和 [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)）。

存储库结构如下所示：

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

可以看见我们既未签入 `packages` 文件夹，也未签入任何 `.targets` 文件。

但我们签入了 `nuget.exe`，因为生成过程中需要它。 我们遵循广泛使用的约定，在共享的 `tools` 文件夹中签入它。

源代码位于 `src` 文件夹下。 虽然我们的演示仅使用单个解决方案，但是不难想象此文件夹包含不止一个解决方案。

### <a name="ignore-files"></a>忽略文件

> [!Note]
> [NuGet 客户端当前存在一个已知 bug](https://nuget.codeplex.com/workitem/4072)，它导致客户端依然将 `packages` 文件夹添加到版本控制。 一种解决方法是禁用源代码管理集成。 为了做到这一点，与解决方案并行的 `.nuget` 文件夹中需要一个 `Nuget.Config ` 文件。 如果此文件夹尚不存在，请先创建一个。 在 [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md) 中，添加以下内容：

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

为了与不希望签入**包**文件夹的版本控制进行通信，我们还为 git (`.gitignore`) 和 TF 版本控制 (`.tfignore`) 添加了忽略文件。 这些文件描述不希望签入的文件模式。

`.gitignore` 文件如下所示：

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

`.gitignore` 文件[非常强大](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html)。 例如，如果需要通常情况下不签入 `packages` 文件夹的内容，但需要遵循之前有关签入 `.targets` 文件的指南，则可以替换为以下规则：

    packages
    !packages/**/*.targets

这将排除所有 `packages` 文件夹，但会重新包含所有包含的 `.targets` 文件。 顺便说一下，可以[在此](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)找到专门针对 Visual Studio 开发人员需求定制的 `.gitignore` 文件模板。

TF 版本控制通过 [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) 文件支持相似的机制。 语法几乎是相同的：

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a>build.proj

为进行演示，我们将生成过程控制到相当简单。 我们将创建一个 MSBuild 项目来生成所有包，同时确保在生成解决方案之前还原包。

此项目将有三个常规目标（`Clean`、`Build` 和 `Rebuild`），以及一个新目标 `RestorePackages`。

- `Build` 和 `Rebuild` 目标均依赖于 `RestorePackages`。 这将确保你可以运行 `Build` 和 `Rebuild`，并依赖于要还原的包。
- `Clean`、`Build` 和 `Rebuild` 调用所有解决方案文件上的相应 MSBuild 目标。
- `RestorePackages` 目标调用每个解决方案文件的 `nuget.exe`。 这通过使用 [MSBuild 批处理功能](/visualstudio/msbuild/msbuild-batching)完成。

结果如下所示：

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a>配置 Team Build

Team Build 提供不同的过程模板。 我们使用 Team Foundation Service 进行本演示。 但 TFS 的本地安装将非常相似。

Git 和 TF 版本控制有不同的 Team Build 模板，因此以下步骤将随着使用的版本控制系统变化。 在这两种情况下，只需选择 build.proj 作为需要生成的项目。

我们先来看看适用于 git 的过程模板。 在基于 git 的模板中，通过 `Solution to build` 属性选择生成：

![适用于 git 的生成过程](media/PackageRestoreTeamBuildGit.png)

请注意，此属性是在存储库中的一个位置。 由于 `build.proj` 位于根目录中，因此只需使用 `build.proj`。 如果将生成文件放在名为 `tools` 的文件夹下，该值将为 `tools\build.proj`。

在 TF 版本控制模板中，通过 `Projects` 属性选择项目：

![适用于 TFVC 的生成过程](media/PackageRestoreTeamBuildTFVC.png)

与基于 git 的模板不同，TF 版本控制支持选取器（右侧带三个点的按钮）。 因此，我们建议使用它们来选择项目，以避免任何键入错误。
