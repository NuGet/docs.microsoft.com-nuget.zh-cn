---
title: NuGet CLI 帮助命令
description: Nuget.exe help 命令的引用
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: dbfc803e24c824d30e128d6e86cfa3c43660668f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="2ec1c-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="2ec1c-103">help or ?</span></span> <span data-ttu-id="2ec1c-104">命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2ec1c-104">command (NuGet CLI)</span></span>

<span data-ttu-id="2ec1c-105">**适用于：** 所有&bullet;**受支持的版本**： 所有</span><span class="sxs-lookup"><span data-stu-id="2ec1c-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="2ec1c-106">显示常规帮助信息和帮助有关特定命令的信息。</span><span class="sxs-lookup"><span data-stu-id="2ec1c-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="2ec1c-107">用法</span><span class="sxs-lookup"><span data-stu-id="2ec1c-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="2ec1c-108">其中 [命令] 标识要显示帮助其特定的命令。</span><span class="sxs-lookup"><span data-stu-id="2ec1c-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="2ec1c-109">使用某些命令，请注意指定*帮助*第一，作为家`nuget help install`，因为包 nuget.org 上名为"帮助"。如果你可以用以下命令`nuget install help`，不会获取有关安装命令的帮助，但将改为安装名为帮助的程序包。</span><span class="sxs-lookup"><span data-stu-id="2ec1c-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="2ec1c-110">选项</span><span class="sxs-lookup"><span data-stu-id="2ec1c-110">Options</span></span>

| <span data-ttu-id="2ec1c-111">选项</span><span class="sxs-lookup"><span data-stu-id="2ec1c-111">Option</span></span> | <span data-ttu-id="2ec1c-112">描述</span><span class="sxs-lookup"><span data-stu-id="2ec1c-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2ec1c-113">全部</span><span class="sxs-lookup"><span data-stu-id="2ec1c-113">All</span></span> | <span data-ttu-id="2ec1c-114">获取所有可用的命令; 帮助打印的详细的信息如果将给特定的命令被忽略。</span><span class="sxs-lookup"><span data-stu-id="2ec1c-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="2ec1c-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2ec1c-115">ConfigFile</span></span> | <span data-ttu-id="2ec1c-116">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="2ec1c-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2ec1c-117">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="2ec1c-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2ec1c-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2ec1c-118">ForceEnglishOutput</span></span> | <span data-ttu-id="2ec1c-119">*（3.5 +)* 强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="2ec1c-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2ec1c-120">帮助</span><span class="sxs-lookup"><span data-stu-id="2ec1c-120">Help</span></span> | <span data-ttu-id="2ec1c-121">显示的帮助帮助命令本身的信息。</span><span class="sxs-lookup"><span data-stu-id="2ec1c-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="2ec1c-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="2ec1c-122">Markdown</span></span> | <span data-ttu-id="2ec1c-123">打印 markdown 格式一起使用时的详细的帮助`-All`。</span><span class="sxs-lookup"><span data-stu-id="2ec1c-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="2ec1c-124">否则将忽略。</span><span class="sxs-lookup"><span data-stu-id="2ec1c-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="2ec1c-125">非交互式</span><span class="sxs-lookup"><span data-stu-id="2ec1c-125">NonInteractive</span></span> | <span data-ttu-id="2ec1c-126">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="2ec1c-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2ec1c-127">详细级别</span><span class="sxs-lookup"><span data-stu-id="2ec1c-127">Verbosity</span></span> | <span data-ttu-id="2ec1c-128">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="2ec1c-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2ec1c-129">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2ec1c-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2ec1c-130">示例</span><span class="sxs-lookup"><span data-stu-id="2ec1c-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
