---
title: NuGet CLI 规范命令
description: nuget.exe spec 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17603fa30a75c7906f867c96c5d77f31732eaa59
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622559"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="a72c8-103"> (NuGet CLI 的 spec 命令) </span><span class="sxs-lookup"><span data-stu-id="a72c8-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="a72c8-104">**适用于：** 创建包的 &bullet; **支持版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="a72c8-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a72c8-105">`.nuspec`为新包生成文件。</span><span class="sxs-lookup"><span data-stu-id="a72c8-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="a72c8-106">如果在与项目文件相同的文件夹中运行 (`.csproj` ， `.vbproj` `.fsproj`) `spec` 创建一个标记化 `.nuspec` 文件。</span><span class="sxs-lookup"><span data-stu-id="a72c8-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="a72c8-107">有关其他信息，请参阅 [创建包](../../create-packages/creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="a72c8-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a72c8-108">使用情况</span><span class="sxs-lookup"><span data-stu-id="a72c8-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="a72c8-109">其中 `<packageID>` 是要保存到文件中的可选包标识符 `.nuspec` 。</span><span class="sxs-lookup"><span data-stu-id="a72c8-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="a72c8-110">选项</span><span class="sxs-lookup"><span data-stu-id="a72c8-110">Options</span></span>

- **`-AssemblyPath`**

  <span data-ttu-id="a72c8-111">指定要用于元数据的程序集的路径。</span><span class="sxs-lookup"><span data-stu-id="a72c8-111">Specifies the path to the assembly to use for metadata.</span></span>

- **`-Force`**

  <span data-ttu-id="a72c8-112">覆盖任何现有 `.nuspec` 文件。</span><span class="sxs-lookup"><span data-stu-id="a72c8-112">Overwrites any existing `.nuspec` file.</span></span>


- **`-ForceEnglishOutput`**

  <span data-ttu-id="a72c8-113">\* (3.5 +) \* 使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="a72c8-113">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="a72c8-114">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="a72c8-114">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="a72c8-115">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="a72c8-115">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="a72c8-116">指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="a72c8-116">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="a72c8-117">另请参阅 [环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a72c8-117">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a72c8-118">示例</span><span class="sxs-lookup"><span data-stu-id="a72c8-118">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
