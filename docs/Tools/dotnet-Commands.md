---
title: dotNet NuGet 命令 |Microsoft 文档
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 使用 dotnet 命令行界面的 NuGet 相关命令短引用。
keywords: dotnet NuGet 命令、 dotnet 包、 dotnet 还原、 dotnet nuget 局部变量、 dotnet nuget 推送和 dotnet nuget 删除
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 352145701fba509e21e774a429d227e7427a1f0d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="1ceee-104">dotNet 命令</span><span class="sxs-lookup"><span data-stu-id="1ceee-104">dotNet commands</span></span>

<span data-ttu-id="1ceee-105">`dotnet`命令行界面，在 Windows、 Mac OS X 和 Linux 运行，提供了大量基本 nuget.exe 命令，如下所示。</span><span class="sxs-lookup"><span data-stu-id="1ceee-105">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="1ceee-106">如果 dotnet 满足你的需求，不需要使用`nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="1ceee-106">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="1ceee-107">有关完整信息`dotnet`，请参阅[.NET 核心命令行界面 (CLI) 工具](/dotnet/core/tools/?tabs=netcore2x)。</span><span class="sxs-lookup"><span data-stu-id="1ceee-107">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="1ceee-108">包消耗</span><span class="sxs-lookup"><span data-stu-id="1ceee-108">Package consumption</span></span>

- <span data-ttu-id="1ceee-109">[**dotnet 添加包**](/dotnet/core/tools/dotnet-add-package): 包将引用添加到项目文件中，然后运行`dotnet restore`安装该包。</span><span class="sxs-lookup"><span data-stu-id="1ceee-109">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="1ceee-110">[**dotnet 删除包**](/dotnet/core/tools/dotnet-remove-package)： 从项目文件中删除的包引用。</span><span class="sxs-lookup"><span data-stu-id="1ceee-110">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="1ceee-111">[**dotnet 还原**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x)： 还原的依赖关系和项目的工具。</span><span class="sxs-lookup"><span data-stu-id="1ceee-111">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="1ceee-112">截至 NuGet 4.0 中，这将运行的相同代码`nuget restore`。</span><span class="sxs-lookup"><span data-stu-id="1ceee-112">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="1ceee-113">[**dotnet nuget 局部变量**](/dotnet/core/tools/dotnet-nuget-locals)： 列出的位置*全局包*， *http 缓存*，和*temp*文件夹和清除的内容这些文件夹。</span><span class="sxs-lookup"><span data-stu-id="1ceee-113">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="1ceee-114">创建包</span><span class="sxs-lookup"><span data-stu-id="1ceee-114">Package creation</span></span>

- <span data-ttu-id="1ceee-115">[**dotnet 包**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x)： 包代码放在一个 NuGet 程序包。</span><span class="sxs-lookup"><span data-stu-id="1ceee-115">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="1ceee-116">截至 NuGet 4.0 中，这将运行的相同代码`nuget pack`。</span><span class="sxs-lookup"><span data-stu-id="1ceee-116">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="1ceee-117">[**dotnet nuget 推送**](/dotnet/core/tools/dotnet-nuget-push)： 将包推送到服务器并发布它适用于 nuget.org、 Visual Studio Team Services 和第三方 NuGet 服务器。</span><span class="sxs-lookup"><span data-stu-id="1ceee-117">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="1ceee-118">[**dotnet nuget 删除**](/dotnet/core/tools/dotnet-nuget-delete)： 删除或 unlists 从一台主机，适用于 nuget.org、 Visual Studio Team Services 和第三方 NuGet 服务器包。</span><span class="sxs-lookup"><span data-stu-id="1ceee-118">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
