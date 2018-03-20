---
title: "对 Visual Studio 中的 NuGet 包还原进行故障排除 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "介绍 Visual Studio 中常见的 NuGet 还原错误以及相应的故障排除方法。"
keywords: "NuGet 包还原, 还原包, 故障排除, 故障排除"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-package-restore-errors"></a>包还原错误疑难解答

本文着重介绍还原包时遇到的常见错误以及相应的解决步骤。 有关还原包的完整详细信息，请参阅[包还原](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)。

如果此处的说明对你没有帮助，[请在 GitHub 上提交问题](https://github.com/NuGet/docs.microsoft.com-nuget/issues)，以便我们可以更仔细地检查你的情况。 请勿使用可能出现在该页面上的“此页面有帮助吗?”控件， 因为它无法让我们与你联系以获取详细信息。

## <a name="quick-solution-for-visual-studio-users"></a>适用于 Visual Studio 用户的快速解决方案

如果使用 Visual Studio，请首先按如下方式启用包还原。 否则，请继续执行后面的部分。

1. 选择“工具”>“NuGet 包管理器”>“包管理器设置”菜单命令。
1. 在“包还原”下设置这两个选项。
1. 选择“确定”。
1. 再次生成项目。

![在“工具”/“选项”中启用 NuGet 包还原](../consume-packages/media/restore-01-autorestoreoptions.png)

也可以在 `NuGet.config` 文件中更改这些设置；请参阅[同意](#consent)部分。

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>此项目引用了此计算机上缺少的 NuGet 程序包

完整错误消息：

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

当你尝试生成包含对一个或多个 NuGet 包的引用的项目，但这些包当前未缓存在项目中时，发生了此错误。 （如果项目使用 `packages.config`，则将包缓存在解决方案根目录的 `packages` 文件夹中；或者如果项目使用 PackageReference 格式，则将其缓存到 `obj/project.assets.json` 文件中。）

当你从源代码管理或其他下载获得项目的源代码时，通常会发生这种情况。 包通常从源代码管理或下载中省略，因为它们可以从包源（例如 nuget.org）中还原（请参阅[包和源代码管理](Packages-and-Source-Control.md)）。 否则，包含它们会导致存储库膨胀或创建不必要的大型 .zip 文件。

使用下列方法之一还原包：

- 在 Visual Studio 中，通过以下方法启用包还原：选择“工具”>“NuGet 包管理器”>“包管理器设置”菜单命令，在“包还原”下设置这两个选项，然后选择“确定”。 然后再次生成解决方案。
- 对于 .NET Core 项目，运行 `dotnet restore` 或 `dotnet build`（它会自动运行还原）。
- 在命令行上运行 `nuget restore`（使用 `dotnet` 创建的项目除外，这种情况下请使用 `dotnet restore`）。
- 在包含使用 PackageReference 格式的项目的命令行上，运行 `msbuild /t:restore`。

成功还原后，应会看到 `packages` 文件夹（使用 `packages.config` 时）或 `obj/project.assets.json` 文件（使用 PackageReference 时）。 该项目现在应能成功生成。 如果没有，请[在 GitHub 上提交问题](https://github.com/NuGet/docs.microsoft.com-nuget/issues)，以便我们跟进。

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>找不到资产文件 project.assets.json

完整错误消息：

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

此错误出现的原因与[上一部分](#missing)中所述的原因相同，并具有相同的补救措施。 例如，在从源代码管理获取的 .NET Core 项目上运行 `msbuild` 不会自动还原包。 在这种情况下，请运行 `msbuild /t:restore`，然后运行 `msbuild`，或使用 `dotnet build`（它会自动还原包）。

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

请注意，如果直接在 `nuget.config` 中编辑 `packageRestore` 设置，请重启 Visual Studio，以便“选项”对话框显示当前值。

## <a name="other-potential-conditions"></a>其他潜在条件

- 由于缺少文件，你可能会遇到生成错误，并看到提示使用 NuGet 还原来下载它们的消息。 但是，运行还原时可能会出现：“所有包都已安装，无可还原项。” 在这种情况下，请删除 `packages` 文件夹（使用 `packages.config` 时）或 `obj/project.assets.json` 文件（使用 PackageReference 时）并再次运行还原。

- 从源代码管理获取项目时，项目文件夹可能设置为只读。 更改文件夹权限并尝试重新还原包。

- 你可能使用了旧版本的 NuGet。 请访问 [ nuget.org/downloads](https://www.nuget.org/downloads) 了解最新建议版本。 对于 Visual Studio 2015，建议使用 3.6.0。

如果遇到其他问题，请[在 GitHub 上提交问题](https://github.com/NuGet/docs.microsoft.com-nuget/issues)，以便我们获得更多详细信息。