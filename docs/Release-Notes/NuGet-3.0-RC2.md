---
title: NuGet 3.0 RC2 发行说明
description: 发行说明 NuGet 3.0 RC2 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: eb8b514fa967cc6ef850483b6b2a5df3ab27a550
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="58ec9-103">NuGet 3.0 RC2 发行说明</span><span class="sxs-lookup"><span data-stu-id="58ec9-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="58ec9-104">[NuGet 3.0 RC 发行说明](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 发行说明](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="58ec9-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="58ec9-105">NuGet 3.0 RC2 于 2015 年 6 月 3 日发布为 Visual Studio 2015 扩展库中的过渡版本和[Codeplex](https://nuget.codeplex.com/releases/view/615507)。</span><span class="sxs-lookup"><span data-stu-id="58ec9-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="58ec9-106">此版本有大量的重要的 bug 修复和性能改进，我们认为重要之前已完成的 Visual Studio 2015 版本。</span><span class="sxs-lookup"><span data-stu-id="58ec9-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="58ec9-107">此 NuGet 扩展版本仅可用于 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="58ec9-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="58ec9-108">我们已关闭，总共 158 问题在此版本中，并可以检查[GitHub 上的问题的完整列表](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01)。</span><span class="sxs-lookup"><span data-stu-id="58ec9-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="58ec9-109">已解决的最主要问题的摘要</span><span class="sxs-lookup"><span data-stu-id="58ec9-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="58ec9-110">包管理器窗口刷新一次时，将调用频繁网络更新</span><span class="sxs-lookup"><span data-stu-id="58ec9-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="58ec9-111">将更改为安装在程序包管理器中的视图时延迟滚动</span><span class="sxs-lookup"><span data-stu-id="58ec9-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="58ec9-112">应在后台线程上运行网络调用</span><span class="sxs-lookup"><span data-stu-id="58ec9-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="58ec9-113">添加不显示预览窗口复选框</span><span class="sxs-lookup"><span data-stu-id="58ec9-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="58ec9-114">添加的进程限制以减少处理器使用率</span><span class="sxs-lookup"><span data-stu-id="58ec9-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="58ec9-115">改进了可移植类库引用处理</span><span class="sxs-lookup"><span data-stu-id="58ec9-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="58ec9-116">记忆式键入功能服务不区分大小写</span><span class="sxs-lookup"><span data-stu-id="58ec9-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="58ec9-117">更新，以重新引入基本身份验证凭据</span><span class="sxs-lookup"><span data-stu-id="58ec9-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="58ec9-118">改进的错误日志记录</span><span class="sxs-lookup"><span data-stu-id="58ec9-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="58ec9-119">改进了的 powershell 调用更新包时的错误消息</span><span class="sxs-lookup"><span data-stu-id="58ec9-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="58ec9-120">下载此[更新到了 NuGet 扩展](https://nuget.codeplex.com/releases/view/615507)从 Codeplex 和请留意[我们的博客](http://blog.nuget.org)了解详细的进度和公告 NuGet 3.0 ！</span><span class="sxs-lookup"><span data-stu-id="58ec9-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>