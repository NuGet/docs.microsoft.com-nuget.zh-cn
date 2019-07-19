---
title: NuGet CLI 源命令
description: 针对 nuget.exe 源命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327594"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="0abba-103">sources 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="0abba-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="0abba-104">**适用于:** 包消耗, 发布&bullet; **支持的版本:** 全部</span><span class="sxs-lookup"><span data-stu-id="0abba-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="0abba-105">管理位于用户范围配置文件或指定配置文件中的源的列表。</span><span class="sxs-lookup"><span data-stu-id="0abba-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="0abba-106">用户范围配置文件位于`%appdata%\NuGet\NuGet.Config` (Windows) 和`~/.nuget/NuGet/NuGet.Config` (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="0abba-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="0abba-107">请注意，nuget.org 的源 URL 是 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="0abba-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="0abba-108">用法</span><span class="sxs-lookup"><span data-stu-id="0abba-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="0abba-109">其中`<operation>`是*List、Add、Remove、Enable、Disable*或*Update* `<name>`中的一个, 是源的名称, `<source>`是源的 URL。</span><span class="sxs-lookup"><span data-stu-id="0abba-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="0abba-110">一次只能在一个源上操作。</span><span class="sxs-lookup"><span data-stu-id="0abba-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="0abba-111">选项</span><span class="sxs-lookup"><span data-stu-id="0abba-111">Options</span></span>

| <span data-ttu-id="0abba-112">选项</span><span class="sxs-lookup"><span data-stu-id="0abba-112">Option</span></span> | <span data-ttu-id="0abba-113">描述</span><span class="sxs-lookup"><span data-stu-id="0abba-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0abba-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="0abba-114">ConfigFile</span></span> | <span data-ttu-id="0abba-115">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="0abba-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="0abba-116">如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="0abba-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="0abba-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="0abba-117">ForceEnglishOutput</span></span> | <span data-ttu-id="0abba-118">*(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="0abba-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="0abba-119">格式</span><span class="sxs-lookup"><span data-stu-id="0abba-119">Format</span></span> | <span data-ttu-id="0abba-120">适用于`Detailed` `Short`操作, 可以为 (默认值) 或。 `list`</span><span class="sxs-lookup"><span data-stu-id="0abba-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="0abba-121">Help</span><span class="sxs-lookup"><span data-stu-id="0abba-121">Help</span></span> | <span data-ttu-id="0abba-122">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="0abba-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="0abba-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="0abba-123">NonInteractive</span></span> | <span data-ttu-id="0abba-124">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="0abba-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="0abba-125">Password</span><span class="sxs-lookup"><span data-stu-id="0abba-125">Password</span></span> | <span data-ttu-id="0abba-126">指定用于对源进行身份验证的密码。</span><span class="sxs-lookup"><span data-stu-id="0abba-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="0abba-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="0abba-127">StorePasswordInClearText</span></span> | <span data-ttu-id="0abba-128">指示以未加密的文本而不是存储加密的窗体的默认行为来存储密码。</span><span class="sxs-lookup"><span data-stu-id="0abba-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="0abba-129">UserName</span><span class="sxs-lookup"><span data-stu-id="0abba-129">UserName</span></span> | <span data-ttu-id="0abba-130">指定用于对源进行身份验证的用户名。</span><span class="sxs-lookup"><span data-stu-id="0abba-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="0abba-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="0abba-131">Verbosity</span></span> | <span data-ttu-id="0abba-132">指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="0abba-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="0abba-133">请确保在与 nuget.exe 一起用于访问包源的用户上下文中添加源密码。</span><span class="sxs-lookup"><span data-stu-id="0abba-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="0abba-134">密码将以加密形式存储在配置文件中, 并且只能在对其进行加密的用户上下文中解密。</span><span class="sxs-lookup"><span data-stu-id="0abba-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="0abba-135">例如, 在使用生成服务器还原 NuGet 包时, 必须使用运行生成服务器任务的相同 Windows 用户对密码进行加密。</span><span class="sxs-lookup"><span data-stu-id="0abba-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="0abba-136">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0abba-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0abba-137">示例</span><span class="sxs-lookup"><span data-stu-id="0abba-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
