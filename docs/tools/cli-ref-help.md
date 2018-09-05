---
title: NuGet CLI 帮助命令
description: Nuget.exe help 命令参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546558"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="b901e-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="b901e-103">help or ?</span></span> <span data-ttu-id="b901e-104">命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b901e-104">command (NuGet CLI)</span></span>

<span data-ttu-id="b901e-105">**适用于：** 所有&bullet;**支持的版本**： 所有</span><span class="sxs-lookup"><span data-stu-id="b901e-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="b901e-106">显示常规技术信息和帮助有关特定命令的信息。</span><span class="sxs-lookup"><span data-stu-id="b901e-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="b901e-107">用法</span><span class="sxs-lookup"><span data-stu-id="b901e-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="b901e-108">其中 [command]，标识要为其显示帮助特定的命令。</span><span class="sxs-lookup"><span data-stu-id="b901e-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="b901e-109">某些命令，请注意以指定*帮助*首先，作为与`nuget help install`，因为名为 nuget.org 上的"帮助"的包。如果你向命令提供`nuget install help`，你不会在安装命令上获取帮助，但将改为安装名为帮助的包。</span><span class="sxs-lookup"><span data-stu-id="b901e-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="b901e-110">选项</span><span class="sxs-lookup"><span data-stu-id="b901e-110">Options</span></span>

| <span data-ttu-id="b901e-111">选项</span><span class="sxs-lookup"><span data-stu-id="b901e-111">Option</span></span> | <span data-ttu-id="b901e-112">描述</span><span class="sxs-lookup"><span data-stu-id="b901e-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b901e-113">全部</span><span class="sxs-lookup"><span data-stu-id="b901e-113">All</span></span> | <span data-ttu-id="b901e-114">获取所有可用的命令; 帮助打印的详细的信息提供特定的命令将被忽略。</span><span class="sxs-lookup"><span data-stu-id="b901e-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="b901e-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b901e-115">ConfigFile</span></span> | <span data-ttu-id="b901e-116">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="b901e-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b901e-117">如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。</span><span class="sxs-lookup"><span data-stu-id="b901e-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b901e-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b901e-118">ForceEnglishOutput</span></span> | <span data-ttu-id="b901e-119">*（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="b901e-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b901e-120">帮助</span><span class="sxs-lookup"><span data-stu-id="b901e-120">Help</span></span> | <span data-ttu-id="b901e-121">显示帮助信息用于帮助命令本身。</span><span class="sxs-lookup"><span data-stu-id="b901e-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="b901e-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="b901e-122">Markdown</span></span> | <span data-ttu-id="b901e-123">打印 markdown 格式与一起使用时的详细的帮助`-All`。</span><span class="sxs-lookup"><span data-stu-id="b901e-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="b901e-124">否则将忽略。</span><span class="sxs-lookup"><span data-stu-id="b901e-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="b901e-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b901e-125">NonInteractive</span></span> | <span data-ttu-id="b901e-126">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="b901e-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b901e-127">详细级别</span><span class="sxs-lookup"><span data-stu-id="b901e-127">Verbosity</span></span> | <span data-ttu-id="b901e-128">指定的输出中显示的详细信息：*正常*，*静默*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="b901e-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b901e-129">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b901e-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b901e-130">示例</span><span class="sxs-lookup"><span data-stu-id="b901e-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
