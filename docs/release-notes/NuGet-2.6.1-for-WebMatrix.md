---
title: NuGet 2.6.1 for WebMatrix 发行说明
description: 发行说明适用于 NuGet 2.6.1 的 WebMatrix 包括已知的问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550312"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="bfbeb-103">NuGet 2.6.1 for WebMatrix 发行说明</span><span class="sxs-lookup"><span data-stu-id="bfbeb-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="bfbeb-104">[NuGet 2.6 发行说明](../release-notes/nuget-2.6.md) | [NuGet 2.7 发行说明](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="bfbeb-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="bfbeb-105">NuGet 团队于 2014 年 3 月 26 日发布的 WebMatrix 的更新的 NuGet 包管理器扩展。</span><span class="sxs-lookup"><span data-stu-id="bfbeb-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="bfbeb-106">可以从安装此更新[WebMatrix 扩展库](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery)使用以下步骤：</span><span class="sxs-lookup"><span data-stu-id="bfbeb-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="bfbeb-107">打开 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="bfbeb-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="bfbeb-108">单击主页功能区中的扩展图标</span><span class="sxs-lookup"><span data-stu-id="bfbeb-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="bfbeb-109">选择更新选项卡</span><span class="sxs-lookup"><span data-stu-id="bfbeb-109">Select the Updates tab</span></span>
1. <span data-ttu-id="bfbeb-110">单击此项可更新到 2.6.1 的 NuGet 包管理器</span><span class="sxs-lookup"><span data-stu-id="bfbeb-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="bfbeb-111">关闭并重新启动 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="bfbeb-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="bfbeb-112">值得注意的更改</span><span class="sxs-lookup"><span data-stu-id="bfbeb-112">Notable Changes</span></span>

<span data-ttu-id="bfbeb-113">最大的问题用户此扩展更新解决两个已经遇到过 WebMatrix 中的使用 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="bfbeb-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="bfbeb-114">第一种是 NuGet 架构版本错误和第二个是指向零字节 Dll 错误`bin`文件夹。</span><span class="sxs-lookup"><span data-stu-id="bfbeb-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="bfbeb-115">NuGet 架构版本错误</span><span class="sxs-lookup"><span data-stu-id="bfbeb-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="bfbeb-116">WebMatrix 3 已自发布以来，到适用于 NuGet 包需要新的架构版本的 NuGet 已引入新功能。</span><span class="sxs-lookup"><span data-stu-id="bfbeb-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="bfbeb-117">在尝试管理 NuGet 程序包在您的网站，这些新的包可能会导致你在 WebMatrix 中看到的错误。</span><span class="sxs-lookup"><span data-stu-id="bfbeb-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![出现了错误。](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="bfbeb-121">此最新版本提供了与最新的 NuGet 包，防止发生此错误的兼容性。</span><span class="sxs-lookup"><span data-stu-id="bfbeb-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="bfbeb-122">现在可以在 WebMatrix 中安装新版本的包包括 Microsoft.AspNet.WebPages。</span><span class="sxs-lookup"><span data-stu-id="bfbeb-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="bfbeb-123">这些包的一些已使用的 NuGet 功能，如[XDT 配置转换](../release-notes/nuget-2.6.md#xdt)，这不受支持的在 WebMatrix 中到目前为止。</span><span class="sxs-lookup"><span data-stu-id="bfbeb-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="bfbeb-124">Bin 文件夹中的零字节 Dll</span><span class="sxs-lookup"><span data-stu-id="bfbeb-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="bfbeb-125">某些用户报告的后安装 NuGet 中的包中包含 Dll 复制到 bin 的 WebMatrix Dll 显示`bin`0 字节的文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="bfbeb-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="bfbeb-126">这将在运行时中断该应用程序。</span><span class="sxs-lookup"><span data-stu-id="bfbeb-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="bfbeb-127">[此问题](https://nuget.codeplex.com/workitem/4060)现已修复。</span><span class="sxs-lookup"><span data-stu-id="bfbeb-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="bfbeb-128">其他最新的改进</span><span class="sxs-lookup"><span data-stu-id="bfbeb-128">Other Recent Improvements</span></span>

<span data-ttu-id="bfbeb-129">NuGet 包管理器 2.8 for Visual Studio 发布时，我们还为 WebMatrix 发布 NuGet 包管理器 2.5.0。</span><span class="sxs-lookup"><span data-stu-id="bfbeb-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="bfbeb-130">虽然这中所述[NuGet 2.8 发行说明](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)，我们没有提到特定的新功能引入了该更新。</span><span class="sxs-lookup"><span data-stu-id="bfbeb-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="bfbeb-131">全部更新</span><span class="sxs-lookup"><span data-stu-id="bfbeb-131">Update All</span></span>

<span data-ttu-id="bfbeb-132">现在，您可以更新所有在一个步骤中的 web 站点的包 ！</span><span class="sxs-lookup"><span data-stu-id="bfbeb-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="bfbeb-133">在 WebMatrix 中打开 NuGet 扩展时，所有程序包的列表上看到库、 安装，和具有可用的更新。</span><span class="sxs-lookup"><span data-stu-id="bfbeb-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="bfbeb-134">以前，必须单独更新每个包，但现在没有显示在更新选项卡的有用"全部更新"按钮。</span><span class="sxs-lookup"><span data-stu-id="bfbeb-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![单击全部更新，以使用可用的更新来更新所有包](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="bfbeb-136">覆盖现有文件</span><span class="sxs-lookup"><span data-stu-id="bfbeb-136">Overwrite Existing Files</span></span>

<span data-ttu-id="bfbeb-137">安装时包含您的网站中已存在的文件的包，NuGet 已始终只以无提示方式忽略这些文件 （保留不动现有文件）。</span><span class="sxs-lookup"><span data-stu-id="bfbeb-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="bfbeb-138">这可能导致包已安装，或当事实上没有正确更新的印象。</span><span class="sxs-lookup"><span data-stu-id="bfbeb-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="bfbeb-139">NuGet 现在将提示输入覆盖文件。</span><span class="sxs-lookup"><span data-stu-id="bfbeb-139">NuGet will now prompt for files to be overwritten.</span></span>

![文件冲突解决方法](./media/NuGet-2.8/webmatrix-overwrite-file.png)
