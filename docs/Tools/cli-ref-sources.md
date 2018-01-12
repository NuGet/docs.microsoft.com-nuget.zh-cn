---
title: "NuGet CLI 源命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 997ce736-91ba-4cd2-88c9-b4b168e3130a
description: "参考 nuget.exe 源命令"
keywords: "nuget 源引用，源命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2eca8557840c467a60f5f708efe242cd83609164
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="1fba8-104">源命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1fba8-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="1fba8-105">**适用于：**包消耗、 发布&bullet;**受支持的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="1fba8-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="1fba8-106">管理的源位于列表`%AppData%\NuGet\NuGet.Config`或指定的配置文件。</span><span class="sxs-lookup"><span data-stu-id="1fba8-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

<span data-ttu-id="1fba8-107">请注意，nuget.org 的源 URL 是`https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="1fba8-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="1fba8-108">用法</span><span class="sxs-lookup"><span data-stu-id="1fba8-108">Usage</span></span>

```
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="1fba8-109">其中`<operation>`是之一*列表、 添加、 删除、 启用、 禁用*或*更新*，`<name>`是源，名称和`<source>`是源的 URL。</span><span class="sxs-lookup"><span data-stu-id="1fba8-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="1fba8-110">选项</span><span class="sxs-lookup"><span data-stu-id="1fba8-110">Options</span></span>

| <span data-ttu-id="1fba8-111">选项</span><span class="sxs-lookup"><span data-stu-id="1fba8-111">Option</span></span> | <span data-ttu-id="1fba8-112">描述</span><span class="sxs-lookup"><span data-stu-id="1fba8-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1fba8-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1fba8-113">ConfigFile</span></span> | <span data-ttu-id="1fba8-114">*（2.5 +)* NuGet 要应用的配置文件。</span><span class="sxs-lookup"><span data-stu-id="1fba8-114">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="1fba8-115">如果未指定， *%AppData%\NuGet\NuGet.Config*使用。</span><span class="sxs-lookup"><span data-stu-id="1fba8-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="1fba8-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1fba8-116">ForceEnglishOutput</span></span> | <span data-ttu-id="1fba8-117">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="1fba8-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1fba8-118">格式</span><span class="sxs-lookup"><span data-stu-id="1fba8-118">Format</span></span> | <span data-ttu-id="1fba8-119">适用于`list`操作并可以是`Detailed`（默认值） 或`Short`。</span><span class="sxs-lookup"><span data-stu-id="1fba8-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="1fba8-120">帮助</span><span class="sxs-lookup"><span data-stu-id="1fba8-120">Help</span></span> | <span data-ttu-id="1fba8-121">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="1fba8-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="1fba8-122">非交互式</span><span class="sxs-lookup"><span data-stu-id="1fba8-122">NonInteractive</span></span> | <span data-ttu-id="1fba8-123">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="1fba8-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1fba8-124">Password</span><span class="sxs-lookup"><span data-stu-id="1fba8-124">Password</span></span> | <span data-ttu-id="1fba8-125">指定与源进行身份验证的密码。</span><span class="sxs-lookup"><span data-stu-id="1fba8-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="1fba8-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="1fba8-126">StorePasswordInClearText</span></span> | <span data-ttu-id="1fba8-127">指示要将密码存储在未加密的文本，而不是存储以加密的形式的默认行为。</span><span class="sxs-lookup"><span data-stu-id="1fba8-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="1fba8-128">UserName</span><span class="sxs-lookup"><span data-stu-id="1fba8-128">UserName</span></span> | <span data-ttu-id="1fba8-129">指定与源进行身份验证的用户名。</span><span class="sxs-lookup"><span data-stu-id="1fba8-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="1fba8-130">详细级别</span><span class="sxs-lookup"><span data-stu-id="1fba8-130">Verbosity</span></span> | <span data-ttu-id="1fba8-131">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="1fba8-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

> [!Note]
> <span data-ttu-id="1fba8-132">请确保添加在相同的用户上下文的源的密码，如 nuget.exe 更高版本用于访问包源。</span><span class="sxs-lookup"><span data-stu-id="1fba8-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="1fba8-133">密码将以加密形式存储在配置文件中，因为它已加密仅可以在相同的用户上下文中解密。</span><span class="sxs-lookup"><span data-stu-id="1fba8-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="1fba8-134">因此，例如当你使用的生成服务器具有相同的生成服务器任务将在其下运行的 Windows 用户还原 NuGet 程序包必须加密密码。</span><span class="sxs-lookup"><span data-stu-id="1fba8-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="1fba8-135">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1fba8-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1fba8-136">示例</span><span class="sxs-lookup"><span data-stu-id="1fba8-136">Examples</span></span>

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
