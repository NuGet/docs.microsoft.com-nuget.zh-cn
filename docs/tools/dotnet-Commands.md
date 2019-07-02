---
title: dotnet CLI NuGet 命令
description: 短 NuGet 相关的命令，使用 dotnet 命令行接口的引用。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496471"
---
# <a name="dotnet-cli-commands"></a><span data-ttu-id="97d89-103">dotnet CLI 命令</span><span class="sxs-lookup"><span data-stu-id="97d89-103">dotnet CLI commands</span></span>

<span data-ttu-id="97d89-104">`dotnet`命令行接口 (CLI)，在 Windows、 Mac OS X 和 Linux 运行，提供了许多基本命令，例如安装、 还原和发布包。</span><span class="sxs-lookup"><span data-stu-id="97d89-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="97d89-105">如果 dotnet 满足你的需求，不需要使用`nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="97d89-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="97d89-106">有关使用这些命令来使用包的示例，请参阅[安装和管理包使用 dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="97d89-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="97d89-107">使用以下命令以创建包的示例，请参阅[创建和发布包使用 dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="97d89-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="97d89-108">有关完整的命令参考`dotnet`CLI，请参阅[.NET Core 命令行接口 (CLI) 工具](/dotnet/core/tools/?tabs=netcore2x)。</span><span class="sxs-lookup"><span data-stu-id="97d89-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="97d89-109">包使用</span><span class="sxs-lookup"><span data-stu-id="97d89-109">Package consumption</span></span>

- <span data-ttu-id="97d89-110">[**dotnet 添加包**](/dotnet/core/tools/dotnet-add-package):添加包引用的项目文件，则会运行`dotnet restore`安装该包。</span><span class="sxs-lookup"><span data-stu-id="97d89-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="97d89-111">[**dotnet 中删除程序包**](/dotnet/core/tools/dotnet-remove-package):从项目文件中删除的包引用。</span><span class="sxs-lookup"><span data-stu-id="97d89-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="97d89-112">[**dotnet 还原**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x):还原依赖项和项目的工具。</span><span class="sxs-lookup"><span data-stu-id="97d89-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="97d89-113">截至 NuGet 4.0 中，这将运行的相同代码`nuget restore`。</span><span class="sxs-lookup"><span data-stu-id="97d89-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="97d89-114">[**dotnet nuget 局部变量**](/dotnet/core/tools/dotnet-nuget-locals):列出的位置*全局包*， *http 缓存*，并*temp*文件夹和清除这些文件夹的内容。</span><span class="sxs-lookup"><span data-stu-id="97d89-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>
- <span data-ttu-id="97d89-115">[**dotnet 新 nugetconfig**](/dotnet/core/tools/dotnet-new):创建[ `nuget.config` ](../reference/nuget-config-file.md)文件来配置 NuGet 的行为。</span><span class="sxs-lookup"><span data-stu-id="97d89-115">[**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new): Creates a [`nuget.config`](../reference/nuget-config-file.md) file to configure NuGet's behavior.</span></span>

## <a name="package-creation"></a><span data-ttu-id="97d89-116">创建包</span><span class="sxs-lookup"><span data-stu-id="97d89-116">Package creation</span></span>

- <span data-ttu-id="97d89-117">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x):将代码打包到 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="97d89-117">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span>
- <span data-ttu-id="97d89-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push):将包发布到 NuGet 服务器。</span><span class="sxs-lookup"><span data-stu-id="97d89-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Publishes a package to a NuGet server.</span></span> <span data-ttu-id="97d89-119">适用于 nuget.org 中，Azure 项目，并[第三方 NuGet 服务器](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="97d89-119">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
- <span data-ttu-id="97d89-120">[**dotnet nuget 删除**](/dotnet/core/tools/dotnet-nuget-delete):删除或取消列出包从 NuGet 服务器。</span><span class="sxs-lookup"><span data-stu-id="97d89-120">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a NuGet server.</span></span> <span data-ttu-id="97d89-121">适用于 nuget.org 中，Azure 项目，并[第三方 NuGet 服务器](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="97d89-121">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
