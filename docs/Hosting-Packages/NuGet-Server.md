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
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server 是由 .NET Foundation 提供的包，其创建的 ASP.NET 应用程序可在运行 IIS 的任何服务器上托管包源。 简而言之，NuGet.Server 通过 HTTP（尤其是 OData）在服务器上提供文件夹。 其设置方法十分简单，最适用于简单的方案。

1. 在 Visual Studio 中创建空的 ASP.NET Web 应用程序并向其添加 NuGet.Server 包。
1. 配置应用程序中的 `Packages` 文件夹并添加包。
1. 将应用程序部署到适合的客户端。

以下各节使用 C# 详细演练此过程。

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>使用 NuGet.Server 创建和部署 ASP.NET Web 应用程序

1. 在 Visual Studio 中，选择“文件”>“新建”>“项目”，设置 .NET Framework 4.6 的目标框架（见下图），搜索“ASP.NET”，然后选择适用于 C# 的“ASP.NET Web 应用程序 (.NET Framework)”模板。

    ![将 .NET Framework 目标设置为 4.6](media/Hosting_01-NuGet.Server-Set4.6.png)

1. 为应用程序提供除 NuGet.Server 之外的合适名称，选择“确定”，在接下来出现的对话框中选择“空”模板，然后选择“确定”。

1. 如果面向 .NET Framework 4.6，请右键单击项目，选择“管理 NuGet 包”，然后在“包管理器 UI”中搜索 NuGet.Server 包的最新版本并安装。 （也可以使用 `Install-Package NuGet.Server` 从包管理器控制台安装。）

    ![安装 NuGet.Server 包](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > 如果 Web 应用程序面向 .NET Framework 4.5.2，则必须改为安装 NuGet 服务器 2.10.3。

1. 安装 NuGet.Server 会将空 Web 应用程序转换成包源。 此操作会在应用程序中创建 `Packages` 文件夹，并覆盖 `web.config` 以包括其他设置（请参阅该文件中的注释部分以获取详细信息）。

1. 要在向服务器发布应用程序时在源中提供包，请将其 `.nupkg` 文件添加到 Visual Studio 中的 `Packages` 文件夹，然后将“生成操作”设置为“内容”，将“复制到输出目录”设置为“始终复制”：

    ![将包复制到项目中的包文件夹](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. 在 Visual Studio 本地运行网站（不进行调试，即 Ctrl+F5）。 主页提供包源 URL：

    ![NuGet.Server 的应用程序的默认主页](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. 单击上述框选区域中的“此处”可查看 OData 包源。

1. 首次运行应用程序时，NuGet.Server 会重新构建 `Packages` 文件夹，以包含每个包的文件夹。 这符合 NuGet 3.3 中引入的用于提高性能的[本地存储布局](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands)。 添加更多包时，请继续遵照此结构。

1. 测试本地部署后，请根据需要将应用程序部署到任何其他内部或外部网站。
1. 部署到 `http://<domain>` 后，用于包源的 URL 将为 `http://<domain>/nuget`。

## <a name="configuring-the-packages-folder"></a>配置包文件夹

对于 `NuGet.Server` 1.5 和更高版本，可使用 `web.config` 中的 `appSetting/packagesPath` 值更具体地配置包文件夹：

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` 可以是绝对或虚拟路径。

省略 `packagesPath` 或将其留空时，包文件夹是默认的 `~/Packages`。

## <a name="adding-packages-to-the-feed-externally"></a>以外部方式向源添加包

NuGet.Server 站点运行后，如果在 `web.config` 中设置了 API 密钥值，则可使用 nuget.exe 添加或删除包。

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

如果服务器已受保护或不需要其他 API 密钥（例如，在本地团队网络上使用专用服务器时），可将 `requireApiKey` 设置为 `false`。 然后，有权访问服务器的所有用户均可推送或删除包。