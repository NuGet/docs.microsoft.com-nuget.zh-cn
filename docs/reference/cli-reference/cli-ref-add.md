---
title: NuGet CLI 添加命令
description: nuget.exe add 命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 096d2f7a61a3c861ce2084368500ab8e8b21f212
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776089"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="ae17a-103"> (NuGet CLI 添加命令) </span><span class="sxs-lookup"><span data-stu-id="ae17a-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="ae17a-104">**适用** 于：包发布 &bullet; **支持的版本**： 3.3 +</span><span class="sxs-lookup"><span data-stu-id="ae17a-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="ae17a-105">将指定的包添加到 (文件夹或 UNC 路径的非 HTTP 包源中) 在层次结构布局中，其中为包 ID 和版本号创建了文件夹。</span><span class="sxs-lookup"><span data-stu-id="ae17a-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="ae17a-106">例如：</span><span class="sxs-lookup"><span data-stu-id="ae17a-106">For example:</span></span>

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

<span data-ttu-id="ae17a-107">针对包源还原或更新时，分层布局提供明显更好的性能。</span><span class="sxs-lookup"><span data-stu-id="ae17a-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="ae17a-108">若要将包中的所有文件展开到目标包源，请使用 `-Expand` 开关。</span><span class="sxs-lookup"><span data-stu-id="ae17a-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="ae17a-109">这通常会导致在目标中出现其他子文件夹，例如 `tools` 和 `lib` 。</span><span class="sxs-lookup"><span data-stu-id="ae17a-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="ae17a-110">使用情况</span><span class="sxs-lookup"><span data-stu-id="ae17a-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="ae17a-111">其中， `<packagePath>` 是要添加的包的路径名，并指定要将 `<sourcePath>` 包添加到的基于文件夹的包源。</span><span class="sxs-lookup"><span data-stu-id="ae17a-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="ae17a-112">HTTP 源不受支持。</span><span class="sxs-lookup"><span data-stu-id="ae17a-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="ae17a-113">选项</span><span class="sxs-lookup"><span data-stu-id="ae17a-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="ae17a-114">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="ae17a-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ae17a-115">如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="ae17a-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="ae17a-116">将包中的所有文件添加到包源。</span><span class="sxs-lookup"><span data-stu-id="ae17a-116">Adds all the files in the package to the package source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="ae17a-117">*(3.5 +)* 使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="ae17a-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>
<span data-ttu-id="ae17a-118">使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="ae17a-118">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="ae17a-119">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="ae17a-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="ae17a-120">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="ae17a-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

   <span data-ttu-id="ae17a-121">指定将向其添加 nupkg 的包源（文件夹或 UNC 共享）。</span><span class="sxs-lookup"><span data-stu-id="ae17a-121">Specifies the package source, which is a folder or UNC share, to which the nupkg will be added.</span></span> <span data-ttu-id="ae17a-122">Http 源不受支持。</span><span class="sxs-lookup"><span data-stu-id="ae17a-122">Http sources are not supported.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="ae17a-123">指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="ae17a-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="ae17a-124">另请参阅 [环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ae17a-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ae17a-125">示例</span><span class="sxs-lookup"><span data-stu-id="ae17a-125">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
