---
title: 用于 Visual Studio 的 NuGet 凭据提供程序
description: NuGet 凭据提供程序通过在 Visual Studio 扩展中实现 IVsCredentialProvider 接口馈送进行身份验证。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e8d8ae22300b55b93badb65864163d959105dca2
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2018
ms.locfileid: "42793898"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>在 Visual Studio 中使用 NuGet 凭据提供程序的源进行身份验证

NuGet Visual Studio 扩展 3.6 + 支持可以使 NuGet 能够使用已验证的源的凭据提供程序。
安装 Visual Studio 的 NuGet 凭据提供程序后，NuGet Visual Studio 扩展将自动获取和刷新用于根据需要已验证的源的凭据。

示例实现可在[VsCredentialProvider 示例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)。

从开始 4.8 + 在 Visual Studio 中的 NuGet 支持，新的跨平台身份验证插件，但它们不是出于性能原因，建议的方法。

> [!Note]
> 用于 Visual Studio 的 NuGet 凭据提供程序必须作为常规的 Visual Studio 扩展安装，并且需要[Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe)或更高版本。
>
> 用于 Visual Studio 的 NuGet 凭据提供程序仅适用于 Visual Studio 中 （不在 dotnet 还原或 nuget.exe）。 Nuget.exe 凭据提供程序，请参阅[nuget.exe 凭据提供程序](nuget-exe-Credential-providers.md)。
> 有关凭据 dotnet 和 msbuild 中的提供程序请参阅[NuGet 跨平台插件](nuget-cross-platform-authentication-plugin.md)

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Visual Studio 的可用 NuGet 凭据提供程序

没有内置于 Visual Studio NuGet 扩展的凭据提供程序以支持 Visual Studio Team Services。

NuGet Visual Studio 扩展使用内部`VsCredentialProviderImporter`这还扫描插件凭据提供程序。 这些插件凭据提供程序必须能够发现作为导出类型的 MEF `IVsCredentialProvider`。

可用的插件凭据提供程序包括：

- [适用于 Visual Studio 2017 的 MyGet 凭据提供程序](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>创建 Visual Studio 的 NuGet 凭据提供程序

NuGet Visual Studio 扩展 3.6 + 实现内部 CredentialService 用来获取凭据。 CredentialService 具有内置和插件凭据提供程序的列表。 获取凭据之前，将按顺序尝试每个提供程序。

在凭据获取凭据服务将尝试按以下顺序停止立即获取凭据的凭据提供程序：

1. NuGet 配置文件中提取的凭据 (使用内置`SettingsCredentialProvider`)。
1. 如果包源是在 Visual Studio Team Services`VisualStudioAccountProvider`将使用。
1. 将按顺序尝试所有其他插件 Visual Studio 的凭据提供程序。
1. 尝试按顺序使用跨平台的凭据提供程序的所有 NuGet。
1. 如果已获取不使用凭据，将凭据使用标准的基本身份验证对话框提示用户。

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>实现 IVsCredentialProvider.GetCredentialsAsync

若要创建 Visual Studio 的 NuGet 凭据提供程序，创建一个 Visual Studio 扩展，公开公共 MEF 导出实现`IVsCredentialProvider`类型，并遵循下面所述的原则。

```cs
public interface IVsCredentialProvider
{
    Task<ICredentials> GetCredentialsAsync(
        Uri uri,
        IWebProxy proxy,
        bool isProxyRequest,
        bool isRetry,
        bool nonInteractive,
        CancellationToken cancellationToken);
}
```

示例实现可在[VsCredentialProvider 示例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)。

Visual Studio 的每个 NuGet 凭据提供程序必须：

1. 确定是否它可提供凭据的目标 URI 启动凭据获取之前。 如果提供商无法提供凭据的目标的源，则它应返回`null`。
1. 如果提供程序无法处理请求的目标 URI，但不能提供的凭据，则应引发异常。

Visual Studio 的自定义 NuGet 凭据提供程序必须实现`IVsCredentialProvider`中提供的接口[NuGet.VisualStudio 包](https://www.nuget.org/packages/NuGet.VisualStudio/)。

#### <a name="getcredentialasync"></a>GetCredentialAsync

| 输入的参数 |描述|
| ----------------|-----------|
| Uri uri | 正在为其请求凭据包源 Uri。|
| IWebProxy 代理 | 若要在网络上通信时使用的 web 代理。 如果不没有配置任何代理身份验证，则为 null。 |
| bool isProxyRequest | 如果此请求获取代理身份验证凭据，则为 true。 如果实现用于获取代理凭据无效，应返回 null。 |
| bool isRetry | 如果凭据以前请求过，此 Uri，但提供的凭据不允许经授权的访问权限，则为 true。 |
| 非交互式 bool | 如果为 true，则必须取消所有用户提示的凭据提供程序并将其改为使用默认值。 |
| CancellationToken cancellationToken | 应检查此取消标记，以确定操作要求凭据已被取消。 |

**返回值**： 凭据对象实现[`System.Net.ICredentials`接口](/dotnet/api/system.net.icredentials?view=netstandard-2.0)。
