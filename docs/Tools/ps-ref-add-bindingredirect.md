---
title: "NuGet 添加 BindingRedirect PowerShell 参考 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 90f4dcb0-6e5a-4948-8ea9-62e0d061d95a
description: "Visual Studio 中的 NuGet 包管理器控制台中添加 BindingRedirect PowerShell 命令参考。"
keywords: "NuGet 包管理器控制台，NuGet Powershell 命令，NuGet Powershell 参考，添加 BindingRedirect"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6a3232af925f75713168421e68f2773060c5ebaa
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="f3b89-104">添加-BindingRedirect （Visual Studio 中的包管理器控制台）</span><span class="sxs-lookup"><span data-stu-id="f3b89-104">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f3b89-105">*仅在内可用[NuGet 程序包管理器控制台](Package-Manager-Console.md)Windows 上的 Visual Studio 中。*</span><span class="sxs-lookup"><span data-stu-id="f3b89-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f3b89-106">检查项目输出路径中的所有程序集，并在必要时，将绑定重定向添加到应用程序或 web 配置文件。</span><span class="sxs-lookup"><span data-stu-id="f3b89-106">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="f3b89-107">安装程序包时，将自动运行此命令。</span><span class="sxs-lookup"><span data-stu-id="f3b89-107">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="f3b89-108">绑定重定向和为何使用它们的详细信息，请参阅[重定向程序集版本](/dotnet/framework/configure-apps/redirect-assembly-versions).NET 文档中。</span><span class="sxs-lookup"><span data-stu-id="f3b89-108">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="f3b89-109">语法</span><span class="sxs-lookup"><span data-stu-id="f3b89-109">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f3b89-110">参数</span><span class="sxs-lookup"><span data-stu-id="f3b89-110">Parameters</span></span>

| <span data-ttu-id="f3b89-111">参数</span><span class="sxs-lookup"><span data-stu-id="f3b89-111">Parameter</span></span> | <span data-ttu-id="f3b89-112">描述</span><span class="sxs-lookup"><span data-stu-id="f3b89-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f3b89-113">ProjectName</span><span class="sxs-lookup"><span data-stu-id="f3b89-113">ProjectName</span></span> | <span data-ttu-id="f3b89-114">（必需）要向其中添加绑定重定向项目。</span><span class="sxs-lookup"><span data-stu-id="f3b89-114">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="f3b89-115">-ProjectName 交换机本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="f3b89-115">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="f3b89-116">任何这些参数接受管道输入或通配符字符。</span><span class="sxs-lookup"><span data-stu-id="f3b89-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f3b89-117">通用参数</span><span class="sxs-lookup"><span data-stu-id="f3b89-117">Common Parameters</span></span>

<span data-ttu-id="f3b89-118">`Add-BindingRedirect`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="f3b89-118">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f3b89-119">示例</span><span class="sxs-lookup"><span data-stu-id="f3b89-119">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```