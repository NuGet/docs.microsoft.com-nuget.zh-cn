---
title: "NuGet CLI help 命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe help 命令的引用"
keywords: "nuget 帮助参考，帮助命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 97f72e1be0df6e97f8b06696b2b3861800e4ea08
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="3f62f-104">帮助或？</span><span class="sxs-lookup"><span data-stu-id="3f62f-104">help or ?</span></span> <span data-ttu-id="3f62f-105">命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3f62f-105">command (NuGet CLI)</span></span>

<span data-ttu-id="3f62f-106">**适用于：**所有&bullet;**受支持的版本**： 所有</span><span class="sxs-lookup"><span data-stu-id="3f62f-106">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="3f62f-107">显示常规帮助信息和帮助有关特定命令的信息。</span><span class="sxs-lookup"><span data-stu-id="3f62f-107">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="3f62f-108">用法</span><span class="sxs-lookup"><span data-stu-id="3f62f-108">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="3f62f-109">其中 [命令] 标识要显示帮助其特定的命令。</span><span class="sxs-lookup"><span data-stu-id="3f62f-109">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="3f62f-110">使用某些命令，请注意指定*帮助*第一，作为家`nuget help install`，因为包 nuget.org 上名为"帮助"。如果你可以用以下命令`nuget install help`，你将安装命令获取帮助，但将改为安装名为帮助的程序包。</span><span class="sxs-lookup"><span data-stu-id="3f62f-110">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you'll not get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="3f62f-111">选项</span><span class="sxs-lookup"><span data-stu-id="3f62f-111">Options</span></span>

| <span data-ttu-id="3f62f-112">选项</span><span class="sxs-lookup"><span data-stu-id="3f62f-112">Option</span></span> | <span data-ttu-id="3f62f-113">描述</span><span class="sxs-lookup"><span data-stu-id="3f62f-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3f62f-114">全部</span><span class="sxs-lookup"><span data-stu-id="3f62f-114">All</span></span> | <span data-ttu-id="3f62f-115">获取所有可用的命令; 帮助打印的详细的信息如果将给特定的命令被忽略。</span><span class="sxs-lookup"><span data-stu-id="3f62f-115">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="3f62f-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3f62f-116">ConfigFile</span></span> | <span data-ttu-id="3f62f-117">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="3f62f-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3f62f-118">如果未指定， *%AppData%\NuGet\NuGet.Config*使用。</span><span class="sxs-lookup"><span data-stu-id="3f62f-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="3f62f-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3f62f-119">ForceEnglishOutput</span></span> | <span data-ttu-id="3f62f-120">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="3f62f-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3f62f-121">帮助</span><span class="sxs-lookup"><span data-stu-id="3f62f-121">Help</span></span> | <span data-ttu-id="3f62f-122">显示的帮助帮助命令本身的信息。</span><span class="sxs-lookup"><span data-stu-id="3f62f-122">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="3f62f-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="3f62f-123">Markdown</span></span> | <span data-ttu-id="3f62f-124">打印 markdown 格式一起使用时的详细的帮助`-All`。</span><span class="sxs-lookup"><span data-stu-id="3f62f-124">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="3f62f-125">否则将忽略。</span><span class="sxs-lookup"><span data-stu-id="3f62f-125">Ignored otherwise.</span></span> |
| <span data-ttu-id="3f62f-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="3f62f-126">NonInteractive</span></span> | <span data-ttu-id="3f62f-127">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="3f62f-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3f62f-128">详细级别</span><span class="sxs-lookup"><span data-stu-id="3f62f-128">Verbosity</span></span> | <span data-ttu-id="3f62f-129">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="3f62f-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3f62f-130">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3f62f-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3f62f-131">示例</span><span class="sxs-lookup"><span data-stu-id="3f62f-131">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
