---
title: NuGet 3.4-RC 发行说明
description: NuGet 3.4 RC 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780237"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="093ee-103">NuGet 3.4-RC 发行说明</span><span class="sxs-lookup"><span data-stu-id="093ee-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="093ee-104">[NuGet 3.3 发行说明](../release-notes/nuget-3.3.md)  | [NuGet 3.4 发行说明](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="093ee-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="093ee-105">NuGet 3.4-RC 于3月3日发布2016，与 Visual Studio 2015 Update 2 RC 一起发布，并且是使用一些思维原则构建的：</span><span class="sxs-lookup"><span data-stu-id="093ee-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="093ee-106">跨平台支持</span><span class="sxs-lookup"><span data-stu-id="093ee-106">Cross-Platform support</span></span>
* <span data-ttu-id="093ee-107">性能改进</span><span class="sxs-lookup"><span data-stu-id="093ee-107">Performance improvements</span></span>
* <span data-ttu-id="093ee-108">细微的 UI 改进</span><span class="sxs-lookup"><span data-stu-id="093ee-108">Minor UI improvements</span></span>

<span data-ttu-id="093ee-109">此 RC 中提供了以下功能，并对3.4 最终版本进行了更多规划。</span><span class="sxs-lookup"><span data-stu-id="093ee-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="093ee-110">新功能</span><span class="sxs-lookup"><span data-stu-id="093ee-110">New Features</span></span>

* <span data-ttu-id="093ee-111">NuGet 客户端现在支持存储库中的 gzip 内容编码</span><span class="sxs-lookup"><span data-stu-id="093ee-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="093ee-112">Xproj 项目中的包支持 Pdb</span><span class="sxs-lookup"><span data-stu-id="093ee-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="093ee-113">在 contentFiles 元素中支持 iOS 和 Android 生成操作</span><span class="sxs-lookup"><span data-stu-id="093ee-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="093ee-114">支持 netstandard 和 netstandardapp framework 名字对象</span><span class="sxs-lookup"><span data-stu-id="093ee-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="093ee-115">新的用户界面功能</span><span class="sxs-lookup"><span data-stu-id="093ee-115">New User Interface Features</span></span>

* <span data-ttu-id="093ee-116">显著提高性能，尤其是在已安装、更新和合并选项卡上</span><span class="sxs-lookup"><span data-stu-id="093ee-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="093ee-117">"已安装" 和 "更新" 选项卡现在按字母顺序排序</span><span class="sxs-lookup"><span data-stu-id="093ee-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="093ee-118">添加了允许刷新搜索的刷新按钮</span><span class="sxs-lookup"><span data-stu-id="093ee-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="093ee-119">更新和改进</span><span class="sxs-lookup"><span data-stu-id="093ee-119">Updates and Improvements</span></span>

* <span data-ttu-id="093ee-120">在中引用 `project.json` 的包含浮动版本的包在每次生成时都不会更新。</span><span class="sxs-lookup"><span data-stu-id="093ee-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="093ee-121">相反，它们仅在强制还原、清理、重新生成或修改时才进行更新 `project.json` 。</span><span class="sxs-lookup"><span data-stu-id="093ee-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="093ee-122">使用 NuGet 配置 UI 时，不再将 nuget.org 存储库源强制转换为项目配置。</span><span class="sxs-lookup"><span data-stu-id="093ee-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="093ee-123">NuGet 不再还原共享项目中的包，也不写入锁定文件。</span><span class="sxs-lookup"><span data-stu-id="093ee-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="093ee-124">我们已改进网络故障并重试处理，使其无法访问或响应缓慢服务器。</span><span class="sxs-lookup"><span data-stu-id="093ee-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="093ee-125">在 Visual Studio 包管理器 UI 中，键盘和鼠标的行为得到了改善。</span><span class="sxs-lookup"><span data-stu-id="093ee-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="093ee-126">现在，我们支持 DNX 中的最新 `project.json` 架构。</span><span class="sxs-lookup"><span data-stu-id="093ee-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="093ee-127">已知问题</span><span class="sxs-lookup"><span data-stu-id="093ee-127">Known Issues</span></span>

<span data-ttu-id="093ee-128">我们继续跟踪 GitHub 问题列表中的问题，可在以下位置找到： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="093ee-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>