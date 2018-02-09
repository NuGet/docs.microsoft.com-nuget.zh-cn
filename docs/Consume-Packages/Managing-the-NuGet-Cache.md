---
title: "如何在 NuGet 中管理包缓存 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "如何管理计算机上存在的不同 NuGet 包缓存，安装或还原包时会用到这些包缓存。"
keywords: "NuGet 包缓存, 包缓存, NuGet 缓存, 管理缓存, 本地 NuGet 缓存, 全局 NuGet 缓存, NuGet 局部变量命令, 清除缓存"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 84bc34e02572a912fb86ce1a5cf54d8ff212ac6e
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2018
---
# <a name="managing-the-nuget-cache"></a><span data-ttu-id="dcc18-104">管理 NuGet 缓存</span><span class="sxs-lookup"><span data-stu-id="dcc18-104">Managing the NuGet cache</span></span>

<span data-ttu-id="dcc18-105">NuGet 管理多个本地缓存，以避免下载计算机上已经存在的包并提供离线支持。</span><span class="sxs-lookup"><span data-stu-id="dcc18-105">NuGet manages several local caches to avoid downloading packages that are already on the computer, and to provide offline support.</span></span> <span data-ttu-id="dcc18-106">在没有网络连接的情况下安装或重新安装包时，NuGet 会自动回退到缓存。</span><span class="sxs-lookup"><span data-stu-id="dcc18-106">NuGet automatically falls back to the cache when installing or reinstalling packages without a network connection.</span></span>

<span data-ttu-id="dcc18-107">可通过[局部变量命令](../tools/cli-ref-locals.md)使用缓存位置：</span><span class="sxs-lookup"><span data-stu-id="dcc18-107">Cache locations are available using the [locals command](../tools/cli-ref-locals.md):</span></span>

```cli
nuget locals all -list
```

<span data-ttu-id="dcc18-108">典型输出如下所示：</span><span class="sxs-lookup"><span data-stu-id="dcc18-108">Typical output is as follows:</span></span>

```output
http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder
```

<span data-ttu-id="dcc18-109">如果安装包时遇到问题或想要确保从远程库安装包，请使用 `locals -clear` 选项：</span><span class="sxs-lookup"><span data-stu-id="dcc18-109">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals -clear` option:</span></span>

```cli
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

<span data-ttu-id="dcc18-110">请注意，目前仅支持从 NuGet 命令行管理缓存，而不支持在 Visual Studio 中或通过包管理器控制台管理缓存。</span><span class="sxs-lookup"><span data-stu-id="dcc18-110">Note that managing the cache is presently supported only from the NuGet command line, and not within Visual Studio or through the Package Manager Console.</span></span> <span data-ttu-id="dcc18-111">此外，NuGet 3.6 及更高版本中不支持管理 2.x 缓存。</span><span class="sxs-lookup"><span data-stu-id="dcc18-111">Also, managing the 2.x cache is not supported in NuGet 3.6 and later.</span></span>

<span data-ttu-id="dcc18-112">使用 `nuget locals` 时可能出现以下错误：</span><span class="sxs-lookup"><span data-stu-id="dcc18-112">The following errors can occur when using `nuget locals`:</span></span>

- <span data-ttu-id="dcc18-113">**清除本地资源失败：无法删除一个或多个文件**</span><span class="sxs-lookup"><span data-stu-id="dcc18-113">**Clearing local resources failed: Unable to delete one or more files**</span></span>
- <span data-ttu-id="dcc18-114">**目录不为空**</span><span class="sxs-lookup"><span data-stu-id="dcc18-114">**The directory is not empty**</span></span>

<span data-ttu-id="dcc18-115">这表明你无权删除缓存中的文件，或缓存中的一个或多个文件正被另一进程使用，必须关闭这些文件，然后才能进行删除。</span><span class="sxs-lookup"><span data-stu-id="dcc18-115">These indicate that you either do not have permission to delete files in the cache, or that one or more files in the cache are in use by another process, which must be closed before the those files can be removed.</span></span>
