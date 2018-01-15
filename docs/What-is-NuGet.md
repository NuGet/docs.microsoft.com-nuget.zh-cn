---
title: "NuGet 及其功能介绍 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/26/2017
ms.topic: hero-article
ms.prod: nuget
ms.technology: 
ms.assetid: c3faf278-4cbf-4733-96f6-9ee9f7203af9
description: "全面介绍 NuGet 及其功能"
keywords: "NuGet 包管理器, 使用, 包创建, 包托管"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2bc6a9e154df287fee6a7e00cc1349dfa2100643
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="an-introduction-to-nuget"></a>NuGet 简介

适用于任何现代开发平台的基本工具可充当一种机制，通过这种机制，开发人员可以创建、共享和使用有用的代码。 通常，此类代码捆绑到“包”中，其中包含编译的代码（如 DLL）以及在使用这些包的项目中所需的其他内容。

对于 .NET，共享代码的机制则为 NuGet，其定义如何创建、托管和使用面向 .NET 的包，并针对每个角色提供适用工具。 

简单来说，NuGet 包是具有 `.nupkg` 扩展的单个 ZIP 文件，此扩展包含编译代码 (Dll)、与该代码相关的其他文件以及描述性清单（包含包版本号等信息）。 库开发人员创建包文件并将其发布到主机。 包使用者接收这些包，将它们添加到项目，然后在项目代码中调用该库的功能。 随后，NuGet 自身负责处理所有中间详细信息。

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>包在创建者、主机和使用者之间的流

作为主机角色时，NuGet 自身负责在 [nuget.org](https://www.nuget.org) 中维护包含 60,000 多个唯一且公开提供的包的中央存储库。这些包每天供数以百万的 .NET 开发人员使用。 NuGet 还支持在云中、在私有网络中或者甚至直接在本地文件系统以私密方式托管包。 通过此做法，这些包将仅供特定组织或客户群体中的开发人员使用。 [托管自己的 NuGet 源](Hosting-Packages/Overview.md)中提供了对相关选项的说明。

无论主机的本质是什么，它都可作为包创建者和包使用者之间的连接点。 创建者生成有用的 NuGet 包并将其发布到主机。 然后，使用者可以在可访问的主机上搜索有用且兼容的包，下载包并将其包含在项目中。 在项目中安装包后，包的 API 将可用于其余项目代码。

![包创建者、包主机和包使用者之间的关系](media/nuget-roles.png)

在此情况下，“兼容”包指：此包所包含的程序集应至少针对与使用项目的目标框架兼容的一个目标 .NET Framework 而生成。 为使包广泛兼容，包创建者需为各种目标框架编译单独的程序集，并将所有这些程序集包含在同一个包中。 使用者安装该包时，NuGet 将仅提取项目所需的程序集。 这能将包在该项目生成的最终应用程序和/或程序集中的占用量降到最低。

## <a name="nuget-tools"></a>NuGet 工具

除托管支持外，NuGet 还提供各种供创建者和使用者使用的工具：

| 工具 | 平台 | 适用方案 | 描述 |
| --- | --- | --- | --- |
| [nuget.exe CLI](Tools/nuget-exe-CLI-Reference.md) | 全部 | 创建、使用 | 提供所有 NuGet 功能，包括一些专门适用于包创建者、仅适用于使用者和适用于两者的命令。 例如，包创建者使用 `nuget pack` 命令通过各种程序集和相关文件创建包，包使用者使用 `nuget install` 在项目中包含包，而所有人都可使用 `nuget config` 设置 NuGet 配置变量。  |
| [包管理器 UI](Tools/Package-Manager-UI.md) | Windows 版 Visual Studio | 使用 | 提供用于在 .NET 项目中安装和管理包的易用 UI。 | 
| [管理 NuGet UI](/visualstudio/mac/nuget-walkthrough) | Visual Studio for Mac | 使用 | 提供用于在 .NET 项目中安装和管理包的易用 UI。 |
| [包管理器控制台](Tools/Package-Manager-Console.md) | Windows 版 Visual Studio | 使用 | 提供用于在 .NET 项目中安装和管理包的 [PowerShell 命令](Tools/Powershell-Reference.md)。 | 
| [dotnet CLI](Tools/dotnet-Commands.md) | 全部 | 创建、使用 | 直接在 .NET Core 工具链中提供特定 NuGet CLI 功能。 |
| [MSBuild](Schema/msbuild-targets.md) | Windows | 创建、使用 | 支持创建包和还原项目中直接通过 MSBuild 工具链使用的包。 |

如上文所述，与 NuGet 配合使用的工具很大程度上取决于用户要创建（和发布）包还是使用包以及所使用的平台。 有关具体详细信息，请参阅[包创建工作流](Create-Packages/Overview-and-Workflow.md)和[包使用工作流](Consume-Packages/Overview-and-Workflow.md)主题以及这些部分中的其他主题。 

包创建者通常也是使用者，因为他们以其他 NuGet 包中已存在的功能作为生成基础。 当然，这些包反过来可能也需要依赖其他包。

## <a name="managing-dependencies"></a>管理依赖项

在其他人的工作基础上轻松生成，这是使程序包管理系统如此强大的方法之一。 相应地，大部分 NuGet 的用途就是代表项目管理该依赖项树或“关系图”。 简单来说，你仅需要关注在项目中直接使用的包。 如果任何这些包本身使用其他包（这些包可以使用包），NuGet 将负责所有这些下层依赖项。

下图显示一个依赖于五个包的项目，这些包反过来也依赖于许多其他包。  

![.NET 项目的 NuGet 依赖项关系图示例](media/dependency-graph.png)

请注意，某些包在依赖项关系图中多次出现。 例如，包 B 有三个不同的使用者，并且每个使用者可能为该包指定不同版本（未显示）。 这是一种常见情况，幸运的是，NuGet 将执行所有困难工作来确定包 B 的哪一版本可满足所有使用者。 随后，无论依赖项关系图多么复杂，NuGet 都将对所有包执行相同操作。

有关 NuGet 如何实现此服务的更多详细信息，请参阅[依赖项解析](Consume-Packages/Dependency-Resolution.md)。

## <a name="tracking-references-and-restoring-packages"></a>跟踪引用和还原包

项目可在开发人员计算机、源代码管理存储库、生成服务器等位置之间轻松移动，因此将 NuGet 包中的二进制程序集直接绑定到项目非常不切实际。 这不仅会使项目的每个副本出现不必要的膨胀（并且浪费源代码管理存储库中的空间），还会使包二进制文件难以更新到新版本（因为这需要更新项目的所有副本）。 

而 NuGet 只需保留项目所依赖包（包括顶层和下层依赖项）的引用列表，并根据请求提供还原所有引用包的方法（如[包还原](Consume-Packages/Package-Restore.md)中所述）。 也就是说，每当你将某个主机中的包安装到项目中时，NuGet 都将在此引用列表中记录包标识符和版本号。 （当然，卸载包将从列表中删除此信息。） 

![NuGet 引用列表在包安装时创建，可用于在其他位置还原包](media/nuget-restore.png)

只需引用列表，NuGet 随后即可随时从公共和/或私有主机重新安装（即还原）所有这些包。 （出于此原因，nuget.org 不允许永久性删除已发布的包，但可以隐藏；请参阅[删除包](Policies/deleting-packages.md)）。将项目提交到源代码管理存储库或将其以其他方式进行共享时，只需包含引用列表，不需要包含任何包二进制文件（请参阅[包和源代码管理](Consume-Packages/Packages-and-Source-Control.md)）。

接收项目的计算机（如获得项目副本并将其作为自动部署系统的一部分的生成服务器）仅会在需要时要求 NuGet 还原依赖项。 Visual Studio Team Services 等生成系统会针对此确切目的提供“NuGet 还原”步骤。 类似地，当开发人员获得项目副本（如克隆存储库时）并随后打开 Visual Studio 中的项目和运行生成时，Visual Studio 会自动还原必要的 NuGet 包。 开发人员还可以在包管理器控制台中使用 `nuget restore` CLI 命令或 `Install-Package` cmdlet 随时指示 NuGet 还原包。

显然，开发人员接下来关注的 NuGet 的主要角色则是代表项目维护该引用列表并提供高效还原（和更新）这些引用包的方法。

此目标的确切实现方法已随 NuGet 的不同版本进行演变，并形成如下几种包管理格式：

- [`packages.config`](Schema/packages-config.md)：(NuGet 1.0+) 一种 XML 文件，用于维护项目中所有依赖项的简单列表，包括其他已安装包的依赖项。 
- [`project.json`](Schema/project-json.md)：(NuGet 3.0+) 一种 JSON 文件，用于维护项目依赖项的列表，同时将包的整体信息图存储在关联文件 `project.lock.json` 中。 此结构可提供包括传递还原等优于 `packages.config` 的性能（如[依赖项解析](Consume-Packages/Dependency-Resolution.md)中所述），但通常会用下方的 PackageReference 取代其本身。
- [项目文件中的包引用](Consume-Packages/Package-References-in-Project-Files.md)（也称为“PackageReference”）| (NuGet 4.0+) 维护直接位于项目文件中的项目顶层依赖项的列表，因此无需单独文件。 与 `project.lock.json` 类似，关联文件 `project.assets.json` 动态生成，用于管理整体依赖项关系图。

任何特定项目中所用的包管理格式取决于项目类型以及 NuGet 和 Visual Studio 的可用版本。 若要确认当前使用的格式，只需在安装第一个包后在项目根目录中查找 `packages.config` 或 `project.json`。 如果未看到任一文件，请直接在项目文件中查找 &lt;PackageReference&gt; 元素。

例如，在 Visual Studio 2017 中，除 UWP C# 和 .NET Core 项目使用 PackageReference 外，大多数类型的项目均使用 `packages.config`。 

## <a name="what-else-does-nuget-do"></a>NuGet 的其他功能

现对以上所述内容进行总结，NuGet 提供（作为托管角色）中央 nuget.org 存储库并且支持私有托管。 NuGet 为开发人员提供创建、发布和使用包所需的工具。 最重要的是，NuGet 能维护项目中使用的包的引用列表，并且能够通过该列表还原和更新这些包。

为使这些进程高效运行，NuGet 执行了一些后台优化。 最值得注意的是，NuGet 管理计算机范围和项目特定的包缓存，以此简化安装和重新安装。 对于计算机范围的缓存，在项目中下载和安装的任何包都存储在缓存中，因此在其他项目中安装相同包时则无需再次下载。 当在生成服务器等位置频繁还原大量包时，这显然非常有帮助。 有关此机制及其使用方法的更多详细信息，请参阅[管理 NuGet 缓存](Consume-Packages/Managing-the-Nuget-Cache.md)。

在单个项目中，NuGet 执行大量工作来管理整体依赖项关系图。 （使用 `project.json` 或 &lt;PackageReference&gt; 时，NuGet 将在名为 `project.lock.json` 和 `project.assets.json` 的辅助文件中分别保留该信息。）其中同样包括对相同包的不同版本的多次引用进行解析。

也就是说，项目在具有相同依赖项的一个或多个包上选取依赖项是很常见的情况。 例如，nuget.org 上的某些最有用的实用程序包即由其他许多包使用。 在包含 10 个依赖项的整个依赖项关系图中，你可以对同一个包的不同版本轻松发起 10 种不同的引用。 但是，不能将该包的多个版本引入应用程序本身，因为 NuGet 会挑选出一个适合所有使用者的版本。 （有关本主题的详细信息，请参阅[依赖项解析](Consume-Packages/Dependency-Resolution.md)。）

除此之外，NuGet 维护与如何构造包（包括[本地化](Create-Packages/Creating-Localized-Packages.md)和[调试符号](Create-Packages/Symbol-Packages.md)）和如何引用包（包括[版本范围](reference/package-versioning.md#version-ranges-and-wildcards)和[预发行版本](create-packages/Prerelease-Packages.md)）相关的所有规范。NuGet 还为凭据提供程序（用于访问私有主机）和开发人员（用于编写 Visual Studio 扩展和项目模板）提供 API。

请花一点时间浏览本文档的目录，你将看到其中列出了所有这些功能，还包括自 NuGet 首次发行起的发行说明。

## <a name="comments-contributions-and-issues"></a>评论、建议和问题

最后，我们非常欢迎针对此文档给出评论和建议，只需在任何页面选择“评论”和“编辑”命令，或访问 GitHub 上的[文档存储库](https://github.com/NuGet/docs.microsoft.com-nuget/)和[文档问题列表](https://github.com/NuGet/docs.microsoft.com-nuget/issues)。

我们同样欢迎通过[多种 GitHub 存储库](https://github.com/NuGet/Home)针对 NuGet 本身提出建议；有关 NuGet 的问题，请访问 [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues)。

请尽情享受 NuGet 体验！
