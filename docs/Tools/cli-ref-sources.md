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
ms.openlocfilehash: 52c46dba168e7395d50cb8d8f9775839389e614c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="944a6-104">源命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="944a6-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="944a6-105">**适用于：**包消耗、 发布&bullet;**受支持的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="944a6-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="944a6-106">管理的源位于列表`%AppData%\NuGet\NuGet.Config`或指定的配置文件。</span><span class="sxs-lookup"><span data-stu-id="944a6-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

## <a name="usage"></a><span data-ttu-id="944a6-107">用法</span><span class="sxs-lookup"><span data-stu-id="944a6-107">Usage</span></span>

```
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="944a6-108">其中`<operation>`是之一*列表、 添加、 删除、 启用、 禁用*或*更新*，`<name>`是源，名称和`<source>`是源的 URL。</span><span class="sxs-lookup"><span data-stu-id="944a6-108">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>


## <a name="options"></a><span data-ttu-id="944a6-109">选项</span><span class="sxs-lookup"><span data-stu-id="944a6-109">Options</span></span>

| <span data-ttu-id="944a6-110">选项</span><span class="sxs-lookup"><span data-stu-id="944a6-110">Option</span></span> | <span data-ttu-id="944a6-111">描述</span><span class="sxs-lookup"><span data-stu-id="944a6-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="944a6-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="944a6-112">ConfigFile</span></span> | <span data-ttu-id="944a6-113">*（2.5 +)* NuGet 要应用的配置文件。</span><span class="sxs-lookup"><span data-stu-id="944a6-113">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="944a6-114">如果未指定， *%AppData%\NuGet\NuGet.Config*使用。</span><span class="sxs-lookup"><span data-stu-id="944a6-114">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="944a6-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="944a6-115">ForceEnglishOutput</span></span> | <span data-ttu-id="944a6-116">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="944a6-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="944a6-117">格式</span><span class="sxs-lookup"><span data-stu-id="944a6-117">Format</span></span> | <span data-ttu-id="944a6-118">适用于`list`操作并可以是`Detailed`（默认值） 或`Short`。</span><span class="sxs-lookup"><span data-stu-id="944a6-118">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="944a6-119">帮助</span><span class="sxs-lookup"><span data-stu-id="944a6-119">Help</span></span> | <span data-ttu-id="944a6-120">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="944a6-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="944a6-121">非交互式</span><span class="sxs-lookup"><span data-stu-id="944a6-121">NonInteractive</span></span> | <span data-ttu-id="944a6-122">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="944a6-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="944a6-123">Password</span><span class="sxs-lookup"><span data-stu-id="944a6-123">Password</span></span> | <span data-ttu-id="944a6-124">指定与源进行身份验证的密码。</span><span class="sxs-lookup"><span data-stu-id="944a6-124">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="944a6-125">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="944a6-125">StorePasswordInClearText</span></span> | <span data-ttu-id="944a6-126">指示要将密码存储在未加密的文本，而不是存储以加密的形式的默认行为。</span><span class="sxs-lookup"><span data-stu-id="944a6-126">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="944a6-127">UserName</span><span class="sxs-lookup"><span data-stu-id="944a6-127">UserName</span></span> | <span data-ttu-id="944a6-128">指定与源进行身份验证的用户名。</span><span class="sxs-lookup"><span data-stu-id="944a6-128">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="944a6-129">详细级别</span><span class="sxs-lookup"><span data-stu-id="944a6-129">Verbosity</span></span> | <span data-ttu-id="944a6-130">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="944a6-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

> [!Note]
> <span data-ttu-id="944a6-131">请确保添加在相同的用户上下文的源的密码，如 nuget.exe 更高版本用于访问包源。</span><span class="sxs-lookup"><span data-stu-id="944a6-131">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="944a6-132">密码将以加密形式存储在配置文件中，因为它已加密仅可以在相同的用户上下文中解密。</span><span class="sxs-lookup"><span data-stu-id="944a6-132">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="944a6-133">因此，例如当你使用的生成服务器具有相同的生成服务器任务将在其下运行的 Windows 用户还原 NuGet 程序包必须加密密码。</span><span class="sxs-lookup"><span data-stu-id="944a6-133">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="944a6-134">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="944a6-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="944a6-135">示例</span><span class="sxs-lookup"><span data-stu-id="944a6-135">Examples</span></span>

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
