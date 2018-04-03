---
title: 使用 dotnet CLI 创建和发布 NuGet 包 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/24/2018
ms.topic: quickstart
ms.prod: nuget
ms.technology: ''
description: 使用 .NET Core CLI dotnet 创建和发布 NuGet 包的演练教程。
keywords: NuGet 包创建, NuGet 包发布, NuGet 教程, dotnet 发布 NuGet 包
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 536e39ae64649ca1c11afa95c20872515e9e4c83
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="1d2b6-104">创建和发布包</span><span class="sxs-lookup"><span data-stu-id="1d2b6-104">Create and publish a package</span></span>

<span data-ttu-id="1d2b6-105">从 .NET 类库创建 NuGet 包并使用 `dotnet` 命令行接口 (CLI) 将其发布到 nuget.org 是很简单的过程。</span><span class="sxs-lookup"><span data-stu-id="1d2b6-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d2b6-106">系统必备</span><span class="sxs-lookup"><span data-stu-id="1d2b6-106">Prerequisites</span></span>

1. <span data-ttu-id="1d2b6-107">安装包括 `dotnet` CLI 的 [.NET Core SDK](https://www.microsoft.com/net/download/)。</span><span class="sxs-lookup"><span data-stu-id="1d2b6-107">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span>

1. <span data-ttu-id="1d2b6-108">如果你还没有帐户，请[在 nuget.org 上注册一个免费帐户](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)。</span><span class="sxs-lookup"><span data-stu-id="1d2b6-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="1d2b6-109">创建新帐户会发送确认电子邮件。</span><span class="sxs-lookup"><span data-stu-id="1d2b6-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="1d2b6-110">必须先确认该帐户，才能上传包。</span><span class="sxs-lookup"><span data-stu-id="1d2b6-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="1d2b6-111">创建类库项目</span><span class="sxs-lookup"><span data-stu-id="1d2b6-111">Create a class library project</span></span>

<span data-ttu-id="1d2b6-112">你可以使用现有的 .NET 类库项目用于要打包的代码，或者创建一个简单的项目，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1d2b6-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="1d2b6-113">创建一个名为 `AppLogger` 的文件夹并更改到其中。</span><span class="sxs-lookup"><span data-stu-id="1d2b6-113">Create a folder called `AppLogger` and change into it.</span></span>

1. <span data-ttu-id="1d2b6-114">创建使用 `dotnet new classlib` 的项目，它使用项目当前文件夹的名称。</span><span class="sxs-lookup"><span data-stu-id="1d2b6-114">Create the project using `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="1d2b6-115">将包元数据添加到项目文件</span><span class="sxs-lookup"><span data-stu-id="1d2b6-115">Add package metadata to the project file</span></span>

<span data-ttu-id="1d2b6-116">每个 NuGet 包都需要一个清单，用以描述包的内容和依赖项。</span><span class="sxs-lookup"><span data-stu-id="1d2b6-116">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="1d2b6-117">在最终包中，清单是基于项目文件中包含的 NuGet 元数据属性生成的 `.nuspec` 文件。</span><span class="sxs-lookup"><span data-stu-id="1d2b6-117">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="1d2b6-118">打开项目文件 (`.csproj`)，并在退出的 `<PropertyGroup>` 标记内添加以下最小属性，并根据需要更改值：</span><span class="sxs-lookup"><span data-stu-id="1d2b6-118">Open your project file (`.csproj`) and add the following minimal properties inside the exiting `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="1d2b6-119">为包提供一个在 nuget.org 中唯一或你使用的任何主机的标识符。</span><span class="sxs-lookup"><span data-stu-id="1d2b6-119">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="1d2b6-120">对于本次演练，我们建议在名称中包含“Sample”或“Test”，因为稍后的发布步骤确实会使该包公开显示（尽管实际上不太可能有人会使用它）。</span><span class="sxs-lookup"><span data-stu-id="1d2b6-120">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="1d2b6-121">添加 [NuGet 元数据属性](/dotnet/core/tools/csproj#nuget-metadata-properties)中描述的任何可选属性。</span><span class="sxs-lookup"><span data-stu-id="1d2b6-121">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="1d2b6-122">对于面向公共使用而生成的包，请特别注意 **PackageTags** 属性，因为这些标记可帮助其他人查找包并了解其用途。</span><span class="sxs-lookup"><span data-stu-id="1d2b6-122">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="1d2b6-123">运行 pack 命令</span><span class="sxs-lookup"><span data-stu-id="1d2b6-123">Run the pack command</span></span>

<span data-ttu-id="1d2b6-124">若要从项目中生成 NuGet 包（`.nupkg` 文件），运行 `dotnet pack` 命令，它也会自动生成项目：</span><span class="sxs-lookup"><span data-stu-id="1d2b6-124">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="1d2b6-125">输出显示 `.nupkg` 文件的路径：</span><span class="sxs-lookup"><span data-stu-id="1d2b6-125">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="1d2b6-126">在生成期间自动生成包</span><span class="sxs-lookup"><span data-stu-id="1d2b6-126">Automatically generate package on build</span></span>

<span data-ttu-id="1d2b6-127">若要在运行 `dotnet build` 时自动运行 `dotnet pack`，请将以下行添加到 `<PropertyGroup>` 中的项目文件内：</span><span class="sxs-lookup"><span data-stu-id="1d2b6-127">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="1d2b6-128">发布包</span><span class="sxs-lookup"><span data-stu-id="1d2b6-128">Publish the package</span></span>

<span data-ttu-id="1d2b6-129">有了 `.nupkg` 文件后，可以使用 `dotnet nuget push` 命令以及从 nuget.org 获取的 API 密钥将其发布到 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="1d2b6-129">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="1d2b6-130">获取 API 密钥</span><span class="sxs-lookup"><span data-stu-id="1d2b6-130">Acquire your API key</span></span>

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="1d2b6-131">用 dotnet nuget push 发布</span><span class="sxs-lookup"><span data-stu-id="1d2b6-131">Publish with dotnet nuget push</span></span>

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="1d2b6-132">发布错误</span><span class="sxs-lookup"><span data-stu-id="1d2b6-132">Publish errors</span></span>

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="1d2b6-133">管理已发布的包</span><span class="sxs-lookup"><span data-stu-id="1d2b6-133">Manage the published package</span></span>

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="1d2b6-134">相关主题</span><span class="sxs-lookup"><span data-stu-id="1d2b6-134">Related topics</span></span>

- [<span data-ttu-id="1d2b6-135">创建包</span><span class="sxs-lookup"><span data-stu-id="1d2b6-135">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="1d2b6-136">发布包</span><span class="sxs-lookup"><span data-stu-id="1d2b6-136">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="1d2b6-137">支持多个目标框架</span><span class="sxs-lookup"><span data-stu-id="1d2b6-137">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="1d2b6-138">包版本控制</span><span class="sxs-lookup"><span data-stu-id="1d2b6-138">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="1d2b6-139">创建本地化包</span><span class="sxs-lookup"><span data-stu-id="1d2b6-139">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="1d2b6-140">给包签名</span><span class="sxs-lookup"><span data-stu-id="1d2b6-140">Signing packages</span></span>](../create-packages/Sign-a-package.md)
