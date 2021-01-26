---
title: 用于 Visual Studio 的 NuGet 凭据提供程序
description: 通过在 Visual Studio 扩展中实现 IVsCredentialProvider 接口，NuGet 凭据提供程序对源进行身份验证。
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: f324f1e27e0d718571525152fcf16b55b900dbaa
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777755"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>在 Visual Studio 中通过 NuGet 凭据提供程序对源进行身份验证

NuGet Visual Studio 扩展 3.6 + 支持凭据提供程序，这些提供程序允许 NuGet 使用经过身份验证的源。
安装适用于 Visual Studio 的 NuGet 凭据提供程序后，NuGet Visual Studio 扩展会根据需要自动获取和刷新经过身份验证的源的凭据。

可在 [VsCredentialProvider 示例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)中找到示例实现。

在 Visual Studio 中，NuGet 使用内部， `VsCredentialProviderImporter` 后者还会扫描插件凭据提供程序。 这些插件凭据提供程序必须可被发现为类型的 MEF 导出 `IVsCredentialProvider` 。

从 Visual Studio 中的 4.8 + NuGet 开始，还支持新的跨平台身份验证插件，但出于性能方面的原因，不建议采用这些方法。

> [!Note]
> 用于 Visual Studio 的 NuGet 凭据提供程序必须安装为常规 Visual Studio 扩展，并需要 [Visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) 或更高版本。
>
> 用于 Visual Studio 的 NuGet 凭据提供程序仅适用于 Visual Studio 中 (dotnet restore 或 nuget.exe) 。 有关 nuget.exe 的凭据提供程序，请参阅 [nuget.exe 凭据提供程序](nuget-exe-Credential-providers.md)。
> 对于 dotnet 和 msbuild 中的凭据提供程序，请参阅 [NuGet 跨平台插件](nuget-cross-platform-authentication-plugin.md)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>为 Visual Studio 创建 NuGet 凭据提供程序

NuGet Visual Studio 扩展 3.6 + 实现了用于获取凭据的内部 CredentialService。 CredentialService 包含内置和插件凭据提供程序的列表。 每个提供程序按顺序尝试，直到获取凭据。

获取凭据时，凭据服务将按以下顺序尝试凭据提供程序，获取凭据后立即停止：

1. 将使用内置)  (从 NuGet 配置文件中提取凭据 `SettingsCredentialProvider` 。
1. 如果包源位于 Visual Studio Team Services 上，则 `VisualStudioAccountProvider` 将使用。
1. 将按顺序尝试所有其他插件 Visual Studio 凭据提供程序。
1. 尝试按顺序使用所有 NuGet 跨平台凭据提供程序。
1. 如果尚未获取任何凭据，则系统会提示用户使用标准的基本身份验证对话框来输入凭据。

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>实现 IVsCredentialProvider. GetCredentialsAsync

若要为 Visual Studio 创建 NuGet 凭据提供程序，请创建一个 Visual Studio 扩展，该扩展公开实现该类型的公共 MEF 导出 `IVsCredentialProvider` ，并遵循下面所述的原则。

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

可在 [VsCredentialProvider 示例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)中找到示例实现。

适用于 Visual Studio 的每个 NuGet 凭据提供程序必须：

1. 确定是否可以在启动凭据获取之前为目标 URI 提供凭据。 如果提供程序无法为目标源提供凭据，则它应返回 `null` 。
1. 如果提供程序处理目标 URI 的请求，但无法提供凭据，则应引发异常。

Visual Studio 的自定义 NuGet 凭据提供程序必须实现 `IVsCredentialProvider` [VisualStudio 包](https://www.nuget.org/packages/NuGet.VisualStudio/)中提供的接口。

#### <a name="getcredentialasync"></a>GetCredentialAsync

| 输入参数 |说明|
| ----------------|-----------|
| Uri uri | 正在为其请求凭据的包源 Uri。|
| IWebProxy 代理 | 网络上通信时要使用的 Web 代理。 如果未配置代理身份验证，则为 Null。 |
| bool isProxyRequest | 如果此请求将获取代理身份验证凭据，则为 True。 如果实现对于获取代理凭据无效，则应返回 null。 |
| bool isRetry | 如果以前已为此 Uri 请求凭据，但提供的凭据不允许授权访问，则为 True。 |
| bool 非交互式 | 如果为 true，则凭据提供程序必须禁止显示所有用户提示并改用默认值。 |
| CancellationToken cancellationToken | 应检查此取消标记以确定请求凭据的操作是否已取消。 |

**返回值**：实现 [ `System.Net.ICredentials` 接口](/dotnet/api/system.net.icredentials?view=netstandard-2.0)的凭据对象。
