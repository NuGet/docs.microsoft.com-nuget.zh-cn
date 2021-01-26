---
title: NuGet 3.0 RC2 发行说明
description: NuGet 3.0 RC2 发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780272"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="4cea4-103">NuGet 3.0 RC2 发行说明</span><span class="sxs-lookup"><span data-stu-id="4cea4-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="4cea4-104">[NuGet 3.0 RC 发行说明](../release-notes/nuget-3.0-RC.md)  | [NuGet 3.0 发行说明](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="4cea4-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="4cea4-105">在3.0 年6月3日发布了 NuGet RC2 2015，作为 Visual Studio 2015 扩展库和 [Codeplex](https://nuget.codeplex.com/releases/view/615507)提供的中间版本。</span><span class="sxs-lookup"><span data-stu-id="4cea4-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="4cea4-106">此版本有很多重要的 bug 修复和性能改进，我们认为在完成的 Visual Studio 2015 版本之前必须发布这些修补程序和性能。</span><span class="sxs-lookup"><span data-stu-id="4cea4-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="4cea4-107">此 NuGet 扩展版本仅适用于 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="4cea4-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="4cea4-108">在此版本中，我们已解决了158问题，你可以在 [GitHub 上查看问题的完整列表](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01)。</span><span class="sxs-lookup"><span data-stu-id="4cea4-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="4cea4-109">解决的首要问题摘要</span><span class="sxs-lookup"><span data-stu-id="4cea4-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="4cea4-110">当程序包管理器窗口刷新时频繁进行网络更新调用</span><span class="sxs-lookup"><span data-stu-id="4cea4-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="4cea4-111">更改为包管理器中已安装的视图时的延迟滚动</span><span class="sxs-lookup"><span data-stu-id="4cea4-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="4cea4-112">应在后台线程上运行网络调用</span><span class="sxs-lookup"><span data-stu-id="4cea4-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="4cea4-113">添加了 "不显示预览窗口" 复选框</span><span class="sxs-lookup"><span data-stu-id="4cea4-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="4cea4-114">添加了进程限制以减少处理器使用率</span><span class="sxs-lookup"><span data-stu-id="4cea4-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="4cea4-115">改进的可移植类库引用处理</span><span class="sxs-lookup"><span data-stu-id="4cea4-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="4cea4-116">自动完成服务区分大小写</span><span class="sxs-lookup"><span data-stu-id="4cea4-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="4cea4-117">用于重新引入基本身份验证凭据的更新</span><span class="sxs-lookup"><span data-stu-id="4cea4-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="4cea4-118">改进了错误日志记录</span><span class="sxs-lookup"><span data-stu-id="4cea4-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="4cea4-119">在调用更新包时改进了 powershell 错误消息</span><span class="sxs-lookup"><span data-stu-id="4cea4-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="4cea4-120">请从 Codeplex 将此 [更新下载到 nuget 扩展](https://nuget.codeplex.com/releases/view/615507) ，并在 [博客](http://blog.nuget.org) 上关注 nuget 3.0 的更多进度和公告！</span><span class="sxs-lookup"><span data-stu-id="4cea4-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>