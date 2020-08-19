---
title: NuGet CLI 初始化命令
description: nuget.exe init 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3b830d678a473c917b70bd46900bdb0206d3652e
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623079"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="02a77-103">init 命令 (NuGet CLI) </span><span class="sxs-lookup"><span data-stu-id="02a77-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="02a77-104">**适用于：** 创建包的 &bullet; **支持版本：** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="02a77-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="02a77-105">使用 " [添加" 命令](cli-ref-add.md)所述的分层布局，将平面文件夹中的所有包复制到目标文件夹。</span><span class="sxs-lookup"><span data-stu-id="02a77-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="02a77-106">也就是说，使用 `init` 等效于对 `add` 文件夹中的每个包使用命令。</span><span class="sxs-lookup"><span data-stu-id="02a77-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="02a77-107">对于 `add` ，目标必须是本地文件夹或 UNC 路径;不支持 HTTP 包存储库，如 nuget.org 或专用服务器。</span><span class="sxs-lookup"><span data-stu-id="02a77-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="02a77-108">使用情况</span><span class="sxs-lookup"><span data-stu-id="02a77-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="02a77-109">其中 `<source>` ，是包含包的文件夹， `<destination>` 是要将包复制到的本地文件夹或 UNC 路径名。</span><span class="sxs-lookup"><span data-stu-id="02a77-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="02a77-110">选项</span><span class="sxs-lookup"><span data-stu-id="02a77-110">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="02a77-111">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="02a77-111">The NuGet configuration file to apply.</span></span> <span data-ttu-id="02a77-112">如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="02a77-112">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="02a77-113">添加添加到包源的每个包中的所有文件;与 `-Expand` `add` 命令相同。</span><span class="sxs-lookup"><span data-stu-id="02a77-113">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="02a77-114">\* (3.5 +) \* 使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="02a77-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="02a77-115">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="02a77-115">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="02a77-116">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="02a77-116">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="02a77-117">指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="02a77-117">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="02a77-118">另请参阅 [环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="02a77-118">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="02a77-119">示例</span><span class="sxs-lookup"><span data-stu-id="02a77-119">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
