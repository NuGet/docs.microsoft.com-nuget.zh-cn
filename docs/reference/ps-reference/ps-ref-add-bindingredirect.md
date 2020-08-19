---
title: NuGet BindingRedirect PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中的 BindingRedirect PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f5ba4bd8140fa8cac7da8bf1351ad5448671b768
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623118"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="5dc91-103">在 Visual Studio 中添加-BindingRedirect (程序包管理器控制台) </span><span class="sxs-lookup"><span data-stu-id="5dc91-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="5dc91-104">*仅在 Windows 上的 Visual Studio 中的 [包管理器控制台](../../consume-packages/install-use-packages-powershell.md) 内可用。*</span><span class="sxs-lookup"><span data-stu-id="5dc91-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="5dc91-105">检查项目的输出路径中的所有程序集，并在必要时向应用程序或 web 配置文件添加绑定重定向。</span><span class="sxs-lookup"><span data-stu-id="5dc91-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="5dc91-106">安装包时，会自动运行此命令。</span><span class="sxs-lookup"><span data-stu-id="5dc91-106">This command is run automatically when installing a package.</span></span>

> [!NOTE]
> <span data-ttu-id="5dc91-107">这仅适用于使用 packages.config 文件的方案。</span><span class="sxs-lookup"><span data-stu-id="5dc91-107">This only applies to scenarios using a packages.config file.</span></span> <span data-ttu-id="5dc91-108">有关详细信息，请参阅 [NuGet packages.config 文件引用](~/reference/packages-config.md)。</span><span class="sxs-lookup"><span data-stu-id="5dc91-108">For more information, see [NuGet packages.config file reference](~/reference/packages-config.md).</span></span>

<span data-ttu-id="5dc91-109">有关绑定重定向及其使用原因的详细信息，请参阅 .NET 文档中的 [重定向程序集版本](/dotnet/framework/configure-apps/redirect-assembly-versions) 。</span><span class="sxs-lookup"><span data-stu-id="5dc91-109">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="5dc91-110">语法</span><span class="sxs-lookup"><span data-stu-id="5dc91-110">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="5dc91-111">参数</span><span class="sxs-lookup"><span data-stu-id="5dc91-111">Parameters</span></span>

| <span data-ttu-id="5dc91-112">参数</span><span class="sxs-lookup"><span data-stu-id="5dc91-112">Parameter</span></span> | <span data-ttu-id="5dc91-113">说明</span><span class="sxs-lookup"><span data-stu-id="5dc91-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5dc91-114">项目名称</span><span class="sxs-lookup"><span data-stu-id="5dc91-114">ProjectName</span></span> | <span data-ttu-id="5dc91-115">需要 () 项目添加绑定重定向。</span><span class="sxs-lookup"><span data-stu-id="5dc91-115">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="5dc91-116">-项目开关本身是可选的。</span><span class="sxs-lookup"><span data-stu-id="5dc91-116">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="5dc91-117">这些参数都不接受管道输入或通配符。</span><span class="sxs-lookup"><span data-stu-id="5dc91-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="5dc91-118">通用参数</span><span class="sxs-lookup"><span data-stu-id="5dc91-118">Common Parameters</span></span>

<span data-ttu-id="5dc91-119">`Add-BindingRedirect` 支持以下 [常见的 PowerShell 参数](https://go.microsoft.com/fwlink/?LinkID=113216)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。</span><span class="sxs-lookup"><span data-stu-id="5dc91-119">`Add-BindingRedirect` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="5dc91-120">示例</span><span class="sxs-lookup"><span data-stu-id="5dc91-120">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```
