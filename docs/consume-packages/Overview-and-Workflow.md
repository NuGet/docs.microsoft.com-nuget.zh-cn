---
title: 使用 NuGet 包的概述和工作流
description: 概述在项目中使用 NuGet 包的流程，其中提供该流程其他特定部分的链接。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: 765b48b474aee17415f53491514bf6e9d50af010
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="package-consumption-workflow"></a>包使用工作流

在 nuget.org 和组织可能会建立的私有包库之间，可以找到数以万计的非常有用的包，这些包可在应用和服务中使用。 无论源在哪里，使用包时都遵循相同的常规工作流。

![前往包源、查找包、在项目中安装包然后添加 using 语句和对包 API 的调用的流](media/Overview-01-GeneralFlow.png)

\* _仅限 Visual Studio 和 dotnet.ex`。Nuget 安装命令不会修改项目文件或 packages.config；必须手动管理条目。_

有关详细信息，请参阅[查找和选择包](../consume-packages/finding-and-choosing-packages.md)和[安装 NuGet 包的不同方式](ways-to-install-a-package.md)。

NuGet 会记住每个已安装包的标识和版本号，并将其录制到 [`packages.config`](../reference/packages-config.md) 或项目文件（使用 [PackageReference](../consume-packages/package-references-in-project-files.md)）中，具体取决于项目类型和 NuGet 版本。 使用 NuGet 4.0+，PackageReference 为首选方法，虽然这可在 Visual Studio 中通过[包管理器 UI 选项](../tools/package-manager-ui.md)进行配置。 在任何情况下，可以随时在相应文件中进行搜索，查看项目依赖项的完整列表。

> [!Tip]
> 随时检查要在软件中使用的每个包的许可证是非常明智的做法。 在 nuget.org 中，可以在每个包的说明页右侧找到“许可信息”链接。 如果包未指定许可条款，请直接通过包页面上的“联系所有者”链接与包所有者联系。 Microsoft 不向用户授予任何第三方包提供程序的知识产权许可，同时不对第三方提供的信息承担任何责任。

安装包时，NuGet 通常会检查此包是否已存在于其缓存中。 可手动从命令行中清除此缓存，如[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)中所述。

NuGet 还可以确保包支持的目标框架与你的项目兼容。 如果包中不包含兼容的程序集，NuGet 将显示一个错误。 请参阅[解决包不兼容错误](dependency-resolution.md#resolving-incompatible-package-errors)。

将项目代码添加到源存储库时，通常不需要包含 NuGet 包。 如果用户要在后期克隆存储库或获取项目（包括 Visual Studio Team Services 等系统上的生成代理），则必须在运行生成前还原必要的包：

![通过克隆存储库并使用任一还原命令来还原 NuGet 包的流](media/Overview-02-RestoreFlow.png)

[程序包还原](../consume-packages/package-restore.md)使用项目文件中的信息或 `packages.config` 重新安装所有依赖项。 请注意，此相关流程不尽相同，如[依赖项解析](../consume-packages/dependency-resolution.md)中所述。 此外，上图并未显示包管理器控制台的还原命令，因为已经在 Visual Studio 的上下文中使用了该控制台，它通常会自动还原包并提供所示的解决方案级别命令。

有时需要重新安装项目中已包含的包，这可能导致重新安装依赖项。 使用 `nuget reinstall` 命令或使用 NuGet 包管理器控制台可轻松执行此操作。 有关详细信息，请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md)。

最后一点，NuGet 的行为由 `Nuget.Config` 文件驱动。 有多个文件可用于集中处理不同级别的特定设置，如[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)中所述。

享受利用 NuGet 包高效处理代码的体验！
