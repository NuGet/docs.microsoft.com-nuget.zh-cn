---
title: NuGet CLI 源命令
description: Nuget.exe 的参考源命令
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7ef856f783c8e11cdb40edb0d1c1458730d87262
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548103"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="9b6f7-103">sources 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="9b6f7-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="9b6f7-104">**适用于：** 包使用、 发布&bullet;**支持的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="9b6f7-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="9b6f7-105">管理用户作用域配置文件或指定的配置文件中的源的列表。</span><span class="sxs-lookup"><span data-stu-id="9b6f7-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="9b6f7-106">用户作用域配置文件位于`%appdata%\NuGet\NuGet.Config`(Windows) 和`~/.nuget/NuGet/NuGet.Config`(Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="9b6f7-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="9b6f7-107">请注意，nuget.org 的源 URL 是 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="9b6f7-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="9b6f7-108">用法</span><span class="sxs-lookup"><span data-stu-id="9b6f7-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="9b6f7-109">其中`<operation>`是之一*列表中，添加、 删除、 启用、 禁用*或*更新*，`<name>`是源的名称和`<source>`是源的 URL。</span><span class="sxs-lookup"><span data-stu-id="9b6f7-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="9b6f7-110">选项</span><span class="sxs-lookup"><span data-stu-id="9b6f7-110">Options</span></span>

| <span data-ttu-id="9b6f7-111">选项</span><span class="sxs-lookup"><span data-stu-id="9b6f7-111">Option</span></span> | <span data-ttu-id="9b6f7-112">描述</span><span class="sxs-lookup"><span data-stu-id="9b6f7-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9b6f7-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="9b6f7-113">ConfigFile</span></span> | <span data-ttu-id="9b6f7-114">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="9b6f7-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9b6f7-115">如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。</span><span class="sxs-lookup"><span data-stu-id="9b6f7-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="9b6f7-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="9b6f7-116">ForceEnglishOutput</span></span> | <span data-ttu-id="9b6f7-117">*（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="9b6f7-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="9b6f7-118">格式</span><span class="sxs-lookup"><span data-stu-id="9b6f7-118">Format</span></span> | <span data-ttu-id="9b6f7-119">适用于`list`操作可以是`Detailed`（默认值） 或`Short`。</span><span class="sxs-lookup"><span data-stu-id="9b6f7-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="9b6f7-120">帮助</span><span class="sxs-lookup"><span data-stu-id="9b6f7-120">Help</span></span> | <span data-ttu-id="9b6f7-121">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="9b6f7-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="9b6f7-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="9b6f7-122">NonInteractive</span></span> | <span data-ttu-id="9b6f7-123">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="9b6f7-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="9b6f7-124">Password</span><span class="sxs-lookup"><span data-stu-id="9b6f7-124">Password</span></span> | <span data-ttu-id="9b6f7-125">指定与源进行身份验证的密码。</span><span class="sxs-lookup"><span data-stu-id="9b6f7-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="9b6f7-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="9b6f7-126">StorePasswordInClearText</span></span> | <span data-ttu-id="9b6f7-127">指示要将密码存储在未加密的文本，而不是存储以加密的形式的默认行为。</span><span class="sxs-lookup"><span data-stu-id="9b6f7-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="9b6f7-128">UserName</span><span class="sxs-lookup"><span data-stu-id="9b6f7-128">UserName</span></span> | <span data-ttu-id="9b6f7-129">指定与源进行身份验证的用户名。</span><span class="sxs-lookup"><span data-stu-id="9b6f7-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="9b6f7-130">详细级别</span><span class="sxs-lookup"><span data-stu-id="9b6f7-130">Verbosity</span></span> | <span data-ttu-id="9b6f7-131">指定的输出中显示的详细信息：*正常*，*静默*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="9b6f7-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="9b6f7-132">请务必添加相同的用户上下文的源的密码，如 nuget.exe 更高版本用于访问包源。</span><span class="sxs-lookup"><span data-stu-id="9b6f7-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="9b6f7-133">密码将以加密形式存储在配置文件中，因为它已加密仅可以在相同的用户上下文解密。</span><span class="sxs-lookup"><span data-stu-id="9b6f7-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="9b6f7-134">因此，例如当您使用的生成服务器具有相同的 Windows 用户，其下运行生成服务器任务会还原 NuGet 包必须加密密码。</span><span class="sxs-lookup"><span data-stu-id="9b6f7-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="9b6f7-135">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9b6f7-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9b6f7-136">示例</span><span class="sxs-lookup"><span data-stu-id="9b6f7-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
