---
title: "NuGet 生态系统概述 |Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 生态系统中的完整资源，包括 NuGet 源、非 Microsoft NuGet 项目、实用程序和培训材料。"
keywords: "NuGet 生态系统, 非 Microsoft NuGet 项目, NuGet 开放源代码, NuGet 实用程序, NuGet 培训材料"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7c1e457c034f239fbea4e75f24851ea38182a294
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="an-overview-of-the-nuget-ecosystem"></a>NuGet 生态系统概述

自 2010 年推出以来，NuGet 提供了良好的机遇来改善和自动化开发过程的不同方面。

由于 NuGet 是根据限制性弱的 [Apache v2 许可证](http://choosealicense.com/licenses/apache/)许可的开放源代码，因此其他项目可以利用 NuGet，公司也可在其产品中生成对 NuGet 的支持。 无论是对于开源项目还是企业应用程序开发，NuGet 和以 NuGet 为基础生成的其他应用程序提供了广泛的工具生态系统，以便改善软件开发过程。

由于开发人员的贡献，所有这些项目都能够进行创新。 正如参与到 NuGet 本身中去，也通过报告缺陷和新功能创意、提供反馈、编写文档以及参与代码，尽力对这些项目做出贡献。

## <a name="net-foundation-projects"></a>.NET Foundation 项目

NuGet 为 Microsoft 开发平台提供了免费的开放源代码程序包管理系统。 它包含一些客户端工具以及一组服务，这些工具和服务构成了[正式 NuGet 库](http://www.nuget.org)。 一经组合，便形成受 [.NET Foundation](http://www.dotnetfoundation.org/) 控制的 NuGet 项目。

NuGet 组织包含 GitHub 上的各种存储库。 [https://github.com/Nuget/Home](https://github.com/Nuget/Home) 概述了所有存储库以及可在何处找到各种 NuGet 组件。

## <a name="microsoft-projects"></a>Microsoft 项目

Microsoft 对 NuGet 的开发做出了巨大的贡献。 Microsoft 员工做出的所有贡献也均为开放源代码，并将捐赠（包括版权）给 .NET Foundation。

## <a name="non-microsoft-projects"></a>非 Microsoft 项目

许多其他个人和公司也为 NuGet 生态系统做出了重要贡献。 此处所列每个项目的许可证可能与核心 NuGet 组件的不同，因此请在使用前确认许可条款是否可接受：

- [AppVeyor CI](https://www.appveyor.com/)
- [Artifactory](https://www.jfrog.com/artifactory/)
- [BoxStarter](http://boxstarter.org/)
- [Chocolatey](https://chocolatey.org/)
- [CoApp](http://coapp.org/)
- [JetBrains ReSharper](https://resharper-plugins.jetbrains.com/)
- [JetBrains TeamCity](https://www.jetbrains.com/teamcity/)
- [Klondike](https://github.com/themotleyfool/Klondike)
- [MinimalNugetServer](https://github.com/TanukiSharp/MinimalNugetServer)
- [MyGet（或 NuGet 即服务）](http://www.myget.org/)
- [NuGet 包资源管理器](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [NuGet 服务器](http://nugetserver.net/)
- [OctopusDeploy](https://octopus.com/)
- [Paket](https://fsprojects.github.io/Paket/)
- [ProGet (Inedo)](http://inedo.com/proget)
- [scriptcs](http://scriptcs.net/)
- [SharpDevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin 和 MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>其他基于 NuGet 的实用程序

以下是在 NuGet 基础上生成的工具和实用程序：

- [Glimpse 扩展](http://getglimpse.com/Packages)（插件均为包）
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Orchard](http://www.orchardproject.net/)（CMS 模块从 Orchard 库中托管的 v1 NuGet 源提取）
- [NuGet 服务器的 Java 实现](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest)（发表新包发布推文的 Twitter 自动程序）
- [DefinitelyTyped](http://definitelytyped.org/)（[发布到 NuGet](http://www.nuget.org/packages?q=DefinitelyTyped) 的[自动化](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript 类型定义）

## <a name="training-materials-and-references"></a>培训材料和参考资料

使用新工具或技术通常伴有学习曲线。 幸运的是，NuGet 完全没有陡峭的学习曲线！ 事实上，任何人都可以快速[入门包的使用](../quickstart/use-a-package.md)。

即便如此，创作包（尤其是好的包）以及在自动生成和部署过程中利用 NuGet，需要在以下资源上花费更多时间：

- [NuGet 博客](http://blog.nuget.org/)
- [Twitter 上的 NuGet 团队，@nuget](http://twitter.com/nuget)
- 书籍：
  - [Apress Pro NuGet](http://bit.ly/ProNuGet)
  - [NuGet 2 基础知识](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>单个包的文档

[NuDoq](http://nudoq.org) 提供了适用于 NuGet 包的直接访问、更新和文档。

NuDoq 定期轮询 nuget.org 库服务器以获取最新的包更新，解压缩并处理库文档文件，以及相应地对站点进行更新。

## <a name="adding-your-project"></a>添加项目

如果有 NuGet 生态系统项目，且是对本页有价值的补充，请向本页提交带编辑的拉取请求。
