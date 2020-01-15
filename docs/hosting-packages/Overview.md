---
title: 承载自己的 NuGet 源概述
description: 概述了本地或远程承载自己的 NuGet 包源或库的打开。
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 81acf15ac69d78d39d2784e77c18ba38bfea126d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385537"
---
# <a name="hosting-your-own-nuget-feeds"></a>承载自己的 NuGet 源

可能希望将包仅发布到有限受众（例如，组织或工作组），而不是将其公开发布。 此外，一些公司可能希望限制其开发人员可以使用的第三方库，使他们从有限包源（而不是 nuget.org）中提取内容。

对于所有此类目的，NuGet 支持通过以下方式设置专用包源：

- 本地源：包只需放置在合适的网络文件共享中，理想情况下使用 `nuget init` 和 `nuget add` 创建分层文件夹结构 (NuGet 3.3+)。 有关详细信息，请参阅[本地源](../hosting-packages/local-feeds.md)。
- NuGet.Server：通过本地 HTTP 服务器提供包。 有关详细信息，请参阅 [NuGet.Server](../hosting-packages/nuget-server.md)。
- NuGet 库：在使用 [NuGet 库项目](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com) 的 Internet 服务器上承载包。 NuGet 库提供用户管理和功能，如丰富的 Web UI，它允许从浏览器中搜索和浏览包，这与 nuget.org 相似。

另外还有其他几种 NuGet 宿主产品支持远程专用源，例如 [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) 和 [GitHub 包注册表](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)。 下面列出了此类产品：

- JFrog 的 [Artifactory](https://www.jfrog.com/artifactory/)。
- [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) 也可通过 Team Foundation Server 2017 以及更高版本获得。
- [BaGet](https://github.com/loic-sharma/BaGet) 构建与 ASP.NET Core 基础上的 NuGet V3 服务器的开源实现
- [Cloudsmith](https://cloudsmith.io/l/nuget-feed/)：一种完全托管的包管理 SaaS
- [GitHub 包注册表](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [LiGet](https://github.com/ai-traders/liget)：在 docker 中 kestrel 上运行的 NuGet V2 服务器的开放源代码实现
- [MyGet](https://myget.org)
- Sonatype 中的 [Nexus 存储库 OSS](https://www.sonatype.com/nexus-repository-oss)。
- [NuGet 服务器（开放源代码）](https://github.com/svenkle/nuget-server)，与 Inedo 的 NuGet 服务器相似的开放源代码实现
- [NuGet 服务器](http://nugetserver.net/)，Inedo 的社区项目
- Inedo 的 [ProGet](https://inedo.com/proget)
- [Sleet](https://github.com/emgarten/sleet)（开放源代码 NuGet V3 静态源生成器）
- JetBrains 的 [TeamCity](https://www.jetbrains.com/teamcity/)。

无论包是什么样的承载方式，均可将其添加到 `NuGet.Config` 中的可用源列表以便访问。 此操作可在 Visual Studio 中执行（如[包源](../consume-packages/install-use-packages-visual-studio.md#package-sources)中所述），或使用 [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) 从命令行执行操作。 源的路径可以是本地文件夹路径名、网络名称或 URL。
