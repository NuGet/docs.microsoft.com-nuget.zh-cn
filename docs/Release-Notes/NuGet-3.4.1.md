---
title: "NuGet 3.4.1 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "发行说明，了解 NuGet 3.4.1 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。"
keywords: "NuGet 3.4.1 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c2e22b6c22c55fd51bd1d20d52b4b7b07c5a205c
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-341-release-notes"></a><span data-ttu-id="796fe-104">NuGet 3.4.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="796fe-104">NuGet 3.4.1 Release Notes</span></span>

<span data-ttu-id="796fe-105">[NuGet 3.4 发行说明](../release-notes/nuget-3.4.md) | [NuGet 上面 3.4.2 发行说明](../release-notes/nuget-3.4.2.md)</span><span class="sxs-lookup"><span data-stu-id="796fe-105">[NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md) | [NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md)</span></span>

<span data-ttu-id="796fe-106">NuGet 3.4.1 已于 2016 年 3 月 30，在作为 Visual Studio 2015 Update 2 并选择 Visual Studio 15 预览版发行解决发现 3.4 版本中的几个问题的同时发布。</span><span class="sxs-lookup"><span data-stu-id="796fe-106">NuGet 3.4.1 was released March 30, 2016 at the same time as the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release to address several issues that were identified in the 3.4 release.</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="796fe-107">更新和改进</span><span class="sxs-lookup"><span data-stu-id="796fe-107">Updates and Improvements</span></span>

* <span data-ttu-id="796fe-108">已更正了阻止浏览问题包从具有的最小的 Visual Studio 安装的 Visual Studio UI</span><span class="sxs-lookup"><span data-stu-id="796fe-108">Corrected an issue that prevented browsing packages from the Visual Studio UI with a minimum Visual Studio install</span></span>
* <span data-ttu-id="796fe-109">更正查找 Visual Studio 的问题`lucene.net.dll`</span><span class="sxs-lookup"><span data-stu-id="796fe-109">Corrected an issue with Visual Studio locating `lucene.net.dll`</span></span>
* <span data-ttu-id="796fe-110">NuGet 扩展安装或更新之后，所有源不应为默认存储库源。</span><span class="sxs-lookup"><span data-stu-id="796fe-110">All sources should not be the default repository source after a NuGet extension install or update.</span></span>  <span data-ttu-id="796fe-111">你可以选择加入此功能从配置设置。</span><span class="sxs-lookup"><span data-stu-id="796fe-111">You can opt-in to this feature from the configuration settings.</span></span>

<span data-ttu-id="796fe-112">我们继续在我们的 GitHub 问题列表，可在上跟踪问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="796fe-112">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>