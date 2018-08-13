---
title: 承载自己的 NuGet 源概述
description: 概述了本地或远程承载自己的 NuGet 包源或库的打开。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 95750bc926c242c02112f68a5aebf43c5fdb9a46
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508291"
---
# <a name="hosting-your-own-nuget-feeds"></a>承载自己的 NuGet 源

可能希望将包仅发布到有限受众（例如，组织或工作组），而不是将其公开发布。 此外，一些公司可能希望限制其开发人员可以使用的第三方库，使他们从有限包源（而不是 nuget.org）中提取内容。

对于所有此类目的，NuGet 支持通过以下方式设置专用包源：

- 本地源：包只需放置在合适的网络文件共享中，理想情况下使用 `nuget init` 和 `nuget add` 创建分层文件夹结构 (NuGet 3.3+)。 有关详细信息，请参阅[本地源](../hosting-packages/local-feeds.md)。
- NuGet.Server：通过本地 HTTP 服务器提供包。 有关详细信息，请参阅 [NuGet.Server](../hosting-packages/nuget-server.md)。
- NuGet 库：在使用 [NuGet 库项目](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com) 的 Internet 服务器上承载包。 NuGet 库提供用户管理和功能，如丰富的 Web UI，它允许从浏览器中搜索和浏览包，这与 nuget.org 相似。

还有其他几个 NuGet 承载产品也支持远程专用源，其中包括：

- [Visual Studio Team Services 包管理](https://www.visualstudio.com/docs/package/nuget/publish)，Team Foundation Server 2017 及更高版本上也提供此产品。
- [MyGet](http://myget.org)
- Inedo 的 [ProGet](http://inedo.com/proget)
- [NuGet 服务器](http://nugetserver.net/)，Inedo 的社区项目
- [NuGet 服务器（开放源代码）](http://nuget-server.net)，与 Inedo 的 NuGet 服务器相似的开放源代码实现
- [LiGet](https://github.com/ai-traders/liget)：在 docker 中 kestrel 上运行的 NuGet V2 服务器的开放源代码实现
- [BaGet](https://github.com/loic-sharma/BaGet) 构建与 ASP.NET Core 基础上的 NuGet V3 服务器的开源实现
- JFrog 的 [Artifactory](https://www.jfrog.com/artifactory/)。
- Sonatype 的 [Nexus](http://www.sonatype.org/nexus/)。
- JetBrains 的 [TeamCity](https://www.jetbrains.com/teamcity/)。

无论包是什么样的承载方式，均可将其添加到 `NuGet.Config` 中的可用源列表以便访问。 此操作可在 Visual Studio 中执行（如[包源](../tools/package-manager-ui.md#package-sources)中所述），或使用 [`nuget sources`](../tools/cli-ref-sources.md) 从命令行执行操作。 源的路径可以是本地文件夹路径名、网络名称或 URL。
