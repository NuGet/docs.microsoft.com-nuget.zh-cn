---
title: "使用 NuGet 包的概述和工作流 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "概述在项目中使用 NuGet 包的流程，其中提供该流程其他特定部分的链接。"
keywords: "NuGet 包使用, NuGet 使用概述, NuGet 使用工作流, 包使用工作流, 包使用概述"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 731e0d3eb4ccb887624e4e46a18b4cc77857a784
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="package-consumption-workflow"></a>包使用工作流

在 nuget.org 和组织可能会建立的私有包库之间，可以找到数以万计的非常有用的包，这些包可在应用和服务中使用。 无论源在哪里，使用包时都需要按照下方显示的常规工作流。 有关详细信息，请参阅[查找和选择包](../consume-packages/finding-and-choosing-packages.md)和[安装 NuGet 包的不同方式](ways-to-install-a-package.md)。

![前往包源、查找包、在项目中安装包然后添加 using 语句和对包 API 的调用的流](media/Overview-01-GeneralFlow.png)

\* 使用命令行中的 `nuget install` 的情况除外，此时需要手动编辑配置文件。请参阅 [install 命令引用](../tools/cli-ref-install.md)。

NuGet 会记住每个已安装包的标识和版本号，并将其录制到 [`packages.config`](../reference/packages-config.md) 或项目文件中，具体取决于项目类型和 NuGet 版本。 使用 NuGet 4.0+，默认情况下通常[将依赖项存储在项目文件中或 PackageReference](../consume-packages/package-references-in-project-files.md)，但可通过[程序包管理器 UI 选项](../tools/package-manager-ui.md)在 Visual Studio 中配置。 在任何情况下，可以随时在相应文件中进行搜索，查看项目依赖项的完整列表。

> [!Tip]
> 随时检查要在软件中使用的每个包的许可证是非常明智的做法。 在 nuget.org 中，可以在每个包的说明页右侧找到“许可信息”链接。 如果包未指定许可条款，请直接通过包页面上的“联系所有者”链接与包所有者联系。 Microsoft 不向用户授予任何第三方包提供程序的知识产权许可，同时不对第三方提供的信息承担任何责任。

安装包时，NuGet 通常会检查此包是否已存在于其缓存中。 可手动从命令行中清除此缓存，如[管理 NuGet 缓存](../consume-packages/managing-the-nuget-cache.md)中所述。

NuGet 还可以确保包支持的目标框架与你的项目兼容。 如果包中不包含兼容的程序集，NuGet 将显示错误消息。 请参阅[解决包不兼容错误](dependency-resolution.md#resolving-incompatible-package-errors)。

将项目代码添加到源存储库时，通常不需要包含 NuGet 包。 如果要在后期克隆存储库（该存储库在 Visual Studio Team Services 等系统上包含生成代理），则必须在运行生成前还原必要的包：

![通过克隆存储库并使用任一还原命令来还原 NuGet 包的流](media/Overview-02-RestoreFlow.png)

[程序包还原](../consume-packages/package-restore.md)使用项目文件中的信息或 `packages.config` 重新安装所有依赖项。 请注意，此相关流程不尽相同，如[依赖项解析](../consume-packages/dependency-resolution.md)中所述。

有时需要重新安装项目中已包含的包，这可能导致重新安装依赖项。 通过 NuGet 命令行使用 `reinstall` 或使用 NuGet 包管理器控制台可轻松执行此操作。 有关详细信息，请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md)。

最后一点，NuGet 的行为由 `Nuget.Config` 配置文件驱动。 有多个文件可用于集中处理不同级别的特定设置，如[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)中所述。

享受利用 NuGet 包高效处理代码的体验！
