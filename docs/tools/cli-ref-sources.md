---
title: NuGet CLI 源命令
description: Nuget.exe 的参考源命令
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610618"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="88575-103">sources 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="88575-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="88575-104">**适用于：** 包使用、 发布&bullet;**支持的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="88575-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="88575-105">管理用户作用域配置文件或指定的配置文件中的源的列表。</span><span class="sxs-lookup"><span data-stu-id="88575-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="88575-106">用户作用域配置文件位于`%appdata%\NuGet\NuGet.Config`(Windows) 和`~/.nuget/NuGet/NuGet.Config`(Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="88575-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="88575-107">请注意，nuget.org 的源 URL 是 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="88575-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="88575-108">用法</span><span class="sxs-lookup"><span data-stu-id="88575-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="88575-109">其中`<operation>`是之一*列表中，添加、 删除、 启用、 禁用*或*更新*，`<name>`是源的名称和`<source>`是源的 URL。</span><span class="sxs-lookup"><span data-stu-id="88575-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="88575-110">您可以一次操作上只有一个源。</span><span class="sxs-lookup"><span data-stu-id="88575-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="88575-111">选项</span><span class="sxs-lookup"><span data-stu-id="88575-111">Options</span></span>

| <span data-ttu-id="88575-112">选项</span><span class="sxs-lookup"><span data-stu-id="88575-112">Option</span></span> | <span data-ttu-id="88575-113">描述</span><span class="sxs-lookup"><span data-stu-id="88575-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="88575-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="88575-114">ConfigFile</span></span> | <span data-ttu-id="88575-115">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="88575-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="88575-116">如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。</span><span class="sxs-lookup"><span data-stu-id="88575-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="88575-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="88575-117">ForceEnglishOutput</span></span> | <span data-ttu-id="88575-118">*（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="88575-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="88575-119">格式</span><span class="sxs-lookup"><span data-stu-id="88575-119">Format</span></span> | <span data-ttu-id="88575-120">适用于`list`操作可以是`Detailed`（默认值） 或`Short`。</span><span class="sxs-lookup"><span data-stu-id="88575-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="88575-121">Help</span><span class="sxs-lookup"><span data-stu-id="88575-121">Help</span></span> | <span data-ttu-id="88575-122">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="88575-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="88575-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="88575-123">NonInteractive</span></span> | <span data-ttu-id="88575-124">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="88575-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="88575-125">Password</span><span class="sxs-lookup"><span data-stu-id="88575-125">Password</span></span> | <span data-ttu-id="88575-126">指定与源进行身份验证的密码。</span><span class="sxs-lookup"><span data-stu-id="88575-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="88575-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="88575-127">StorePasswordInClearText</span></span> | <span data-ttu-id="88575-128">指示要将密码存储在未加密的文本，而不是存储以加密的形式的默认行为。</span><span class="sxs-lookup"><span data-stu-id="88575-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="88575-129">UserName</span><span class="sxs-lookup"><span data-stu-id="88575-129">UserName</span></span> | <span data-ttu-id="88575-130">指定与源进行身份验证的用户名。</span><span class="sxs-lookup"><span data-stu-id="88575-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="88575-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="88575-131">Verbosity</span></span> | <span data-ttu-id="88575-132">指定的输出中显示的详细信息：*正常*，*静默*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="88575-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="88575-133">请务必添加相同的用户上下文的源的密码，如 nuget.exe 更高版本用于访问包源。</span><span class="sxs-lookup"><span data-stu-id="88575-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="88575-134">密码将以加密形式存储在配置文件中，因为它已加密仅可以在相同的用户上下文解密。</span><span class="sxs-lookup"><span data-stu-id="88575-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="88575-135">因此，例如当您使用的生成服务器具有相同的 Windows 用户，其下运行生成服务器任务会还原 NuGet 包必须加密密码。</span><span class="sxs-lookup"><span data-stu-id="88575-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="88575-136">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="88575-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="88575-137">示例</span><span class="sxs-lookup"><span data-stu-id="88575-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
