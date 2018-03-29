---
title: NuGet 添加 BindingRedirect PowerShell 参考 |Microsoft 文档
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Visual Studio 中的 NuGet 包管理器控制台中添加 BindingRedirect PowerShell 命令参考。
keywords: NuGet 包管理器控制台，NuGet Powershell 命令，NuGet Powershell 参考，添加 BindingRedirect
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 2a337bd61295f436b49c56c1680d07ccc6a8c403
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="e11af-104">添加-BindingRedirect （Visual Studio 中的包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="e11af-104">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e11af-105">*仅在内可用[NuGet 程序包管理器控制台](package-manager-console.md)Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="e11af-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e11af-106">检查项目输出路径中的所有程序集，并在必要时，将绑定重定向添加到应用程序或 web 配置文件。</span><span class="sxs-lookup"><span data-stu-id="e11af-106">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="e11af-107">安装程序包时，将自动运行此命令。</span><span class="sxs-lookup"><span data-stu-id="e11af-107">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="e11af-108">绑定重定向和为何使用它们的详细信息，请参阅[重定向程序集版本](/dotnet/framework/configure-apps/redirect-assembly-versions).NET 文档中。</span><span class="sxs-lookup"><span data-stu-id="e11af-108">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="e11af-109">语法</span><span class="sxs-lookup"><span data-stu-id="e11af-109">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="e11af-110">参数</span><span class="sxs-lookup"><span data-stu-id="e11af-110">Parameters</span></span>

| <span data-ttu-id="e11af-111">参数</span><span class="sxs-lookup"><span data-stu-id="e11af-111">Parameter</span></span> | <span data-ttu-id="e11af-112">描述</span><span class="sxs-lookup"><span data-stu-id="e11af-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e11af-113">ProjectName</span><span class="sxs-lookup"><span data-stu-id="e11af-113">ProjectName</span></span> | <span data-ttu-id="e11af-114">（必需）要向其中添加绑定重定向项目。</span><span class="sxs-lookup"><span data-stu-id="e11af-114">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="e11af-115">-ProjectName 交换机本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="e11af-115">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="e11af-116">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="e11af-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e11af-117">通用参数</span><span class="sxs-lookup"><span data-stu-id="e11af-117">Common Parameters</span></span>

<span data-ttu-id="e11af-118">`Add-BindingRedirect` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="e11af-118">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e11af-119">示例</span><span class="sxs-lookup"><span data-stu-id="e11af-119">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```