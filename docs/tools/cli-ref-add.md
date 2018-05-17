---
title: NuGet CLI 添加命令
description: Nuget.exe 的引用添加命令
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4a4201a321ffe0f7fb61f4e98012a1a2d7d8fda4
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="1d746-103">add 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1d746-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="1d746-104">**适用于**： 包发布&bullet;**受支持的版本**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="1d746-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="1d746-105">将指定的包添加到其中的包 ID 和版本号创建文件夹层次结构布局中的非 HTTP 包源 （文件夹或 UNC 路径）。</span><span class="sxs-lookup"><span data-stu-id="1d746-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="1d746-106">例如：</span><span class="sxs-lookup"><span data-stu-id="1d746-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="1d746-107">还原或更新时对包源，则层次结构布局提供显著提高性能。</span><span class="sxs-lookup"><span data-stu-id="1d746-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="1d746-108">若要对目标包源扩展包中的所有文件，使用`-Expand`切换。</span><span class="sxs-lookup"><span data-stu-id="1d746-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="1d746-109">这通常会出现在该目标，如其他子文件夹中`tools`和`lib`。</span><span class="sxs-lookup"><span data-stu-id="1d746-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="1d746-110">用法</span><span class="sxs-lookup"><span data-stu-id="1d746-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="1d746-111">其中`<packagePath>`到包后，若要添加，路径名和`<sourcePath>`指定包将添加到基于文件夹的包源。</span><span class="sxs-lookup"><span data-stu-id="1d746-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="1d746-112">不支持 HTTP 源。</span><span class="sxs-lookup"><span data-stu-id="1d746-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="1d746-113">选项</span><span class="sxs-lookup"><span data-stu-id="1d746-113">Options</span></span>

| <span data-ttu-id="1d746-114">选项</span><span class="sxs-lookup"><span data-stu-id="1d746-114">Option</span></span> | <span data-ttu-id="1d746-115">描述</span><span class="sxs-lookup"><span data-stu-id="1d746-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1d746-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1d746-116">ConfigFile</span></span> | <span data-ttu-id="1d746-117">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="1d746-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1d746-118">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="1d746-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1d746-119">Expand</span><span class="sxs-lookup"><span data-stu-id="1d746-119">Expand</span></span> | <span data-ttu-id="1d746-120">将包中的所有文件都添加到包源。</span><span class="sxs-lookup"><span data-stu-id="1d746-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="1d746-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1d746-121">ForceEnglishOutput</span></span> | <span data-ttu-id="1d746-122">*（3.5 +)* 强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="1d746-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1d746-123">帮助</span><span class="sxs-lookup"><span data-stu-id="1d746-123">Help</span></span> | <span data-ttu-id="1d746-124">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="1d746-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="1d746-125">非交互式</span><span class="sxs-lookup"><span data-stu-id="1d746-125">NonInteractive</span></span> | <span data-ttu-id="1d746-126">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="1d746-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1d746-127">详细级别</span><span class="sxs-lookup"><span data-stu-id="1d746-127">Verbosity</span></span> | <span data-ttu-id="1d746-128">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="1d746-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="1d746-129">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1d746-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1d746-130">示例</span><span class="sxs-lookup"><span data-stu-id="1d746-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
