---
title: dotnet CLI NuGet 命令
description: 使用 dotnet 命令行界面的 NuGet 相关命令的简短参考。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 87cb3c8153931a0917338de9f7001406b5e12dfc
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699817"
---
# <a name="dotnet-cli-commands"></a><span data-ttu-id="33947-103">.NET CLI 命令</span><span class="sxs-lookup"><span data-stu-id="33947-103">dotnet CLI commands</span></span>

<span data-ttu-id="33947-104">`dotnet`命令行界面 (CLI) ，在 Windows、Mac OS X 和 Linux 上运行，它提供了许多必要的命令，例如安装、还原和发布程序包。</span><span class="sxs-lookup"><span data-stu-id="33947-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="33947-105">如果 dotnet 满足你的需求，则无需使用 `nuget.exe` 。</span><span class="sxs-lookup"><span data-stu-id="33947-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="33947-106">有关使用这些命令来使用包的示例，请参阅 [使用 DOTNET CLI 安装和管理包](../consume-packages/install-use-packages-dotnet-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="33947-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="33947-107">有关使用这些命令创建包的示例，请参阅 [使用 DOTNET CLI 创建和发布包](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="33947-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="33947-108">有关 cli 的完整命令参考 `dotnet` ，请参阅 [.net Core 命令行界面 (cli) 工具](/dotnet/core/tools/?tabs=netcore2x)。</span><span class="sxs-lookup"><span data-stu-id="33947-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="33947-109">包消耗</span><span class="sxs-lookup"><span data-stu-id="33947-109">Package consumption</span></span>

- <span data-ttu-id="33947-110">[**dotnet 添加包**](/dotnet/core/tools/dotnet-add-package)：向项目文件添加包引用，然后运行 `dotnet restore` 以安装包。</span><span class="sxs-lookup"><span data-stu-id="33947-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="33947-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package)：从项目文件中删除包引用。</span><span class="sxs-lookup"><span data-stu-id="33947-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="33947-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x)：还原项目的依赖项和工具。</span><span class="sxs-lookup"><span data-stu-id="33947-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="33947-113">从 NuGet 4.0 开始，它运行与 `nuget restore` 相同的代码。</span><span class="sxs-lookup"><span data-stu-id="33947-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="33947-114">[**dotnet nuget 局部变量**](/dotnet/core/tools/dotnet-nuget-locals)：列出 *全局包*、 *http 缓存* 和 *临时* 文件夹的位置，并清除这些文件夹的内容。</span><span class="sxs-lookup"><span data-stu-id="33947-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>
- <span data-ttu-id="33947-115">[**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new)：创建 [`nuget.config`](../reference/nuget-config-file.md) 文件以配置 NuGet 的行为。</span><span class="sxs-lookup"><span data-stu-id="33947-115">[**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new): Creates a [`nuget.config`](../reference/nuget-config-file.md) file to configure NuGet's behavior.</span></span>

## <a name="package-creation"></a><span data-ttu-id="33947-116">包创建</span><span class="sxs-lookup"><span data-stu-id="33947-116">Package creation</span></span>

- <span data-ttu-id="33947-117">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x)：将代码打包到 NuGet 包中。</span><span class="sxs-lookup"><span data-stu-id="33947-117">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span>
- <span data-ttu-id="33947-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push)：将包发布到 nuget 服务器。</span><span class="sxs-lookup"><span data-stu-id="33947-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Publishes a package to a NuGet server.</span></span> <span data-ttu-id="33947-119">适用于 nuget.org、Azure Artifacts 和 [第三方 nuget 服务器](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="33947-119">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
- <span data-ttu-id="33947-120">[**dotnet nuget 删除**](/dotnet/core/tools/dotnet-nuget-delete)：从 nuget 服务器中删除或取消列出包。</span><span class="sxs-lookup"><span data-stu-id="33947-120">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a NuGet server.</span></span> <span data-ttu-id="33947-121">适用于 nuget.org、Azure Artifacts 和 [第三方 nuget 服务器](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="33947-121">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
- <span data-ttu-id="33947-122">[**dotnet nuget 验证**](/dotnet/core/tools/dotnet-nuget-verify)：验证已签名的 nuget 包。</span><span class="sxs-lookup"><span data-stu-id="33947-122">[**dotnet nuget verify**](/dotnet/core/tools/dotnet-nuget-verify): Verifies a signed NuGet package.</span></span>
