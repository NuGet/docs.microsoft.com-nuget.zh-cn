---
title: NuGet 添加 BindingRedirect PowerShell 参考
description: 在 Visual Studio 中的 NuGet 包管理器控制台中添加 BindingRedirect PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5f318ddfb2bb8498ab3e608f8036be05dcb0706
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842542"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="e5850-103">Add-BindingRedirect （Visual Studio 中的程序包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="e5850-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e5850-104">*仅在内可用[程序包管理器控制台](package-manager-console.md)在 Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="e5850-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e5850-105">检查项目的输出路径中的所有程序集，并在必要时，将绑定重定向添加到应用程序或 web 配置文件。</span><span class="sxs-lookup"><span data-stu-id="e5850-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="e5850-106">安装包时，将自动运行此命令。</span><span class="sxs-lookup"><span data-stu-id="e5850-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="e5850-107">有关绑定的绑定重定向以及为什么使用它们的详细信息，请参阅[重定向程序集版本](/dotnet/framework/configure-apps/redirect-assembly-versions).NET 文档中。</span><span class="sxs-lookup"><span data-stu-id="e5850-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="e5850-108">语法</span><span class="sxs-lookup"><span data-stu-id="e5850-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="e5850-109">参数</span><span class="sxs-lookup"><span data-stu-id="e5850-109">Parameters</span></span>

| <span data-ttu-id="e5850-110">参数</span><span class="sxs-lookup"><span data-stu-id="e5850-110">Parameter</span></span> | <span data-ttu-id="e5850-111">描述</span><span class="sxs-lookup"><span data-stu-id="e5850-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e5850-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="e5850-112">ProjectName</span></span> | <span data-ttu-id="e5850-113">（必需）要将绑定重定向添加到项目。</span><span class="sxs-lookup"><span data-stu-id="e5850-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="e5850-114">-ProjectName 开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="e5850-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="e5850-115">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="e5850-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e5850-116">通用参数</span><span class="sxs-lookup"><span data-stu-id="e5850-116">Common Parameters</span></span>

<span data-ttu-id="e5850-117">`Add-BindingRedirect` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable，详细、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="e5850-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e5850-118">示例</span><span class="sxs-lookup"><span data-stu-id="e5850-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```