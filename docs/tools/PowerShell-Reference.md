---
title: NuGet PowerShell 参考
description: 对 Visual Studio 中的 NuGet 包管理器控制台中可用的 PowerShell 命令的完整引用。
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 977e06d36962366abd69f1c7f21ef33eca4e5029
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426127"
---
# <a name="powershell-reference"></a><span data-ttu-id="c8d9d-103">PowerShell 参考</span><span class="sxs-lookup"><span data-stu-id="c8d9d-103">PowerShell reference</span></span>

<span data-ttu-id="c8d9d-104">包管理器控制台提供了下面列出与 NuGet 交互通过特定命令的 Windows 上的 Visual Studio 中的 PowerShell 接口。</span><span class="sxs-lookup"><span data-stu-id="c8d9d-104">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="c8d9d-105">（在控制台不是在 Visual Studio for mac 中目前可用的）使用控制台的指南，请参阅[安装和管理包使用 PowerShell](../tools/package-manager-console.md)主题。</span><span class="sxs-lookup"><span data-stu-id="c8d9d-105">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see [Install and manage packages using PowerShell](../tools/package-manager-console.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="c8d9d-106">所有 PowerShell 命令仅都与包使用。</span><span class="sxs-lookup"><span data-stu-id="c8d9d-106">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="c8d9d-107">任何 PowerShell 命令不与创建和发布包除外的范围内包也可以是其他包的使用者。</span><span class="sxs-lookup"><span data-stu-id="c8d9d-107">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="c8d9d-108">此处列出的命令特定于 Visual Studio 中的包管理器控制台，并且不同于[包管理的模块命令](/powershell/module/packagemanagement/?view=powershell-6)常规的 PowerShell 环境中提供。</span><span class="sxs-lookup"><span data-stu-id="c8d9d-108">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/?view=powershell-6) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="c8d9d-109">具体而言，每个环境包含在另一个中, 不可用的命令，并具有相同名称的命令在其特定的参数也可能存在差异。</span><span class="sxs-lookup"><span data-stu-id="c8d9d-109">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="c8d9d-110">当在 Visual Studio 中使用包管理控制台，命令和本主题中所述的自变量应用。</span><span class="sxs-lookup"><span data-stu-id="c8d9d-110">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="c8d9d-111">常用命令</span><span class="sxs-lookup"><span data-stu-id="c8d9d-111">Common Commands</span></span> | <span data-ttu-id="c8d9d-112">描述</span><span class="sxs-lookup"><span data-stu-id="c8d9d-112">Description</span></span> | <span data-ttu-id="c8d9d-113">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="c8d9d-113">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="c8d9d-114">Install-Package</span><span class="sxs-lookup"><span data-stu-id="c8d9d-114">Install-Package</span></span>](ps-ref-install-package.md) | <span data-ttu-id="c8d9d-115">将包及其依赖项安装到项目。</span><span class="sxs-lookup"><span data-stu-id="c8d9d-115">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="c8d9d-116">全部</span><span class="sxs-lookup"><span data-stu-id="c8d9d-116">All</span></span> |
| [<span data-ttu-id="c8d9d-117">Update-Package</span><span class="sxs-lookup"><span data-stu-id="c8d9d-117">Update-Package</span></span>](ps-ref-update-package.md) | <span data-ttu-id="c8d9d-118">更新包和及其依赖项或在项目中的所有包。</span><span class="sxs-lookup"><span data-stu-id="c8d9d-118">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="c8d9d-119">全部</span><span class="sxs-lookup"><span data-stu-id="c8d9d-119">All</span></span> |
| [<span data-ttu-id="c8d9d-120">Find-Package</span><span class="sxs-lookup"><span data-stu-id="c8d9d-120">Find-Package</span></span>](ps-ref-find-package.md) | <span data-ttu-id="c8d9d-121">搜索使用的包 ID 或关键字的包源。</span><span class="sxs-lookup"><span data-stu-id="c8d9d-121">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="c8d9d-122">3.0+</span><span class="sxs-lookup"><span data-stu-id="c8d9d-122">3.0+</span></span> |
| [<span data-ttu-id="c8d9d-123">Get-Package</span><span class="sxs-lookup"><span data-stu-id="c8d9d-123">Get-Package</span></span>](ps-ref-get-package.md) | <span data-ttu-id="c8d9d-124">检索安装在本地存储库中的包的列表，或列出的包源中可用的包。</span><span class="sxs-lookup"><span data-stu-id="c8d9d-124">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="c8d9d-125">全部</span><span class="sxs-lookup"><span data-stu-id="c8d9d-125">All</span></span> |

| <span data-ttu-id="c8d9d-126">辅助命令</span><span class="sxs-lookup"><span data-stu-id="c8d9d-126">Secondary Commands</span></span> | <span data-ttu-id="c8d9d-127">描述</span><span class="sxs-lookup"><span data-stu-id="c8d9d-127">Description</span></span> | <span data-ttu-id="c8d9d-128">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="c8d9d-128">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="c8d9d-129">Add-BindingRedirect</span><span class="sxs-lookup"><span data-stu-id="c8d9d-129">Add-BindingRedirect</span></span>](ps-ref-add-bindingredirect.md) | <span data-ttu-id="c8d9d-130">检查项目的输出路径中的所有程序集并将添加到绑定重定向`app.config`或`web.config`在必要时。</span><span class="sxs-lookup"><span data-stu-id="c8d9d-130">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="c8d9d-131">全部</span><span class="sxs-lookup"><span data-stu-id="c8d9d-131">All</span></span> |
| [<span data-ttu-id="c8d9d-132">Get-Project</span><span class="sxs-lookup"><span data-stu-id="c8d9d-132">Get-Project</span></span>](ps-ref-get-project.md) | <span data-ttu-id="c8d9d-133">显示默认值或指定的项目有关的信息。</span><span class="sxs-lookup"><span data-stu-id="c8d9d-133">Displays information about the default or specified project.</span></span> | <span data-ttu-id="c8d9d-134">3.0+</span><span class="sxs-lookup"><span data-stu-id="c8d9d-134">3.0+</span></span> |
| [<span data-ttu-id="c8d9d-135">Open-PackagePage</span><span class="sxs-lookup"><span data-stu-id="c8d9d-135">Open-PackagePage</span></span>](ps-ref-open-packagepage.md) | <span data-ttu-id="c8d9d-136">将启动默认浏览器与项目、 许可证或指定包的报告滥用 URL。</span><span class="sxs-lookup"><span data-stu-id="c8d9d-136">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="c8d9d-137">3\.0 + 中不推荐使用</span><span class="sxs-lookup"><span data-stu-id="c8d9d-137">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="c8d9d-138">Register-TabExpansion</span><span class="sxs-lookup"><span data-stu-id="c8d9d-138">Register-TabExpansion</span></span>](ps-ref-register-tabexpansion.md) | <span data-ttu-id="c8d9d-139">注册命令，它允许您创建自定义的扩展的常用参数值的参数的选项卡扩展。</span><span class="sxs-lookup"><span data-stu-id="c8d9d-139">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="c8d9d-140">全部</span><span class="sxs-lookup"><span data-stu-id="c8d9d-140">All</span></span> |
| [<span data-ttu-id="c8d9d-141">Sync-Package</span><span class="sxs-lookup"><span data-stu-id="c8d9d-141">Sync-Package</span></span>](ps-ref-sync-package.md) | <span data-ttu-id="c8d9d-142">获取安装的版本的包从指定项目并同步到解决方案中项目的其余部分的版本。</span><span class="sxs-lookup"><span data-stu-id="c8d9d-142">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="c8d9d-143">3.0+</span><span class="sxs-lookup"><span data-stu-id="c8d9d-143">3.0+</span></span> |
| [<span data-ttu-id="c8d9d-144">Uninstall-Package</span><span class="sxs-lookup"><span data-stu-id="c8d9d-144">Uninstall-Package</span></span>](ps-ref-uninstall-package.md) | <span data-ttu-id="c8d9d-145">从项目中，有选择性地删除其依赖项中删除包。</span><span class="sxs-lookup"><span data-stu-id="c8d9d-145">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="c8d9d-146">全部</span><span class="sxs-lookup"><span data-stu-id="c8d9d-146">All</span></span> |

<span data-ttu-id="c8d9d-147">有关完整的详细帮助其中任何命令，在控制台中，只需运行以下命令使用相关的命令名：</span><span class="sxs-lookup"><span data-stu-id="c8d9d-147">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="c8d9d-148">包管理器控制台的所有命令都支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):</span><span class="sxs-lookup"><span data-stu-id="c8d9d-148">All Package Manager Console commands support the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216):</span></span>

- <span data-ttu-id="c8d9d-149">调试</span><span class="sxs-lookup"><span data-stu-id="c8d9d-149">Debug</span></span>
- <span data-ttu-id="c8d9d-150">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="c8d9d-150">ErrorAction</span></span>
- <span data-ttu-id="c8d9d-151">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="c8d9d-151">ErrorVariable</span></span>
- <span data-ttu-id="c8d9d-152">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="c8d9d-152">OutBuffer</span></span>
- <span data-ttu-id="c8d9d-153">OutVariable</span><span class="sxs-lookup"><span data-stu-id="c8d9d-153">OutVariable</span></span>
- <span data-ttu-id="c8d9d-154">PipelineVariable</span><span class="sxs-lookup"><span data-stu-id="c8d9d-154">PipelineVariable</span></span>
- <span data-ttu-id="c8d9d-155">详细</span><span class="sxs-lookup"><span data-stu-id="c8d9d-155">Verbose</span></span>
- <span data-ttu-id="c8d9d-156">WarningAction</span><span class="sxs-lookup"><span data-stu-id="c8d9d-156">WarningAction</span></span>
- <span data-ttu-id="c8d9d-157">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="c8d9d-157">WarningVariable</span></span>

<span data-ttu-id="c8d9d-158">有关详细信息，请参阅[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) PowerShell 文档中。</span><span class="sxs-lookup"><span data-stu-id="c8d9d-158">For details, refer to [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in the PowerShell documentation.</span></span>
