---
title: NuGet CLI 源命令
description: nuget.exe 源命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 73c9cea8200a1ab1937d25a9a611ae7f2a943dba
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622585"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="6c103-103">源命令 (NuGet CLI) </span><span class="sxs-lookup"><span data-stu-id="6c103-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="6c103-104">**适用于：** 包消耗，发布 &bullet; **支持的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="6c103-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="6c103-105">管理位于用户范围配置文件或指定配置文件中的源的列表。</span><span class="sxs-lookup"><span data-stu-id="6c103-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="6c103-106">用户范围配置文件位于 `%appdata%\NuGet\NuGet.Config` (Windows) 和 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="6c103-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="6c103-107">请注意，nuget.org 的源 URL 是 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="6c103-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="6c103-108">使用情况</span><span class="sxs-lookup"><span data-stu-id="6c103-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="6c103-109">其中 `<operation>` 是 *List、Add、Remove、Enable、Disable* 或 *Update*中的一个， `<name>` 是源的名称， `<source>` 是源的 URL。</span><span class="sxs-lookup"><span data-stu-id="6c103-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="6c103-110">一次只能在一个源上操作。</span><span class="sxs-lookup"><span data-stu-id="6c103-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="6c103-111">选项</span><span class="sxs-lookup"><span data-stu-id="6c103-111">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="6c103-112">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="6c103-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6c103-113">如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="6c103-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="6c103-114">\* (3.5 +) \* 使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="6c103-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Format`**

  <span data-ttu-id="6c103-115">适用于 `list` 操作，可以 `Detailed` (默认) 或 `Short` 。</span><span class="sxs-lookup"><span data-stu-id="6c103-115">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span>

- **`-?|-help`**

  <span data-ttu-id="6c103-116">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="6c103-116">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="6c103-117">源的名称。</span><span class="sxs-lookup"><span data-stu-id="6c103-117">Name of the source.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="6c103-118">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="6c103-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Password`**

  <span data-ttu-id="6c103-119">指定用于对源进行身份验证的密码。</span><span class="sxs-lookup"><span data-stu-id="6c103-119">Specifies the password for authenticating with the source.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="6c103-120"> (s) 源的包的路径。</span><span class="sxs-lookup"><span data-stu-id="6c103-120">Path to the package(s) source.</span></span>

- **`-StorePasswordInClearText`**

  <span data-ttu-id="6c103-121">指示以未加密的文本而不是存储加密的窗体的默认行为来存储密码。</span><span class="sxs-lookup"><span data-stu-id="6c103-121">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span>

- **`-UserName`**

  <span data-ttu-id="6c103-122">指定用于对源进行身份验证的用户名。</span><span class="sxs-lookup"><span data-stu-id="6c103-122">Specifies the user name for authenticating with the source.</span></span>

- **`-ValidAuthenticationTypes`**

  <span data-ttu-id="6c103-123">此源的有效身份验证类型的逗号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="6c103-123">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="6c103-124">默认情况下，所有身份验证类型都是有效的。</span><span class="sxs-lookup"><span data-stu-id="6c103-124">By default, all authentication types are valid.</span></span> <span data-ttu-id="6c103-125">示例：`basic,negotiate`。</span><span class="sxs-lookup"><span data-stu-id="6c103-125">Example: `basic,negotiate`.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="6c103-126">指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="6c103-126">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

> [!Note]
> <span data-ttu-id="6c103-127">请确保在与 nuget.exe 稍后用于访问包源的用户上下文中添加源密码。</span><span class="sxs-lookup"><span data-stu-id="6c103-127">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="6c103-128">密码将以加密形式存储在配置文件中，并且只能在对其进行加密的用户上下文中解密。</span><span class="sxs-lookup"><span data-stu-id="6c103-128">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="6c103-129">例如，在使用生成服务器还原 NuGet 包时，必须使用运行生成服务器任务的相同 Windows 用户对密码进行加密。</span><span class="sxs-lookup"><span data-stu-id="6c103-129">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="6c103-130">另请参阅 [环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6c103-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="6c103-131">示例</span><span class="sxs-lookup"><span data-stu-id="6c103-131">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
