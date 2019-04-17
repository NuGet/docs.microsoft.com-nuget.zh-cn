---
title: NuGet CLI 添加命令
description: Nuget.exe 的引用添加命令
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545829"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="46aaa-103">add 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="46aaa-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="46aaa-104">**适用于**： 包发布&bullet;**支持的版本**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="46aaa-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="46aaa-105">将指定的包添加到层次结构的布局，其中包 ID 和版本编号创建的文件夹中的非 HTTP 包源 （文件夹或 UNC 路径）。</span><span class="sxs-lookup"><span data-stu-id="46aaa-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="46aaa-106">例如：</span><span class="sxs-lookup"><span data-stu-id="46aaa-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="46aaa-107">还原或更新时对包源，层次结构布局提供了显著提高性能。</span><span class="sxs-lookup"><span data-stu-id="46aaa-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="46aaa-108">若要扩展到的目标包源的包中的所有文件，使用`-Expand`切换。</span><span class="sxs-lookup"><span data-stu-id="46aaa-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="46aaa-109">这通常会出现在该目标，如其他子文件夹中`tools`和`lib`。</span><span class="sxs-lookup"><span data-stu-id="46aaa-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="46aaa-110">用法</span><span class="sxs-lookup"><span data-stu-id="46aaa-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="46aaa-111">其中`<packagePath>`是要添加的包的路径名和`<sourcePath>`指定可向其添加包的基于文件夹的包源。</span><span class="sxs-lookup"><span data-stu-id="46aaa-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="46aaa-112">不支持 HTTP 源。</span><span class="sxs-lookup"><span data-stu-id="46aaa-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="46aaa-113">选项</span><span class="sxs-lookup"><span data-stu-id="46aaa-113">Options</span></span>

| <span data-ttu-id="46aaa-114">选项</span><span class="sxs-lookup"><span data-stu-id="46aaa-114">Option</span></span> | <span data-ttu-id="46aaa-115">描述</span><span class="sxs-lookup"><span data-stu-id="46aaa-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="46aaa-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="46aaa-116">ConfigFile</span></span> | <span data-ttu-id="46aaa-117">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="46aaa-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="46aaa-118">如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。</span><span class="sxs-lookup"><span data-stu-id="46aaa-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="46aaa-119">Expand</span><span class="sxs-lookup"><span data-stu-id="46aaa-119">Expand</span></span> | <span data-ttu-id="46aaa-120">将包中的所有文件都添加到包源。</span><span class="sxs-lookup"><span data-stu-id="46aaa-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="46aaa-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="46aaa-121">ForceEnglishOutput</span></span> | <span data-ttu-id="46aaa-122">*（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="46aaa-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="46aaa-123">Help</span><span class="sxs-lookup"><span data-stu-id="46aaa-123">Help</span></span> | <span data-ttu-id="46aaa-124">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="46aaa-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="46aaa-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="46aaa-125">NonInteractive</span></span> | <span data-ttu-id="46aaa-126">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="46aaa-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="46aaa-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="46aaa-127">Verbosity</span></span> | <span data-ttu-id="46aaa-128">指定的输出中显示的详细信息：*正常*，*静默*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="46aaa-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="46aaa-129">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="46aaa-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="46aaa-130">示例</span><span class="sxs-lookup"><span data-stu-id="46aaa-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
