---
title: 使用 dotnet CLI 创建和发布 NuGet 包
description: 使用 .NET Core CLI dotnet 创建和发布 NuGet 包的演练教程。
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: f663b1b2176a5f0ae5bc6d82873193638e0efdaa
ms.sourcegitcommit: ba8ad1bd13a4bba3df94374e34e20c425a05af2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2019
ms.locfileid: "68833380"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>快速入门：创建并发布包 (dotnet CLI)

从 .NET 类库创建 NuGet 包并使用 `dotnet` 命令行接口 (CLI) 将其发布到 nuget.org 是很简单的过程。

## <a name="prerequisites"></a>系统必备

1. 安装包括 `dotnet` CLI 的 [.NET Core SDK](https://www.microsoft.com/net/download/)。 从 Visual Studio 2017 开始，dotnet CLI 将自动随任何与 .NET Core 相关的工作负载一起安装。

1. 如果你还没有帐户，请[在 nuget.org 上注册一个免费帐户](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)。 创建新帐户会发送确认电子邮件。 必须先确认该帐户，才能上传包。

## <a name="create-a-class-library-project"></a>创建类库项目

你可以使用现有的 .NET 类库项目用于要打包的代码，或者创建一个简单的项目，如下所示：

1. 创建名为 `AppLogger` 的文件夹。

1. 打开命令提示符并切换到 `AppLogger` 文件夹。

1. 类型 `dotnet new classlib`，它使用项目当前文件夹的名称。

   这会创建新项目。

1. 使用 `dotnet run` 来测试已正确创建的应用。

## <a name="add-package-metadata-to-the-project-file"></a>将包元数据添加到项目文件

每个 NuGet 包都需要一个清单，用以描述包的内容和依赖项。 在最终包中，清单是基于项目文件中包含的 NuGet 元数据属性生成的 `.nuspec` 文件。

1. 打开项目文件 (`.csproj`)，并在现有 `<PropertyGroup>` 标记内至少添加以下属性，同时根据需要更改值：

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > 为包提供一个在 nuget.org 中唯一或你使用的任何主机的标识符。 对于本次演练，我们建议在名称中包含“Sample”或“Test”，因为稍后的发布步骤确实会使该包公开显示（尽管实际上不太可能有人会使用它）。

1. 添加 [NuGet 元数据属性](/dotnet/core/tools/csproj#nuget-metadata-properties)中描述的任何可选属性。

    > [!Note]
    > 对于面向公共使用而生成的包，请特别注意 **PackageTags** 属性，因为这些标记可帮助其他人查找包并了解其用途。

## <a name="run-the-pack-command"></a>运行 pack 命令

若要从项目中生成 NuGet 包（`.nupkg` 文件），运行 `dotnet pack` 命令，它也会自动生成项目：

```cli
# Uses the project file in the current folder by default
dotnet pack
```

输出显示 `.nupkg` 文件的路径：

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>在生成期间自动生成包

若要在运行 `dotnet build` 时自动运行 `dotnet pack`，请将以下行添加到 `<PropertyGroup>` 中的项目文件内：

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>发布包

有了 `.nupkg` 文件后，可以使用 `dotnet nuget push` 命令以及从 nuget.org 获取的 API 密钥将其发布到 nuget.org。

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>获取 API 密钥

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>用 dotnet nuget push 发布

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>发布错误

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>管理已发布的包

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a>后续步骤

祝贺你创建第一个 NuGet 包！

> [!div class="nextstepaction"]
> [创建包](../create-packages/creating-a-package-dotnet-cli.md)

若要了解更多 NuGet 产品，请选择以下链接。

- [发布包](../nuget-org/publish-a-package.md)
- [预发行包](../create-packages/Prerelease-Packages.md)
- [支持多个目标框架](../create-packages/multiple-target-frameworks-project-file.md)
- [包版本控制](../reference/package-versioning.md)
- [创建本地化包](../create-packages/creating-localized-packages.md)
- [创建符号包](../create-packages/symbol-packages-snupkg.md)
- [给包签名](../create-packages/Sign-a-package.md)
