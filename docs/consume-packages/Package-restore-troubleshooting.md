---
title: 对 Visual Studio 中的 NuGet 包还原进行故障排除
description: 介绍 Visual Studio 中常见的 NuGet 还原错误以及相应的故障排除方法。
author: JonDouglas
ms.author: jodou
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 0bd14104695a15d2e4c65a13b271143809c4ba8a
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323617"
---
# <a name="troubleshooting-package-restore-errors"></a>包还原错误疑难解答

本文着重介绍还原包时遇到的常见错误以及相应的解决步骤。 

程序包还原试图将所有程序包依赖项安装到与项目文件 (.csproj  ) 或 packages.config  文件中的程序包引用匹配的相应状态。 （在 Visual Studio 中，这些引用位于解决方案资源管理器的“依赖项 \ NuGet”或“引用”节点中。）   请参阅[还原程序包](../consume-packages/package-restore.md#restore-packages)，以按照要求的步骤还原程序包。 若项目文件 (.csproj  ) 或 packages.config  文件中的程序包引用不正确（它们与使用程序包还原时所需的状态不匹配），则不要使用程序包还原，而需要安装或更新程序包。

如果此处的说明对你没有帮助，[请在 GitHub 上提交问题](https://github.com/NuGet/docs.microsoft.com-nuget/issues)，以便我们可以更仔细地检查你的情况。 请勿使用可能出现在该页面上的“此页面有帮助吗?”控件， 因为它无法让我们与你联系以获取详细信息。

## <a name="quick-solution-for-visual-studio-users"></a>适用于 Visual Studio 用户的快速解决方案

如果使用 Visual Studio，请首先按如下方式启用包还原。 否则，请继续执行后面的部分。

1. 选择“工具”>“NuGet 包管理器”>“包管理器设置”菜单命令  。
1. 在“包还原”下设置这两个选项  。
1. 选择“确定”  。
1. 再次生成项目。

![在“工具”/“选项”中启用 NuGet 包还原](../consume-packages/media/restore-01-autorestoreoptions.png)

也可以在 `NuGet.Config` 文件中更改这些设置；请参阅[同意](#consent)部分。 如果项目是使用集成 MSBuild 的包恢复的较老项目，那么可能需要[迁移](package-restore.md#migrate-to-automatic-package-restore-visual-studio)到自动包恢复。

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>此项目引用了此计算机上缺少的 NuGet 程序包

完整错误消息：

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

当你尝试生成包含对一个或多个 NuGet 包的引用的项目，但这些包当前未安装在计算机上或项目中时，发生了此错误。

- 使用 [PackageReference](package-references-in-project-files.md) 管理格式时，此错误可能是在将 packages.config 迁移到 PackageReference 时遗留下来的，需要从项目文件中[手动删除](/nuget/resources/nuget-faq#working-with-packages)。
- 当使用 [packages.config](../reference/packages-config.md) 时，此错误意味着程序包未安装在解决方案根目录中的 `packages` 文件夹中。

当你从源代码管理或其他下载获得项目的源代码时，通常会发生这种情况。 包通常从源代码管理或下载中省略，因为它们可以从包源（例如 nuget.org）中还原（请参阅[包和源代码管理](Packages-and-Source-Control.md)）。 否则，包含它们会导致存储库膨胀或创建不必要的大型 .zip 文件。

如果项目文件包含包位置的绝对路径，并移动项目，也会发生该错误。

使用下列方法之一还原包：

- 如果已移动项目文件，请直接编辑该文件以更新包引用。
- [Visual Studio](package-restore.md#restore-using-visual-studio)（[自动还原](package-restore.md#restore-packages-automatically-using-visual-studio)或[手动还原](package-restore.md#restore-packages-manually-using-visual-studio)）
- [dotnet CLI](package-restore.md#restore-using-the-dotnet-cli)
- [nuget.exe CLI](package-restore.md#restore-using-the-nugetexe-cli)
- [MSBuild](package-restore.md#restore-using-msbuild)
- [Azure Pipelines](package-restore.md#restore-using-azure-pipelines)
- [Azure DevOps Server](package-restore.md#restore-using-azure-devops-server)

成功还原后，包应显示在 global-packages  文件夹中。 对于使用 PackageReference 的项目，还原应重新创建 `obj/project.assets.json` 文件；对于使用 `packages.config` 的项目，包应显示在项目的 `packages` 文件夹中。 该项目现在应能成功生成。 如果没有，请[在 GitHub 上提交问题](https://github.com/NuGet/docs.microsoft.com-nuget/issues)，以便我们跟进。

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>找不到资产文件 project.assets.json

完整错误消息：

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

`project.assets.json` 文件在使用 PackageReference 管理格式时维护项目的依赖项关系图，用于确保在计算机上安装了所有必需的包。 由于此文件是通过包还原动态生成的，它通常不添加到源代码管理中。 因此，该错误在使用工具生成项目时出现，例如，不自动还原包的 `msbuild`。

在这种情况下，请运行 `msbuild -t:restore`，然后运行 `msbuild`，或使用 `dotnet build`（它会自动还原包）。 也可以使用[上一节](#missing)中的任一包还原方法。

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>由于尚未获得同意，需要还原的一个或多个 NuGet 包无法进行还原

完整错误消息：

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

此错误表示你在 NuGet 配置中禁用了包还原。

可按照前文[适用于 Visual Studio 用户的快速解决方案](#quick-solution-for-visual-studio-users)中所述来更改 Visual Studio 中的适用设置。

也可以直接在适用的 `nuget.config` 文件中编辑这些设置（通常，Windows 上为 `%AppData%\NuGet\NuGet.Config`，Mac/Linux 上为 `~/.nuget/NuGet/NuGet.Config`）。 确保将 `packageRestore` 下的 `enabled` 和 `automatic` 键设置为 True：

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> 如果直接在 `nuget.config` 中编辑 `packageRestore` 设置，请重启 Visual Studio，以便“选项”对话框显示当前值。

## <a name="other-potential-conditions"></a>其他潜在条件

- 由于缺少文件，你可能会遇到生成错误，并看到提示使用 NuGet 还原来下载它们的消息。 但是，运行还原时可能会出现：“所有包都已安装，无可还原项。” 在这种情况下，请删除 `packages` 文件夹（使用 `packages.config` 时）或 `obj/project.assets.json` 文件（使用 PackageReference 时）并再次运行还原。 如果错误仍然存在，请使用命令行中的 `nuget locals all -clear` 或 `dotnet nuget locals all --clear` 以清除 global-packages  文件夹和缓存文件夹，如[管理全局包和缓存文件夹](managing-the-global-packages-and-cache-folders.md)中所述。

- 从源代码管理获取项目时，项目文件夹可能设置为只读。 更改文件夹权限并尝试重新还原包。

- 你可能使用了旧版本的 NuGet。 请访问 [ nuget.org/downloads](https://www.nuget.org/downloads) 了解最新建议版本。 对于 Visual Studio 2015，建议使用 3.6.0。

如果遇到其他问题，请[在 GitHub 上提交问题](https://github.com/NuGet/docs.microsoft.com-nuget/issues)，以便我们获得更多详细信息。
