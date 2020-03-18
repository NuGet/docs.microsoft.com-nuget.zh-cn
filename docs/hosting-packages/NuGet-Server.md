---
title: 使用 NuGet.Server 托管 NuGet 源
description: 如何使用 NuGet.Server 在运行 IIS 的任何服务器上创建和托管 NuGet 包源，从而通过 HTTP 和 OData 提供包。
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 098375b2bba13675ba5d80a27e0226dc2ee39e77
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/10/2020
ms.locfileid: "79059509"
---
# <a name="nugetserver"></a><span data-ttu-id="ab726-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="ab726-103">NuGet.Server</span></span>

<span data-ttu-id="ab726-104">NuGet.Server 是由 .NET Foundation 提供的包，其创建的 ASP.NET 应用程序可在运行 IIS 的任何服务器上托管包源。</span><span class="sxs-lookup"><span data-stu-id="ab726-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="ab726-105">简而言之，NuGet.Server 通过 HTTP（尤其是 OData）在服务器上提供文件夹。</span><span class="sxs-lookup"><span data-stu-id="ab726-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="ab726-106">其设置方法十分简单，最适用于简单的方案。</span><span class="sxs-lookup"><span data-stu-id="ab726-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="ab726-107">在 Visual Studio 中创建空的 ASP.NET Web 应用程序并向其添加 NuGet.Server 包。</span><span class="sxs-lookup"><span data-stu-id="ab726-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="ab726-108">配置应用程序中的 `Packages` 文件夹并添加包。</span><span class="sxs-lookup"><span data-stu-id="ab726-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="ab726-109">将应用程序部署到适合的客户端。</span><span class="sxs-lookup"><span data-stu-id="ab726-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="ab726-110">以下各节使用 C# 详细演练此过程。</span><span class="sxs-lookup"><span data-stu-id="ab726-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="ab726-111">如果对 NuGet.Server 有进一步的疑问，请在 [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues) 上创建问题。</span><span class="sxs-lookup"><span data-stu-id="ab726-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="ab726-112">使用 NuGet.Server 创建和部署 ASP.NET Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="ab726-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="ab726-113">在 Visual Studio 中，选择“文件”>“新建”>“项目”  ，搜索“ASP.NET Web 应用程序 (.NET Framework)”，选择适用于 C# 的匹配模板。</span><span class="sxs-lookup"><span data-stu-id="ab726-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET Web Application (.NET Framework)", select the matching template for C#.</span></span>

    ![选择 .NET Framework Web 项目模板](media/Hosting_00-NuGet.Server-ProjectType.png)

1. <span data-ttu-id="ab726-115">将“框架”设置为“.NET Framework 4.6”  。</span><span class="sxs-lookup"><span data-stu-id="ab726-115">Set **Framework** to ".NET Framework 4.6".</span></span>

    ![为新项目设置目标框架](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="ab726-117">为应用程序提供除 NuGet.Server 之外的合适名称，选择“确定”，在接下来出现的对话框中选择“空”模板，然后选择“确定”    。</span><span class="sxs-lookup"><span data-stu-id="ab726-117">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

    ![选择空 Web 项目](media/Hosting_02-NuGet.Server-Empty.png)

1. <span data-ttu-id="ab726-119">右键单击项目，选择“管理 NuGet 包”  。</span><span class="sxs-lookup"><span data-stu-id="ab726-119">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="ab726-120">如果面向 .NET Framework 4.6，请在“包管理器 UI”中，选择“浏览器”选项卡，然后搜索并安装 NuGet.Server 包的最新版本  。</span><span class="sxs-lookup"><span data-stu-id="ab726-120">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="ab726-121">（也可以使用 `Install-Package NuGet.Server` 从包管理器控制台安装。）如果出现提示，请接受此许可条款。</span><span class="sxs-lookup"><span data-stu-id="ab726-121">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![安装 NuGet.Server 包](media/Hosting_03-NuGet.Server-Package.png)

1. <span data-ttu-id="ab726-123">安装 NuGet.Server 会将空 Web 应用程序转换成包源。</span><span class="sxs-lookup"><span data-stu-id="ab726-123">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="ab726-124">此操作会安装各种其他包，在应用程序中创建 `Packages` 文件夹，并修改 `web.config` 以包括其他设置（请参阅该文件中的注释部分以获取详细信息）。</span><span class="sxs-lookup"><span data-stu-id="ab726-124">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="ab726-125">在 NuGet.Server 包完成对该文件的修改后，仔细检查 `web.config`。</span><span class="sxs-lookup"><span data-stu-id="ab726-125">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="ab726-126">NuGet.Server 可能不会覆盖现有元素，而会创建重复元素。</span><span class="sxs-lookup"><span data-stu-id="ab726-126">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="ab726-127">稍后尝试运行该项目时，这些重复项会导致“内部服务器错误”。</span><span class="sxs-lookup"><span data-stu-id="ab726-127">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="ab726-128">例如，如果 `web.config` 在安装 NuGet.Server 之前包含 `<compilation debug="true" targetFramework="4.5.2" />`，则该包不会覆盖它，而是会插入另一个 `<compilation debug="true" targetFramework="4.6" />`。</span><span class="sxs-lookup"><span data-stu-id="ab726-128">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="ab726-129">在这种情况下，请删除具有较旧框架版本的元素。</span><span class="sxs-lookup"><span data-stu-id="ab726-129">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="ab726-130">在 Visual Studio 本地运行网站（使用“调试”>“开始执行(不调试)”或 Ctrl+F5）  。</span><span class="sxs-lookup"><span data-stu-id="ab726-130">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="ab726-131">主页提供包源 URL，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ab726-131">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="ab726-132">如果发现错误，请仔细检查 `web.config` 是否有重复元素（如前文所述）。</span><span class="sxs-lookup"><span data-stu-id="ab726-132">If you see errors, carefully inspect your `web.config` for duplicate elements as noted earlier.</span></span>

    ![NuGet.Server 的应用程序的默认主页](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  <span data-ttu-id="ab726-134">首次运行应用程序时，NuGet.Server 会重新构建 `Packages` 文件夹，以包含每个包的文件夹。</span><span class="sxs-lookup"><span data-stu-id="ab726-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="ab726-135">这符合 NuGet 3.3 中引入的用于提高性能的[本地存储布局](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands)。</span><span class="sxs-lookup"><span data-stu-id="ab726-135">This matches the [local storage layout](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="ab726-136">添加更多包时，请继续遵照此结构。</span><span class="sxs-lookup"><span data-stu-id="ab726-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="ab726-137">测试本地部署后，请根据需要将应用程序部署到任何其他内部或外部网站。</span><span class="sxs-lookup"><span data-stu-id="ab726-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="ab726-138">部署到 `http://<domain>` 后，用于包源的 URL 将为 `http://<domain>/nuget`。</span><span class="sxs-lookup"><span data-stu-id="ab726-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="ab726-139">以外部方式向源添加包</span><span class="sxs-lookup"><span data-stu-id="ab726-139">Adding packages to the feed externally</span></span>

<span data-ttu-id="ab726-140">NuGet.Server 站点运行后，就可以使用 [nuget push](../reference/cli-reference/cli-ref-push.md) 添加包，前提是在 `web.config` 中设置了 API 密钥值。</span><span class="sxs-lookup"><span data-stu-id="ab726-140">Once a NuGet.Server site is running, you can add packages using [nuget push](../reference/cli-reference/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="ab726-141">安装 NuGet.Server 包后，`web.config` 包含一个空 `appSetting/apiKey` 值：</span><span class="sxs-lookup"><span data-stu-id="ab726-141">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="ab726-142">省略 `apiKey` 或将其留空时，会禁用向源推送包的功能。</span><span class="sxs-lookup"><span data-stu-id="ab726-142">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="ab726-143">要启用此功能，请设置 `apiKey` 的值（理想情况下为强密码），并添加值为 `true` 名为 `appSettings/requireApiKey` 的密钥：</span><span class="sxs-lookup"><span data-stu-id="ab726-143">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="ab726-144">如果服务器已受保护或不需要其他 API 密钥（例如，在本地团队网络上使用专用服务器时），可将 `requireApiKey` 设置为 `false`。</span><span class="sxs-lookup"><span data-stu-id="ab726-144">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="ab726-145">然后，有权访问服务器的所有用户均可推送包。</span><span class="sxs-lookup"><span data-stu-id="ab726-145">All users with access to the server can then push packages.</span></span>

<span data-ttu-id="ab726-146">从 NuGet.Server 3.0.0 开始，推送包的 URL 更改为 `http://<domain>/nuget`。</span><span class="sxs-lookup"><span data-stu-id="ab726-146">Starting with NuGet.Server 3.0.0, the URL for pushing packages was change to `http://<domain>/nuget`.</span></span> <span data-ttu-id="ab726-147">在 3.0.0 版本之前，推送 URL 为 `http://<domain>/api/v2/package`。</span><span class="sxs-lookup"><span data-stu-id="ab726-147">Prior to the 3.0.0 release, the push URL was `http://<domain>/api/v2/package`.</span></span>

<span data-ttu-id="ab726-148">对于 NuGet 3.2.1 和更高版本，除 `/nuget` 外，默认还会通过启动配置（默认为 `NuGetODataConfig.cs`）中的 `enableLegacyPushRoute: true` 选项启用此旧 URL `/api/v2/package`。</span><span class="sxs-lookup"><span data-stu-id="ab726-148">With NuGet 3.2.1 and newer, this legacy URL `/api/v2/package` is enabled in addition to `/nuget` by default via `enableLegacyPushRoute: true` option in your startup config (`NuGetODataConfig.cs` by default).</span></span> <span data-ttu-id="ab726-149">请注意，在同一项目中托管多个源时，此功能不适用。</span><span class="sxs-lookup"><span data-stu-id="ab726-149">Note that this feature does not work when multiple feeds are hosted in the same project.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="ab726-150">从源中删除包</span><span class="sxs-lookup"><span data-stu-id="ab726-150">Removing packages from the feed</span></span>

<span data-ttu-id="ab726-151">使用 NuGet.Server 时，[nuget delete](../reference/cli-reference/cli-ref-delete.md) 命令会从存储库中删除一个包，但前提是包含 API 密钥和注释。</span><span class="sxs-lookup"><span data-stu-id="ab726-151">With NuGet.Server, the [nuget delete](../reference/cli-reference/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="ab726-152">如果想要改变行为以从列表中删除包（将其保留为可用于包还原），请将 `web.config` 中的 `enableDelisting` 键更改为 true。</span><span class="sxs-lookup"><span data-stu-id="ab726-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="ab726-153">配置包文件夹</span><span class="sxs-lookup"><span data-stu-id="ab726-153">Configuring the Packages folder</span></span>

<span data-ttu-id="ab726-154">对于 `NuGet.Server` 1.5 和更高版本，可使用 `web.config` 中的 `appSettings/packagesPath` 值自定义包文件夹：</span><span class="sxs-lookup"><span data-stu-id="ab726-154">With `NuGet.Server` 1.5 and later, you can customize the package folder using the `appSettings/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="ab726-155">`packagesPath` 可以是绝对或虚拟路径。</span><span class="sxs-lookup"><span data-stu-id="ab726-155">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="ab726-156">省略 `packagesPath` 或将其留空时，包文件夹是默认的 `~/Packages`。</span><span class="sxs-lookup"><span data-stu-id="ab726-156">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="making-packages-available-when-you-publish-the-web-app"></a><span data-ttu-id="ab726-157">发布 Web 应用时使包可用</span><span class="sxs-lookup"><span data-stu-id="ab726-157">Making packages available when you publish the web app</span></span>

<span data-ttu-id="ab726-158">要在向服务器发布应用程序时在源中提供包，请将每个 `.nupkg` 文件添加到 Visual Studio 中的 `Packages` 文件夹，然后将每个文件的“生成操作”设置为“内容”，将“复制到输出目录”设置为“始终复制”     ：</span><span class="sxs-lookup"><span data-stu-id="ab726-158">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

![将包复制到项目中的包文件夹](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a><span data-ttu-id="ab726-160">发行说明</span><span class="sxs-lookup"><span data-stu-id="ab726-160">Release Notes</span></span>

<span data-ttu-id="ab726-161">[GitHub 发布页](https://github.com/NuGet/NuGet.Server/releases)上提供了 NuGet 的发行说明。</span><span class="sxs-lookup"><span data-stu-id="ab726-161">Release notes for NuGet.Server are available on the [GitHub release page](https://github.com/NuGet/NuGet.Server/releases).</span></span>
<span data-ttu-id="ab726-162">其中包括有关 bug 修复和新增功能的详细信息。</span><span class="sxs-lookup"><span data-stu-id="ab726-162">This includes details about bug fixes and new features that are added.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="ab726-163">NuGet.Server 支持</span><span class="sxs-lookup"><span data-stu-id="ab726-163">NuGet.Server support</span></span>

<span data-ttu-id="ab726-164">有关使用 NuGet.Server 的其他帮助，请在 [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues) 上创建问题。</span><span class="sxs-lookup"><span data-stu-id="ab726-164">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>
