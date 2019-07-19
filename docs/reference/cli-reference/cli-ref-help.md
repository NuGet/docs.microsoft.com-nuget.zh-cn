---
title: NuGet CLI 帮助命令
description: Nuget.exe help 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327794"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="f1310-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="f1310-103">help or ?</span></span> <span data-ttu-id="f1310-104">命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f1310-104">command (NuGet CLI)</span></span>

<span data-ttu-id="f1310-105">**适用于:** 所有&bullet; **受支持的版本**: 全部</span><span class="sxs-lookup"><span data-stu-id="f1310-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="f1310-106">显示常规帮助信息和有关特定命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="f1310-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="f1310-107">用法</span><span class="sxs-lookup"><span data-stu-id="f1310-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="f1310-108">其中, [命令] 标识要显示其帮助的特定命令。</span><span class="sxs-lookup"><span data-stu-id="f1310-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="f1310-109">对于某些命令, 请注意首先指定*帮助*, `nuget help install`因为在 nuget.org 中有一个名为 "help" 的包。如果你指定了命令`nuget install help`, 则将不会获得有关安装命令的帮助, 但会改为安装名为 help 的程序包。</span><span class="sxs-lookup"><span data-stu-id="f1310-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="f1310-110">选项</span><span class="sxs-lookup"><span data-stu-id="f1310-110">Options</span></span>

| <span data-ttu-id="f1310-111">选项</span><span class="sxs-lookup"><span data-stu-id="f1310-111">Option</span></span> | <span data-ttu-id="f1310-112">描述</span><span class="sxs-lookup"><span data-stu-id="f1310-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f1310-113">全部</span><span class="sxs-lookup"><span data-stu-id="f1310-113">All</span></span> | <span data-ttu-id="f1310-114">打印所有可用命令的详细帮助;如果给定了特定命令, 则忽略。</span><span class="sxs-lookup"><span data-stu-id="f1310-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="f1310-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f1310-115">ConfigFile</span></span> | <span data-ttu-id="f1310-116">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="f1310-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f1310-117">如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="f1310-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f1310-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f1310-118">ForceEnglishOutput</span></span> | <span data-ttu-id="f1310-119">*(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="f1310-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f1310-120">Help</span><span class="sxs-lookup"><span data-stu-id="f1310-120">Help</span></span> | <span data-ttu-id="f1310-121">显示 help 命令本身的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="f1310-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="f1310-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="f1310-122">Markdown</span></span> | <span data-ttu-id="f1310-123">当与`-All`一起使用时, 打印 markdown 格式的详细帮助。</span><span class="sxs-lookup"><span data-stu-id="f1310-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="f1310-124">否则忽略。</span><span class="sxs-lookup"><span data-stu-id="f1310-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="f1310-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f1310-125">NonInteractive</span></span> | <span data-ttu-id="f1310-126">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="f1310-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f1310-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="f1310-127">Verbosity</span></span> | <span data-ttu-id="f1310-128">指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="f1310-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f1310-129">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f1310-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f1310-130">示例</span><span class="sxs-lookup"><span data-stu-id="f1310-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
