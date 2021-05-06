---
title: NuGet.org 上的包自述文件
description: 详细说明如何呈现 NuGet.org 上的自述文件以及遇到问题时要执行的操作。
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a5d68329128c9e9d047fe10e08ce41f1ae0895b4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2021
ms.locfileid: "107902222"
---
# <a name="package-readme-on-nugetorg"></a>NuGet.org 上的包自述文件

[在 NuGet 包中加入自述文件](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile)，以进一步丰富你的包详细信息，并为用户提供更多信息！

这很可能是用户在 NuGet.org 上查看包详细信息页时将看到的第一批元素之一，这是提供良好印象的必要操作！

> [!IMPORTANT]
> NuGet.org 仅支持 [Markdown](https://daringfireball.net/projects/markdown/) 中的自述文件和有限域中的图像。 请参阅我们[允许用于映像的域](#allowed-domains-for-images-and-badges)和[支持的 Markdown 功能](#supported-markdown-features)，以确保自述文件在 NuGet.org 上正确呈现。

## <a name="what-should-my-readme-include"></a>自述文件包括哪些内容？

请考虑在自述文件中包含以下各项：
* 介绍包的内容和功能：它可以解决什么问题？
* 包的使用方法：是否有特定的要求？
* 如果不包含在自述文件中，则提供更全面的文档。
* 至少有几个代码片段/示例或示例图像。
* 提供反馈的方法，如项目问题链接、Twitter、bug 跟踪器或其他平台。
* 提供方式（如果适用）。

请记住，优质字数文件可以提供多种格式、形状和大小！ 如果在 NuGet.org 上已有一个包，则可能是你的存储库已有 `readme.md` 或其他文档文件，该存储库会为 NuGet.org 详细信息页提供又一出色选择。

## <a name="preview-your-readme"></a>预览自述文件

若要在发布到 NuGet.org 之前预览自述文件，请使用 [NuGet.org 上的上传包 Web 门户](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg)上传包，并向下滚动到元数据预览的“自述文件”部分。 结果应如下所示：

![自述文件预览](media\readme-upload-preview.PNG)

请考虑花时间查看和预览你的自述文件，以获得[图像符合性](#allowed-domains-for-images-and-badges)和[支持的格式](#supported-markdown-features)，以确保该文件可为潜在用户提供极佳的第一印象！ 若要在将包自述文件发布到 NuGet.org 时更正其错误，你需要将更新的包版本推送到该修补程序。 提前确保一切正常，可以帮你省却一切烦心。
## <a name="allowed-domains-for-images-and-badges"></a>允许用于图像和徽章的域

出于安全和隐私方面的考虑，NuGet.org 限制了可向受信任的主机呈现图像和徽章的域。 

NuGet.org 允许呈现以下受信任域中的所有图像（包括徽章）：
* api.bintray.com
* api.codacy.com
* api.codeclimate.com
* api.dependabot.com
* api.travis-ci.com
* api.travis-ci.org
* app.fossa.io
* badge.fury.io
* badgen.net
* badges.gitter.im
* bettercodehub.com
* buildstats.info
* camo.githubusercontent.com
* ci.appveyor.com
* circleci.com
* codecov.io
* codefactor.io
* coveralls.io
* dev.azure.com
* github.com/.../workflows/.../badge.svg
* gitlab.com
* img.shields.io
* isitmaintained.com
* opencollective.com
* raw.github.com
* raw.githubusercontent.com
* snyk.io
* sonarcloud.io
* user-images.githubusercontent.com

如果你认为其他域应添加到“允许列表”，请随时[提出问题](https://github.com/NuGet/NuGetGallery/issues)；我们的工程团队将会进行检查，以确保其隐私和安全合规。 系统不会呈现通过不受支持的域托管的相对本地路径和图像的图像，并且将在自述文件预览和包详细信息页面（只对包所有者可见）上生成一条警告。

## <a name="supported-markdown-features"></a>支持的 Markdown 功能
[Markdown](https://daringfireball.net/projects/markdown/) 是一种轻型标记语言，采用纯文本格式语法。 NuGet.org 自述文件通过 [Markdig](https://github.com/lunet-io/markdig) 分析引擎支持 [CommonMark](https://commonmark.org/) 兼容 Markdown。

NuGet.org 目前支持以下 Markdown 功能：
* [标头](https://spec.commonmark.org/0.29/#atx-headings)
* [映像](https://spec.commonmark.org/0.29/#images)
* [特别强调](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [列表](https://spec.commonmark.org/0.29/#lists)
* [链接](https://spec.commonmark.org/0.29/#links)
* [块引用](https://spec.commonmark.org/0.29/#block-quotes)
* [反斜杠转义](https://spec.commonmark.org/0.29/#backslash-escapes)
* [代码范围](https://spec.commonmark.org/0.29/#code-spans)
* [任务列表](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [表](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [表情符号](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [自动链接](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

