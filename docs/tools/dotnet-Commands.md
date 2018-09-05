---
title: dotnet NuGet 命令
description: 短 NuGet 相关的命令，使用 dotnet 命令行接口的引用。
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: 88e058be674ecddc500665bfa3517f19acde0cd7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546311"
---
# <a name="dotnet-commands"></a><span data-ttu-id="995f9-103">dotnet 命令</span><span class="sxs-lookup"><span data-stu-id="995f9-103">dotnet commands</span></span>

<span data-ttu-id="995f9-104">`dotnet`命令行接口，在 Windows、 Mac OS X 和 Linux 运行，提供了许多重要的 nuget.exe 命令，如下所示。</span><span class="sxs-lookup"><span data-stu-id="995f9-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="995f9-105">如果 dotnet 满足你的需求，不需要使用`nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="995f9-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="995f9-106">有关完整信息`dotnet`，请参阅[.NET Core 命令行接口 (CLI) 工具](/dotnet/core/tools/?tabs=netcore2x)。</span><span class="sxs-lookup"><span data-stu-id="995f9-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="995f9-107">包使用</span><span class="sxs-lookup"><span data-stu-id="995f9-107">Package consumption</span></span>

- <span data-ttu-id="995f9-108">[**dotnet 添加包**](/dotnet/core/tools/dotnet-add-package)： 添加包引用的项目文件，则会运行`dotnet restore`安装该包。</span><span class="sxs-lookup"><span data-stu-id="995f9-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="995f9-109">[**dotnet 中删除程序包**](/dotnet/core/tools/dotnet-remove-package)： 从项目文件中删除的包引用。</span><span class="sxs-lookup"><span data-stu-id="995f9-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="995f9-110">[**dotnet 还原**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x)： 恢复依赖项和项目的工具。</span><span class="sxs-lookup"><span data-stu-id="995f9-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="995f9-111">截至 NuGet 4.0 中，这将运行的相同代码`nuget restore`。</span><span class="sxs-lookup"><span data-stu-id="995f9-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="995f9-112">[**dotnet nuget 局部变量**](/dotnet/core/tools/dotnet-nuget-locals)： 列出的位置*全局包*， *http 缓存*，以及*temp*文件夹和清除的内容这些文件夹。</span><span class="sxs-lookup"><span data-stu-id="995f9-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="995f9-113">创建包</span><span class="sxs-lookup"><span data-stu-id="995f9-113">Package creation</span></span>

- <span data-ttu-id="995f9-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x)： 将代码打包到 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="995f9-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="995f9-115">截至 NuGet 4.0 中，这将运行的相同代码`nuget pack`。</span><span class="sxs-lookup"><span data-stu-id="995f9-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="995f9-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push)： 将包推送到服务器，并将它适用于 nuget.org、 Visual Studio Team Services 和第三方 NuGet 服务器发布。</span><span class="sxs-lookup"><span data-stu-id="995f9-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="995f9-117">[**dotnet nuget 删除**](/dotnet/core/tools/dotnet-nuget-delete)： 删除或取消列出包从一台主机，适用于 nuget.org、 Visual Studio Team Services 和第三方 NuGet 服务器。</span><span class="sxs-lookup"><span data-stu-id="995f9-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
