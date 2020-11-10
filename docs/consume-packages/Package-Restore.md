---
title: NuGet 程序包还原
description: 概述 NuGet 如何还原项目依赖的包，包括如何禁用还原和约束版本。
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: 0edfa1f61e6b18ef38689ed2272b2c5992a46ae6
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237843"
---
# <a name="restore-packages-using-package-restore"></a>使用“程序包还原”还原程序包

为了促成更干净的开发环境并减少存储库大小，NuGet“程序包还原”安装了项目文件或 `packages.config` 中列出的所有项目依赖项  。 .NET Core 2.0+ `dotnet build` 和 `dotnet run` 命令执行自动程序包还原。 Visual Studio 可以在构建项目时自动还原包，并且你可以随时通过 Visual Studio、`nuget restore`、`dotnet restore` 和 Mono 的 xbuild 来还原包。

程序包还原确保所有项目的依赖项都可用，无需将其存储在源代码管理中。 要配置源代码管理存储库以排除包二进制文件，请参阅[包和源代码管理](../consume-packages/packages-and-source-control.md)。 

## <a name="package-restore-overview"></a>程序包还原概述

程序包还原首先根据需要安装项目的直接依赖项，然后在整个依赖项关系图中安装这些包的所有依赖项。

如果尚未安装包，NuGet 首先尝试从[缓存](../consume-packages/managing-the-global-packages-and-cache-folders.md)中检索它。 如果包不在缓存中，NuGet 将尝试从 Visual Studio 的“工具” > “选项” > “NuGet 包管理器” > “包源”下的列表中的所有已启用的源下载包     。 在还原期间，NuGet 会忽略包源的顺序，使用来自最先响应请求的源的包。 有关 NuGet 的行为方式的详细信息，请参阅[常见的 NuGet 配置](Configuring-NuGet-Behavior.md)。 

> [!Note]
> 在检查完所有源之前，NuGet 不会指示包还原失败。 届时，NuGet 仅会报告列表中最后一个源的失败。 该错误说明包已不在其他任意源上，尽管没有单独显示这些源的错误。 

## <a name="restore-packages"></a>还原包

程序包还原试图将所有程序包依赖项安装到与项目文件 (.csproj  ) 或 packages.config  文件中的程序包引用相匹配的正确状态。 （在 Visual Studio 中，这些引用位于解决方案资源管理器的“依赖项 \ NuGet”或“引用”节点中。）  

1. 若项目文件中的程序包引用正确，则使用你的首选工具还原程序包。

   - [Visual Studio](#restore-using-visual-studio)（[自动还原](#restore-packages-automatically-using-visual-studio)或[手动还原](#restore-packages-manually-using-visual-studio)）
   - [dotnet CLI](#restore-using-the-dotnet-cli)
   - [nuget.exe CLI](#restore-using-the-nugetexe-cli)
   - [MSBuild](#restore-using-msbuild)
   - [Azure Pipelines](#restore-using-azure-pipelines)
   - [Azure DevOps Server](#restore-using-azure-devops-server)

   若项目文件 (.csproj  ) 或 packages.config  文件中的程序包引用不正确（它们与使用程序包还原时所需的状态不匹配），则需要安装或更新程序包。

   对于使用 PackageReference 的项目，在成功还原后，global-packages 文件夹应显示此包，并且会重新创建 `obj/project.assets.json` 文件。  对于使用 `packages.config` 的项目，项目的 `packages` 文件夹应显示此程序包。 该项目现在应能成功生成。 

2. 运行程序包还原后，若仍出现程序包缺失的情况或与程序包相关的错误（如 Visual Studio 的解决方案资源管理器中出现错误图标），可能需要按照[程序包还原错误疑难解答](package-restore-troubleshooting.md)中的步骤操作，或[重新安装和更新程序包](../consume-packages/reinstalling-and-updating-packages.md)。

   Visual Studio 中的程序包管理器控制台提供了多个灵活的选项，用于重新安装程序包。 请参阅[使用 Package-Update](reinstalling-and-updating-packages.md#using-update-package)。

## <a name="restore-using-visual-studio"></a>使用 Visual Studio 进行还原

在 Windows 上的 Visual Studio 中：

- 自动还原程序包，或

- 手动还原程序包

### <a name="restore-packages-automatically-using-visual-studio"></a>使用 Visual Studio 自动还原程序包

从模板创建项目或生成项目时，是否自动执行程序包还原取决于[启用和禁用程序包还原](#enable-and-disable-package-restore-in-visual-studio)中的选项。 此外，在 NuGet 4.0+ 中，对 SDK 样式的项目（通常是 .NET Core 或 .NET Standard 项目）进行更改时还会自动进行还原。

1. 按照以下方式启用自动程序包还原：选择“工具” > “选项” > “NuGet 程序包管理器”，然后在“程序包还原”下选择“在 Visual Studio 中生成期间自动检查缺少的程序包”。     

   对于非 SDK 样式项目，首先需要选择“允许 NuGet 下载缺少的程序包”，以启动自动还原选项。 

1. 生成项目。

   如果仍未正确安装一个或多个单独的包，“解决方案资源管理器”会显示错误图标  。 右键单击并选择“管理 NuGet 包”，然后使用“包管理器”卸载并重新安装受影响的包   。 有关详细信息，请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md)。

   如果看到错误“此项目引用此计算机上缺少的 NuGet 包”或者“一个或更多 NuGet 包需要还原但无法还原，因为未授予许可”，则[启用自动还原](#enable-and-disable-package-restore-in-visual-studio)。 对于旧项目，亦请参阅[迁移到自动程序包还原](#migrate-to-automatic-package-restore-visual-studio)。 另请参阅[程序包还原疑难解答](Package-restore-troubleshooting.md)。

### <a name="restore-packages-manually-using-visual-studio"></a>使用 Visual Studio 手动还原程序包

1. 选择“工具” > “选项” > “NuGet 程序包管理器”，以启用程序包还原。    在“程序包还原”选项下，选择“允许 NuGet 下载缺少的程序包”。  

1. 在“解决方案资源管理器”中，右键单击解决方案并选择“还原 NuGet 程序包”   。

   如果仍未正确安装一个或多个单独的包，“解决方案资源管理器”会显示错误图标  。 右键单击并选择“管理 NuGet 程序包”，然后使用“程序包管理器”卸载并重新安装受影响的程序包   。 有关详细信息，请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md)。

   如果看到错误“此项目引用此计算机上缺少的 NuGet 包”或者“一个或更多 NuGet 包需要还原但无法还原，因为未授予许可”，则[启用自动还原](#enable-and-disable-package-restore-in-visual-studio)。 对于旧项目，亦请参阅[迁移到自动程序包还原](#migrate-to-automatic-package-restore-visual-studio)。 另请参阅[程序包还原疑难解答](Package-restore-troubleshooting.md)。

### <a name="enable-and-disable-package-restore-in-visual-studio"></a>在 Visual Studio 中启用和禁用程序包还原

在 Visual Studio 中，主要通过“工具” > “选项” > “NuGet 包管理器”控制程序包还原    ：

![通过 NuGet 包管理器选项控制程序包还原](media/Restore-01-AutoRestoreOptions.png)

- “允许 NuGet 下载缺失的包”通过更改 `NuGet.Config` 文件中的 [packageRestore 部分](../reference/nuget-config-file.md#packagerestore-section)的 `packageRestore/enabled` 设置，控制程序包还原的所有窗体（该文件在 Windows 上位于 `%AppData%\NuGet\`，在 Mac/Linux 上位于 `~/.nuget/NuGet/`）  。 在 Visual Studio 中，此设置还可启用解决方案上下文菜单中的 Restore NuGet Packages 命令  。

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    
  > [!Note]
  > 要全局重写 `packageRestore/enabled` 设置，请在启动 Visual Studio 或启动生成之前，将 EnableNuGetPackageRestore 环境变量设为 TRUE 或 FALSE 值  。

- “生成期间在 Visual Studio 中自动检查缺失的包”通过更改 `NuGet.Config` 文件的 [packageRestore 部分](../reference/nuget-config-file.md#packagerestore-section)中的 `packageRestore/automatic` 设置控制自动还原  。 将该选项设置为 True 后，从 Visual Studio 运行生成会自动还原任何缺失的包。 此设置不会影响从 MSBuild 命令行运行的生成。

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

要为计算机上的所有用户启用或禁用程序包还原，开发人员或公司可以将配置设置添加到全局 `nuget.config` 文件。 全局 `nuget.config` 在 Windows 中位于 `%ProgramData%\NuGet\Config` 下，有时在特定的 `\{IDE}\{Version}\{SKU}\`Visual Studio 文件夹下，或者在 Mac/Linux 中位于 `~/.local/share` 下。 然后，各个用户可以按照项目级别的要求有选择地启用还原。 有关 NuGet 如何设置多个配置文件优先级的详细信息，请参阅[常见 NuGet 配置](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。

> [!Important]
> 如果直接在 `nuget.config` 中编辑 `packageRestore` 设置，请重启 Visual Studio，以便“选项”对话框显示当前值  。

### <a name="choose-default-package-management-format"></a>选择默认包管理格式

![通过 NuGet 包管理器选项控制默认包管理格式](media/Restore-02-PackageFormatOptions.png)

NuGet 提供项目可使用包的两种格式：[`PackageReference`](package-references-in-project-files.md) 和 [`packages.config`](../reference/packages-config.md)。 默认格式可从“包管理”标题下的下拉菜单中选择  。 在项目中安装首个包时还会出现一个提示选项。

> [!Note]
> 如果这两种包管理格式均不受项目支持，则会使用与项目兼容的包管理格式，因此所用格式可能并非选项中的默认设置。 此外，NuGet 不会在安装首个包时显示选择提示，即使选项窗口中已选中此选项时亦是如此。
>
> 如果使用包管理器控制台在项目中安装首个包，则即使选项窗口中已选中该选项，NuGet 也不会提示选择格式。

## <a name="restore-using-the-dotnet-cli"></a>使用 dotnet CLI 进行还原

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]

> [!IMPORTANT]
> 若要将缺少的程序包引用添加到项目文件，请使用 [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x)，它也会运行 `restore` 命令。

## <a name="restore-using-the-nugetexe-cli"></a>使用 nuget.exe CLI 进行还原

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

> [!IMPORTANT]
> `restore` 命令不会修改项目文件或 packages.config。  要添加依赖项，请通过 Visual Studio 中的包管理器 UI 或控制台添加包，或修改 packages.config  ，然后运行 `install` 或 `restore`。

## <a name="restore-using-msbuild"></a>使用 MSBuild 进行还原

使用 [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) 命令还原项目文件中通过 PackageReference 列出的程序包。 此命令仅适用于 Visual Studio 2017 及更高版本附带的 NuGet 4.x+ 和 MSBuild 15.1+。 `nuget restore` 和 `dotnet restore` 均对适用项目使用此命令。

1. 打开开发人员命令提示符（在“搜索”框中，键入“开发人员命令提示符”）   。

   用户通常习惯从“开始”菜单中启动“适用于 Visual Studio 的开发人员命令提示符”，因为它将使用 MSBuild 的所有必需路径进行配置  。

2. 切换到包含项目文件的文件夹，然后键入以下命令。

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

3. 键入以下命令以重新生成项目。

   ```cmd
   msbuild
   ```

   确保 MSBuild 输出指示生成已成功完成。
   
> [!Note]
> msbuild 具有 `-restore` 开关，它将运行 `Restore`、重载项目，然后生成。 请参阅[使用一个 MSBuild 命令来还原和生成](/nuget/reference/msbuild-targets#restoring-and-building-with-one-msbuild-command)。

```cmd
# Will restore the project, then build, since build is the default target.
msbuild -restore
```

## <a name="restore-using-azure-pipelines"></a>使用 Azure Pipelines 进行还原

在 Azure Pipelines 上创建生成定义时，请在任意生成任务前将 NuGet [还原](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) 或 .NET Core [还原](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) 任务包括在定义中。 默认情况下，某些生成模板包括还原任务。

## <a name="restore-using-azure-devops-server"></a>使用 Azure DevOps Server 进行还原

如果你使用的是 TFS 2013 或更高版本的 Team Build 模板，Azure DevOps Server 和 TFS 2013 及更高版本会在生成期间自动还原包。 对于较早的 TFS 版本，可以包含一个生成步骤来运行命令行还原选项，或者选择将生成模板迁移到更高版本。 有关详细信息，请参阅[使用 Team Foundation Build 设置程序包还原](../consume-packages/team-foundation-build.md)。

## <a name="constrain-package-versions-with-restore"></a>使用还原约束包版本

NuGet 通过任意方法还原包时，将遵守你在 `packages.config` 或项目文件中指定的任何约束：

- 在 `packages.config` 中，可在依赖项的 `allowedVersion` 属性中指定版本范围。 有关详细信息，请参阅[约束升级版本](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)。 例如：

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- 在项目文件中，可以使用 PackageReference 直接指定依赖项的范围。 例如：

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

在所有情况下，都使用[包版本控制](../concepts/package-versioning.md)中介绍的表示法。

## <a name="force-restore-from-package-sources"></a>强制从包源还原

默认情况下，NuGet 还原操作使用 global-packages 和 http-cache 文件夹中的包，如[管理全局包和缓存文件夹](managing-the-global-packages-and-cache-folders.md)中所述   。

若要避免使用 global-packages  文件夹，请执行下列操作之一：

- 使用 `nuget locals global-packages -clear` 或 `dotnet nuget locals global-packages --clear` 清除文件夹。
- 在进行还原操作之前，使用下列方法之一暂时更改 global-packages 的位置  ：
  - 将 NUGET_PACKAGES 环境变量设置为其他文件夹。
  - 创建 `NuGet.Config` 文件，将 `globalPackagesFolder`（如果使用 PackageReference）或 `repositoryPath`（如果使用 `packages.config`）设置为其他文件夹。 有关详细信息，请参阅[配置设置](../reference/nuget-config-file.md#config-section)。
  - 仅限 MSBuild：指定具有 `RestorePackagesPath` 属性的其他文件夹。

若要避免将缓存用于 HTTP 源，请执行下列操作之一：

- 将 `-NoCache` 选项与 `nuget restore` 结合使用，或者将 `--no-cache` 选项与 `dotnet restore` 结合使用。 这些选项不会影响通过 Visual Studio 包管理器或控制台执行的还原操作。
- 使用 `nuget locals http-cache -clear` 或 `dotnet nuget locals http-cache --clear` 清除缓存。
- 暂时将 NUGET_HTTP_CACHE_PATH 环境变量设置为其他文件夹。

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>迁移到自动程序包还原 (Visual Studio)

对于 NuGet 2.6 及更早版本，以前支持集成 MSBuild 的包恢复，但现在不再支持。 （通常通过右键单击 Visual Studio 中的解决方案并选择“启用 NuGet 程序包还原”  来启用）。 如果项目使用已弃用的集成 MSBuild 的程序包还原，请迁移到自动程序包还原。

使用集成 MSBuild 的程序包还原的项目通常包含带有三个文件的 .nuget  文件夹：NuGet.config  、nuget.exe  和 NuGet.targets  。 NuGet.targets 文件的存在与否决定了 NuGet 是否继续使用集成 MSBuild 的方法，因此在迁移期间必须删除此文件。

要迁移到自动程序包还原，请执行以下操作：

1. 关闭 Visual Studio。
2. 删除 .nuget/nuget.exe  和 .nuget/NuGet.targets  。
3. 对于每个项目文件，删除 `<RestorePackages>` 元素并删除对 NuGet.targets  的任何引用。

要测试自动程序包还原，请执行以下操作：

1. 删除解决方案中的“packages”文件夹  。
2. 在 Visual Studio 中打开解决方案并开始生成。

   自动程序包还原应下载并安装每个依赖包，而不将它们添加到源代码管理中。

## <a name="troubleshooting"></a>疑难解答

请参阅[程序包还原疑难解答](package-restore-troubleshooting.md)。
