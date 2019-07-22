---
title: NuGet 包还原
description: 概述 NuGet 如何还原项目依赖的包，包括如何禁用还原和约束版本。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: e85d8cc3fd9492118bd8f34cfd05f20a9724c281
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842343"
---
# <a name="package-restore-options"></a>包还原选项

为了促成更干净的开发环境并减少存储库大小，NuGet“包还原”安装在项目文件或 `packages.config` 中列出的所有项目依赖项  。 .NET Core 2.0+ `dotnet build` 和 `dotnet run` 命令执行自动包还原。 Visual Studio 可以在构建项目时自动还原包，并且你可以随时通过 Visual Studio、`nuget restore`、`dotnet restore` 和 xoild 在 Mono 上还原包。

包还原确保所有项目的依赖项都可用，无需将其存储在源代码管理中。 要配置源代码管理存储库以排除包二进制文件，请参阅[包和源代码管理](../consume-packages/packages-and-source-control.md)。 

## <a name="package-restore-overview"></a>包还原概述

包还原首先根据需要安装项目的直接依赖项，然后在整个依赖项关系图中安装这些包的所有依赖项。

如果尚未安装包，NuGet 首先尝试从[缓存](../consume-packages/managing-the-global-packages-and-cache-folders.md)中检索它。 如果包不在缓存中，NuGet 将尝试从 Visual Studio 的“工具” > “选项” > “NuGet 包管理器” > “包源”下的列表中的所有已启用的源下载包     。 在还原期间，NuGet 会忽略包源的顺序，使用来自任何首先响应请求的源的包。 有关 NuGet 的行为方式的详细信息，请参阅[常见的 NuGet 配置](Configuring-NuGet-Behavior.md)。 

> [!Note]
> 在检查完所有源之前，NuGet 不会指示包还原失败。 届时，NuGet 仅会报告列表中最后一个源的失败。 该错误说明包已不在其他任意源上，尽管那些源中的任何一个都没有单独显示错误  。

## <a name="restore-packages"></a>还原包

可以通过以下任一方式触发包还原：

- **Visual Studio**：在 Windows 上的 Visual Studio 中，使用以下方法之一。

    - 自动还原包。 当根据[启用和禁用包还原](#enable-and-disable-package-restore-visual-studio)中的选项，从模板创建项目或生成项目时会自动执行包还原。 此外，在 NuGet 4.0+ 中，对 SDK 样式的项目（通常是 .NET Core 或 .NET Standard 项目）进行更改时还会自动进行还原。

    - 手动还原包。 要手动还原，请右键单击解决方案资源管理器中的解决方案，选择“还原 NuGet 包”   。 如果仍未正确安装一个或多个单独的包，“解决方案资源管理器”会显示错误图标  。 右键单击并选择“管理 NuGet 包”，然后使用“包管理器”卸载并重新安装受影响的包   。 有关详细信息，请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md)

    如果看到错误“此项目引用此计算机上缺少的 NuGet 包”或者“一个或更多 NuGet 包需要还原但无法还原，因为未授予许可”，则[启用自动还原](#enable-and-disable-package-restore-visual-studio)。 此外，请参阅[迁移到自动包还原](#migrate-to-automatic-package-restore-visual-studio)和[包还原故障排除](Package-restore-troubleshooting.md)。

- **dotnet CLI**：在命令行中，切换到包含项目的文件夹，然后使用 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 命令还原带有 [PackageReference](../consume-packages/package-references-in-project-files.md) 的项目文件中列出的包。 如果为 .NET Core 2.0 和更高版本，使用 `dotnet build` 和 `dotnet run` 命令可以自动进行还原。  

- **nuget.exe CLI**：在命令行中，切换到包含项目的文件夹，然后使用 [nuget restore](../tools/cli-ref-restore.md) 命令还原项目或解决方案文件或 `packages.config` 中列出的包。 

- **MSBuild**：使用 [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) 命令通过 PackageReference 还原项目文件中列出的包。 此命令仅适用于 Visual Studio 2017 及更高版本附带的 NuGet 4.x+ 和 MSBuild 15.1+。 `nuget restore` 和 `dotnet restore` 均对适用项目使用此命令。

- **Azure Pipelines**：在 Azure Pipelines 上创建生成定义时，请在任意生成任务前将 NuGet [还原](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) 或 .NET Core [还原](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) 任务包括在定义中。 默认情况下，某些生成模板包括还原任务。

- **Azure DevOps Server**：如果你使用的是 TFS 2013 或更高版本的 Team Build 模板，Azure DevOps Server 和 TFS 2013 及更高版本会在生成期间自动还原包。 对于较早的 TFS 版本，可以包含一个生成步骤来运行命令行还原选项，或者选择将生成模板迁移到更高版本。 有关详细信息，请参阅[使用 Team Foundation Build 设置包还原](../consume-packages/team-foundation-build.md)。

## <a name="enable-and-disable-package-restore-visual-studio"></a>启用和禁用包还原 (Visual Studio)

在 Visual Studio 中，主要通过“工具” > “选项” > “NuGet 包管理器”控制包还原    ：

![通过 NuGet 包管理器选项控制包还原](media/Restore-01-AutoRestoreOptions.png)

- “允许 NuGet 下载缺失的包”通过更改 `NuGet.Config` 文件中的 [packageRestore 部分](../reference/nuget-config-file.md#packagerestore-section)的 `packageRestore/enabled` 设置控制包还原的所有窗体（该文件在 Windows 上位于 `%AppData%\NuGet\`，在 Mac/Linux 上位于 `~/.nuget/NuGet/`）  。 在 Visual Studio 中，此设置还可启用解决方案上下文菜单中的 Restore NuGet Packages 命令  。

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

要为计算机上的所有用户启用或禁用包还原，开发人员或公司可以将配置设置添加到全局 `nuget.config` 文件。 全局 `nuget.config` 在 Windows 中位于 `%ProgramData%\NuGet\Config` 下，有时在特定的 `\{IDE}\{Version}\{SKU}\`Visual Studio 文件夹下，或者在 Mac/Linux 中位于 `~/.local/share` 下。 然后，各个用户可以按照项目级别的要求有选择地启用还原。 有关 NuGet 如何设置多个配置文件优先级的详细信息，请参阅[常见 NuGet 配置](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。

> [!Important]
> 如果直接在 `nuget.config` 中编辑 `packageRestore` 设置，请重启 Visual Studio，以便“选项”对话框显示当前值  。

## <a name="constrain-package-versions-with-restore"></a>使用还原约束包版本

NuGet 通过任意方法还原包时，将遵守你在 `packages.config` 或项目文件中指定的任何约束：

- 在 `packages.config` 中，可在依赖项的 `allowedVersion` 属性中指定版本范围。 有关详细信息，请参阅[约束升级版本](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)。 例如:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- 在项目文件中，可以使用 PackageReference 直接指定依赖项的范围。 例如:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

在所有情况下，都使用[包版本控制](../reference/package-versioning.md)中介绍的表示法。

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

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>迁移到自动包还原 (Visual Studio)

对于 NuGet 2.6 及更早版本，以前支持集成 MSBuild 的包恢复，但现在不再支持。 （通常通过右键单击 Visual Studio 中的解决方案并选择“启用 NuGet 包还原”  来启用）。 如果项目使用已弃用的集成 MSBuild 的包还原，请迁移到自动包还原。

使用集成 MSBuild 的包还原的项目通常包含带有三个文件的 .nuget  文件夹：NuGet.config  、nuget.exe  和 NuGet.targets  。 若存在 NuGet.targets  文件，将确定 NuGet 是否将继续使用集成 MSBuild 的方法，因此在迁移期间必须删除此文件。

要迁移到自动包还原，请执行以下操作：

1. 关闭 Visual Studio。
2. 删除 .nuget/nuget.exe  和 .nuget/NuGet.targets  。
3. 对于每个项目文件，删除 `<RestorePackages>` 元素并删除对 NuGet.targets  的任何引用。

要测试自动包还原，请执行以下操作：

1. 删除解决方案中的“packages”文件夹  。
2. 在 Visual Studio 中打开解决方案并开始生成。

   自动包还原应下载并安装每个依赖包，而不将它们添加到源代码管理中。

## <a name="troubleshooting"></a>疑难解答

请参阅[包还原疑难解答](package-restore-troubleshooting.md)。
