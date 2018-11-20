---
title: NuGet 及其功能介绍
description: 全面介绍 NuGet 及其功能
author: karann-msft
ms.author: karann
ms.date: 01/10/2018
ms.topic: overview
ms.openlocfilehash: d688aecaa73cecbfee184e3b13801ed22326a852
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580319"
---
# <a name="an-introduction-to-nuget"></a>NuGet 简介

适用于任何现代开发平台的基本工具可充当一种机制，通过这种机制，开发人员可以创建、共享和使用有用的代码。 通常，此类代码捆绑到“包”中，其中包含编译的代码（如 DLL）以及在使用这些包的项目中所需的其他内容。

对于 .NET（包括 .NET Core），共享代码的 Microsoft 支持的机制则为 NuGet，其定义如何创建、托管和使用面向 .NET 的包，并针对每个角色提供适用工具。

简单来说，NuGet 包是具有 `.nupkg` 扩展的单个 ZIP 文件，此扩展包含编译代码 (Dll)、与该代码相关的其他文件以及描述性清单（包含包版本号等信息）。 使用代码的开发人员共享创建包，并将其发布到公用或专用主机。 包使用者从适合的主机获取这些包，将它们添加到项目，然后在其项目代码中调用包的功能。 随后，NuGet 自身负责处理所有中间详细信息。

由于 NuGet 支持公用 nuget.org 主机旁边的专用主机，因此，可以使用 NuGet 包来共享组织或工作组专用的代码。 此外，你还可以使用 NuGet 包作为一种便捷的方式，将自己的代码用于除你自己项目之外的任何其他项目。 简而言之，NuGet 包是可共享的代码单元，但不需要暗示任何特定的共享方式。

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>包在创建者、主机和使用者之间的流

作为公用主机角色时，NuGet 自身负责在 [nuget.org](https://www.nuget.org) 中维护包含 100,000 多个唯一包的中央存储库。这些包每天供数以百万的 .NET/.Net Core 开发人员使用。 NuGet 还支持在云中（如在 Azure DevOps 上）、在私有网络中或者甚至直接在本地文件系统以私密方式托管包。 通过这样做，这些程序包仅对那些有权访问主机的开发人员可用，使你能够将程序包提供给特定的一组用户。 [托管自己的 NuGet 源](hosting-packages/overview.md)中提供了对相关选项的说明。 通过配置选项，你还可以精确控制任何给定计算机可以访问的主机，从而确保程序包是从特定源（而不是像 nuget.org 这样的公用存储库）获取的。

无论主机的本质是什么，它都可作为包创建者和包使用者之间的连接点。 创建者生成有用的 NuGet 包并将其发布到主机。 然后，使用者可以在可访问的主机上搜索有用且兼容的包，下载包并将其包含在项目中。 在项目中安装包后，包的 API 将可用于其余项目代码。

![包创建者、包主机和包使用者之间的关系](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>包定向兼容性

“兼容”包指：此包所包含的程序集应至少针对与使用项目的目标框架兼容的一个目标 .NET Framework 而生成。 与 UWP 控件一样，开发人员可以创建特定于一个框架的程序包，也可以支持更广泛的目标。 为了最大限度地利用程序包的兼容性，开发人员的目标是所有 .NET 和 .NET Core 项目都可以使用的 [.NET Standard](/dotnet/standard/net-standard)。 对于创建者和使用者而言，这是最有效的方式，因为单个包（通常包含单个程序集）适用于所有使用项目。

另一方面，需要 .NET Standard 之外的 API 的程序包开发人员会为他们希望支持的不同目标框架创建单独的程序集，并将所有这些程序集包含在同一个程序包中（称为“多目标”）。 使用者安装此类包时，NuGet 将仅提取项目需要的程序集。 这能将包在该项目生成的最终应用程序和/或程序集中的占用量降到最低。 当然，多目标包对创建者来说更难维护。

> [!Note]
> 目标 .NET Standard 取代了以前使用各种可移植类库 (PCL) 目标的方法。 因此，此文档着重于为 .NET Standard 创建程序包。

## <a name="nuget-tools"></a>NuGet 工具

除托管支持外，NuGet 还提供各种供创建者和使用者使用的工具。 有关如何获取特定工具的信息，请参阅[安装 NuGet 客户端工具](install-nuget-client-tools.md)。

| 工具 | 平台 | 适用方案 | 描述 |
| --- | --- | --- | --- |
| [nuget.exe CLI](tools/nuget-exe-cli-reference.md) | 全部 | 创建、使用 | 提供所有 NuGet 功能，包括一些专门适用于包创建者、仅适用于使用者和适用于两者的命令。 例如，包创建者使用 `nuget pack` 命令通过各种程序集和相关文件创建包，包使用者使用 `nuget install` 在项目文件夹中包含包，而所有人都可使用 `nuget config` 设置 NuGet 配置变量。 作为与平台无关的工具，NuGet CLI 不会与 Visual Studio 项目交互。 |
| [dotnet CLI](tools/dotnet-Commands.md) | 全部 | 创建、使用 | 直接在 .NET Core 工具链中提供特定 NuGet CLI 功能。 与 NuGet CLI 一样，dotnet CLI 不会与 Visual Studio 项目交互。 |
| [包管理器控制台](tools/package-manager-console.md) | Windows 版 Visual Studio | 使用 | 提供用于在 Visual Studio 项目中安装和管理包的 [PowerShell 命令](tools/Powershell-Reference.md)。 |
| [包管理器 UI](tools/package-manager-ui.md) | Windows 版 Visual Studio | 使用 | 提供用于在 Visual Studio 项目中安装和管理包的易用 UI。 |
| [管理 NuGet UI](/visualstudio/mac/nuget-walkthrough) | Visual Studio for Mac | 使用 | 提供用于在 Visual Studio for Mac 项目中安装和管理包的易用 UI。 |
| [MSBuild](reference/msbuild-targets.md) | Windows | 创建、使用 | 支持创建包和还原项目中直接通过 MSBuild 工具链使用的包。 |

如上文所述，你使用的 NuGet 工具很大程度上取决于用户要创建、使用还是发布程序包以及你所使用的平台。 包创建者通常也是使用者，因为他们以其他 NuGet 包中已存在的功能作为生成基础。 当然，这些包反过来可能也需要依赖其他包。

有关详细信息，请从[包创建工作流](create-packages/Overview-and-Workflow.md)和[包使用工作流](consume-packages/Overview-and-Workflow.md)文章开始。

## <a name="managing-dependencies"></a>管理依赖项

在其他人的工作基础上轻松生成，这是使程序包管理系统成为最强大功能的方法之一。 相应地，大部分 NuGet 的用途就是代表项目管理该依赖关系树或“关系图”。 简单来说，你仅需要关注在项目中直接使用的包。 如果任何这些包本身使用其他包（这些包仍可以使用其他包），NuGet 将负责所有这些下层依赖项。

下图显示一个依赖于五个包的项目，这些包反过来也依赖于许多其他包。

![.NET 项目的 NuGet 依赖项关系图示例](media/dependency-graph.png)

请注意，某些包在依赖项关系图中多次出现。 例如，包 B 有三个不同的使用者，并且每个使用者可能为该包指定不同版本（未显示）。 这是一种常见情况，特别是对于广泛使用的程序包。 幸运的是，NuGet 将执行所有困难的工作来确定包 B 的哪一个版本可满足所有使用者。 随后，无论依赖项关系图多么复杂，NuGet 都将对所有包执行相同操作。

有关 NuGet 如何实现此服务的更多详细信息，请参阅[依赖项解析](consume-packages/dependency-resolution.md)。

## <a name="tracking-references-and-restoring-packages"></a>跟踪引用和还原包

项目可在开发人员计算机、源代码管理存储库、生成服务器等位置之间轻松移动，因此将 NuGet 包的二进制程序集直接绑定到项目非常不切实际。 这样做不仅会使项目的每个副本出现不必要的膨胀（而且会浪费源代码管理存储库中的空间）。 还会使包二进制文件难以更新到新版本（因为这需要更新项目的所有副本）。

而 NuGet 维护一个项目所依赖的包的简单引用列表，包括顶层和下层的依赖关系。 也就是说，每当你将某个主机中的包安装到项目中时，NuGet 都将在此引用列表中记录包标识符和版本号。 （当然，卸载包将从列表中删除此信息。）然后，NuGet 根据请求提供还原所有引用程序包的方法，如[软件包还原](consume-packages/package-restore.md)中所述。

![NuGet 引用列表在包安装时创建，可用于在其他位置还原包](media/nuget-restore.png)

只需引用列表，NuGet 随后即可随时从公共和/或私有主机重新安装&mdash;即“还原”&mdash;所有这些包。 将项目提交到源代码管理存储库或将其以其他方式进行共享时，只需包含引用列表，不需要包含任何包二进制文件（请参阅[包和源代码管理](consume-packages/packages-and-source-control.md)）。

接收项目的计算机（如获得项目副本并将其作为自动部署系统的一部分的生成服务器）仅会在需要时要求 NuGet 还原依赖项。 Azure DevOps 等生成系统会出于此确切目的提供“NuGet 还原”步骤。 同样，当开发人员获取项目副本（如克隆存储库时），他们可以调用 `nuget restore`(NuGet CLI)、`dotnet restore`(dotnet CLI) 或 `Install-Package`（程序包管理器控制台）类似的命令，以获得所有必要的程序包。 对于 Visual Studio 来说，它将在生成项目时自动还原包（前提是启用了自动还原，如[包还原](consume-packages/package-restore.md)中所述）。

显然，开发人员接下来关注的 NuGet 的主要角色则是代表项目维护该引用列表并提供高效还原（和更新）这些引用包的方法。 该列表以两种“包管理格式”中的一种维护，因为将它们称为：

- [`packages.config`](reference/packages-config.md)：(NuGet 1.0+) 一种 XML 文件，用于维护项目中所有依赖项的简单列表，包括其他已安装包的依赖项。 已安装或已还原的包存储在 `packages` 文件夹中。

- [PackageReference](consume-packages/package-references-in-project-files.md)（或“项目文件中的包引用”） | *(NuGet 4.0+)* 维护直接位于项目文件中的项目顶层依赖项的列表，因此无需单独文件。 关联文件 `obj/project.assets.json` 动态生成，以管理项目使用的包的总依赖项关系图以及所有下层依赖项。 PackageReference 始终由 .NET Core 项目使用。

任何特定项目中所用的包管理格式取决于项目类型以及 NuGet（和/或 Visual Studio）的可用版本。 若要确认当前使用的格式，只需在安装第一个包后在项目根目录中查找 `packages.config`。 如果没有该文件，请直接在项目文件中查找 \<PackageReference\> 元素。

当进行选择时，我们建议使用 PackageReference。 出于与旧版兼容目的对 `packages.config` 进行维护，将不再主动对其进行开发。

> [!Tip]
> 各种 `nuget.exe` CLI 命令（如 `nuget install`）不会自动将包添加到引用列表中。 当使用 Visual Studio 包管理器（UI 或控制台）并使用 `dotnet.exe` CLI 时，将更新此列表。

## <a name="what-else-does-nuget-do"></a>NuGet 的其他功能

到目前为止，你已经学习了 NuGet 的以下特征：

- NuGet 提供支持专用托管的中心 nuget.org 存储库。
- NuGet 为开发人员提供创建、发布和使用包所需的工具。
- 最重要的是，NuGet 能维护项目中所用包的引用列表，并且能够通过该列表还原和更新这些包。

为使这些进程高效运行，NuGet 执行了一些后台优化。 最值得注意的是，NuGet 管理包缓存和全局包文件夹，使安装和重新安装过程更为快捷。 缓存可避免下载已在计算机上安装的包。 全局包文件夹允许多个项目共享同一个已安装的包，因此减少了计算机上的 NuGet 的总体占用。 当在生成服务器等位置频繁还原大量包时，缓存和全局包文件夹也非常有帮助。 有关这些机制的详细信息，请参阅[管理全局包和缓存文件夹](consume-packages/managing-the-global-packages-and-cache-folders.md)。

在一个单独的项目中，NuGet 管理整个依赖项关系图，它同样包括解析对同一个包的不同版本的多个引用。 项目在具有相同依赖项的一个或多个包上选取依赖项是很常见的情况。 nuget.org 上的某些最有用的实用程序包即由其他许多包使用。 然后在整个依赖项关系图中，你可以对同一个包的不同版本轻松发起 10 种不同的引用。 为避免将该包的多个版本引入应用程序本身，NuGet 会挑选出一个适合所有使用者的版本。 （有关详细信息，请参阅[依赖项解析](consume-packages/dependency-resolution.md)。）

除此之外，NuGet 维护与如何构造包（包括[本地化](create-packages/creating-localized-packages.md)和[调试符号](create-packages/symbol-packages.md)）和如何引用包（包括[版本范围](reference/package-versioning.md#version-ranges-and-wildcards)和[预发行版本](create-packages/prerelease-packages.md)）相关的所有规范。此外，NuGet 还提供了各种 API 以编程方式使用其服务，并可为编写 Visual Studio 扩展和项目模板的开发人员提供支持。

请花一点时间浏览本文档的目录，你会看到其中列出了所有这些功能，以及自 NuGet 首次发行起的发行说明。

## <a name="comments-contributions-and-issues"></a>评论、建议和问题

最后，我们非常欢迎针对此文档给出评论和建议 &mdash; 只需在任何页面上选择“反馈”和“编辑”命令，或访问 GitHub 上的[文档存储库](https://github.com/NuGet/docs.microsoft.com-nuget/)和[文档问题列表](https://github.com/NuGet/docs.microsoft.com-nuget/issues)。

我们同样欢迎通过[多种 GitHub 存储库](https://github.com/NuGet/Home)针对 NuGet 本身提出建议；有关 NuGet 的问题，请访问 [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues)。

请尽情享受 NuGet 体验！
