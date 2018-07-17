---
title: NuGet CLI 长路径支持
description: Nuget.exe 长路径支持的引用
author: zhili1208
ms.author: lzhi
manager: rob
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 0119be3fd8fd6c2e06e0135de5e498e0730bb0cc
ms.sourcegitcommit: a76ecc58f41c2c5b3536ff4a3f3fcbdf5258177c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39072716"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="c7eb7-103">长路径支持 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c7eb7-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="c7eb7-104">**适用于：** 所有&bullet;**支持的版本：** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="c7eb7-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="c7eb7-105">NuGet.exe 4.8 及更高版本支持长路径的文件和目录的方案，如包、 还原、 安装和大多数其他情况下需要文件路径。</span><span class="sxs-lookup"><span data-stu-id="c7eb7-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="c7eb7-106">所需的操作系统</span><span class="sxs-lookup"><span data-stu-id="c7eb7-106">Required Operating System</span></span>

-   <span data-ttu-id="c7eb7-107">Windows 10 （版本 1607 或更高版本）</span><span class="sxs-lookup"><span data-stu-id="c7eb7-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="c7eb7-108">Windows 10 （2015 年 7 月版本或版本 1511年） 如果您升级到版本 4.6.2 的.NET Framework 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="c7eb7-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="c7eb7-109">Windows Server 2016 （所有版本）</span><span class="sxs-lookup"><span data-stu-id="c7eb7-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="c7eb7-110">启用"Win32 长路径"组策略</span><span class="sxs-lookup"><span data-stu-id="c7eb7-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="c7eb7-111">需要通过设置组策略启用长路径支持这两个系统上。</span><span class="sxs-lookup"><span data-stu-id="c7eb7-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="c7eb7-112">步骤：</span><span class="sxs-lookup"><span data-stu-id="c7eb7-112">Steps:</span></span>
1. <span data-ttu-id="c7eb7-113">启动**组策略编辑器**-键入开始搜索栏中的"编辑组策略"或运行命令 (Windows-R) 运行"gpedit.msc"。</span><span class="sxs-lookup"><span data-stu-id="c7eb7-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="c7eb7-114">在中**本地组策略编辑器**，启用"本地计算机策略/计算机配置/管理模板/所有设置/启用 Win32 长路径"。</span><span class="sxs-lookup"><span data-stu-id="c7eb7-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![长路径策略](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="c7eb7-116">启用其他 NuGet 工具以支持长路径</span><span class="sxs-lookup"><span data-stu-id="c7eb7-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="c7eb7-117">Dotnet CLI 支持长路径而不用考虑操作系统或版本。</span><span class="sxs-lookup"><span data-stu-id="c7eb7-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="c7eb7-118">Visual Studio 或 msbuild /t: restore 尚不支持长路径。</span><span class="sxs-lookup"><span data-stu-id="c7eb7-118">Visual Studio or msbuild /t:restore does not yet support long paths.</span></span>
> -   <span data-ttu-id="c7eb7-119">软件使用 NuGet 库执行还原和其他命令，将支持长路径在同一系统上，NuGet.exe 适用于，如果他们还设置在其 windows longPathAware 清单并为 false，通过 App.Config配置UseLegacyPathHandling[请参阅详细信息](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="c7eb7-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set longPathAware in their windows manifest and configure UseLegacyPathHandling to false via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

