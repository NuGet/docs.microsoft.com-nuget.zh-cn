---
title: 查找和选择 NuGet 包
description: 概述如何查找和选择最适合项目的 NuGet 包，包括有关 NuGet 搜索语法的详细信息。
author: karann-msft
ms.author: karann
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: 81672abf0362e053da2b71c8bd39bd7f96ddf73b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549410"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>针对项目查找和评估 NuGet 包

启动任何 .NET 项目或识别应用或服务的功能需求时，使用可满足该需求的现有 NuGet 包可以大大地省时省力。 这些包可能来自 [nuget.org](http://www.nuget.org/packages/) 中的公共集合，也可能来自组织或其他第三方提供的私有源。

## <a name="finding-packages"></a>查找包

访问 nuget.org 或打开 Visual Studio 中的程序包管理器 UI 时，其中会显示一个包列表，这些包按总下载次数排列。 你可以立即看出在数以百万的 .NET 项目中使用次数最多的包。 很可能前几页列出的某些包就适用于你的项目。

![显示最常用包的 nuget.org/packages 的默认视图](media/Finding-01-Popularity.png)

请注意页面右上角的“包括预发行版”选项。 勾选此选项时，nuget.org 将显示所有版本的包，包括 beta 版本和其他早期版本。 若要仅显示稳定版本，请清除此选项。

对于特定需求，按标记搜索（在 Visual Studio 包管理器或在 nuget.org 等门户中）是发现适用包的最常用方法。 例如，搜索“json”将列出具有该关键字标记的所有 NuGet 包，这些包必然与 JSON 数据格式存在某种关系。

![nuget.org 中“json”的搜索结果](media/Finding-02-SearchResults.png)

还可以使用包 ID 进行搜索（如果知道）。 请参阅下面的[搜索语法](#search-syntax)。

在此情况下，搜索结果将仅按相关性进行排序，因此通常至少需要浏览前几页结果才能找到满足需求的包；也可以优化搜索词，使其更加具体。

### <a name="does-the-package-support-my-projects-target-framework"></a>包是否支持项目的目标框架？

仅当包支持的框架中包含该项目的目标框架时，NuGet 才会在项目中安装包。 如果包不兼容，NuGet 将发出错误。

某些包会直接在 nuget.org 库中列出其支持的框架，但由于这些不是必需数据，因此许多包不会包含此列表。 目前不支持在 nuget.org 中搜索支持特定目标框架的包（此功能处于考虑阶段，请参阅 [NuGet 问题 2936](https://github.com/NuGet/NuGetGallery/issues/2936)）。

幸运的是，你可以通过以下两种方法确定受支持的框架：

1. 尝试在 NuGet 包管理器控制台中使用 [`Install-Package`](../tools/ps-ref-install-package.md) 命令将包安装到项目中。 如果包不兼容，此命令将显示包支持的框架。

1. 在 nuget.org 中包的页面上，使用“信息”下的“手动下载”链接来下载包。 将扩展名从 `.nupkg` 更改为 `.zip`，然后打开文件查看 `lib` 文件夹的内容。 你会看到每个受支持框架的子文件夹，每个子文件夹都以目标框架名字对象 (TFM)（请参阅[目标框架](../reference/target-frameworks.md)）命名。 如果 `lib` 下没有任何子文件夹而只有一个 DLL，此时则必须通过尝试将包安装到项目中来查看其是否兼容。

## <a name="pre-release-packages"></a>预发行包

许多包创建者会提供预览版和 beta 版，他们会继续提供改进并收集其最新版本的反馈。

默认情况下，nuget.org 会在搜索结果中显示预发行包。 若要仅搜索稳定版发布，请清除页面右上角的“包括预发行版”选项

![nuget.org 上的“包括预发行版”复选框](media/Finding-06-include-prerelease.png)

在 Visual Studio 中使用 NuGet 和 dotnet CLI 工具时，NuGet 默认不包括预发行版本。 若要更改此行为，请执行以下操作：

- **Visual Studio 中的包管理器 UI**：在“管理 NuGet 包”UI 中，勾选“包括预发行版”框。 勾选或清除此框将刷新包管理器 UI 和可安装的可用版本列表。

    ![Visual Studio 中的“包括预发行版”复选框](media/Prerelease_02-CheckPrerelease.png)

- **包管理器控制台**：将 `-IncludePrerelease` 开关与 `Find-Package`、`Get-Package`、`Install-Package`、`Sync-Package` 和 `Update-Package` 命令配合使用。 请参阅 [PowerShell 参考](../tools/powershell-reference.md)。

- nuget.exe CLI：将 `-prerelease` 开关与 `install`、`update`、`delete` 和 `mirror` 命令配合使用。 请参阅 [NuGet CLI 参考](../tools/nuget-exe-cli-reference.md)

- dotnet.exe CLI：使用 `-v` 参数指定确切的预发行版本。 请参阅 [dotnet 添加包参考](/dotnet/core/tools/dotnet-add-package)。

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>本机 C++ 包

NuGet 支持本机 C++ 包，这些包可在 Visual Studio 的 C++ 项目中使用。 这将启用项目的“管理 NuGet 包”上下文菜单命令、引入 `native` 目标框架，以及提供 MSBuild 集成。

若要在 [nuget.org](https://www.nuget.org/packages) 中查找本机包，请搜索 `tag:native`。 此类包通常提供 `.targets` 和 `.props` 文件，NuGet 可在将包添加到项目中时自动导入这些文件。

## <a name="evaluating-packages"></a>评估包

评估包用途的最佳方法是下载它并在你的代码中试用（顺便说一下，将对 nuget.org 的所有包进行常规病毒扫描）。 每一个被广泛使用的包起初都仅被少数开发人员采用，你也可能成为早期采用者之一！

同时，使用 NuGet 包则意味着与此包建立依赖关系，因此使用者希望确保包具有耐用性和可靠性。 安装和直接测试包非常耗时，所以还可以通过使用包清单页面中的信息深入了解包的质量：

- *下载统计信息*：在 nuget.org 中，包页面上的“统计信息”部分显示总下载次数、最新版本下载次数以及日平均下载次数。 数值较大则表示已有许多开发人员选择与此包建立依赖关系，这说明此包已获得认可。

    ![包清单页面上的下载统计数据](media/Finding-03-Downloads.png)

- *版本历史记录*：在包页面上，可在“信息”下查找最新更新的日期和查看“版本历史记录”。 维护良好的包应具有最新更新和丰富的版本历史记录。 疏于维护的包则仅具有几次更新，并且通常已长时间未更新。

    ![包清单页面上的版本历史记录](media/Finding-04-VersionHistory.png)

- *最近安装*：在包页面上，选择“统计信息”下的“查看完整统计信息”。完整统计信息页面按版本号显示过去六周的包安装次数。 其他开发人员频繁使用的包通常比鲜有使用的包更值得信赖。

- 支持：在包页面上，选择“信息”下的“项目网站”（如果可用）可查看作者提供的支持选项。 具有专门网站的项目通常具备更好的支持。

- *开发人员历史记录*：在包页面上，选择“所有者”下的某个所有者可查看其已发布的其他包。 具有多个包的所有者更有可能在未来继续对其工作成果提供支持。

- *开源贡献*：很多包都在开源存储库中进行维护，这使依赖于包的开发人员可直接提供 bug 修补程序和功能改进。 任何给定包的贡献历史记录也能反映出积极参与的开发人员的数量。

- *联系所有者*：新晋开发人员同样可以制作出可供使用的优质包，为他们提供向 NuGet 生态系统引入新内容的机会是非常好的做法。 若有此想法，使用清单页面中“信息”下的“联系所有者”选项即可直接联系包开发人员。 他们很可能非常乐于与你合作来满足你的需求！

- 保留包 ID 前缀：许多包所有者已应用并授予了[保留包 ID 前缀](../reference/id-prefix-reservation.md)。 如果 [nuget.org](https://www.nuget.org/) 上或 Visual Studio 中的包 ID 旁有视觉对象复选标记，这意味着包所有者已满足我们的 ID 前缀预留[条件](../reference/id-prefix-reservation.md#id-prefix-reservation-criteria)。 这意味着包所有者清楚了解如何标识自己及其包。

> [!Note]
> 应时刻留意包的许可条款 - 在 nuget.org 中的包清单页面上选择“许可信息”即可查看。如果包未指定许可条款，请直接通过包页面上的“联系所有者”链接与包所有者联系。 Microsoft 不向用户授予任何第三方包提供程序的知识产权许可，同时不对第三方提供的信息承担任何责任。

## <a name="search-syntax"></a>搜索语法

NuGet 包搜索在 nuget.org 上、NuGet CLI 中和 Visual Studio 的 NuGet 包管理器扩展中具有相同的使用方法。 通常可使用关键字和包说明进行搜索。

- **关键字**：搜索操作将查找包含任何给定关键字的相关包。 示例：`modern UI`。 若要搜索包含所有给定关键字的包，请在搜索词之间使用“+”，例如 `modern+UI`。
- **短语**：在引号内输入搜索词可查找与其大小写完全匹配的匹配项。 示例：`"modern UI" package`
- **筛选**：可以按照语法 `<property>:<term>` 使用搜索词来搜索特定属性，其中，`<property>`（区分大小写）可为 `id`、`packageid`、`version`、`title`、`tags`、`author`、`description`、`summary` 和 `owner`。 可将搜索词添加在引号中（如需要），还可以同时搜索多个属性。 此外，按 `id` 属性搜索得到的是子字符串匹配项，而按 `packageid` 搜索将得到确切匹配。 示例：

    ```
    id:NuGet.Core                # Match any part of the id property
    Id:"Nuget.Core"
    ID:jQuery
    title:jquery                 # Searches title as shown on the package listing
    PackageId:jquery             # Match the package id exactly
    id:jquery id:ui              # Search for multiple terms in the id
    id:jquery tags:validation    # Search multiple properties
    id:"jquery.ui"               # Phrase search
    invalid:jquery ui            # Unsupported properties are ignored, so this
                                 # is the same as searching on jquery ui
    ```
