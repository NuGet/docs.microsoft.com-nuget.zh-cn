---
title: NuGet 3.0 发行说明
description: NuGet 3.0.0 包括的发行说明的已知问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551858"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="c258c-103">NuGet 3.0 发行说明</span><span class="sxs-lookup"><span data-stu-id="c258c-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="c258c-104">[NuGet 3.0 RC2 发行说明](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 发行说明](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="c258c-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="c258c-105">NuGet 3.0 作为捆绑扩展到 Visual Studio 2015 发布于 2015 年 7 月 20 日。</span><span class="sxs-lookup"><span data-stu-id="c258c-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="c258c-106">我们推送来提供此版本中的使用 Visual Studio，以便完成更新后的 NuGet 3.0 体验将可用于新的 Visual Studio 用户。</span><span class="sxs-lookup"><span data-stu-id="c258c-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="c258c-107">此 NuGet 扩展版本才可用于 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="c258c-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="c258c-108">我们建议有权访问不可用，因为我们要发布包含对 Windows 10 开发的支持的 Visual Studio 2015 发布更新的最新版本的 Visual Studio 库更新这些开发人员。</span><span class="sxs-lookup"><span data-stu-id="c258c-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="c258c-109">总的来说，我们已关闭的 240 问题在 3.0 版本中，并可以检查[GitHub 上的问题的完整列表](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)。</span><span class="sxs-lookup"><span data-stu-id="c258c-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="c258c-110">已知问题</span><span class="sxs-lookup"><span data-stu-id="c258c-110">Known Issues</span></span>

<span data-ttu-id="c258c-111">出了很多已知问题随此版本中，且所有这些项在我们计划的 3.1 版本，以便与 Windows 10 版本保持一致上年 7 月 29, 中修复。</span><span class="sxs-lookup"><span data-stu-id="c258c-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="c258c-112">您将能够更新你的 Visual Studio 扩展从库或之后的日期来解决这些已知的问题。</span><span class="sxs-lookup"><span data-stu-id="c258c-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="c258c-113">在预览窗口上的"不再显示此信息"标签和包描述窗口中的"作者"标签不提供翻译。</span><span class="sxs-lookup"><span data-stu-id="c258c-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="c258c-114">当你使用 TFS 处理项目源代码管理时，NuGet 不能显示包管理器用户界面如果 Nuget.Config 文件标记为只读的。</span><span class="sxs-lookup"><span data-stu-id="c258c-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="c258c-115">**解决方法**签出该文件从 TFS。</span><span class="sxs-lookup"><span data-stu-id="c258c-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="c258c-116">使用 Visual Studio 深色主题时，黄色 NuGet Powershell 窗口中的"重新启动栏"中的文本不可见。</span><span class="sxs-lookup"><span data-stu-id="c258c-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="c258c-117">**解决方法**使用 Visual Studio 浅色主题。</span><span class="sxs-lookup"><span data-stu-id="c258c-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="c258c-118">已解决的热门问题的摘要</span><span class="sxs-lookup"><span data-stu-id="c258c-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="c258c-119">刷新包管理器窗口时将调用频繁网络更新</span><span class="sxs-lookup"><span data-stu-id="c258c-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="c258c-120">更改为安装在包管理器中的视图时，延迟滚动</span><span class="sxs-lookup"><span data-stu-id="c258c-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="c258c-121">网络调用应在后台线程上运行</span><span class="sxs-lookup"><span data-stu-id="c258c-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="c258c-122">添加了不显示预览窗口复选框</span><span class="sxs-lookup"><span data-stu-id="c258c-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="c258c-123">添加了的过程限制以减少处理器使用情况</span><span class="sxs-lookup"><span data-stu-id="c258c-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="c258c-124">改进的可移植类库参考处理</span><span class="sxs-lookup"><span data-stu-id="c258c-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="c258c-125">记忆式键入功能服务是区分大小写</span><span class="sxs-lookup"><span data-stu-id="c258c-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="c258c-126">更新重新引入基本身份验证凭据</span><span class="sxs-lookup"><span data-stu-id="c258c-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="c258c-127">改进的错误日志记录</span><span class="sxs-lookup"><span data-stu-id="c258c-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="c258c-128">改进了的 powershell 调用更新包时的错误消息</span><span class="sxs-lookup"><span data-stu-id="c258c-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="c258c-129">修复了了解有关选项的信息链接，以防止在 Windows 10 上崩溃，</span><span class="sxs-lookup"><span data-stu-id="c258c-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="c258c-130">请记住预发行版复选框设置</span><span class="sxs-lookup"><span data-stu-id="c258c-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="c258c-131">改进了的收集性能的方式跨解决方案中的项目缓存结果</span><span class="sxs-lookup"><span data-stu-id="c258c-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="c258c-132">可以并行收集多个包</span><span class="sxs-lookup"><span data-stu-id="c258c-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="c258c-133">删除安装包的强制命令</span><span class="sxs-lookup"><span data-stu-id="c258c-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="c258c-134">请密切关注[我们的博客](http://blog.nuget.org)的更多进度和公告如我们准备好提供对 Windows 10 开发的支持。</span><span class="sxs-lookup"><span data-stu-id="c258c-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>