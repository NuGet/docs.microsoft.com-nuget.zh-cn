---
title: "使用 NuGet.Server 托管 NuGet 源 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 45138f80-9717-42c2-8b34-9a1bc1fb3eab
description: "如何使用 NuGet.Server 在运行 IIS 的任何服务器上创建和托管 NuGet 包源，从而通过 HTTP 和 OData 提供包。"
keywords: "NuGet 源, NuGet 库, 远程包源, NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f37b9b711a2bc8c39314214113045a6485f297a8
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="nugetserver"></a><span data-ttu-id="0638c-104">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="0638c-104">NuGet.Server</span></span>

<span data-ttu-id="0638c-105">NuGet.Server 是由 .NET Foundation 提供的包，其创建的 ASP.NET 应用程序可在运行 IIS 的任何服务器上托管包源。</span><span class="sxs-lookup"><span data-stu-id="0638c-105">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="0638c-106">简而言之，NuGet.Server 通过 HTTP（尤其是 OData）在服务器上提供文件夹。</span><span class="sxs-lookup"><span data-stu-id="0638c-106">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="0638c-107">其设置方法十分简单，最适用于简单的方案。</span><span class="sxs-lookup"><span data-stu-id="0638c-107">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="0638c-108">在 Visual Studio 中创建空的 ASP.NET Web 应用程序并向其添加 NuGet.Server 包。</span><span class="sxs-lookup"><span data-stu-id="0638c-108">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="0638c-109">配置应用程序中的 `Packages` 文件夹并添加包。</span><span class="sxs-lookup"><span data-stu-id="0638c-109">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="0638c-110">将应用程序部署到适合的客户端。</span><span class="sxs-lookup"><span data-stu-id="0638c-110">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="0638c-111">以下各节使用 C# 详细演练此过程。</span><span class="sxs-lookup"><span data-stu-id="0638c-111">The following sections walk through this process in detail, using C#.</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="0638c-112">使用 NuGet.Server 创建和部署 ASP.NET Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="0638c-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="0638c-113">在 Visual Studio 中，选择“文件”>“新建”>“项目”，设置 .NET Framework 4.6 的目标框架（见下图），搜索“ASP.NET”，然后选择适用于 C# 的“ASP.NET Web 应用程序 (.NET Framework)”模板。</span><span class="sxs-lookup"><span data-stu-id="0638c-113">In Visual Studio, select **File > New > Project**, set the target framework for .NET Framework 4.6 (see below), search for "ASP.NET", and select the **ASP.NET Web Application (.NET Framework)** template for C#.</span></span>

    ![将 .NET Framework 目标设置为 4.6](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="0638c-115">为应用程序提供除 NuGet.Server 之外的合适名称，选择“确定”，在接下来出现的对话框中选择“空”模板，然后选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="0638c-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template and select OK.</span></span>

1. <span data-ttu-id="0638c-116">如果面向 .NET Framework 4.6，请右键单击项目，选择“管理 NuGet 包”，然后在“包管理器 UI”中搜索 NuGet.Server 包的最新版本并安装。</span><span class="sxs-lookup"><span data-stu-id="0638c-116">Right-click the project, select **Manage NuGet Packages**, and in the Package Manager UI search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="0638c-117">（也可以使用 `Install-Package NuGet.Server` 从包管理器控制台安装。）</span><span class="sxs-lookup"><span data-stu-id="0638c-117">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.)</span></span>

    ![安装 NuGet.Server 包](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > <span data-ttu-id="0638c-119">如果 Web 应用程序面向 .NET Framework 4.5.2，则必须改为安装 NuGet 服务器 2.10.3。</span><span class="sxs-lookup"><span data-stu-id="0638c-119">If your web application targets .NET Framework 4.5.2, you must install NuGet Server **2.10.3** instead.</span></span>

1. <span data-ttu-id="0638c-120">安装 NuGet.Server 会将空 Web 应用程序转换成包源。</span><span class="sxs-lookup"><span data-stu-id="0638c-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="0638c-121">此操作会在应用程序中创建 `Packages` 文件夹，并覆盖 `web.config` 以包括其他设置（请参阅该文件中的注释部分以获取详细信息）。</span><span class="sxs-lookup"><span data-stu-id="0638c-121">It creates a `Packages` folder in the application and overwrites `web.config` to include additional settings (see the comments in that file for details).</span></span>

1. <span data-ttu-id="0638c-122">要在向服务器发布应用程序时在源中提供包，请将其 `.nupkg` 文件添加到 Visual Studio 中的 `Packages` 文件夹，然后将“生成操作”设置为“内容”，将“复制到输出目录”设置为“始终复制”：</span><span class="sxs-lookup"><span data-stu-id="0638c-122">To make packages available in the feed when you publish the application to a server, add their `.nupkg` files to the `Packages` folder in Visual Studio, then set their **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![将包复制到项目中的包文件夹](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="0638c-124">在 Visual Studio 本地运行网站（不进行调试，即 Ctrl+F5）。</span><span class="sxs-lookup"><span data-stu-id="0638c-124">Run the site locally in Visual Studio (without debugging, that is Ctrl+F5).</span></span> <span data-ttu-id="0638c-125">主页提供包源 URL：</span><span class="sxs-lookup"><span data-stu-id="0638c-125">The home page provides the package feed URLs:</span></span>

    ![NuGet.Server 的应用程序的默认主页](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="0638c-127">单击上述框选区域中的“此处”可查看 OData 包源。</span><span class="sxs-lookup"><span data-stu-id="0638c-127">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="0638c-128">首次运行应用程序时，NuGet.Server 会重新构建 `Packages` 文件夹，以包含每个包的文件夹。</span><span class="sxs-lookup"><span data-stu-id="0638c-128">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="0638c-129">这符合 NuGet 3.3 中引入的用于提高性能的[本地存储布局](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands)。</span><span class="sxs-lookup"><span data-stu-id="0638c-129">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="0638c-130">添加更多包时，请继续遵照此结构。</span><span class="sxs-lookup"><span data-stu-id="0638c-130">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="0638c-131">测试本地部署后，请根据需要将应用程序部署到任何其他内部或外部网站。</span><span class="sxs-lookup"><span data-stu-id="0638c-131">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>
1. <span data-ttu-id="0638c-132">部署到 `http://<domain>` 后，用于包源的 URL 将为 `http://<domain>/nuget`。</span><span class="sxs-lookup"><span data-stu-id="0638c-132">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="0638c-133">配置包文件夹</span><span class="sxs-lookup"><span data-stu-id="0638c-133">Configuring the Packages folder</span></span>

<span data-ttu-id="0638c-134">对于 `NuGet.Server` 1.5 和更高版本，可使用 `web.config` 中的 `appSetting/packagesPath` 值更具体地配置包文件夹：</span><span class="sxs-lookup"><span data-stu-id="0638c-134">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="0638c-135">`packagesPath` 可以是绝对或虚拟路径。</span><span class="sxs-lookup"><span data-stu-id="0638c-135">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="0638c-136">省略 `packagesPath` 或将其留空时，包文件夹是默认的 `~/Packages`。</span><span class="sxs-lookup"><span data-stu-id="0638c-136">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="0638c-137">以外部方式向源添加包</span><span class="sxs-lookup"><span data-stu-id="0638c-137">Adding packages to the feed externally</span></span>

<span data-ttu-id="0638c-138">NuGet.Server 站点运行后，如果在 `web.config` 中设置了 API 密钥值，则可使用 nuget.exe 添加或删除包。</span><span class="sxs-lookup"><span data-stu-id="0638c-138">Once a NuGet.Server site is running, you can add or delete packages using nuget.exe provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="0638c-139">安装 NuGet.Server 包后，`web.config` 包含一个空 `appSetting/apiKey` 值：</span><span class="sxs-lookup"><span data-stu-id="0638c-139">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="0638c-140">省略 `apiKey` 或将其留空时，会禁用向源推送包的功能。</span><span class="sxs-lookup"><span data-stu-id="0638c-140">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="0638c-141">要启用此功能，请设置 `apiKey` 的值（理想情况下为强密码），并添加值为 `true` 名为 `appSettings/requireApiKey` 的密钥：</span><span class="sxs-lookup"><span data-stu-id="0638c-141">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="0638c-142">如果服务器已受保护或不需要其他 API 密钥（例如，在本地团队网络上使用专用服务器时），可将 `requireApiKey` 设置为 `false`。</span><span class="sxs-lookup"><span data-stu-id="0638c-142">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="0638c-143">然后，有权访问服务器的所有用户均可推送或删除包。</span><span class="sxs-lookup"><span data-stu-id="0638c-143">All users with access to the server can then push or delete packages.</span></span>