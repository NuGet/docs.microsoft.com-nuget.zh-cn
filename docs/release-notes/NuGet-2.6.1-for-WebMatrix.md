---
title: NuGet 2.6.1 for WebMatrix 发行说明
description: NuGet 2.6.1 for WebMatrix 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780415"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="d2228-103">NuGet 2.6.1 for WebMatrix 发行说明</span><span class="sxs-lookup"><span data-stu-id="d2228-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="d2228-104">[NuGet 2.6 发行说明](../release-notes/nuget-2.6.md)  | [NuGet 2.7 发行说明](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="d2228-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="d2228-105">NuGet 团队在2014年3月26日发布了更新的适用于 WebMatrix 的 NuGet 包管理器扩展。</span><span class="sxs-lookup"><span data-stu-id="d2228-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="d2228-106">可以使用以下步骤从 [WebMatrix 扩展库](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) 安装此更新：</span><span class="sxs-lookup"><span data-stu-id="d2228-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="d2228-107">打开 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="d2228-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="d2228-108">单击 "主页" 功能区中的扩展图标</span><span class="sxs-lookup"><span data-stu-id="d2228-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="d2228-109">选择 "更新" 选项卡</span><span class="sxs-lookup"><span data-stu-id="d2228-109">Select the Updates tab</span></span>
1. <span data-ttu-id="d2228-110">单击以将 NuGet 包管理器更新到2.6。1</span><span class="sxs-lookup"><span data-stu-id="d2228-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="d2228-111">关闭并重新启动 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="d2228-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="d2228-112">显著更改</span><span class="sxs-lookup"><span data-stu-id="d2228-112">Notable Changes</span></span>

<span data-ttu-id="d2228-113">此扩展更新解决了用户在 WebMatrix 中使用 NuGet 包的两个最大问题。</span><span class="sxs-lookup"><span data-stu-id="d2228-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="d2228-114">第一种是 NuGet 架构版本错误，第二种是导致文件夹中的零字节 Dll 出现错误 `bin` 。</span><span class="sxs-lookup"><span data-stu-id="d2228-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="d2228-115">NuGet 架构版本错误</span><span class="sxs-lookup"><span data-stu-id="d2228-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="d2228-116">由于 WebMatrix 3 已发布，因此 NuGet 中引入了新功能，需要 NuGet 包的新架构版本。</span><span class="sxs-lookup"><span data-stu-id="d2228-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="d2228-117">尝试在网站中管理 NuGet 包时，这些新包可能会导致在 WebMatrix 中看到的错误。</span><span class="sxs-lookup"><span data-stu-id="d2228-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![出现了错误。](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="d2228-121">此最新版本提供了与最新 NuGet 包的兼容性，从而防止发生此错误。</span><span class="sxs-lookup"><span data-stu-id="d2228-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="d2228-122">新版本的包（包括 Microsoft）现在可以安装在 WebMatrix 中。</span><span class="sxs-lookup"><span data-stu-id="d2228-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="d2228-123">其中一些包使用的是 NuGet 功能，如 [XDT config 转换](../release-notes/nuget-2.6.md#xdt)，这在 WebMatrix 中目前不受支持。</span><span class="sxs-lookup"><span data-stu-id="d2228-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="d2228-124">Zero-Byte bin 文件夹中的 Dll</span><span class="sxs-lookup"><span data-stu-id="d2228-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="d2228-125">某些用户报告在 WebMatrix 中安装了包含复制到 bin 的 Dll 的 NuGet 包后，Dll 会在文件夹中显示 `bin` 为0字节文件。</span><span class="sxs-lookup"><span data-stu-id="d2228-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="d2228-126">这会在运行时中断应用程序。</span><span class="sxs-lookup"><span data-stu-id="d2228-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="d2228-127">[此问题](https://nuget.codeplex.com/workitem/4060) 现已解决。</span><span class="sxs-lookup"><span data-stu-id="d2228-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="d2228-128">其他最新改进</span><span class="sxs-lookup"><span data-stu-id="d2228-128">Other Recent Improvements</span></span>

<span data-ttu-id="d2228-129">发布适用于 Visual Studio 的 NuGet 包管理器2.8 时，我们还发布了适用于 WebMatrix 的 NuGet 包管理器2.5.0。</span><span class="sxs-lookup"><span data-stu-id="d2228-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="d2228-130">虽然 [NuGet 2.8 发行说明](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)中提到了这一点，但我们并未提到更新引入的特定新功能。</span><span class="sxs-lookup"><span data-stu-id="d2228-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="d2228-131">全部更新</span><span class="sxs-lookup"><span data-stu-id="d2228-131">Update All</span></span>

<span data-ttu-id="d2228-132">现在，你可以在一个步骤中更新网站的所有包！</span><span class="sxs-lookup"><span data-stu-id="d2228-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="d2228-133">当你在 WebMatrix 中打开 NuGet 扩展时，会看到库中所有包的列表、已安装的包以及具有可用更新的包的列表。</span><span class="sxs-lookup"><span data-stu-id="d2228-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="d2228-134">以前，每个包都必须单独更新，但现在 "更新" 选项卡上显示了一个有用的 "全部更新" 按钮。</span><span class="sxs-lookup"><span data-stu-id="d2228-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![单击 "全部更新" 以使用可用更新更新所有包](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="d2228-136">覆盖现有文件</span><span class="sxs-lookup"><span data-stu-id="d2228-136">Overwrite Existing Files</span></span>

<span data-ttu-id="d2228-137">当安装的包包含您的网站中已存在的文件时，NuGet 始终只是以无提示方式忽略这些文件 (仅) 保留现有文件。</span><span class="sxs-lookup"><span data-stu-id="d2228-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="d2228-138">这可能会导致程序包安装或更新正确，但事实上它并不是这样。</span><span class="sxs-lookup"><span data-stu-id="d2228-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="d2228-139">NuGet 现在将提示文件被覆盖。</span><span class="sxs-lookup"><span data-stu-id="d2228-139">NuGet will now prompt for files to be overwritten.</span></span>

![文件冲突解决](./media/NuGet-2.8/webmatrix-overwrite-file.png)
