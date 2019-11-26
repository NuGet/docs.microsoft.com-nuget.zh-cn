---
title: 弃用 nuget.org 上的包
description: 详细介绍包弃用过程以及客户端如何显示此信息
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096885"
---
# <a name="deprecating-packages"></a><span data-ttu-id="3249e-103">弃用包</span><span class="sxs-lookup"><span data-stu-id="3249e-103">Deprecating packages</span></span>

<span data-ttu-id="3249e-104">如果不再维护某个包，或者希望鼓励该包的使用者移到其他包，可将此包弃用。</span><span class="sxs-lookup"><span data-stu-id="3249e-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="3249e-105">如下所示，包弃用与取消列出包不同  ：</span><span class="sxs-lookup"><span data-stu-id="3249e-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="3249e-106">取消列出包会阻止它的发现，因为包会在搜索列表中隐藏  。</span><span class="sxs-lookup"><span data-stu-id="3249e-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="3249e-107">而弃用包可让包的现有使用者了解其是否已在其项目中安装或使用此包  。</span><span class="sxs-lookup"><span data-stu-id="3249e-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="3249e-108">它还让使用者了解弃用原因以及你（包发布者）指定的备用推荐包。</span><span class="sxs-lookup"><span data-stu-id="3249e-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="3249e-109">弃用包后，包仍会列出。</span><span class="sxs-lookup"><span data-stu-id="3249e-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="3249e-110">作为包发布者，你可选择同时弃用和取消列出包。</span><span class="sxs-lookup"><span data-stu-id="3249e-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="3249e-111">弃用工作流</span><span class="sxs-lookup"><span data-stu-id="3249e-111">Deprecation workflow</span></span>
1. <span data-ttu-id="3249e-112">要弃用包，请转到“管理包”，然后选择“弃用”   ：</span><span class="sxs-lookup"><span data-stu-id="3249e-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![转到“弃用包”选项](media/deprecation-select-option.png)

2. <span data-ttu-id="3249e-114">选择要弃用的版本。</span><span class="sxs-lookup"><span data-stu-id="3249e-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="3249e-115">要弃用所有版本，请选中“选择所有版本”选项  。</span><span class="sxs-lookup"><span data-stu-id="3249e-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![选择要弃用的包版本](media/deprecation-select-version.png)

3. <span data-ttu-id="3249e-117">选择弃用原因。</span><span class="sxs-lookup"><span data-stu-id="3249e-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="3249e-118">如果不再维护包，请选择“旧版”选项  。</span><span class="sxs-lookup"><span data-stu-id="3249e-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="3249e-119">如果特定版本有关键 bug，请选择“存在关键 bug”选项  。</span><span class="sxs-lookup"><span data-stu-id="3249e-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="3249e-120">对于其他任何原因，请选择“其他”  。</span><span class="sxs-lookup"><span data-stu-id="3249e-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="3249e-121">始终可为所有者指定备用推荐包（及版本）和自定义消息。</span><span class="sxs-lookup"><span data-stu-id="3249e-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![选择备用包推荐和自定义消息的原因](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="3249e-123">自定义消息仅在 nuget.org 上显示，而不显示在客户端上。</span><span class="sxs-lookup"><span data-stu-id="3249e-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="3249e-124">目前，`dotnet.exe` 和 NuGet 包管理器等客户端不会显示自定义消息。</span><span class="sxs-lookup"><span data-stu-id="3249e-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="3249e-125">有关已弃用包的客户端体验</span><span class="sxs-lookup"><span data-stu-id="3249e-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="3249e-126">某个包一旦被弃用，其使用者就会（根据使用的客户端）通过以下方式收到通知。</span><span class="sxs-lookup"><span data-stu-id="3249e-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="3249e-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3249e-127">Visual Studio</span></span> 
<span data-ttu-id="3249e-128">*自 Visual Studio 2019 版本16.3 起可用*</span><span class="sxs-lookup"><span data-stu-id="3249e-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="3249e-129">Visual Studio 警告称 `Installed` 选项卡上使用了已弃用的包。它将显示有关此包的警告及其弃用信息（内附弃用原因和改用的备用包（若有））。</span><span class="sxs-lookup"><span data-stu-id="3249e-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab. It will show a warning for the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![包管理器的 Visual Studio installed 选项卡上的已弃用的包](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="3249e-131">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="3249e-131">dotnet.exe</span></span>
<span data-ttu-id="3249e-132">*自 .NET SDK 3.0 起可用*</span><span class="sxs-lookup"><span data-stu-id="3249e-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="3249e-133">如果使用 dotnet.exe，则可在解决方案或项目文件夹上运行 `dotnet list package --deprecated` 命令，以获取列表了解已弃用的包及相关弃用信息：</span><span class="sxs-lookup"><span data-stu-id="3249e-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
