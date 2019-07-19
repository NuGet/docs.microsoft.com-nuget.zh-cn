---
title: NuGet CLI setapikey 命令
description: Nuget.exe setapikey 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327604"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="d860d-103">setapikey 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d860d-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="d860d-104">**适用于:** 包消耗, 发布&bullet; **支持的版本:** 全部</span><span class="sxs-lookup"><span data-stu-id="d860d-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d860d-105">将给定服务器 URL 的 API 密钥保存到`NuGet.Config` , 以便不需要为后续命令输入该 URL。</span><span class="sxs-lookup"><span data-stu-id="d860d-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="d860d-106">用法</span><span class="sxs-lookup"><span data-stu-id="d860d-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="d860d-107">其中`<source>`标识服务器, `<key>`是要保存的密钥或密码。</span><span class="sxs-lookup"><span data-stu-id="d860d-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="d860d-108">如果`<source>`省略, 则假定为 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="d860d-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="d860d-109">选项</span><span class="sxs-lookup"><span data-stu-id="d860d-109">Options</span></span>

| <span data-ttu-id="d860d-110">选项</span><span class="sxs-lookup"><span data-stu-id="d860d-110">Option</span></span> | <span data-ttu-id="d860d-111">描述</span><span class="sxs-lookup"><span data-stu-id="d860d-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d860d-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d860d-112">ConfigFile</span></span> | <span data-ttu-id="d860d-113">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="d860d-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d860d-114">如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="d860d-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d860d-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d860d-115">ForceEnglishOutput</span></span> | <span data-ttu-id="d860d-116">*(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="d860d-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d860d-117">Help</span><span class="sxs-lookup"><span data-stu-id="d860d-117">Help</span></span> | <span data-ttu-id="d860d-118">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="d860d-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="d860d-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d860d-119">NonInteractive</span></span> | <span data-ttu-id="d860d-120">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="d860d-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d860d-121">Verbosity</span><span class="sxs-lookup"><span data-stu-id="d860d-121">Verbosity</span></span> | <span data-ttu-id="d860d-122">指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="d860d-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d860d-123">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d860d-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d860d-124">示例</span><span class="sxs-lookup"><span data-stu-id="d860d-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
