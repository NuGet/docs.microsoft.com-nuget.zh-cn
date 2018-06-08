---
title: NuGet 包与源代码管理
description: 介绍有关以下内容的注意事项：如何在版本控制和源代码管理系统中处理 NuGet 包，以及如何使用 Git 和 TFVC 省略包。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9392e3b6f0e9e64935ec27c28806b27a133bbfe8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817527"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="38905-103">在源代码管理系统中省略 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="38905-103">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="38905-104">开发人员通常省略源代码管理存储库中的 NuGet 包，且改为依赖[包还原](package-restore.md)在生成前重新安装项目的依赖项。</span><span class="sxs-lookup"><span data-stu-id="38905-104">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="38905-105">以下是依赖包还原的原因：</span><span class="sxs-lookup"><span data-stu-id="38905-105">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="38905-106">分布式版本控制系统（如 Git）包括存储库中每个文件每个版本的完整副本。</span><span class="sxs-lookup"><span data-stu-id="38905-106">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="38905-107">频繁更新的二进制文件会造成大量膨胀并延长克隆存储库所需的时间。</span><span class="sxs-lookup"><span data-stu-id="38905-107">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="38905-108">当存储库中包含包时，开发人员负责将引用直接添加到磁盘上的包内容中，而不是通过 NuGet 引用包（可导致项目中的硬编码路径名）。</span><span class="sxs-lookup"><span data-stu-id="38905-108">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="38905-109">清理任何未使用包文件夹的解决方案会变得更困难，因为需要确保不删除仍在使用的任何包文件夹。</span><span class="sxs-lookup"><span data-stu-id="38905-109">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="38905-110">通过省略包，可以在代码和所依赖的其他包之间维护清晰的所有权边界。</span><span class="sxs-lookup"><span data-stu-id="38905-110">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="38905-111">许多 NuGet 包已在其自己的源代码管理存储库中进行了维护。</span><span class="sxs-lookup"><span data-stu-id="38905-111">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="38905-112">尽管包还原是 NuGet 的默认行为，但省略源代码管理中的包&mdash;即项目中的 `packages` 文件夹&mdash;仍需进行一些手动操作，详情请见本文。</span><span class="sxs-lookup"><span data-stu-id="38905-112">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="38905-113">使用 Git 省略包</span><span class="sxs-lookup"><span data-stu-id="38905-113">Omitting packages with Git</span></span>

<span data-ttu-id="38905-114">使用 [.gitignore 文件](https://git-scm.com/docs/gitignore)忽略 NuGet 包 (`.nupkg`)、`packages` 文件夹、`project.assets.json` 及其他内容。</span><span class="sxs-lookup"><span data-stu-id="38905-114">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="38905-115">有关参考，请参阅 [Visual Studio 项目的示例 `.gitignore`](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)：</span><span class="sxs-lookup"><span data-stu-id="38905-115">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="38905-116">以下是 `.gitignore` 文件的重要部分：</span><span class="sxs-lookup"><span data-stu-id="38905-116">The important parts of the `.gitignore` file are:</span></span>

```gitignore
# Ignore NuGet Packages
*.nupkg

# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*

# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/

# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config

# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json (NuGet v3); project.assets.json is used in conjunction with the PackageReference
# format (NuGet v4 and .NET Core).
project.lock.json
project.assets.json
```

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="38905-117">使用 Team Foundation 版本控制省略包</span><span class="sxs-lookup"><span data-stu-id="38905-117">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="38905-118">向源代码管理添加项目之前，请尽量按照这些说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="38905-118">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="38905-119">否则，请手动删除存储库中的 `packages` 文件夹并签入该更改，然后才能继续。</span><span class="sxs-lookup"><span data-stu-id="38905-119">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="38905-120">要使用 TFVC 为选定的文件禁用源代码管理集成，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="38905-120">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="38905-121">在解决方案文件夹（`.sln` 文件所在的位置）中创建名为 `.nuget` 的文件夹。</span><span class="sxs-lookup"><span data-stu-id="38905-121">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="38905-122">提示：对于 Windows，若要在 Windows 资源管理器中创建此文件夹，请使用具有尾随点的名称 `.nuget.`。</span><span class="sxs-lookup"><span data-stu-id="38905-122">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="38905-123">在该文件夹中，创建名为 `NuGet.Config` 的文件，将其打开进行编辑。</span><span class="sxs-lookup"><span data-stu-id="38905-123">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="38905-124">至少添加以下文本，其中 [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) 设置指示 Visual Studio 跳过 `packages` 文件夹中的所有内容：</span><span class="sxs-lookup"><span data-stu-id="38905-124">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="38905-125">如果使用的是 TFS 2010 或更早版本，请掩蔽工作区映射中的 `packages` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="38905-125">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="38905-126">对于 TFS 2012 或更高版本或者 Visual Studio Team Services，请按照 [Add Files to the Server](/vsts/tfvc/add-files-server.md?view=vsts#tfignore)（将文件添加到服务器）中所述创建 `.tfignore` 文件。</span><span class="sxs-lookup"><span data-stu-id="38905-126">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [AddFiles to the Server](/vsts/tfvc/add-files-server.md?view=vsts#tfignore).</span></span> <span data-ttu-id="38905-127">在该文件中，包括以下内容以显式忽略对存储库级别上的 `\packages` 文件夹和其他几个中间文件的修改。</span><span class="sxs-lookup"><span data-stu-id="38905-127">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="38905-128">（可以使用具有尾随点的 `.tfignore.` 名称在 Windows 资源管理器中创建文件，但可能需要首先禁用“隐藏已知文件扩展名”选项。）：</span><span class="sxs-lookup"><span data-stu-id="38905-128">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Exclude package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="38905-129">向源代码管理添加 `NuGet.Config` 和 `.tfignore`，并签入更改。</span><span class="sxs-lookup"><span data-stu-id="38905-129">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
