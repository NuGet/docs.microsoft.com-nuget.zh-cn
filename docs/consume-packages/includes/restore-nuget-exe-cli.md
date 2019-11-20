---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860585"
---
<span data-ttu-id="0ba4d-101">使用 [restore](../../reference/cli-reference/cli-ref-restore.md) 命令可下载并安装“包”文件夹中缺少的所有包。 </span><span class="sxs-lookup"><span data-stu-id="0ba4d-101">Use the [restore](../../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="0ba4d-102">对于迁移到 PackageReference 的项目，请使用 [msbuild -t:restore](../package-restore.md#restore-using-msbuild) 还原程序包。</span><span class="sxs-lookup"><span data-stu-id="0ba4d-102">For projects migrated to PackageReference, use [msbuild -t:restore](../package-restore.md#restore-using-msbuild) to restore packages instead.</span></span>

<span data-ttu-id="0ba4d-103">`restore` 仅将包添加到磁盘，但不会更改项目的依赖项。</span><span class="sxs-lookup"><span data-stu-id="0ba4d-103">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="0ba4d-104">要还原项目依赖项，请修改 `packages.config`，然后使用 `restore` 命令。</span><span class="sxs-lookup"><span data-stu-id="0ba4d-104">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="0ba4d-105">与其他 `nuget.exe` CLI 命令一样，先打开命令行并切换到包含项目文件的目录。</span><span class="sxs-lookup"><span data-stu-id="0ba4d-105">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="0ba4d-106">使用 `restore` 还原包：</span><span class="sxs-lookup"><span data-stu-id="0ba4d-106">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```