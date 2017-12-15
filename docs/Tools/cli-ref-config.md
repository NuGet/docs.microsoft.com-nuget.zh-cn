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
ms.openlocfilehash: 12a8b51dd11b9bc3a496e02e869cdeb95e67b9e3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="e8665-104">config 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e8665-104">config command (NuGet CLI)</span></span>

<span data-ttu-id="e8665-105">**适用于：**所有&bullet;**受支持的版本**： 所有</span><span class="sxs-lookup"><span data-stu-id="e8665-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="e8665-106">获取或设置 NuGet 配置值。</span><span class="sxs-lookup"><span data-stu-id="e8665-106">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="e8665-107">对于其他用法，请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="e8665-107">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="e8665-108">有关允许的密钥名称的详细信息，请参阅[NuGet 配置文件引用](../Schema/nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="e8665-108">For details on allowable key names, refer to the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="e8665-109">用法</span><span class="sxs-lookup"><span data-stu-id="e8665-109">Usage</span></span>

```
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="e8665-110">其中`<name>`和`<value>`指定在配置中设置的键 / 值对。</span><span class="sxs-lookup"><span data-stu-id="e8665-110">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="e8665-111">根据需要，可以指定任意数量的对。</span><span class="sxs-lookup"><span data-stu-id="e8665-111">You can specify as many pairs as desired.</span></span> <span data-ttu-id="e8665-112">若要删除一个值，指定的名称和`=`登录，但没有值。</span><span class="sxs-lookup"><span data-stu-id="e8665-112">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="e8665-113">在 NuGet 3.4 +`<value>`可以使用[环境变量](cli-ref-environment-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="e8665-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="e8665-114">选项</span><span class="sxs-lookup"><span data-stu-id="e8665-114">Options</span></span>

| <span data-ttu-id="e8665-115">选项</span><span class="sxs-lookup"><span data-stu-id="e8665-115">Option</span></span> | <span data-ttu-id="e8665-116">描述</span><span class="sxs-lookup"><span data-stu-id="e8665-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e8665-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="e8665-117">AsPath</span></span> | <span data-ttu-id="e8665-118">返回配置值为路径，忽略时`-Set`使用。</span><span class="sxs-lookup"><span data-stu-id="e8665-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="e8665-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e8665-119">ConfigFile</span></span> | <span data-ttu-id="e8665-120">*（2.5 +)* NuGet 要修改的配置文件。</span><span class="sxs-lookup"><span data-stu-id="e8665-120">*(2.5+)* The NuGet configuration file to modify.</span></span> <span data-ttu-id="e8665-121">如果未指定， *%AppData%\NuGet\NuGet.Config*使用。</span><span class="sxs-lookup"><span data-stu-id="e8665-121">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="e8665-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e8665-122">ForceEnglishOutput</span></span> | <span data-ttu-id="e8665-123">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="e8665-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e8665-124">帮助</span><span class="sxs-lookup"><span data-stu-id="e8665-124">Help</span></span> | <span data-ttu-id="e8665-125">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="e8665-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="e8665-126">非交互式</span><span class="sxs-lookup"><span data-stu-id="e8665-126">NonInteractive</span></span> | <span data-ttu-id="e8665-127">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="e8665-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e8665-128">详细级别</span><span class="sxs-lookup"><span data-stu-id="e8665-128">Verbosity</span></span> | <span data-ttu-id="e8665-129">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="e8665-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="e8665-130">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e8665-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="e8665-131">示例</span><span class="sxs-lookup"><span data-stu-id="e8665-131">Examples</span></span>

```
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
