---
title: NuGet BindingRedirect PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中的 BindingRedirect PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d3d156cf882229260e8cf55f8ece2804aec36dc9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384979"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="bec2f-103">Add-BindingRedirect （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="bec2f-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="bec2f-104">*仅在 Windows 上的 Visual Studio 中的[包管理器控制台](../../consume-packages/install-use-packages-powershell.md)内可用。*</span><span class="sxs-lookup"><span data-stu-id="bec2f-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="bec2f-105">检查项目的输出路径中的所有程序集，并在必要时向应用程序或 web 配置文件添加绑定重定向。</span><span class="sxs-lookup"><span data-stu-id="bec2f-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="bec2f-106">安装包时，会自动运行此命令。</span><span class="sxs-lookup"><span data-stu-id="bec2f-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="bec2f-107">有关绑定重定向及其使用原因的详细信息，请参阅 .NET 文档中的[重定向程序集版本](/dotnet/framework/configure-apps/redirect-assembly-versions)。</span><span class="sxs-lookup"><span data-stu-id="bec2f-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="bec2f-108">语法</span><span class="sxs-lookup"><span data-stu-id="bec2f-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="bec2f-109">参数</span><span class="sxs-lookup"><span data-stu-id="bec2f-109">Parameters</span></span>

| <span data-ttu-id="bec2f-110">参数</span><span class="sxs-lookup"><span data-stu-id="bec2f-110">Parameter</span></span> | <span data-ttu-id="bec2f-111">描述</span><span class="sxs-lookup"><span data-stu-id="bec2f-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bec2f-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="bec2f-112">ProjectName</span></span> | <span data-ttu-id="bec2f-113">请求要向其添加绑定重定向的项目。</span><span class="sxs-lookup"><span data-stu-id="bec2f-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="bec2f-114">-项目开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="bec2f-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="bec2f-115">这些参数都不接受管道输入或通配符。</span><span class="sxs-lookup"><span data-stu-id="bec2f-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="bec2f-116">通用参数</span><span class="sxs-lookup"><span data-stu-id="bec2f-116">Common Parameters</span></span>

<span data-ttu-id="bec2f-117">`Add-BindingRedirect` 支持以下[常见的 PowerShell 参数](https://go.microsoft.com/fwlink/?LinkID=113216)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="bec2f-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="bec2f-118">示例</span><span class="sxs-lookup"><span data-stu-id="bec2f-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```