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
# <a name="package-readme-on-nugetorg"></a><span data-ttu-id="e45a2-103">NuGet.org 上的包自述文件</span><span class="sxs-lookup"><span data-stu-id="e45a2-103">Package readme on NuGet.org</span></span>

<span data-ttu-id="e45a2-104">[在 NuGet 包中加入自述文件](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile)，以进一步丰富你的包详细信息，并为用户提供更多信息！</span><span class="sxs-lookup"><span data-stu-id="e45a2-104">[Include a readme file in your NuGet package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) to make your package details richer and more informative for your users!</span></span>

<span data-ttu-id="e45a2-105">这很可能是用户在 NuGet.org 上查看包详细信息页时将看到的第一批元素之一，这是提供良好印象的必要操作！</span><span class="sxs-lookup"><span data-stu-id="e45a2-105">This is likely one of the first elements users will see when they view your package details page on NuGet.org and is essential to making a good impression!</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e45a2-106">NuGet.org 仅支持 [Markdown](https://daringfireball.net/projects/markdown/) 中的自述文件和有限域中的图像。</span><span class="sxs-lookup"><span data-stu-id="e45a2-106">NuGet.org only supports readme files in [Markdown](https://daringfireball.net/projects/markdown/) and images from a limited set of domains.</span></span> <span data-ttu-id="e45a2-107">请参阅我们[允许用于映像的域](#allowed-domains-for-images-and-badges)和[支持的 Markdown 功能](#supported-markdown-features)，以确保自述文件在 NuGet.org 上正确呈现。</span><span class="sxs-lookup"><span data-stu-id="e45a2-107">See our [allowed domains for images](#allowed-domains-for-images-and-badges) and [supported Markdown features](#supported-markdown-features) to ensure your readme renders correctly on NuGet.org.</span></span>

## <a name="what-should-my-readme-include"></a><span data-ttu-id="e45a2-108">自述文件包括哪些内容？</span><span class="sxs-lookup"><span data-stu-id="e45a2-108">What should my readme include?</span></span>

<span data-ttu-id="e45a2-109">请考虑在自述文件中包含以下各项：</span><span class="sxs-lookup"><span data-stu-id="e45a2-109">Consider including the following items in your readme:</span></span>
* <span data-ttu-id="e45a2-110">介绍包的内容和功能：它可以解决什么问题？</span><span class="sxs-lookup"><span data-stu-id="e45a2-110">An introduction to what your package is and does - what problems does it solve?</span></span>
* <span data-ttu-id="e45a2-111">包的使用方法：是否有特定的要求？</span><span class="sxs-lookup"><span data-stu-id="e45a2-111">How to get started with your package - are there any specific requirements?</span></span>
* <span data-ttu-id="e45a2-112">如果不包含在自述文件中，则提供更全面的文档。</span><span class="sxs-lookup"><span data-stu-id="e45a2-112">Links to more comprehensive documentation if not included in the readme itself.</span></span>
* <span data-ttu-id="e45a2-113">至少有几个代码片段/示例或示例图像。</span><span class="sxs-lookup"><span data-stu-id="e45a2-113">At least a few code snippets/samples or example images.</span></span>
* <span data-ttu-id="e45a2-114">提供反馈的方法，如项目问题链接、Twitter、bug 跟踪器或其他平台。</span><span class="sxs-lookup"><span data-stu-id="e45a2-114">Where and how to leave feedback such as link to the project issues, Twitter, bug tracker, or other platform.</span></span>
* <span data-ttu-id="e45a2-115">提供方式（如果适用）。</span><span class="sxs-lookup"><span data-stu-id="e45a2-115">How to contribute, if applicable.</span></span>

<span data-ttu-id="e45a2-116">请记住，优质字数文件可以提供多种格式、形状和大小！</span><span class="sxs-lookup"><span data-stu-id="e45a2-116">Keep in mind, high quality readmes can come in a wide variety of formats, shapes, and sizes!</span></span> <span data-ttu-id="e45a2-117">如果在 NuGet.org 上已有一个包，则可能是你的存储库已有 `readme.md` 或其他文档文件，该存储库会为 NuGet.org 详细信息页提供又一出色选择。</span><span class="sxs-lookup"><span data-stu-id="e45a2-117">If you already have a package available on NuGet.org, chances are that you already have a `readme.md` or other documentation file in your repository that would be a great addition to your NuGet.org details page.</span></span>

## <a name="preview-your-readme"></a><span data-ttu-id="e45a2-118">预览自述文件</span><span class="sxs-lookup"><span data-stu-id="e45a2-118">Preview your readme</span></span>

<span data-ttu-id="e45a2-119">若要在发布到 NuGet.org 之前预览自述文件，请使用 [NuGet.org 上的上传包 Web 门户](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg)上传包，并向下滚动到元数据预览的“自述文件”部分。</span><span class="sxs-lookup"><span data-stu-id="e45a2-119">To preview your readme file before it's live on NuGet.org, upload your package using the [Upload Package web portal on NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) and scroll down to the "Readme File" section of the metadata preview.</span></span> <span data-ttu-id="e45a2-120">结果应如下所示：</span><span class="sxs-lookup"><span data-stu-id="e45a2-120">It should look something like this:</span></span>

![自述文件预览](media\readme-upload-preview.PNG)

<span data-ttu-id="e45a2-122">请考虑花时间查看和预览你的自述文件，以获得[图像符合性](#allowed-domains-for-images-and-badges)和[支持的格式](#supported-markdown-features)，以确保该文件可为潜在用户提供极佳的第一印象！</span><span class="sxs-lookup"><span data-stu-id="e45a2-122">Consider taking time to review and preview your readme file for [image compliance](#allowed-domains-for-images-and-badges) and [supported formatting](#supported-markdown-features) to make sure it gives a great first impression to potential users!</span></span> <span data-ttu-id="e45a2-123">若要在将包自述文件发布到 NuGet.org 时更正其错误，你需要将更新的包版本推送到该修补程序。</span><span class="sxs-lookup"><span data-stu-id="e45a2-123">To correct mistakes on your package readme once it's published to NuGet.org, you will need to push an updated package version with the fix.</span></span> <span data-ttu-id="e45a2-124">提前确保一切正常，可以帮你省却一切烦心。</span><span class="sxs-lookup"><span data-stu-id="e45a2-124">Making sure everything looks good in advance may save you headache down the road.</span></span>
## <a name="allowed-domains-for-images-and-badges"></a><span data-ttu-id="e45a2-125">允许用于图像和徽章的域</span><span class="sxs-lookup"><span data-stu-id="e45a2-125">Allowed domains for images and badges</span></span>

<span data-ttu-id="e45a2-126">出于安全和隐私方面的考虑，NuGet.org 限制了可向受信任的主机呈现图像和徽章的域。</span><span class="sxs-lookup"><span data-stu-id="e45a2-126">Due to security and privacy concerns, NuGet.org restricts the domains from which images and badges can be rendered to trusted hosts.</span></span> 

<span data-ttu-id="e45a2-127">NuGet.org 允许呈现以下受信任域中的所有图像（包括徽章）：</span><span class="sxs-lookup"><span data-stu-id="e45a2-127">NuGet.org allows all images, including badges, from the following trusted domains to be rendered:</span></span>
* <span data-ttu-id="e45a2-128">api.bintray.com</span><span class="sxs-lookup"><span data-stu-id="e45a2-128">api.bintray.com</span></span>
* <span data-ttu-id="e45a2-129">api.codacy.com</span><span class="sxs-lookup"><span data-stu-id="e45a2-129">api.codacy.com</span></span>
* <span data-ttu-id="e45a2-130">api.codeclimate.com</span><span class="sxs-lookup"><span data-stu-id="e45a2-130">api.codeclimate.com</span></span>
* <span data-ttu-id="e45a2-131">api.dependabot.com</span><span class="sxs-lookup"><span data-stu-id="e45a2-131">api.dependabot.com</span></span>
* <span data-ttu-id="e45a2-132">api.travis-ci.com</span><span class="sxs-lookup"><span data-stu-id="e45a2-132">api.travis-ci.com</span></span>
* <span data-ttu-id="e45a2-133">api.travis-ci.org</span><span class="sxs-lookup"><span data-stu-id="e45a2-133">api.travis-ci.org</span></span>
* <span data-ttu-id="e45a2-134">app.fossa.io</span><span class="sxs-lookup"><span data-stu-id="e45a2-134">app.fossa.io</span></span>
* <span data-ttu-id="e45a2-135">badge.fury.io</span><span class="sxs-lookup"><span data-stu-id="e45a2-135">badge.fury.io</span></span>
* <span data-ttu-id="e45a2-136">badgen.net</span><span class="sxs-lookup"><span data-stu-id="e45a2-136">badgen.net</span></span>
* <span data-ttu-id="e45a2-137">badges.gitter.im</span><span class="sxs-lookup"><span data-stu-id="e45a2-137">badges.gitter.im</span></span>
* <span data-ttu-id="e45a2-138">bettercodehub.com</span><span class="sxs-lookup"><span data-stu-id="e45a2-138">bettercodehub.com</span></span>
* <span data-ttu-id="e45a2-139">buildstats.info</span><span class="sxs-lookup"><span data-stu-id="e45a2-139">buildstats.info</span></span>
* <span data-ttu-id="e45a2-140">camo.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="e45a2-140">camo.githubusercontent.com</span></span>
* <span data-ttu-id="e45a2-141">ci.appveyor.com</span><span class="sxs-lookup"><span data-stu-id="e45a2-141">ci.appveyor.com</span></span>
* <span data-ttu-id="e45a2-142">circleci.com</span><span class="sxs-lookup"><span data-stu-id="e45a2-142">circleci.com</span></span>
* <span data-ttu-id="e45a2-143">codecov.io</span><span class="sxs-lookup"><span data-stu-id="e45a2-143">codecov.io</span></span>
* <span data-ttu-id="e45a2-144">codefactor.io</span><span class="sxs-lookup"><span data-stu-id="e45a2-144">codefactor.io</span></span>
* <span data-ttu-id="e45a2-145">coveralls.io</span><span class="sxs-lookup"><span data-stu-id="e45a2-145">coveralls.io</span></span>
* <span data-ttu-id="e45a2-146">dev.azure.com</span><span class="sxs-lookup"><span data-stu-id="e45a2-146">dev.azure.com</span></span>
* <span data-ttu-id="e45a2-147">github.com/.../workflows/.../badge.svg</span><span class="sxs-lookup"><span data-stu-id="e45a2-147">github.com/.../workflows/.../badge.svg</span></span>
* <span data-ttu-id="e45a2-148">gitlab.com</span><span class="sxs-lookup"><span data-stu-id="e45a2-148">gitlab.com</span></span>
* <span data-ttu-id="e45a2-149">img.shields.io</span><span class="sxs-lookup"><span data-stu-id="e45a2-149">img.shields.io</span></span>
* <span data-ttu-id="e45a2-150">isitmaintained.com</span><span class="sxs-lookup"><span data-stu-id="e45a2-150">isitmaintained.com</span></span>
* <span data-ttu-id="e45a2-151">opencollective.com</span><span class="sxs-lookup"><span data-stu-id="e45a2-151">opencollective.com</span></span>
* <span data-ttu-id="e45a2-152">raw.github.com</span><span class="sxs-lookup"><span data-stu-id="e45a2-152">raw.github.com</span></span>
* <span data-ttu-id="e45a2-153">raw.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="e45a2-153">raw.githubusercontent.com</span></span>
* <span data-ttu-id="e45a2-154">snyk.io</span><span class="sxs-lookup"><span data-stu-id="e45a2-154">snyk.io</span></span>
* <span data-ttu-id="e45a2-155">sonarcloud.io</span><span class="sxs-lookup"><span data-stu-id="e45a2-155">sonarcloud.io</span></span>
* <span data-ttu-id="e45a2-156">user-images.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="e45a2-156">user-images.githubusercontent.com</span></span>

<span data-ttu-id="e45a2-157">如果你认为其他域应添加到“允许列表”，请随时[提出问题](https://github.com/NuGet/NuGetGallery/issues)；我们的工程团队将会进行检查，以确保其隐私和安全合规。</span><span class="sxs-lookup"><span data-stu-id="e45a2-157">If you feel that another domain should be added to the allow-list, please feel free to [file an issue](https://github.com/NuGet/NuGetGallery/issues) and it will be reviewed by our engineering team for privacy and security compliance.</span></span> <span data-ttu-id="e45a2-158">系统不会呈现通过不受支持的域托管的相对本地路径和图像的图像，并且将在自述文件预览和包详细信息页面（只对包所有者可见）上生成一条警告。</span><span class="sxs-lookup"><span data-stu-id="e45a2-158">Images with relative local paths and images hosted from unsupported domains will not be rendered and will produce a warning on the readme file preview and package details page that is only visible to the package owners.</span></span>

## <a name="supported-markdown-features"></a><span data-ttu-id="e45a2-159">支持的 Markdown 功能</span><span class="sxs-lookup"><span data-stu-id="e45a2-159">Supported Markdown features</span></span>
<span data-ttu-id="e45a2-160">[Markdown](https://daringfireball.net/projects/markdown/) 是一种轻型标记语言，采用纯文本格式语法。</span><span class="sxs-lookup"><span data-stu-id="e45a2-160">[Markdown](https://daringfireball.net/projects/markdown/) is a lightweight markup language with plain text formatting syntax.</span></span> <span data-ttu-id="e45a2-161">NuGet.org 自述文件通过 [Markdig](https://github.com/lunet-io/markdig) 分析引擎支持 [CommonMark](https://commonmark.org/) 兼容 Markdown。</span><span class="sxs-lookup"><span data-stu-id="e45a2-161">NuGet.org readmes support [CommonMark](https://commonmark.org/) compliant Markdown through the [Markdig](https://github.com/lunet-io/markdig) parsing engine.</span></span>

<span data-ttu-id="e45a2-162">NuGet.org 目前支持以下 Markdown 功能：</span><span class="sxs-lookup"><span data-stu-id="e45a2-162">NuGet.org currently supports the following Markdown features:</span></span>
* [<span data-ttu-id="e45a2-163">标头</span><span class="sxs-lookup"><span data-stu-id="e45a2-163">Headers</span></span>](https://spec.commonmark.org/0.29/#atx-headings)
* [<span data-ttu-id="e45a2-164">映像</span><span class="sxs-lookup"><span data-stu-id="e45a2-164">Images</span></span>](https://spec.commonmark.org/0.29/#images)
* [<span data-ttu-id="e45a2-165">特别强调</span><span class="sxs-lookup"><span data-stu-id="e45a2-165">Extra emphasis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [<span data-ttu-id="e45a2-166">列表</span><span class="sxs-lookup"><span data-stu-id="e45a2-166">Lists</span></span>](https://spec.commonmark.org/0.29/#lists)
* [<span data-ttu-id="e45a2-167">链接</span><span class="sxs-lookup"><span data-stu-id="e45a2-167">Links</span></span>](https://spec.commonmark.org/0.29/#links)
* [<span data-ttu-id="e45a2-168">块引用</span><span class="sxs-lookup"><span data-stu-id="e45a2-168">Block quotes</span></span>](https://spec.commonmark.org/0.29/#block-quotes)
* [<span data-ttu-id="e45a2-169">反斜杠转义</span><span class="sxs-lookup"><span data-stu-id="e45a2-169">Backslash escapes</span></span>](https://spec.commonmark.org/0.29/#backslash-escapes)
* [<span data-ttu-id="e45a2-170">代码范围</span><span class="sxs-lookup"><span data-stu-id="e45a2-170">Code spans</span></span>](https://spec.commonmark.org/0.29/#code-spans)
* [<span data-ttu-id="e45a2-171">任务列表</span><span class="sxs-lookup"><span data-stu-id="e45a2-171">Task lists</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [<span data-ttu-id="e45a2-172">表</span><span class="sxs-lookup"><span data-stu-id="e45a2-172">Tables</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [<span data-ttu-id="e45a2-173">表情符号</span><span class="sxs-lookup"><span data-stu-id="e45a2-173">Emojis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [<span data-ttu-id="e45a2-174">自动链接</span><span class="sxs-lookup"><span data-stu-id="e45a2-174">Auto-links</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

