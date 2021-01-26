---
title: NuGet PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中提供的 PowerShell 命令的完整引用。
author: JonDouglas
ms.author: jodou
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 98bea8a225f4864953f898ef57b26e9093f7c2e9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779363"
---
# <a name="powershell-reference"></a><span data-ttu-id="47942-103">PowerShell 参考</span><span class="sxs-lookup"><span data-stu-id="47942-103">PowerShell reference</span></span>

<span data-ttu-id="47942-104">程序包管理器控制台在 Windows 上的 Visual Studio 中提供了一个 PowerShell 接口，可通过下面列出的特定命令与 NuGet 交互。</span><span class="sxs-lookup"><span data-stu-id="47942-104">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="47942-105"> (控制台目前在 Visual Studio for Mac 中不可用。 ) 有关使用控制台的指南，请参阅 [使用程序包管理器控制台安装和管理包](../consume-packages/install-use-packages-powershell.md) 主题。</span><span class="sxs-lookup"><span data-stu-id="47942-105">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="47942-106">所有 PowerShell 命令仅与包消耗相关。</span><span class="sxs-lookup"><span data-stu-id="47942-106">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="47942-107">除了包还可以是其他包的使用者以外，没有任何 PowerShell 命令都与创建和发布包相关。</span><span class="sxs-lookup"><span data-stu-id="47942-107">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="47942-108">此处列出的命令特定于 Visual Studio 中的包管理器控制台，它不同于常规 PowerShell 环境中提供的[包管理模块命令](/powershell/module/packagemanagement/?view=powershell-6)。</span><span class="sxs-lookup"><span data-stu-id="47942-108">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/?view=powershell-6) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="47942-109">具体而言，每个环境都有一些命令，这些命令在其他环境中不可用，而具有相同名称的命令在其特定参数中也可能不同。</span><span class="sxs-lookup"><span data-stu-id="47942-109">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="47942-110">使用 Visual Studio 中的包管理控制台时，本主题中所述的命令和参数适用。</span><span class="sxs-lookup"><span data-stu-id="47942-110">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="47942-111">常见命令</span><span class="sxs-lookup"><span data-stu-id="47942-111">Common Commands</span></span> | <span data-ttu-id="47942-112">说明</span><span class="sxs-lookup"><span data-stu-id="47942-112">Description</span></span> | <span data-ttu-id="47942-113">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="47942-113">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="47942-114">Install-Package</span><span class="sxs-lookup"><span data-stu-id="47942-114">Install-Package</span></span>](ps-reference/ps-ref-install-package.md) | <span data-ttu-id="47942-115">将程序包及其依赖项安装到项目中。</span><span class="sxs-lookup"><span data-stu-id="47942-115">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="47942-116">全部</span><span class="sxs-lookup"><span data-stu-id="47942-116">All</span></span> |
| [<span data-ttu-id="47942-117">Update-Package</span><span class="sxs-lookup"><span data-stu-id="47942-117">Update-Package</span></span>](ps-reference/ps-ref-update-package.md) | <span data-ttu-id="47942-118">更新包及其依赖项或项目中的所有包。</span><span class="sxs-lookup"><span data-stu-id="47942-118">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="47942-119">全部</span><span class="sxs-lookup"><span data-stu-id="47942-119">All</span></span> |
| [<span data-ttu-id="47942-120">Find-Package</span><span class="sxs-lookup"><span data-stu-id="47942-120">Find-Package</span></span>](ps-reference/ps-ref-find-package.md) | <span data-ttu-id="47942-121">使用包 ID 或关键字搜索包源。</span><span class="sxs-lookup"><span data-stu-id="47942-121">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="47942-122">3.0+</span><span class="sxs-lookup"><span data-stu-id="47942-122">3.0+</span></span> |
| [<span data-ttu-id="47942-123">Get-Package</span><span class="sxs-lookup"><span data-stu-id="47942-123">Get-Package</span></span>](ps-reference/ps-ref-get-package.md) | <span data-ttu-id="47942-124">检索本地存储库中安装的包的列表，或列出包源中可用的包。</span><span class="sxs-lookup"><span data-stu-id="47942-124">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="47942-125">全部</span><span class="sxs-lookup"><span data-stu-id="47942-125">All</span></span> |

| <span data-ttu-id="47942-126">辅助命令</span><span class="sxs-lookup"><span data-stu-id="47942-126">Secondary Commands</span></span> | <span data-ttu-id="47942-127">说明</span><span class="sxs-lookup"><span data-stu-id="47942-127">Description</span></span> | <span data-ttu-id="47942-128">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="47942-128">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="47942-129">Add-BindingRedirect</span><span class="sxs-lookup"><span data-stu-id="47942-129">Add-BindingRedirect</span></span>](ps-reference/ps-ref-add-bindingredirect.md) | <span data-ttu-id="47942-130">检查项目的输出路径中的所有程序集，并将绑定重定向添加到 `app.config` 或 `web.config` （如果需要）。</span><span class="sxs-lookup"><span data-stu-id="47942-130">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="47942-131">全部</span><span class="sxs-lookup"><span data-stu-id="47942-131">All</span></span> |
| [<span data-ttu-id="47942-132">Get-Project</span><span class="sxs-lookup"><span data-stu-id="47942-132">Get-Project</span></span>](ps-reference/ps-ref-get-project.md) | <span data-ttu-id="47942-133">显示有关默认项目或指定项目的信息。</span><span class="sxs-lookup"><span data-stu-id="47942-133">Displays information about the default or specified project.</span></span> | <span data-ttu-id="47942-134">3.0+</span><span class="sxs-lookup"><span data-stu-id="47942-134">3.0+</span></span> |
| [<span data-ttu-id="47942-135">Open-PackagePage</span><span class="sxs-lookup"><span data-stu-id="47942-135">Open-PackagePage</span></span>](ps-reference/ps-ref-open-packagepage.md) | <span data-ttu-id="47942-136">用指定包的项目、许可证或报表滥用 URL 启动默认浏览器。</span><span class="sxs-lookup"><span data-stu-id="47942-136">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="47942-137">3.0 + 中弃用</span><span class="sxs-lookup"><span data-stu-id="47942-137">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="47942-138">注册-Tabexpansion 控制</span><span class="sxs-lookup"><span data-stu-id="47942-138">Register-TabExpansion</span></span>](ps-reference/ps-ref-register-tabexpansion.md) | <span data-ttu-id="47942-139">为命令的参数注册选项卡展开，使你可以为常用参数值创建自定义扩展。</span><span class="sxs-lookup"><span data-stu-id="47942-139">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="47942-140">全部</span><span class="sxs-lookup"><span data-stu-id="47942-140">All</span></span> |
| [<span data-ttu-id="47942-141">Sync-Package</span><span class="sxs-lookup"><span data-stu-id="47942-141">Sync-Package</span></span>](ps-reference/ps-ref-sync-package.md) | <span data-ttu-id="47942-142">获取指定项目中已安装包的版本，并将该版本同步到解决方案中项目的其余部分。</span><span class="sxs-lookup"><span data-stu-id="47942-142">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="47942-143">3.0+</span><span class="sxs-lookup"><span data-stu-id="47942-143">3.0+</span></span> |
| [<span data-ttu-id="47942-144">Uninstall-Package</span><span class="sxs-lookup"><span data-stu-id="47942-144">Uninstall-Package</span></span>](ps-reference/ps-ref-uninstall-package.md) | <span data-ttu-id="47942-145">从项目中删除包，并可以选择删除其依赖项。</span><span class="sxs-lookup"><span data-stu-id="47942-145">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="47942-146">全部</span><span class="sxs-lookup"><span data-stu-id="47942-146">All</span></span> |

<span data-ttu-id="47942-147">若要获取有关控制台中任何这些命令的完整详细信息，只需运行以下命令名称：</span><span class="sxs-lookup"><span data-stu-id="47942-147">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="47942-148">所有程序包管理器控制台命令都支持以下 [常见的 PowerShell 参数](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：</span><span class="sxs-lookup"><span data-stu-id="47942-148">All Package Manager Console commands support the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters):</span></span>

- <span data-ttu-id="47942-149">调试</span><span class="sxs-lookup"><span data-stu-id="47942-149">Debug</span></span>
- <span data-ttu-id="47942-150">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="47942-150">ErrorAction</span></span>
- <span data-ttu-id="47942-151">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="47942-151">ErrorVariable</span></span>
- <span data-ttu-id="47942-152">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="47942-152">OutBuffer</span></span>
- <span data-ttu-id="47942-153">OutVariable</span><span class="sxs-lookup"><span data-stu-id="47942-153">OutVariable</span></span>
- <span data-ttu-id="47942-154">PipelineVariable</span><span class="sxs-lookup"><span data-stu-id="47942-154">PipelineVariable</span></span>
- <span data-ttu-id="47942-155">详细</span><span class="sxs-lookup"><span data-stu-id="47942-155">Verbose</span></span>
- <span data-ttu-id="47942-156">WarningAction</span><span class="sxs-lookup"><span data-stu-id="47942-156">WarningAction</span></span>
- <span data-ttu-id="47942-157">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="47942-157">WarningVariable</span></span>

<span data-ttu-id="47942-158">有关详细信息，请参阅 PowerShell 文档中的 [about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters) 。</span><span class="sxs-lookup"><span data-stu-id="47942-158">For details, refer to [about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters) in the PowerShell documentation.</span></span>