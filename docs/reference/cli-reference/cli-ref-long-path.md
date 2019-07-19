---
title: NuGet CLI 长路径支持
description: 支持 nuget.exe 长路径的参考
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 42b5b7d863d22d7aad99a65700ca11bcc2861db1
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327674"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="9731b-103">长路径支持 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="9731b-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="9731b-104">**适用于:** 所有&bullet; **支持的版本:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="9731b-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="9731b-105">Nuget.exe 4.8 和更高版本支持文件和目录的长路径, 适用于打包、还原、安装和需要文件路径的大多数其他方案。</span><span class="sxs-lookup"><span data-stu-id="9731b-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="9731b-106">所需操作系统</span><span class="sxs-lookup"><span data-stu-id="9731b-106">Required Operating System</span></span>

-   <span data-ttu-id="9731b-107">Windows 10 (版本1607或更高版本)</span><span class="sxs-lookup"><span data-stu-id="9731b-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="9731b-108">如果将 .NET Framework 升级到版本4.6.2 或更高版本, 则 Windows 10 (2015 年7月版或版本 1511)。</span><span class="sxs-lookup"><span data-stu-id="9731b-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="9731b-109">Windows Server 2016 (所有版本)</span><span class="sxs-lookup"><span data-stu-id="9731b-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="9731b-110">启用 "Win32 长路径" 组策略</span><span class="sxs-lookup"><span data-stu-id="9731b-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="9731b-111">需要通过设置组策略在这些系统上启用长路径支持。</span><span class="sxs-lookup"><span data-stu-id="9731b-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="9731b-112">逐步</span><span class="sxs-lookup"><span data-stu-id="9731b-112">Steps:</span></span>
1. <span data-ttu-id="9731b-113">启动**组策略编辑器**-在 "开始" 搜索栏中键入 "编辑组策略", 或从 "运行" 命令运行 "gpedit.msc" (Windows-R)。</span><span class="sxs-lookup"><span data-stu-id="9731b-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="9731b-114">在**本地组策略编辑器**中, 启用 "本地计算机策略/计算机配置/管理模板/所有设置/启用 Win32 长路径"。</span><span class="sxs-lookup"><span data-stu-id="9731b-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![长路径策略](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="9731b-116">启用其他 NuGet 工具以支持长路径</span><span class="sxs-lookup"><span data-stu-id="9731b-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="9731b-117">Dotnet CLI 支持长路径, 而不考虑操作系统或版本。</span><span class="sxs-lookup"><span data-stu-id="9731b-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="9731b-118">Visual Studio 或 msbuild t:restore 尚不支持长路径。</span><span class="sxs-lookup"><span data-stu-id="9731b-118">Visual Studio or msbuild -t:restore does not yet support long paths.</span></span>
> -   <span data-ttu-id="9731b-119">使用 NuGet 库执行还原和其他命令的软件将支持 Nuget.exe 在同一系统上的长路径, 前提是它们还在其 windows 清单中设置 longPathAware, 并通过 App.config[将 UseLegacyPathHandling 配置为 false查看详细信息](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="9731b-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set longPathAware in their windows manifest and configure UseLegacyPathHandling to false via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

