---
title: NuGet CLI 添加命令
description: Nuget.exe add 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327854"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="0f55b-103">add 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="0f55b-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="0f55b-104">**适用**于: 包发布&bullet; **支持的版本**:3.3+</span><span class="sxs-lookup"><span data-stu-id="0f55b-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="0f55b-105">将指定的包添加到分层布局中的非 HTTP 包源 (文件夹或 UNC 路径), 其中为包 ID 和版本号创建了文件夹。</span><span class="sxs-lookup"><span data-stu-id="0f55b-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="0f55b-106">例如:</span><span class="sxs-lookup"><span data-stu-id="0f55b-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="0f55b-107">针对包源还原或更新时, 分层布局提供明显更好的性能。</span><span class="sxs-lookup"><span data-stu-id="0f55b-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="0f55b-108">若要将包中的所有文件展开到目标包源, 请使用`-Expand`开关。</span><span class="sxs-lookup"><span data-stu-id="0f55b-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="0f55b-109">这通常会导致在目标中出现其他子文件夹, 例如`tools`和`lib`。</span><span class="sxs-lookup"><span data-stu-id="0f55b-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="0f55b-110">用法</span><span class="sxs-lookup"><span data-stu-id="0f55b-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="0f55b-111">其中`<packagePath>` , 是要添加的包的路径名, 并`<sourcePath>`指定要将包添加到的基于文件夹的包源。</span><span class="sxs-lookup"><span data-stu-id="0f55b-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="0f55b-112">HTTP 源不受支持。</span><span class="sxs-lookup"><span data-stu-id="0f55b-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="0f55b-113">选项</span><span class="sxs-lookup"><span data-stu-id="0f55b-113">Options</span></span>

| <span data-ttu-id="0f55b-114">选项</span><span class="sxs-lookup"><span data-stu-id="0f55b-114">Option</span></span> | <span data-ttu-id="0f55b-115">描述</span><span class="sxs-lookup"><span data-stu-id="0f55b-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0f55b-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="0f55b-116">ConfigFile</span></span> | <span data-ttu-id="0f55b-117">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="0f55b-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="0f55b-118">如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="0f55b-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="0f55b-119">Expand</span><span class="sxs-lookup"><span data-stu-id="0f55b-119">Expand</span></span> | <span data-ttu-id="0f55b-120">将包中的所有文件添加到包源。</span><span class="sxs-lookup"><span data-stu-id="0f55b-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="0f55b-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="0f55b-121">ForceEnglishOutput</span></span> | <span data-ttu-id="0f55b-122">*(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="0f55b-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="0f55b-123">Help</span><span class="sxs-lookup"><span data-stu-id="0f55b-123">Help</span></span> | <span data-ttu-id="0f55b-124">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="0f55b-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="0f55b-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="0f55b-125">NonInteractive</span></span> | <span data-ttu-id="0f55b-126">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="0f55b-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="0f55b-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="0f55b-127">Verbosity</span></span> | <span data-ttu-id="0f55b-128">指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="0f55b-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="0f55b-129">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0f55b-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0f55b-130">示例</span><span class="sxs-lookup"><span data-stu-id="0f55b-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
