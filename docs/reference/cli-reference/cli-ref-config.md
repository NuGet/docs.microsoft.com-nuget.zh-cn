---
title: NuGet CLI config 命令
description: nuget.exe config 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7d0c1c51f40cba9a5b69f209ffbd995451bfeb9f
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622871"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="7defe-103">配置命令 (NuGet CLI) </span><span class="sxs-lookup"><span data-stu-id="7defe-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="7defe-104">**适用于：** 所有 &bullet; **受支持的版本**：全部</span><span class="sxs-lookup"><span data-stu-id="7defe-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="7defe-105">获取或设置 NuGet 配置值。</span><span class="sxs-lookup"><span data-stu-id="7defe-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="7defe-106">有关其他用法，请参阅 [常见 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="7defe-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="7defe-107">有关允许的密钥名称的详细信息，请参阅 [NuGet 配置文件参考](../nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="7defe-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="7defe-108">使用情况</span><span class="sxs-lookup"><span data-stu-id="7defe-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="7defe-109">其中 `<name>` ，并 `<value>` 指定要在配置中设置的键值对。</span><span class="sxs-lookup"><span data-stu-id="7defe-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="7defe-110">您可以根据需要指定任意数量对。</span><span class="sxs-lookup"><span data-stu-id="7defe-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="7defe-111">若要删除值，请指定名称和 `=` 符号但不指定值。</span><span class="sxs-lookup"><span data-stu-id="7defe-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="7defe-112">有关允许的密钥名称，请参阅 [NuGet 配置文件参考](../nuget-config-file.md)。</span><span class="sxs-lookup"><span data-stu-id="7defe-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="7defe-113">在 NuGet 3.4 + 中， `<value>` 可以使用 [环境变量](cli-ref-environment-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="7defe-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="7defe-114">选项</span><span class="sxs-lookup"><span data-stu-id="7defe-114">Options</span></span>


- **`AsPath`**

  <span data-ttu-id="7defe-115">将配置值作为路径返回，使用时将忽略此值 `-Set` 。</span><span class="sxs-lookup"><span data-stu-id="7defe-115">Returns the config value as a path, ignored when `-Set` is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="7defe-116">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="7defe-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7defe-117">如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="7defe-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="7defe-118">\* (3.5 +) \* 使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="7defe-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="7defe-119">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="7defe-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="7defe-120">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="7defe-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-Set`**

  <span data-ttu-id="7defe-121">要在配置中设置的键/值对的一个。</span><span class="sxs-lookup"><span data-stu-id="7defe-121">One on more key-value pairs to be set in config.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="7defe-122">指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="7defe-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="7defe-123">另请参阅 [环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7defe-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="7defe-124">示例</span><span class="sxs-lookup"><span data-stu-id="7defe-124">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
