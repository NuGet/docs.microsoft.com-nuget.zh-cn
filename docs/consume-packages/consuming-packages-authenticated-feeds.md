---
title: 使用经过身份验证的源中的包
description: 在所有 NuGet 客户端方案中使用经过身份验证的源中的包
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231739"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>使用经过身份验证的源中的包

除了 nuget.org [公共源](https://api.nuget.org/v3/index.json)外，NuGet 客户端能够与文件源和专用 http 源交互。


要向专用 http 源进行身份验证，可以使用以下两种方式：

* 在 [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials) 中添加凭据
* 根据所用的客户端，使用一种扩展性模型进行身份验证。

## <a name="nuget-clients-authentication-extensibility"></a>NuGet 客户端的身份验证扩展性

对于各种 NuGet 客户端，专用源提供程序本身负责进行身份验证。
所有 NuGet 客户端都具有支持此方式的扩展性方法。 这些方法包括 Visual Studio 扩展或可与 NuGet 通信以检索凭据的插件。

### <a name="visual-studio"></a>Visual Studio

在 Visual Studio 中，NuGet 公开了一个源提供程序可以实现并向其客户提供的接口。 如需了解详情，请参阅介绍[如何创建 Visual Studio 凭据提供程序](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)的文档。

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>Visual Studio 的可用 NuGet 凭据提供程序

Visual Studio 中有一个支持 Azure DevOps 的内置凭据提供程序。


可用的插件凭据提供程序包括：

* [适用于 Visual Studio 的 MyGet 凭据提供程序](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

当 `nuget.exe` 需要凭据来向源进行身份验证时，它会采用以下方式查找凭据：

1. 在 `NuGet.config` 文件中查找凭据。
1. 使用 V2 插件凭据提供程序
1. 使用 V1 插件凭据提供程序
1. 然后，NuGet 会提示用户在命令行上提供凭据。

#### <a name="nugetexe-and-v2-credential-providers"></a>nuget.exe 和 V2 凭据提供程序

在 `4.8` 版中，NuGet 定义了一种新的身份验证插件机制（以下称为 V2 凭据提供程序）。
若要发现和安装这些提供程序，请参阅 [NuGet 跨平台插件](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。

#### <a name="nugetexe-and-v1-credential-providers"></a>nuget.exe 和 V1 凭据提供程序

在 `3.3` 版本中，NuGet 引入了首版身份验证插件。
若要发现和安装这些提供程序，请参阅 [nuget.exe 凭据提供程序](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)

#### <a name="available-credential-providers-for-nugetexe"></a>nuget.exe 的可用凭据提供程序

* [Azure DevOps V2 凭据提供程序](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later)或 [Azure Artifacts 凭据提供程序](https://github.com/microsoft/artifacts-credprovider)

对于 Visual Studio 2017 15.9 及更高版本，Azure DevOps 凭据提供程序捆绑在 Visual Studio 中。
如果 `nuget.exe` 使用来自该特定 Visual Studio 工具集的 MSBuild，则系统会自动发现该插件。

### <a name="dotnetexe"></a>dotnet.exe

当 `dotnet.exe` 需要凭据来向源进行身份验证时，它会采用以下方式查找凭据：

1. 在 `NuGet.config` 文件中查找凭据。
1. 使用 V2 插件凭据提供程序

默认情况下，`dotnet.exe` 不是交互式的，因此可能需要传递 `--interactive` 标志，将工具指向用于身份验证的程序块。

#### <a name="dotnetexe-and-v2-credential-providers"></a>dotnet.exe 和 V2 凭据提供程序

在 SDK `2.2.100` 版本中，NuGet 定义了一种适用于所有客户端的身份验证插件机制。
若要发现和安装这些提供程序，请参阅 [NuGet 跨平台插件](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。

#### <a name="available-credential-providers-for-dotnetexe"></a>dotnet.exe 的可用凭据提供程序

* [Azure Artifacts 凭据提供程序](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>MSBuild.exe

当 `MSBuild.exe` 需要凭据来向源进行身份验证时，它会采用以下方式查找凭据：

1. 在 `NuGet.config` 文件中查找凭据
1. 使用 V2 插件凭据提供程序

默认情况下，`MSBuild.exe` 不是交互式的，因此你可能需要设置 `/p:NuGetInteractive=true` 属性，将工具指向用于身份验证的程序块。

#### <a name="msbuildexe-and-v2-credential-providers"></a>MSBuild.exe 和 V2 凭据提供程序

在 Visual Studio 2019 Update 9 中，NuGet 定义了一种适用于所有客户端的身份验证插件机制。
若要发现和安装这些提供程序，请参阅 [NuGet 跨平台插件](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。

#### <a name="available-credential-providers-for-msbuildexe"></a>MSBuild.exe 的可用凭据提供程序

* [Azure Artifacts 凭据提供程序](https://github.com/microsoft/artifacts-credprovider)

对于 Visual Studio 2017 Update 9 及更高版本，Azure DevOps 凭据提供程序捆绑在 Visual Studio 中。 无需执行其他步骤。
