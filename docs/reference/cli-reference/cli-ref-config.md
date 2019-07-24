---
title: NuGet CLI config 命令
description: 针对 nuget.exe config 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 384e708187a747221de103720cc51af07acf713e
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433321"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="626c1-103">config 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="626c1-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="626c1-104">**适用于:** 所有&bullet; **受支持的版本**: 全部</span><span class="sxs-lookup"><span data-stu-id="626c1-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="626c1-105">获取或设置 NuGet 配置值。</span><span class="sxs-lookup"><span data-stu-id="626c1-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="626c1-106">有关其他用法, 请参阅[常见 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="626c1-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="626c1-107">有关允许的密钥名称的详细信息, 请参阅[NuGet 配置文件参考](../nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="626c1-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="626c1-108">用法</span><span class="sxs-lookup"><span data-stu-id="626c1-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="626c1-109">其中`<name>` , `<value>`并指定要在配置中设置的键值对。</span><span class="sxs-lookup"><span data-stu-id="626c1-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="626c1-110">您可以根据需要指定任意数量对。</span><span class="sxs-lookup"><span data-stu-id="626c1-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="626c1-111">若要删除值, 请指定名称和`=`符号但不指定值。</span><span class="sxs-lookup"><span data-stu-id="626c1-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="626c1-112">有关允许的密钥名称, 请参阅[NuGet 配置文件参考](../nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="626c1-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="626c1-113">在 NuGet 3.4 + 中`<value>` , 可以使用[环境变量](cli-ref-environment-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="626c1-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="626c1-114">选项</span><span class="sxs-lookup"><span data-stu-id="626c1-114">Options</span></span>

| <span data-ttu-id="626c1-115">选项</span><span class="sxs-lookup"><span data-stu-id="626c1-115">Option</span></span> | <span data-ttu-id="626c1-116">描述</span><span class="sxs-lookup"><span data-stu-id="626c1-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="626c1-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="626c1-117">AsPath</span></span> | <span data-ttu-id="626c1-118">将配置值作为路径返回, 使用时`-Set`将忽略此值。</span><span class="sxs-lookup"><span data-stu-id="626c1-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="626c1-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="626c1-119">ConfigFile</span></span> | <span data-ttu-id="626c1-120">要修改的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="626c1-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="626c1-121">如果未指定, 则使用默认文件-`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.config/NuGet/NuGet.Config` (Mac/Linux) 或`~/.nuget/NuGet/NuGet.Config` (因 OS 分发而异)。</span><span class="sxs-lookup"><span data-stu-id="626c1-121">If not specified, the default file is used -`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.config/NuGet/NuGet.Config`  (Mac/Linux) or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution).</span></span>|
| <span data-ttu-id="626c1-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="626c1-122">ForceEnglishOutput</span></span> | <span data-ttu-id="626c1-123">*(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="626c1-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="626c1-124">Help</span><span class="sxs-lookup"><span data-stu-id="626c1-124">Help</span></span> | <span data-ttu-id="626c1-125">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="626c1-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="626c1-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="626c1-126">NonInteractive</span></span> | <span data-ttu-id="626c1-127">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="626c1-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="626c1-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="626c1-128">Verbosity</span></span> | <span data-ttu-id="626c1-129">指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="626c1-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="626c1-130">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="626c1-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="626c1-131">示例</span><span class="sxs-lookup"><span data-stu-id="626c1-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
