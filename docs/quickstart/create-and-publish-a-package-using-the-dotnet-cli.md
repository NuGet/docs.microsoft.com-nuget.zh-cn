---
title: 使用 dotnet CLI 创建和发布 NuGet 包
description: 使用 .NET Core CLI dotnet 创建和发布 NuGet 包的演练教程。
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 8c09d6d5662ed6ff0deffa5d45b823ad0992f399
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231300"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="d29ef-103">快速入门：创建和发布包 (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="d29ef-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="d29ef-104">从 .NET 类库创建 NuGet 包并使用 `dotnet` 命令行接口 (CLI) 将其发布到 nuget.org 是很简单的过程。</span><span class="sxs-lookup"><span data-stu-id="d29ef-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d29ef-105">必备条件</span><span class="sxs-lookup"><span data-stu-id="d29ef-105">Prerequisites</span></span>

1. <span data-ttu-id="d29ef-106">安装包括 [ CLI 的 ](https://www.microsoft.com/net/download/).NET Core SDK`dotnet`。</span><span class="sxs-lookup"><span data-stu-id="d29ef-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="d29ef-107">从 Visual Studio 2017 开始，dotnet CLI 将自动随任何与 .NET Core 相关的工作负载一起安装。</span><span class="sxs-lookup"><span data-stu-id="d29ef-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="d29ef-108">如果你还没有帐户，请[在 nuget.org 上注册一个免费帐户](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)。</span><span class="sxs-lookup"><span data-stu-id="d29ef-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="d29ef-109">创建新帐户会发送确认电子邮件。</span><span class="sxs-lookup"><span data-stu-id="d29ef-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="d29ef-110">必须先确认该帐户，才能上传包。</span><span class="sxs-lookup"><span data-stu-id="d29ef-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="d29ef-111">创建类库项目</span><span class="sxs-lookup"><span data-stu-id="d29ef-111">Create a class library project</span></span>

<span data-ttu-id="d29ef-112">你可以使用现有的 .NET 类库项目用于要打包的代码，或者创建一个简单的项目，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d29ef-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="d29ef-113">创建名为 `AppLogger` 的文件夹。</span><span class="sxs-lookup"><span data-stu-id="d29ef-113">Create a folder called `AppLogger`.</span></span>

1. <span data-ttu-id="d29ef-114">打开命令提示符并切换到 `AppLogger` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="d29ef-114">Open a command prompt and switch to the `AppLogger` folder.</span></span>

1. <span data-ttu-id="d29ef-115">类型 `dotnet new classlib`，它使用项目当前文件夹的名称。</span><span class="sxs-lookup"><span data-stu-id="d29ef-115">Type `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

   <span data-ttu-id="d29ef-116">这会创建新项目。</span><span class="sxs-lookup"><span data-stu-id="d29ef-116">This creates the new project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="d29ef-117">将包元数据添加到项目文件</span><span class="sxs-lookup"><span data-stu-id="d29ef-117">Add package metadata to the project file</span></span>

<span data-ttu-id="d29ef-118">每个 NuGet 包都需要一个清单，用以描述包的内容和依赖项。</span><span class="sxs-lookup"><span data-stu-id="d29ef-118">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="d29ef-119">在最终包中，清单是基于项目文件中包含的 NuGet 元数据属性生成的 `.nuspec` 文件。</span><span class="sxs-lookup"><span data-stu-id="d29ef-119">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="d29ef-120">打开项目文件 (`.csproj`)，并在现有 `<PropertyGroup>` 标记内至少添加以下属性，同时根据需要更改值：</span><span class="sxs-lookup"><span data-stu-id="d29ef-120">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="d29ef-121">为包提供一个在 nuget.org 中唯一或你使用的任何主机的标识符。</span><span class="sxs-lookup"><span data-stu-id="d29ef-121">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="d29ef-122">对于本次演练，我们建议在名称中包含“Sample”或“Test”，因为稍后的发布步骤确实会使该包公开显示（尽管实际上不太可能有人会使用它）。</span><span class="sxs-lookup"><span data-stu-id="d29ef-122">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="d29ef-123">添加 [NuGet 元数据属性](/dotnet/core/tools/csproj#nuget-metadata-properties)中描述的任何可选属性。</span><span class="sxs-lookup"><span data-stu-id="d29ef-123">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="d29ef-124">对于面向公共使用而生成的包，请特别注意 **PackageTags** 属性，因为这些标记可帮助其他人查找包并了解其用途。</span><span class="sxs-lookup"><span data-stu-id="d29ef-124">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="d29ef-125">运行 pack 命令</span><span class="sxs-lookup"><span data-stu-id="d29ef-125">Run the pack command</span></span>

<span data-ttu-id="d29ef-126">若要从项目中生成 NuGet 包（`.nupkg` 文件），运行 `dotnet pack` 命令，它也会自动生成项目：</span><span class="sxs-lookup"><span data-stu-id="d29ef-126">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="d29ef-127">输出显示 `.nupkg` 文件的路径：</span><span class="sxs-lookup"><span data-stu-id="d29ef-127">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="d29ef-128">在生成期间自动生成包</span><span class="sxs-lookup"><span data-stu-id="d29ef-128">Automatically generate package on build</span></span>

<span data-ttu-id="d29ef-129">若要在运行 `dotnet pack` 时自动运行 `dotnet build`，请将以下行添加到 `<PropertyGroup>` 中的项目文件内：</span><span class="sxs-lookup"><span data-stu-id="d29ef-129">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="d29ef-130">发布包</span><span class="sxs-lookup"><span data-stu-id="d29ef-130">Publish the package</span></span>

<span data-ttu-id="d29ef-131">有了 `.nupkg` 文件后，可以使用 `dotnet nuget push` 命令以及从 nuget.org 获取的 API 密钥将其发布到 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="d29ef-131">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="d29ef-132">获取 API 密钥</span><span class="sxs-lookup"><span data-stu-id="d29ef-132">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="d29ef-133">用 dotnet nuget push 发布</span><span class="sxs-lookup"><span data-stu-id="d29ef-133">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="d29ef-134">发布错误</span><span class="sxs-lookup"><span data-stu-id="d29ef-134">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="d29ef-135">管理已发布的包</span><span class="sxs-lookup"><span data-stu-id="d29ef-135">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-video"></a><span data-ttu-id="d29ef-136">相关视频</span><span class="sxs-lookup"><span data-stu-id="d29ef-136">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-the-NET-CLI-5-of-5/player]

<span data-ttu-id="d29ef-137">在[第 9 频道](https://channel9.msdn.com/Series/NuGet-101)和 [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_) 上查找更多 NuGet 视频。</span><span class="sxs-lookup"><span data-stu-id="d29ef-137">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d29ef-138">后续步骤</span><span class="sxs-lookup"><span data-stu-id="d29ef-138">Next steps</span></span>

<span data-ttu-id="d29ef-139">祝贺你创建第一个 NuGet 包！</span><span class="sxs-lookup"><span data-stu-id="d29ef-139">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d29ef-140">创建包</span><span class="sxs-lookup"><span data-stu-id="d29ef-140">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)

<span data-ttu-id="d29ef-141">若要了解更多 NuGet 产品，请选择以下链接。</span><span class="sxs-lookup"><span data-stu-id="d29ef-141">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="d29ef-142">发布包</span><span class="sxs-lookup"><span data-stu-id="d29ef-142">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="d29ef-143">预发行包</span><span class="sxs-lookup"><span data-stu-id="d29ef-143">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="d29ef-144">支持多个目标框架</span><span class="sxs-lookup"><span data-stu-id="d29ef-144">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="d29ef-145">包版本控制</span><span class="sxs-lookup"><span data-stu-id="d29ef-145">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="d29ef-146">创建本地化包</span><span class="sxs-lookup"><span data-stu-id="d29ef-146">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="d29ef-147">创建符号包</span><span class="sxs-lookup"><span data-stu-id="d29ef-147">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="d29ef-148">给包签名</span><span class="sxs-lookup"><span data-stu-id="d29ef-148">Signing packages</span></span>](../create-packages/Sign-a-package.md)
