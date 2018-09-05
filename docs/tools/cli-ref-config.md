---
title: NuGet CLI config 命令
description: Nuget.exe config 命令参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 376b69186ad22d4d94a1df51146b833a1f6f9bd9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546473"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="63e59-103">配置命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="63e59-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="63e59-104">**适用于：** 所有&bullet;**支持的版本**： 所有</span><span class="sxs-lookup"><span data-stu-id="63e59-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="63e59-105">获取或设置 NuGet 配置值。</span><span class="sxs-lookup"><span data-stu-id="63e59-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="63e59-106">有关其他用法，请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="63e59-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="63e59-107">有关允许的密钥名称的详细信息，请参阅[NuGet 配置文件引用](../reference/nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="63e59-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="63e59-108">用法</span><span class="sxs-lookup"><span data-stu-id="63e59-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="63e59-109">其中`<name>`和`<value>`指定要在配置中设置的键-值对。</span><span class="sxs-lookup"><span data-stu-id="63e59-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="63e59-110">您可以根据需要指定任意多个对。</span><span class="sxs-lookup"><span data-stu-id="63e59-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="63e59-111">若要删除一个值，指定名称和`=`登录而没有值。</span><span class="sxs-lookup"><span data-stu-id="63e59-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="63e59-112">有关允许的密钥名称，请参阅[NuGet 配置文件引用](../reference/nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="63e59-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="63e59-113">在 NuGet 3.4 + 中，`<value>`可以使用[环境变量](cli-ref-environment-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="63e59-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="63e59-114">选项</span><span class="sxs-lookup"><span data-stu-id="63e59-114">Options</span></span>

| <span data-ttu-id="63e59-115">选项</span><span class="sxs-lookup"><span data-stu-id="63e59-115">Option</span></span> | <span data-ttu-id="63e59-116">描述</span><span class="sxs-lookup"><span data-stu-id="63e59-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="63e59-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="63e59-117">AsPath</span></span> | <span data-ttu-id="63e59-118">返回配置值作为路径，忽略时`-Set`使用。</span><span class="sxs-lookup"><span data-stu-id="63e59-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="63e59-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="63e59-119">ConfigFile</span></span> | <span data-ttu-id="63e59-120">要修改的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="63e59-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="63e59-121">如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。</span><span class="sxs-lookup"><span data-stu-id="63e59-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="63e59-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="63e59-122">ForceEnglishOutput</span></span> | <span data-ttu-id="63e59-123">*（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="63e59-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="63e59-124">帮助</span><span class="sxs-lookup"><span data-stu-id="63e59-124">Help</span></span> | <span data-ttu-id="63e59-125">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="63e59-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="63e59-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="63e59-126">NonInteractive</span></span> | <span data-ttu-id="63e59-127">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="63e59-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="63e59-128">详细级别</span><span class="sxs-lookup"><span data-stu-id="63e59-128">Verbosity</span></span> | <span data-ttu-id="63e59-129">指定的输出中显示的详细信息：*正常*，*静默*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="63e59-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="63e59-130">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="63e59-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="63e59-131">示例</span><span class="sxs-lookup"><span data-stu-id="63e59-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
