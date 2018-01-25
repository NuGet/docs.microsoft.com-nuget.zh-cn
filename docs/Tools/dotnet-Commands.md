---
title: "dotNet NuGet 命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "使用 dotnet 命令行界面的 NuGet 相关命令短引用。"
keywords: "dotnet NuGet 命令、 dotnet 包、 dotnet 还原、 dotnet nuget 局部变量、 dotnet nuget 推送和 dotnet nuget 删除"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d06e4590ab87b68e7846a13b2eba0f59eb9529d6
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="7f9fe-104">dotNet 命令</span><span class="sxs-lookup"><span data-stu-id="7f9fe-104">dotNet commands</span></span>

<span data-ttu-id="7f9fe-105">DotNet 命令行界面，在 Windows、 Mac OS X 和 Linux 上运行，提供了大量基本 nuget.exe 命令如下所示。</span><span class="sxs-lookup"><span data-stu-id="7f9fe-105">The DotNet command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="7f9fe-106">其中 dotnet 提供了所需的命令，不需要下载 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="7f9fe-106">Where dotnet provides the desired commands, it's not necessary to download nuget.exe.</span></span>

- <span data-ttu-id="7f9fe-107">[**dotnet 包**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x)： 包代码放在一个 NuGet 程序包。</span><span class="sxs-lookup"><span data-stu-id="7f9fe-107">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="7f9fe-108">截至 NuGet 4.0 中，这将运行的相同代码`nuget pack`。</span><span class="sxs-lookup"><span data-stu-id="7f9fe-108">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="7f9fe-109">[**dotnet 还原**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x)： 还原的依赖关系和项目的工具。</span><span class="sxs-lookup"><span data-stu-id="7f9fe-109">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="7f9fe-110">截至 NuGet 4.0 中，这将运行的相同代码`nuget restore`。</span><span class="sxs-lookup"><span data-stu-id="7f9fe-110">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="7f9fe-111">[**dotnet nuget 局部变量**](/dotnet/core/tools/dotnet-nuget-locals)： 清除或列出-请求的本地 NuGet 资源，如 http 缓存、 临时缓存或计算机范围全局包文件夹。</span><span class="sxs-lookup"><span data-stu-id="7f9fe-111">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as http the -request cache, temporary cache, or machine-wide global packages folder.</span></span>
- <span data-ttu-id="7f9fe-112">[**dotnet nuget 推送**](/dotnet/core/tools/dotnet-nuget-push)： 将包推送到服务器并发布它适用于 nuget.org、 Visual Studio Team Services 或任何第三方 NuGet 服务器。</span><span class="sxs-lookup"><span data-stu-id="7f9fe-112">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
- <span data-ttu-id="7f9fe-113">[**dotnet nuget 删除**](/dotnet/core/tools/dotnet-nuget-delete)： 删除或 unlists 程序包的来源的服务器，适用于 nuget.org、 Visual Studio Team Services 或任何第三方 NuGet 服务器。</span><span class="sxs-lookup"><span data-stu-id="7f9fe-113">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a  server, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
