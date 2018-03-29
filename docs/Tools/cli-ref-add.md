---
title: NuGet CLI 将命令添加 |Microsoft 文档
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe 的引用添加命令
keywords: nuget 添加引用，添加包命令
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 48e093cbae2cecb1652e17a9b26920107aa8aef7
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="c85e7-104">添加命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c85e7-104">add command (NuGet CLI)</span></span>

<span data-ttu-id="c85e7-105">**适用于**： 包发布&bullet;**受支持的版本**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="c85e7-105">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="c85e7-106">将指定的包添加到其中的包 ID 和版本号创建文件夹层次结构布局中的非 HTTP 包源 （文件夹或 UNC 路径）。</span><span class="sxs-lookup"><span data-stu-id="c85e7-106">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="c85e7-107">例如：</span><span class="sxs-lookup"><span data-stu-id="c85e7-107">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="c85e7-108">还原或更新时对包源，则层次结构布局提供显著提高性能。</span><span class="sxs-lookup"><span data-stu-id="c85e7-108">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="c85e7-109">若要对目标包源扩展包中的所有文件，使用`-Expand`切换。</span><span class="sxs-lookup"><span data-stu-id="c85e7-109">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="c85e7-110">这通常会出现在该目标，如其他子文件夹中`tools`和`lib`。</span><span class="sxs-lookup"><span data-stu-id="c85e7-110">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="c85e7-111">用法</span><span class="sxs-lookup"><span data-stu-id="c85e7-111">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="c85e7-112">其中`<packagePath>`到包后，若要添加，路径名和`<sourcePath>`指定包将添加到基于文件夹的包源。</span><span class="sxs-lookup"><span data-stu-id="c85e7-112">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="c85e7-113">不支持 HTTP 源。</span><span class="sxs-lookup"><span data-stu-id="c85e7-113">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="c85e7-114">选项</span><span class="sxs-lookup"><span data-stu-id="c85e7-114">Options</span></span>

| <span data-ttu-id="c85e7-115">选项</span><span class="sxs-lookup"><span data-stu-id="c85e7-115">Option</span></span> | <span data-ttu-id="c85e7-116">描述</span><span class="sxs-lookup"><span data-stu-id="c85e7-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c85e7-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c85e7-117">ConfigFile</span></span> | <span data-ttu-id="c85e7-118">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="c85e7-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c85e7-119">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="c85e7-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c85e7-120">Expand</span><span class="sxs-lookup"><span data-stu-id="c85e7-120">Expand</span></span> | <span data-ttu-id="c85e7-121">将包中的所有文件都添加到包源。</span><span class="sxs-lookup"><span data-stu-id="c85e7-121">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="c85e7-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c85e7-122">ForceEnglishOutput</span></span> | <span data-ttu-id="c85e7-123">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="c85e7-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c85e7-124">帮助</span><span class="sxs-lookup"><span data-stu-id="c85e7-124">Help</span></span> | <span data-ttu-id="c85e7-125">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="c85e7-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="c85e7-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c85e7-126">NonInteractive</span></span> | <span data-ttu-id="c85e7-127">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="c85e7-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c85e7-128">详细级别</span><span class="sxs-lookup"><span data-stu-id="c85e7-128">Verbosity</span></span> | <span data-ttu-id="c85e7-129">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="c85e7-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c85e7-130">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c85e7-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c85e7-131">示例</span><span class="sxs-lookup"><span data-stu-id="c85e7-131">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
