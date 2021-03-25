---
title: 包创作最佳做法
description: 创建高质量 NuGet 包的最佳做法的一般指南。
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: 7475cf655876f2c127e79a16ccf67c0c723d164f
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859065"
---
# <a name="package-authoring-best-practices"></a>包创作最佳做法

本指南旨在为 NuGet 包作者创建和发布高质量包提供轻型参考。 它主要重点介绍特定于包的最佳做法，如元数据和打包。 有关生成高质量库的更深入的建议，请参阅 .NET [开放源代码库指南](https://docs.microsoft.com/dotnet/standard/library-guidance/)。

## <a name="types-of-recommendations"></a>建议类型

每篇文章介绍四种类型的建议：“请执行”、“请考虑”、、“请避免”、和“请勿”。 建议类型表示了应遵循的程度。

应始终遵循“请执行”建议。 例如：

✔️ 请包含描述其用途的包的简短说明。

在另一方面，“请考虑”建议是在一般情况下要遵循的建议，但存在该规则的合法例外：

✔️ 请考虑选择带有满足 NuGet 前缀预留[条件](https://docs.microsoft.com/nuget/reference/id-prefix-reservation)的前缀的 NuGet 包名称。

“请避免”建议是指在一般情况下不应执行的操作，但有时也可以打破规则：

❌ 请避免使用需要确切版本的 NuGet 包引用。

最后，“请勿”建议是指在大多数情况下不得执行的操作：

❌ 请勿使用 `LicenseUrl` 元数据属性。

## <a name="create-a-nuget-package"></a>创建 NuGet 包

创建 NuGet 包的最新建议方法是通过 [SDK 样式的项目](https://docs.microsoft.com/nuget/resources/check-project-format)。 SDK 样式的项目属性（包括[目标框架](https://docs.microsoft.com/dotnet/standard/frameworks)和[包元数据](#package-metadata)）是在[项目文件](https://docs.microsoft.com/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file)中定义的。

通过在 [Visual Studio](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli) 或 [dotnet CLI](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli) 中定义所需的属性和打包，从 SDK 样式的项目创建包。

✔️ 创建 SDK 样式的项目，并使用 Visual Studio 或 dotnet CLI 创建（打包）包。

有关包创建的更详细指南，包括必要的客户端工具、项目文件示例和命令，请参阅[使用 dotnet CLI 创建 NuGet 包](https://docs.microsoft.com/nuget/create-packages/creating-a-package-dotnet-cli)。

若要帮助决定要面向的 .NET 框架，请参阅我们的[跨平台目标的最新指南](https://docs.microsoft.com/dotnet/standard/library-guidance/cross-platform-targeting)。

## <a name="package-metadata"></a>包元数据

元数据是任何 NuGet 包的基础组件。 你的元数据质量会极大地影响包的可发现性、可用性和可靠性。

在 Visual Studio 中，指定包元数据的建议方法是转到“项目”>“[项目名称] 属性”>“包”。

还可以[直接在项目文件中指定](https://docs.microsoft.com/nuget/create-packages/creating-a-package-msbuild#set-properties)包元数据元素。

下面是一个表映射，其中描述可用的包元数据元素：

| Visual Studio 属性名称                   | [项目文件/MSBuild 属性名称](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                          | [Nuspec 属性名称](https://docs.microsoft.com/nuget/reference/nuspec#general-form-and-schema) | 说明                                                                                                       |
|-----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| [`Package id`](#package-id)                   | [`PackageId`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageid)                                                            | [`id`](https://docs.microsoft.com/nuget/reference/nuspec#id)                                      | 包名称或标识符。                    |
| [`Package version`](#package-version)         | [`PackageVersion`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageversion)                                                  | [`version`](https://docs.microsoft.com/nuget/reference/nuspec#version)                            | NuGet 包版本。                                           |
| [`Authors`](#authors)                         | [`Authors`](https://docs.microsoft.com/dotnet/core/tools/csproj#authors)                                                                | [`authors`](https://docs.microsoft.com/nuget/reference/nuspec#authors)                            | 以逗号分隔的包作者列表，通常使用个人或组织的“友好名称”。                             |
| [`Description`](#description)                 | [`Description`](https://docs.microsoft.com/dotnet/core/tools/csproj#description)                                                        | [`description`](https://docs.microsoft.com/nuget/reference/nuspec#description)                    | 对包的描述。                                                                |
| [`Copyright`](#copyright)                     | [`Copyright`](https://docs.microsoft.com/dotnet/core/tools/csproj#copyright)                                                            | [`copyright`](https://docs.microsoft.com/nuget/reference/nuspec#copyright)                        | 包的版权详细信息。                                                                      |
| [`Licensing - Expression`](#licensing)        | [`PackageLicenseExpression`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file) | [`license type="expression"`](https://docs.microsoft.com/nuget/reference/nuspec#license)          | SPDX 许可证表达式。       |
| [`Licensing - File`](#licensing)              | [`PackageLicenseFile`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)       | [`license type="file"`](https://docs.microsoft.com/nuget/reference/nuspec#license)                | 自定义许可证文件的路径。                                               |
| [`Project URL`](#project-url)                 | `PackageProjectUrl`                                                                                                                     | [`projectUrl`](https://docs.microsoft.com/nuget/reference/nuspec#projecturl)                      | 项目主页的 URL。                                                                                   |
| [`Icon File`](#icon)                          | [`PackageIcon`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                  | [`icon`](https://docs.microsoft.com/nuget/reference/nuspec#icon)                                  | 包图标图像文件的路径。                                                                      |
| [`Repository URL`](#repository-type-and-url)  | [`RepositoryUrl`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositoryurl)                                                    | [`repository url`](https://docs.microsoft.com/nuget/reference/nuspec#repository)               | 从中生成包的存储库的 URL。                                                           |
| [`Repository type`](#repository-type-and-url) | [`RepositoryType`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositorytype)                                                 | [`repository type`](https://docs.microsoft.com/nuget/reference/nuspec#repository)              | 存储库 URL 指向的存储库的类型（即“git”）。                                                   |
| [`Tags`](#tags)                               | [`PackageTags`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagetags)                                                        | [`tags`](https://docs.microsoft.com/nuget/reference/nuspec#tags)                                  | 描述包的标记和关键字的空格分隔列表。 搜索包时使用标记。 |
| [`Release notes`](#release-notes)             | [`PackageReleaseNotes`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                                          | [`releaseNotes`](https://docs.microsoft.com/nuget/reference/nuspec#releasenotes)                  | 在此版本的包中进行的更改的说明。                                                 |

### <a name="package-id"></a>包 ID

如果你要发布全新的包：

✔️ 请选择唯一的包 ID，并与 NuGet.org 上的现有包明确区分。
> 可以通过在 NuGet.org 上搜索 ID 或检查是否存在以下链接来检查包 ID 是否是唯一的和可区分的： https://www.nuget.org/packages/<package 名称\> 。

✔️ 请考虑选择带有满足 NuGet [前缀预留条件](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation#id-prefix-reservation-criteria)的前缀的 NuGet 包名称。
> 保留包的前缀 ID 将可以获得已验证的复选标记：![图像](media/Verified-check-mark.png)
> 
> 若要了解详细信息，请查看[包 ID 前缀预留文档](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation)。

### <a name="package-version"></a>包版本

✔️ 请考虑使用 [SemVer](https://semver.org/) 控制 NuGet 包的版本。
> 实质上，这意味着使用 Major.Minor.Patch[-prerelease] 格式。

✔️ 如果包不稳定或处于预览阶段，则将包作为[预发布包](https://docs.microsoft.com/nuget/create-packages/prerelease-packages)发布。

请参阅 [.NET 库版本控制指南](https://docs.microsoft.com/dotnet/standard/library-guidance/versioning)了解更多高级指南。

### <a name="authors"></a>Authors

✔️ 请使用“作者”字段作为你或你的组织的“友好名称”。
> 例如，如果我的 NuGet.org 用户名为“jdoe”，则将“Jane Doe”用作“作者”字段可帮助使用者将我识别为作者。 如果我的组织的 NuGet.org 用户名为“ContosoToolkit”，则使用“Contoso Corporation”可能更具识别性，并激发更多使用者信任。
### <a name="description"></a>说明

✔️ 请包括描述包的简短说明（最多 4000 个字符）。
> 包说明是 NuGet 搜索中最重要的字段之一，可能是潜在使用者在确定包是否适用时查看的第一个方面。

### <a name="copyright"></a>Copyright

✔️ 请考虑对你的包使用版权“Copyright (c) <名称/公司\> <年\>”。
>版权声明实质上表示：未经你的允许，不可复制你的工作。 在包中包含版权声明非常简单，不会造成任何损害！

示例：版权所有 (c) Contoso 2020

### <a name="licensing"></a>许可

✔️ [在包中包含许可证表达式或许可证文件](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)。
> [!IMPORTANT]
> 没有许可证的项目默认为[独家版权](https://choosealicense.com/no-permission/)，这意味着你未授予任何人使用你的项目的权限。

❌ 请勿使用已弃用的 `LicenseUrl` 元数据属性。
> 这会带来法律歧义，因为 URL 中的许可证更改将以追溯方式更改以前的包版本显示的许可证。

#### <a name="if-your-package-is-open-source"></a>如果你的包是[开放源代码](https://opensource.org/osd)

✔️ 请[选择开放源代码许可证](https://choosealicense.com/)，使包开放源代码。
> “开放源代码许可证是符合开放源代码定义的许可证 - 简而言之，它们允许免费使用、修改和共享软件。” - 开放源代码计划。 若要了解有关开放源代码软件和开放源代码计划的详细信息，请查看 https://opensource.org/ 。

✔️ 请考虑[在包中包含许可证表达式](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)。
> 如果许可证表达式可以使用你的包，或者如果许可证已更改，则它们会最明显地表现出来并让使用者更清楚地知道。 
> [!Note]
> NuGet.org 仅接受开放源代码计划或免费软件基金会批准的许可证的许可证表达式。

#### <a name="if-your-package-is-not-open-source"></a>如果你的包未开放源代码

✔️ 请[在包中包含许可证文件](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)。
> 可以将任何许可证文件（.txt 或 .md）（包括非标准许可证）添加到你的包。 

### <a name="project-url"></a>项目 URL

✔️ 请考虑包括指向关联项目、存储库或公司网站的链接。
> 你的项目网站应拥有用户需要了解的有关你的包的一切，并且很可能是用户查找文档的位置。

### <a name="icon"></a>图标

✔️ 请考虑[包含包的图标](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)，以帮助在视觉上对其进行区分。 它是一个相对较小的添加内容，可以提高对包质量的认知度。
> 图标可以特定于单个包，也可以是品牌徽标。

✔️ 请使用属于 128x128 并具有透明背景的图像 (PNG)，以获得最佳查看结果。
> NuGet 会根据显示它的客户端自动缩放图像。

❌ 请勿使用已弃用的 `IconUrl` 元数据属性。

### <a name="repository-type-and-url"></a>存储库类型和 URL

✔️考虑设置[源链接](https://docs.microsoft.com/dotnet/standard/library-guidance/sourcelink)，以自动将源代码管理元数据添加到 NuGet 包，使库更易于调试。
> 源链接会自动将 `Repository URL` 和 `Repository Type` 添加到包元数据中。 它还添加与包版本关联的特定提交。

### <a name="tags"></a>标记

✔️ 请包括多个标记，其中包含与包相关的关键术语，以增强可发现性。
> 在 NuGet. org 的搜索算法中考虑包括标记，这对于不在包 ID 中但相关的术语特别有用。

例如，如果我发布了一个包以将字符串记录到控制台中，我将包括：“日志记录、日志、控制台、字符串、输出”

### <a name="release-notes"></a>发行说明

✔️ 请考虑包括发行说明，其中每个更新说明了所做的更改。
> 虽然发行说明不需要特定的格式，但建议包括以下内容：
>
> 1. 中断性变更
> 2. 新增功能
> 3. Bug 修复
> 
> 如果你已在存储库中跟踪发行说明或更改日志，则还可以包含指向相关文件的链接。

## <a name="related-topics"></a>相关主题

- [创建并发布包 (dotnet CLI)](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli)
- [创建并发布包 (Visual Studio)](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli)
