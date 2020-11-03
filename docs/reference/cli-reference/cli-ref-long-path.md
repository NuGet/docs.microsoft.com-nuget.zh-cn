---
title: NuGet CLI 长路径支持
description: nuget.exe 长路径支持的参考
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 1143da911c80125a9d60e4b98798b11871e9988a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238187"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="81776-103"> (NuGet CLI) 的长路径支持</span><span class="sxs-lookup"><span data-stu-id="81776-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="81776-104">**适用于：** 所有 &bullet; **支持的版本：** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="81776-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="81776-105">NuGet.exe 4.8 和更高版本支持文件和目录的长路径，适用于打包、还原、安装和需要文件路径的大多数其他方案。</span><span class="sxs-lookup"><span data-stu-id="81776-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="81776-106">所需操作系统</span><span class="sxs-lookup"><span data-stu-id="81776-106">Required Operating System</span></span>

-   <span data-ttu-id="81776-107">Windows 10 (版本1607或更高版本) </span><span class="sxs-lookup"><span data-stu-id="81776-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="81776-108">如果将 .NET Framework 升级到4.6.2 或更高版本，则 Windows 10 (7 2015 月发行版或 1511) 版本。</span><span class="sxs-lookup"><span data-stu-id="81776-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="81776-109">Windows Server 2016 (所有版本) </span><span class="sxs-lookup"><span data-stu-id="81776-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="81776-110">启用 "Win32 长路径" 组策略</span><span class="sxs-lookup"><span data-stu-id="81776-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="81776-111">需要通过设置组策略在这些系统上启用长路径支持。</span><span class="sxs-lookup"><span data-stu-id="81776-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="81776-112">步骤：</span><span class="sxs-lookup"><span data-stu-id="81776-112">Steps:</span></span>
1. <span data-ttu-id="81776-113">在 "开始" 搜索栏中启动 **组策略编辑器** "" 编辑组策略 "，或从" 运行 "命令 (Windows-R) 运行" gpedit.msc "。</span><span class="sxs-lookup"><span data-stu-id="81776-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="81776-114">在 **本地组策略编辑器** 中，启用 "本地计算机策略/计算机配置/管理模板/所有设置/启用 Win32 长路径"。</span><span class="sxs-lookup"><span data-stu-id="81776-114">In the **Local Group Policy Editor** , enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![长路径策略](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="81776-116">启用其他 NuGet 工具以支持长路径</span><span class="sxs-lookup"><span data-stu-id="81776-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="81776-117">Dotnet CLI 支持长路径，而不考虑操作系统或版本。</span><span class="sxs-lookup"><span data-stu-id="81776-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="81776-118">Visual Studio 或 `msbuild -t:restore` 尚不支持长路径。</span><span class="sxs-lookup"><span data-stu-id="81776-118">Visual Studio or `msbuild -t:restore` does not yet support long paths.</span></span>
> -   <span data-ttu-id="81776-119">使用 NuGet 库执行还原和其他命令的软件将支持在 NuGet.exe 工作的同一系统上的长路径，如果它们也 `longPathAware` 在 windows 清单中设置并 `UseLegacyPathHandling` 通过配置为 `false` via App.Config [查看详细信息](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)</span><span class="sxs-lookup"><span data-stu-id="81776-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set `longPathAware` in their windows manifest and configure `UseLegacyPathHandling` to `false` via App.Config [See more information](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)</span></span>