---
title: NuGet 添加 BindingRedirect PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中添加 BindingRedirect PowerShell 命令参考。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7f1f2ef23e54ee48b577a2796b7f7b5f4c7eb284
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="4b3a4-103">Add-BindingRedirect （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="4b3a4-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4b3a4-104">*仅在内可用[NuGet 程序包管理器控制台](package-manager-console.md)Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="4b3a4-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="4b3a4-105">检查项目输出路径中的所有程序集，并在必要时，将绑定重定向添加到应用程序或 web 配置文件。</span><span class="sxs-lookup"><span data-stu-id="4b3a4-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="4b3a4-106">安装程序包时，将自动运行此命令。</span><span class="sxs-lookup"><span data-stu-id="4b3a4-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="4b3a4-107">绑定重定向和为何使用它们的详细信息，请参阅[重定向程序集版本](/dotnet/framework/configure-apps/redirect-assembly-versions).NET 文档中。</span><span class="sxs-lookup"><span data-stu-id="4b3a4-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="4b3a4-108">语法</span><span class="sxs-lookup"><span data-stu-id="4b3a4-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="4b3a4-109">参数</span><span class="sxs-lookup"><span data-stu-id="4b3a4-109">Parameters</span></span>

| <span data-ttu-id="4b3a4-110">参数</span><span class="sxs-lookup"><span data-stu-id="4b3a4-110">Parameter</span></span> | <span data-ttu-id="4b3a4-111">描述</span><span class="sxs-lookup"><span data-stu-id="4b3a4-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4b3a4-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="4b3a4-112">ProjectName</span></span> | <span data-ttu-id="4b3a4-113">（必需）要向其中添加绑定重定向项目。</span><span class="sxs-lookup"><span data-stu-id="4b3a4-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="4b3a4-114">-ProjectName 交换机本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="4b3a4-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="4b3a4-115">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="4b3a4-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4b3a4-116">通用参数</span><span class="sxs-lookup"><span data-stu-id="4b3a4-116">Common Parameters</span></span>

<span data-ttu-id="4b3a4-117">`Add-BindingRedirect` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="4b3a4-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4b3a4-118">示例</span><span class="sxs-lookup"><span data-stu-id="4b3a4-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```