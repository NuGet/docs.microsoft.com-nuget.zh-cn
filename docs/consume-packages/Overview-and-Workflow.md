---
title: 使用 NuGet 包的概述和工作流
description: 概述在项目中使用 NuGet 包的流程，其中提供该流程其他特定部分的链接。
author: karann-msft
ms.author: karann
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: eeae62a09a9f405d27cd113ff586393f6305ba47
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426715"
---
# <a name="package-consumption-workflow"></a>包使用工作流

在 nuget.org 和组织可能会建立的私有包库之间，可以找到数以万计的非常有用的包，这些包可在应用和服务中使用。 无论源在哪里，使用包时都遵循相同的常规工作流。

![前往包源、查找包、在项目中安装包然后添加 using 语句和对包 API 的调用的流](media/Overview-01-GeneralFlow.png)

\* _仅 Visual Studio 和 `dotnet.exe`。`nuget install` 命令不会修改项目文件或 `packages.config` 文件；必须手动管理条目。_

有关详细信息，请参阅[查找和选择包](../consume-packages/finding-and-choosing-packages.md)和[安装包时会发生什么情况？](../concepts/package-installation-process.md)。

NuGet 会记住每个已安装包的标识和版本号，并将其录制到项目文件（使用 [PackageReference](../consume-packages/package-references-in-project-files.md)）或 [`packages.config`](../reference/packages-config.md) 中，具体取决于项目类型和 NuGet 版本。 若为 NuGet 4.0+，则 PackageReference 为首选方法，虽然这可在 Visual Studio 中通过[包管理器 UI](../tools/package-manager-ui.md) 进行配置。 在任何情况下，可以随时在相应文件中进行搜索，查看项目依赖项的完整列表。

> [!Tip]
> 随时检查要在软件中使用的每个包的许可证是非常明智的做法。 在 nuget.org 中，可以在每个包的说明页右侧找到“许可信息”链接  。 如果包未指定许可条款，请直接通过包页面上的“联系所有者”链接与包所有者联系  。 Microsoft 不向用户授予任何第三方包提供程序的知识产权许可，同时不对第三方提供的信息承担任何责任。

安装包时，NuGet 通常会检查此包是否已存在于其缓存中。 可手动从命令行中清除此缓存，如[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)中所述。

NuGet 还可以确保包支持的目标框架与你的项目兼容。 如果包中不包含兼容的程序集，NuGet 将显示一个错误。 请参阅[解决包不兼容错误](dependency-resolution.md#resolving-incompatible-package-errors)。

将项目代码添加到源存储库时，通常不需要包含 NuGet 包。 如果用户要在后期克隆存储库或获取项目（包括 Visual Studio Team Services 等系统上的生成代理），则必须在运行生成前还原必要的包：

![通过克隆存储库并使用任一还原命令来还原 NuGet 包的流](media/Overview-02-RestoreFlow.png)

[程序包还原](../consume-packages/package-restore.md)使用项目文件中的信息或 `packages.config` 重新安装所有依赖项。 请注意，此相关流程不尽相同，如[依赖项解析](../consume-packages/dependency-resolution.md)中所述。 此外，上图并未显示包管理器控制台的还原命令，因为已经在 Visual Studio 的上下文中使用了该控制台，它通常会自动还原包并提供所示的解决方案级别命令。

有时需要重新安装项目中已包含的包，这可能导致重新安装依赖项。 使用 `nuget reinstall` 命令或使用 NuGet 包管理器控制台可轻松执行此操作。 有关详细信息，请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md)。

最后一点，NuGet 的行为由 `Nuget.Config` 文件驱动。 有多个文件可用于集中处理不同级别的特定设置，如[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)中所述。

## <a name="ways-to-install-a-nuget-package"></a>安装 NuGet 包的方式

使用下表中的任何方法下载和安装 NuGet 包。

| 工具 | 说明 |
| --- | --- |
| [dotnet.exe CLI](install-use-packages-dotnet-cli.md) | （所有平台）用于 .NET Core 和 .NET Standard 库，以及用于面向 .NET Framework 的 SDK 样式项目的 CLI 工具（请参阅 [SDK 属性](/dotnet/core/tools/csproj#additions)）。 检索由 \<package_name\> 标识的包，并添加对项目文件的引用。 同时还要检索和安装依赖项。 |
| Visual Studio | （Windows 和 Mac）提供 UI，用户可以通过此 UI 浏览、选择包，并从指定包源将包及其依赖项安装到项目中。 将对已安装的程序包引用添加到项目文件。<ul><li>[使用 Visual Studio 安装和管理包](../tools/package-manager-ui.md)</li><li>[在项目中包括 NuGet 包 (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| [Visual Studio 中的 PowerShell](../tools/package-manager-console.md) | （仅限 Windows）检索并将用 \<package_name\> 识别的包从所选源安装到解决方案的指定项目中，然后添加对项目文件的引用。 同时还要检索和安装依赖项。 |
| [nuget.exe CLI](install-use-packages-dotnet-cli.md) | （所有平台）用于 .NET Framework 库和面向 .NET Standard 库的非 SDK 样式项目的 CLI 工具。 检索用 \<package_name\> 识别的包，将其内容展开到当前目录下的文件夹中；还可以检索 `packages.config` 文件中列出的所有包。 同时还要检索和安装依赖项，但对项目文件或 `packages.config` 不作任何更改。 |
