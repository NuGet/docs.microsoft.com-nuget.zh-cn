---
title: NuGet 3.0 发行说明
description: NuGet 3.0.0 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776553"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="5b6e1-103">NuGet 3.0 发行说明</span><span class="sxs-lookup"><span data-stu-id="5b6e1-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="5b6e1-104">[NuGet 3.0 RC2 发行说明](../release-notes/nuget-3.0-RC2.md)  | [NuGet 3.1 发行说明](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="5b6e1-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="5b6e1-105">NuGet 3.0 于年7月20日发布2015，作为 Visual Studio 2015 的捆绑扩展。</span><span class="sxs-lookup"><span data-stu-id="5b6e1-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="5b6e1-106">我们已推出 Visual Studio 提供此版本，以使新的 Visual Studio 用户可以使用完整的更新 NuGet 3.0 体验。</span><span class="sxs-lookup"><span data-stu-id="5b6e1-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="5b6e1-107">此 NuGet 扩展版本仅适用于 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="5b6e1-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="5b6e1-108">我们建议那些有权访问 Visual Studio 库的开发人员更新到可用的最新版本，因为我们将在 Visual Studio 2015 版本中发布更新，该版本包含对 Windows 10 开发的支持。</span><span class="sxs-lookup"><span data-stu-id="5b6e1-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="5b6e1-109">在3.0 发行版中，我们已解决了240问题，你可以在 [GitHub 上查看问题的完整列表](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)。</span><span class="sxs-lookup"><span data-stu-id="5b6e1-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="5b6e1-110">已知问题</span><span class="sxs-lookup"><span data-stu-id="5b6e1-110">Known Issues</span></span>

<span data-ttu-id="5b6e1-111">此发行版中提供了许多已知问题，所有这些项目都在我们的计划3.1 版本中得到修复，与7月29日发布的 Windows 10 一致。</span><span class="sxs-lookup"><span data-stu-id="5b6e1-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="5b6e1-112">你可以从或之后的库中更新你的 Visual Studio 扩展，以解决这些已知问题。</span><span class="sxs-lookup"><span data-stu-id="5b6e1-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="5b6e1-113">对于 "预览" 窗口中的 "不再显示此项" 标签和 "包说明" 窗口中的 "作者" 标签，不提供翻译。</span><span class="sxs-lookup"><span data-stu-id="5b6e1-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="5b6e1-114">使用 TFS 源代码管理处理项目时，如果 Nuget.Config 文件标记为只读，NuGet 将无法显示包管理器用户界面。</span><span class="sxs-lookup"><span data-stu-id="5b6e1-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="5b6e1-115">**解决方法** 从 TFS 签出文件。</span><span class="sxs-lookup"><span data-stu-id="5b6e1-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="5b6e1-116">使用 Visual Studio 深色主题时，NuGet Powershell 窗口中的黄色 "重新启动栏" 中的文本将不可见。</span><span class="sxs-lookup"><span data-stu-id="5b6e1-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="5b6e1-117">**解决方法** 使用 Visual Studio 浅色主题。</span><span class="sxs-lookup"><span data-stu-id="5b6e1-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="5b6e1-118">解决的首要问题摘要</span><span class="sxs-lookup"><span data-stu-id="5b6e1-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="5b6e1-119">当程序包管理器窗口刷新时频繁进行网络更新调用</span><span class="sxs-lookup"><span data-stu-id="5b6e1-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="5b6e1-120">更改为包管理器中已安装的视图时的延迟滚动</span><span class="sxs-lookup"><span data-stu-id="5b6e1-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="5b6e1-121">应在后台线程上运行网络调用</span><span class="sxs-lookup"><span data-stu-id="5b6e1-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="5b6e1-122">添加了 "不显示预览窗口" 复选框</span><span class="sxs-lookup"><span data-stu-id="5b6e1-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="5b6e1-123">添加了进程限制以减少处理器使用率</span><span class="sxs-lookup"><span data-stu-id="5b6e1-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="5b6e1-124">改进的可移植类库引用处理</span><span class="sxs-lookup"><span data-stu-id="5b6e1-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="5b6e1-125">自动完成服务区分大小写</span><span class="sxs-lookup"><span data-stu-id="5b6e1-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="5b6e1-126">用于重新引入基本身份验证凭据的更新</span><span class="sxs-lookup"><span data-stu-id="5b6e1-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="5b6e1-127">改进了错误日志记录</span><span class="sxs-lookup"><span data-stu-id="5b6e1-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="5b6e1-128">在调用更新包时改进了 powershell 错误消息</span><span class="sxs-lookup"><span data-stu-id="5b6e1-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="5b6e1-129">修复了 "了解选项" 链接以防止在 Windows 10 上崩溃</span><span class="sxs-lookup"><span data-stu-id="5b6e1-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="5b6e1-130">记住预发布复选框设置</span><span class="sxs-lookup"><span data-stu-id="5b6e1-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="5b6e1-131">通过跨解决方案中的项目缓存结果提高了收集性能</span><span class="sxs-lookup"><span data-stu-id="5b6e1-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="5b6e1-132">可以并行收集多个包</span><span class="sxs-lookup"><span data-stu-id="5b6e1-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="5b6e1-133">已删除安装包-force 命令</span><span class="sxs-lookup"><span data-stu-id="5b6e1-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="5b6e1-134">请关注 [我们的博客](http://blog.nuget.org) ，了解更多进度和公告，因为我们已准备好为 Windows 10 开发提供支持。</span><span class="sxs-lookup"><span data-stu-id="5b6e1-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>