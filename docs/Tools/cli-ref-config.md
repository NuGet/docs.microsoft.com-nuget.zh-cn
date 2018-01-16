---
title: "NuGet CLI config 命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a50295ff-8be9-47d9-a260-822e899334cb
description: "Nuget.exe config 命令参考"
keywords: "nuget 配置引用，config 命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f49751d9747687177e3b6c1890ee9d2919be8d0e
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="9c0bd-104">config 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="9c0bd-104">config command (NuGet CLI)</span></span>

<span data-ttu-id="9c0bd-105">**适用于：**所有&bullet;**受支持的版本**： 所有</span><span class="sxs-lookup"><span data-stu-id="9c0bd-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="9c0bd-106">获取或设置 NuGet 配置值。</span><span class="sxs-lookup"><span data-stu-id="9c0bd-106">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="9c0bd-107">对于其他用法，请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="9c0bd-107">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="9c0bd-108">有关允许的密钥名称的详细信息，请参阅[NuGet 配置文件引用](../Schema/nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="9c0bd-108">For details on allowable key names, refer to the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="9c0bd-109">用法</span><span class="sxs-lookup"><span data-stu-id="9c0bd-109">Usage</span></span>

```
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="9c0bd-110">其中`<name>`和`<value>`指定在配置中设置的键 / 值对。</span><span class="sxs-lookup"><span data-stu-id="9c0bd-110">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="9c0bd-111">根据需要，可以指定任意数量的对。</span><span class="sxs-lookup"><span data-stu-id="9c0bd-111">You can specify as many pairs as desired.</span></span> <span data-ttu-id="9c0bd-112">若要删除一个值，指定的名称和`=`登录，但没有值。</span><span class="sxs-lookup"><span data-stu-id="9c0bd-112">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="9c0bd-113">有关允许的密钥名称，请参阅[NuGet 配置文件引用](../Schema/nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="9c0bd-113">For allowable key names, see the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

<span data-ttu-id="9c0bd-114">在 NuGet 3.4 +`<value>`可以使用[环境变量](cli-ref-environment-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="9c0bd-114">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="9c0bd-115">选项</span><span class="sxs-lookup"><span data-stu-id="9c0bd-115">Options</span></span>

| <span data-ttu-id="9c0bd-116">选项</span><span class="sxs-lookup"><span data-stu-id="9c0bd-116">Option</span></span> | <span data-ttu-id="9c0bd-117">描述</span><span class="sxs-lookup"><span data-stu-id="9c0bd-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9c0bd-118">AsPath</span><span class="sxs-lookup"><span data-stu-id="9c0bd-118">AsPath</span></span> | <span data-ttu-id="9c0bd-119">返回配置值为路径，忽略时`-Set`使用。</span><span class="sxs-lookup"><span data-stu-id="9c0bd-119">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="9c0bd-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="9c0bd-120">ConfigFile</span></span> | <span data-ttu-id="9c0bd-121">*（2.5 +)* NuGet 要修改的配置文件。</span><span class="sxs-lookup"><span data-stu-id="9c0bd-121">*(2.5+)* The NuGet configuration file to modify.</span></span> <span data-ttu-id="9c0bd-122">如果未指定， *%AppData%\NuGet\NuGet.Config*使用。</span><span class="sxs-lookup"><span data-stu-id="9c0bd-122">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="9c0bd-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="9c0bd-123">ForceEnglishOutput</span></span> | <span data-ttu-id="9c0bd-124">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="9c0bd-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="9c0bd-125">帮助</span><span class="sxs-lookup"><span data-stu-id="9c0bd-125">Help</span></span> | <span data-ttu-id="9c0bd-126">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="9c0bd-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="9c0bd-127">非交互式</span><span class="sxs-lookup"><span data-stu-id="9c0bd-127">NonInteractive</span></span> | <span data-ttu-id="9c0bd-128">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="9c0bd-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="9c0bd-129">详细级别</span><span class="sxs-lookup"><span data-stu-id="9c0bd-129">Verbosity</span></span> | <span data-ttu-id="9c0bd-130">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="9c0bd-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="9c0bd-131">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9c0bd-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="9c0bd-132">示例</span><span class="sxs-lookup"><span data-stu-id="9c0bd-132">Examples</span></span>

```
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
