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
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server 是由 .NET Foundation 提供的包，其创建的 ASP.NET 应用程序可在运行 IIS 的任何服务器上托管包源。 简而言之，NuGet.Server 通过 HTTP（尤其是 OData）在服务器上提供文件夹。 其设置方法十分简单，最适用于简单的方案。

1. 在 Visual Studio 中创建空的 ASP.NET Web 应用程序并向其添加 NuGet.Server 包。
1. 配置应用程序中的 `Packages` 文件夹并添加包。
1. 将应用程序部署到适合的客户端。

以下各节使用 C# 详细演练此过程。

如果对 NuGet.Server 有进一步的疑问，请在 [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues) 上创建问题。

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>使用 NuGet.Server 创建和部署 ASP.NET Web 应用程序

1. 在 Visual Studio 中，选择“文件”>“新建”>“项目”  ，搜索“ASP.NET Web 应用程序 (.NET Framework)”，选择适用于 C# 的匹配模板。

    ![选择 .NET Framework Web 项目模板](media/Hosting_00-NuGet.Server-ProjectType.png)

1. 将“框架”设置为“.NET Framework 4.6”  。

    ![为新项目设置目标框架](media/Hosting_01-NuGet.Server-Set4.6.png)

1. 为应用程序提供除 NuGet.Server 之外的合适名称，选择“确定”，在接下来出现的对话框中选择“空”模板，然后选择“确定”    。

    ![选择空 Web 项目](media/Hosting_02-NuGet.Server-Empty.png)

1. 右键单击项目，选择“管理 NuGet 包”  。

1. 如果面向 .NET Framework 4.6，请在“包管理器 UI”中，选择“浏览器”选项卡，然后搜索并安装 NuGet.Server 包的最新版本  。 （也可以使用 `Install-Package NuGet.Server` 从包管理器控制台安装。）如果出现提示，请接受此许可条款。

    ![安装 NuGet.Server 包](media/Hosting_03-NuGet.Server-Package.png)

1. 安装 NuGet.Server 会将空 Web 应用程序转换成包源。 此操作会安装各种其他包，在应用程序中创建 `Packages` 文件夹，并修改 `web.config` 以包括其他设置（请参阅该文件中的注释部分以获取详细信息）。

    > [!Important]
    > 在 NuGet.Server 包完成对该文件的修改后，仔细检查 `web.config`。 NuGet.Server 可能不会覆盖现有元素，而会创建重复元素。 稍后尝试运行该项目时，这些重复项会导致“内部服务器错误”。 例如，如果 `web.config` 在安装 NuGet.Server 之前包含 `<compilation debug="true" targetFramework="4.5.2" />`，则该包不会覆盖它，而是会插入另一个 `<compilation debug="true" targetFramework="4.6" />`。 在这种情况下，请删除具有较旧框架版本的元素。

1. 在 Visual Studio 本地运行网站（使用“调试”>“开始执行(不调试)”或 Ctrl+F5）  。 主页提供包源 URL，如下所示。 如果发现错误，请仔细检查 `web.config` 是否有重复元素（如前文所述）。

    ![NuGet.Server 的应用程序的默认主页](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  首次运行应用程序时，NuGet.Server 会重新构建 `Packages` 文件夹，以包含每个包的文件夹。 这符合 NuGet 3.3 中引入的用于提高性能的[本地存储布局](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands)。 添加更多包时，请继续遵照此结构。

1. 测试本地部署后，请根据需要将应用程序部署到任何其他内部或外部网站。

1. 部署到 `http://<domain>` 后，用于包源的 URL 将为 `http://<domain>/nuget`。

## <a name="adding-packages-to-the-feed-externally"></a>以外部方式向源添加包

NuGet.Server 站点运行后，就可以使用 [nuget push](../reference/cli-reference/cli-ref-push.md) 添加包，前提是在 `web.config` 中设置了 API 密钥值。

安装 NuGet.Server 包后，`web.config` 包含一个空 `appSetting/apiKey` 值：

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

省略 `apiKey` 或将其留空时，会禁用向源推送包的功能。

要启用此功能，请设置 `apiKey` 的值（理想情况下为强密码），并添加值为 `true` 名为 `appSettings/requireApiKey` 的密钥：

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

如果服务器已受保护或不需要其他 API 密钥（例如，在本地团队网络上使用专用服务器时），可将 `requireApiKey` 设置为 `false`。 然后，有权访问服务器的所有用户均可推送包。

从 NuGet.Server 3.0.0 开始，推送包的 URL 更改为 `http://<domain>/nuget`。 在 3.0.0 版本之前，推送 URL 为 `http://<domain>/api/v2/package`。

对于 NuGet 3.2.1 和更高版本，除 `/nuget` 外，默认还会通过启动配置（默认为 `NuGetODataConfig.cs`）中的 `enableLegacyPushRoute: true` 选项启用此旧 URL `/api/v2/package`。 请注意，在同一项目中托管多个源时，此功能不适用。

## <a name="removing-packages-from-the-feed"></a>从源中删除包

使用 NuGet.Server 时，[nuget delete](../reference/cli-reference/cli-ref-delete.md) 命令会从存储库中删除一个包，但前提是包含 API 密钥和注释。

如果想要改变行为以从列表中删除包（将其保留为可用于包还原），请将 `web.config` 中的 `enableDelisting` 键更改为 true。

## <a name="configuring-the-packages-folder"></a>配置包文件夹

对于 `NuGet.Server` 1.5 和更高版本，可使用 `web.config` 中的 `appSettings/packagesPath` 值自定义包文件夹：

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` 可以是绝对或虚拟路径。

省略 `packagesPath` 或将其留空时，包文件夹是默认的 `~/Packages`。

## <a name="making-packages-available-when-you-publish-the-web-app"></a>发布 Web 应用时使包可用

要在向服务器发布应用程序时在源中提供包，请将每个 `.nupkg` 文件添加到 Visual Studio 中的 `Packages` 文件夹，然后将每个文件的“生成操作”设置为“内容”，将“复制到输出目录”设置为“始终复制”     ：

![将包复制到项目中的包文件夹](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a>发行说明

[GitHub 发布页](https://github.com/NuGet/NuGet.Server/releases)上提供了 NuGet 的发行说明。
其中包括有关 bug 修复和新增功能的详细信息。

## <a name="nugetserver-support"></a>NuGet.Server 支持

有关使用 NuGet.Server 的其他帮助，请在 [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues) 上创建问题。
