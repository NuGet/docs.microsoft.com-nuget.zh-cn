---
title: "NuGet 3.0 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "发行说明，了解 NuGet 3.0.0 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。"
keywords: "NuGet 3.0.0 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ef8557c37105eb7915919c7b15d41d024921761f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="71fbf-104">NuGet 3.0 发行说明</span><span class="sxs-lookup"><span data-stu-id="71fbf-104">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="71fbf-105">[NuGet 3.0 RC2 发行说明](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 发行说明](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="71fbf-105">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="71fbf-106">NuGet 3.0 于 2015 年 7 月 20 日发布为 Visual Studio 2015 的捆绑扩展。</span><span class="sxs-lookup"><span data-stu-id="71fbf-106">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="71fbf-107">我们推送以提供使用 Visual Studio 的此版本，以便完成更新的 NuGet 3.0 体验将可用于新的 Visual Studio 用户。</span><span class="sxs-lookup"><span data-stu-id="71fbf-107">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="71fbf-108">此 NuGet 扩展版本仅可用于 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="71fbf-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="71fbf-109">我们建议这些开发人员有权访问不可用，因为我们要包含适用于 Windows 10 开发支持的 Visual Studio 2015 的发布后，将很快发布更新的最新版本的 Visual Studio 库更新。</span><span class="sxs-lookup"><span data-stu-id="71fbf-109">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="71fbf-110">我们已关闭，总共 240 问题在 3.0 版本中，并可以检查[GitHub 上的问题的完整列表](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)。</span><span class="sxs-lookup"><span data-stu-id="71fbf-110">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="71fbf-111">已知问题</span><span class="sxs-lookup"><span data-stu-id="71fbf-111">Known Issues</span></span>

<span data-ttu-id="71fbf-112">有大量的时候附带此版本的已知问题，我们计划的 3.1 版本，以便在年 7 月 29 上保持一致随着 Windows 10 的发布中修复所有这些项。</span><span class="sxs-lookup"><span data-stu-id="71fbf-112">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="71fbf-113">你将能够更新你从库该日期以解决这些已知的问题或之后的 Visual Studio 扩展。</span><span class="sxs-lookup"><span data-stu-id="71fbf-113">You will be able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="71fbf-114">在预览窗口上的"不再显示此对话框"标签和包描述窗口中的"作者"标签不提供转换。</span><span class="sxs-lookup"><span data-stu-id="71fbf-114">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="71fbf-115">当你通过使用 TFS 处理项目源代码管理时，NuGet 不能显示包管理器用户界面如果 Nuget.Config 文件标记为只读的。</span><span class="sxs-lookup"><span data-stu-id="71fbf-115">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="71fbf-116">**解决方法**签出该文件从 TFS。</span><span class="sxs-lookup"><span data-stu-id="71fbf-116">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="71fbf-117">当你使用 Visual Studio 深色主题时，黄色 NuGet Powershell 窗口中的"重新启动栏"中的文本不可见。</span><span class="sxs-lookup"><span data-stu-id="71fbf-117">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="71fbf-118">**解决方法**使用 Visual Studio 浅色主题。</span><span class="sxs-lookup"><span data-stu-id="71fbf-118">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="71fbf-119">已解决的最主要问题的摘要</span><span class="sxs-lookup"><span data-stu-id="71fbf-119">Summary of top issues resolved</span></span>

* [<span data-ttu-id="71fbf-120">包管理器窗口刷新一次时，将调用频繁网络更新</span><span class="sxs-lookup"><span data-stu-id="71fbf-120">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="71fbf-121">将更改为安装在程序包管理器中的视图时延迟滚动</span><span class="sxs-lookup"><span data-stu-id="71fbf-121">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="71fbf-122">应在后台线程上运行网络调用</span><span class="sxs-lookup"><span data-stu-id="71fbf-122">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="71fbf-123">添加不显示预览窗口复选框</span><span class="sxs-lookup"><span data-stu-id="71fbf-123">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="71fbf-124">添加的进程限制以减少处理器使用率</span><span class="sxs-lookup"><span data-stu-id="71fbf-124">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="71fbf-125">改进了可移植类库引用处理</span><span class="sxs-lookup"><span data-stu-id="71fbf-125">Improved portable-class-library reference handling</span></span>
    * [<span data-ttu-id="71fbf-126">https://github.com/NuGet/Home/issues/562</span><span class="sxs-lookup"><span data-stu-id="71fbf-126">https://github.com/NuGet/Home/issues/562</span></span>](https://github.com/NuGet/Home/issues/562)
    * [<span data-ttu-id="71fbf-127">https://github.com/NuGet/Home/issues/454</span><span class="sxs-lookup"><span data-stu-id="71fbf-127">https://github.com/NuGet/Home/issues/454</span></span>](https://github.com/NuGet/Home/issues/454)
    * [<span data-ttu-id="71fbf-128">https://github.com/NuGet/Home/issues/440</span><span class="sxs-lookup"><span data-stu-id="71fbf-128">https://github.com/NuGet/Home/issues/440</span></span>](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="71fbf-129">记忆式键入功能服务不区分大小写</span><span class="sxs-lookup"><span data-stu-id="71fbf-129">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="71fbf-130">更新，以重新引入基本身份验证凭据</span><span class="sxs-lookup"><span data-stu-id="71fbf-130">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="71fbf-131">改进的错误日志记录</span><span class="sxs-lookup"><span data-stu-id="71fbf-131">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="71fbf-132">改进了的 powershell 调用更新包时的错误消息</span><span class="sxs-lookup"><span data-stu-id="71fbf-132">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="71fbf-133">固定的了解有关选项的信息链接，以防止在 Windows 10 上发生故障</span><span class="sxs-lookup"><span data-stu-id="71fbf-133">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="71fbf-134">请记住预发行版复选框设置</span><span class="sxs-lookup"><span data-stu-id="71fbf-134">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="71fbf-135">通过跨解决方案中的项目中缓存结果的改进的收集性能</span><span class="sxs-lookup"><span data-stu-id="71fbf-135">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="71fbf-136">可以并行收集多个包</span><span class="sxs-lookup"><span data-stu-id="71fbf-136">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="71fbf-137">删除安装包的强制命令</span><span class="sxs-lookup"><span data-stu-id="71fbf-137">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="71fbf-138">请留意[我们的博客](http://blog.nuget.org)了解详细的进度和公告如我们准备好为 Windows 10 开发提供支持。</span><span class="sxs-lookup"><span data-stu-id="71fbf-138">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>