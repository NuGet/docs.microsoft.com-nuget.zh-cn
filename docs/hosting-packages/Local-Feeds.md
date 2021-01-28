---
title: 设置本地 NuGet 源
description: 如何在本地网络上使用文件夹创建 NuGet 包的本地源
author: JonDouglas
ms.author: jodou
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 1eb194c9ddaee05281749c7a0420cbaf77044fe3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774034"
---
# <a name="local-feeds"></a><span data-ttu-id="bb77c-103">本地源</span><span class="sxs-lookup"><span data-stu-id="bb77c-103">Local feeds</span></span>

<span data-ttu-id="bb77c-104">本地 NuGet 包源只是本地网络（甚至自己的计算机）上放置包的分层文件夹结构。</span><span class="sxs-lookup"><span data-stu-id="bb77c-104">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="bb77c-105">然后，这些源可在使用 CLI、包管理器 UI 和包管理器控制台的所有其他 NuGet 操作中用作包源。</span><span class="sxs-lookup"><span data-stu-id="bb77c-105">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="bb77c-106">若要启用源，请使用[包管理器 UI](../consume-packages/install-use-packages-visual-studio.md#package-sources) 或 [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) 命令将其路径名（如 `\\myserver\packages`）添加到源列表中。</span><span class="sxs-lookup"><span data-stu-id="bb77c-106">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md#package-sources) or the [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="bb77c-107">NuGet 3.3+ 中支持分层文件夹结构。</span><span class="sxs-lookup"><span data-stu-id="bb77c-107">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="bb77c-108">较旧版本的 NuGet 仅使用包含包的一个文件夹，其性能远低于层次结构。</span><span class="sxs-lookup"><span data-stu-id="bb77c-108">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="bb77c-109">初始化和维护分层文件夹</span><span class="sxs-lookup"><span data-stu-id="bb77c-109">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="bb77c-110">分层版本控制的文件夹树具有以下常规结构：</span><span class="sxs-lookup"><span data-stu-id="bb77c-110">The hierarchical versioned folder tree has the following general structure:</span></span>

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      └─<other files>
```

<span data-ttu-id="bb77c-111">当使用 [`nuget add`](../reference/cli-reference/cli-ref-add.md) 命令将包复制到源时，NuGet 自动创建此结构：</span><span class="sxs-lookup"><span data-stu-id="bb77c-111">NuGet creates this structure automatically when you use the [`nuget add`](../reference/cli-reference/cli-ref-add.md) command to copy a package to the feed:</span></span>

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="bb77c-112">`nuget add` 命令一次仅用于一个包，这在设置具有多个包的源时会造成不便。</span><span class="sxs-lookup"><span data-stu-id="bb77c-112">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="bb77c-113">在此情况下，请使用 [`nuget init`](../reference/cli-reference/cli-ref-init.md) 命令将文件夹中的所有包复制到源，就像在每个源上单独运行 `nuget add`。</span><span class="sxs-lookup"><span data-stu-id="bb77c-113">In such cases, use the [`nuget init`](../reference/cli-reference/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="bb77c-114">例如，以下命令将所有包从 `c:\packages` 复制到 `\\myserver\packages` 上的分层树中：</span><span class="sxs-lookup"><span data-stu-id="bb77c-114">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```cli
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="bb77c-115">与 `add` 命令一样，`init` 为每个包标识符创建文件夹，每个文件夹中包含具有相应包的版本号文件夹。</span><span class="sxs-lookup"><span data-stu-id="bb77c-115">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
