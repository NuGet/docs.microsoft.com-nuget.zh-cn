---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825166"
---
<span data-ttu-id="d66ed-101">使用 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 命令还原项目文件中列出的包（请参阅 [PackageReference](../../consume-packages/package-references-in-project-files.md)）。</span><span class="sxs-lookup"><span data-stu-id="d66ed-101">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="d66ed-102">使用 .NET Core 2.0 和更高版本，通过 `dotnet build` 和 `dotnet run` 自动完成还原。</span><span class="sxs-lookup"><span data-stu-id="d66ed-102">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="d66ed-103">从 NuGet 4.0 开始，它运行与 `nuget restore` 相同的代码。</span><span class="sxs-lookup"><span data-stu-id="d66ed-103">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="d66ed-104">与其他 `dotnet` CLI 命令一样，先打开命令行并切换到包含项目文件的目录。</span><span class="sxs-lookup"><span data-stu-id="d66ed-104">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="d66ed-105">使用 `dotnet restore` 还原包：</span><span class="sxs-lookup"><span data-stu-id="d66ed-105">To restore a package using `dotnet restore`:</span></span>

```dotnetcli
dotnet restore 
```