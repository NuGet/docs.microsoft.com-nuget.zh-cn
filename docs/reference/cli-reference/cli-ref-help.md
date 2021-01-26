---
title: NuGet CLI 帮助命令
description: nuget.exe help 命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5d91638c4a6f167ea8a04e5dfa2905cb55084ddd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779357"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="af0e3-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="af0e3-103">help or ?</span></span> <span data-ttu-id="af0e3-104"> (NuGet CLI) 的命令</span><span class="sxs-lookup"><span data-stu-id="af0e3-104">command (NuGet CLI)</span></span>

<span data-ttu-id="af0e3-105">**适用于：** 所有 &bullet; **受支持的版本**：全部</span><span class="sxs-lookup"><span data-stu-id="af0e3-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="af0e3-106">显示常规帮助信息和有关特定命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="af0e3-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="af0e3-107">使用情况</span><span class="sxs-lookup"><span data-stu-id="af0e3-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="af0e3-108">其中，[命令] 标识要显示其帮助的特定命令。</span><span class="sxs-lookup"><span data-stu-id="af0e3-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="af0e3-109">对于某些命令，请注意首先指定 *帮助* ， `nuget help install` 因为在 nuget.org 中有一个名为 "help" 的包。如果你指定了命令 `nuget install help` ，则将不会获得有关安装命令的帮助，但会改为安装名为 help 的程序包。</span><span class="sxs-lookup"><span data-stu-id="af0e3-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="af0e3-110">选项</span><span class="sxs-lookup"><span data-stu-id="af0e3-110">Options</span></span>

- **`-All`**

  <span data-ttu-id="af0e3-111">打印所有可用命令的详细帮助;如果给定了特定命令，则忽略。</span><span class="sxs-lookup"><span data-stu-id="af0e3-111">Print detailed help for all available commands; ignored if a specific command is given.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="af0e3-112">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="af0e3-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="af0e3-113">如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="af0e3-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="af0e3-114">*(3.5 +)* 使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="af0e3-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="af0e3-115">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="af0e3-115">Displays help information for the command.</span></span>

- **`-Markdown`**

  <span data-ttu-id="af0e3-116">当与一起使用时，打印 markdown 格式的详细帮助 `-All` 。</span><span class="sxs-lookup"><span data-stu-id="af0e3-116">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="af0e3-117">否则忽略。</span><span class="sxs-lookup"><span data-stu-id="af0e3-117">Ignored otherwise.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="af0e3-118">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="af0e3-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="af0e3-119">指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="af0e3-119">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="af0e3-120">另请参阅 [环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="af0e3-120">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="af0e3-121">示例</span><span class="sxs-lookup"><span data-stu-id="af0e3-121">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
