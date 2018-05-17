---
title: NuGet CLI 源命令
description: 参考 nuget.exe 源命令
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d588ff09075ad75b76b7dd3645f3cdff29f6f093
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="ee9a3-103">sources 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ee9a3-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="ee9a3-104">**适用于：** 包消耗、 发布&bullet;**受支持的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="ee9a3-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ee9a3-105">管理位于用户作用域配置文件或指定的配置文件的源的列表。</span><span class="sxs-lookup"><span data-stu-id="ee9a3-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="ee9a3-106">用户作用域配置文件位于`%appdata%\NuGet\NuGet.Config`(Windows) 和`~/.nuget/NuGet/NuGet.Config`(Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="ee9a3-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="ee9a3-107">请注意，nuget.org 的源 URL 是 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="ee9a3-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="ee9a3-108">用法</span><span class="sxs-lookup"><span data-stu-id="ee9a3-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="ee9a3-109">其中`<operation>`是之一*列表、 添加、 删除、 启用、 禁用*或*更新*，`<name>`是源，名称和`<source>`是源的 URL。</span><span class="sxs-lookup"><span data-stu-id="ee9a3-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="ee9a3-110">选项</span><span class="sxs-lookup"><span data-stu-id="ee9a3-110">Options</span></span>

| <span data-ttu-id="ee9a3-111">选项</span><span class="sxs-lookup"><span data-stu-id="ee9a3-111">Option</span></span> | <span data-ttu-id="ee9a3-112">描述</span><span class="sxs-lookup"><span data-stu-id="ee9a3-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ee9a3-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ee9a3-113">ConfigFile</span></span> | <span data-ttu-id="ee9a3-114">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="ee9a3-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ee9a3-115">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="ee9a3-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ee9a3-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ee9a3-116">ForceEnglishOutput</span></span> | <span data-ttu-id="ee9a3-117">*（3.5 +)* 强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="ee9a3-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ee9a3-118">格式</span><span class="sxs-lookup"><span data-stu-id="ee9a3-118">Format</span></span> | <span data-ttu-id="ee9a3-119">适用于`list`操作并可以是`Detailed`（默认值） 或`Short`。</span><span class="sxs-lookup"><span data-stu-id="ee9a3-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="ee9a3-120">帮助</span><span class="sxs-lookup"><span data-stu-id="ee9a3-120">Help</span></span> | <span data-ttu-id="ee9a3-121">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="ee9a3-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="ee9a3-122">非交互式</span><span class="sxs-lookup"><span data-stu-id="ee9a3-122">NonInteractive</span></span> | <span data-ttu-id="ee9a3-123">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="ee9a3-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ee9a3-124">Password</span><span class="sxs-lookup"><span data-stu-id="ee9a3-124">Password</span></span> | <span data-ttu-id="ee9a3-125">指定与源进行身份验证的密码。</span><span class="sxs-lookup"><span data-stu-id="ee9a3-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="ee9a3-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="ee9a3-126">StorePasswordInClearText</span></span> | <span data-ttu-id="ee9a3-127">指示要将密码存储在未加密的文本，而不是存储以加密的形式的默认行为。</span><span class="sxs-lookup"><span data-stu-id="ee9a3-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="ee9a3-128">UserName</span><span class="sxs-lookup"><span data-stu-id="ee9a3-128">UserName</span></span> | <span data-ttu-id="ee9a3-129">指定与源进行身份验证的用户名。</span><span class="sxs-lookup"><span data-stu-id="ee9a3-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="ee9a3-130">详细级别</span><span class="sxs-lookup"><span data-stu-id="ee9a3-130">Verbosity</span></span> | <span data-ttu-id="ee9a3-131">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="ee9a3-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="ee9a3-132">请确保添加在相同的用户上下文的源的密码，如 nuget.exe 更高版本用于访问包源。</span><span class="sxs-lookup"><span data-stu-id="ee9a3-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="ee9a3-133">密码将以加密形式存储在配置文件中，因为它已加密仅可以在相同的用户上下文中解密。</span><span class="sxs-lookup"><span data-stu-id="ee9a3-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="ee9a3-134">因此，例如当你使用的生成服务器具有相同的生成服务器任务将在其下运行的 Windows 用户还原 NuGet 程序包必须加密密码。</span><span class="sxs-lookup"><span data-stu-id="ee9a3-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="ee9a3-135">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ee9a3-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ee9a3-136">示例</span><span class="sxs-lookup"><span data-stu-id="ee9a3-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
