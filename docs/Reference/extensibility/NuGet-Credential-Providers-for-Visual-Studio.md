---
title: NuGet 对 Visual Studio 的凭据提供程序
description: NuGet 的凭据提供程序进行身份验证源通过在 Visual Studio 扩展中实现该 IVsCredentialProvider 接口。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 740df87b0d663aac482d888e916662528ce27030
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>NuGet 的凭据提供程序与 Visual Studio 中的源进行身份验证

NuGet Visual Studio 扩展中 3.6 + 支持启用 NuGet 用于经过身份验证的源的凭据提供程序。
安装 Visual Studio 的 NuGet 凭据提供程序后，NuGet Visual Studio 扩展将自动获取并刷新根据需要经过身份验证源的凭据。

在找不到示例实现[VsCredentialProvider 示例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)。

> [!Note]
> NuGet 对 Visual Studio 的凭据提供程序必须安装为正则 Visual Studio 扩展，将需要[Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) （当前为预览版） 或更高版本。
>
> NuGet 对 Visual Studio 的凭据提供程序仅适用于 Visual Studio 中 （不在 dotnet 还原或 nuget.exe）。 有关通过 nuget.exe 使用凭据提供程序，请参阅[nuget.exe 凭据提供程序](nuget-exe-Credential-providers.md)。

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Visual Studio 的可用 NuGet 凭据提供程序

没有内置于 Visual Studio NuGet 扩展凭据提供程序以支持 Visual Studio Team Services。

NuGet Visual Studio 扩展使用内部`VsCredentialProviderImporter`这还扫描插件凭据提供程序。 这些插件的凭据提供程序必须能够发现作为类型 MEF 导出`IVsCredentialProvider`。

可用的插件凭据提供程序包括：

- [适用于 Visual Studio 2017 的 MyGet 凭据提供程序](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>创建 Visual Studio 的 NuGet 凭据提供程序

NuGet Visual Studio 扩展中 3.6 + 实现内部 CredentialService 用于获取凭据。 CredentialService 具有内置和插件的凭据提供程序的列表。 每个提供程序是按顺序尝试，直到获取凭据。

在凭据获取凭据服务将尝试按以下顺序，停止就会立即获取凭据的凭据提供程序：

1. 凭据将提取从 NuGet 配置文件 (使用内置`SettingsCredentialProvider`)。
1. 如果包源位于 Visual Studio Team Services，`VisualStudioAccountProvider`将使用。
1. 将按顺序尝试所有其他插件的凭据提供程序。
1. 如果已不获取任何凭据，用户将提示输入凭据使用标准的基本身份验证对话框。

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>实现 IVsCredentialProvider.GetCredentialsAsync

若要创建 Visual Studio 的 NuGet 凭据提供程序，创建一个公开公共 MEF 导出实现的 Visual Studio 扩展`IVsCredentialProvider`键入，并遵循下面所述的原则。

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

在找不到示例实现[VsCredentialProvider 示例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)。

Visual Studio 的每个 NuGet 凭据提供程序必须：

1. 确定是否可以在启动凭据获取之前目标 uri 提供凭据。 如果提供程序无法提供凭据的目标的源，则它应返回`null`。
1. 如果提供程序对目标 uri，无法处理请求，但不能提供的凭据，则应引发异常。

用于 Visual Studio 的自定义 NuGet 凭据提供程序必须实现`IVsCredentialProvider`中提供界面[NuGet.VisualStudio 包](https://www.nuget.org/packages/NuGet.VisualStudio/)。

#### <a name="getcredentialasync"></a>GetCredentialAsync

| 输入的参数 |描述|
| ----------------|-----------|
| Uri uri | 正在为其请求凭据是包源 Uri。|
| IWebProxy 代理 | 在网络上进行通信时要使用的 web 代理。 如果不没有配置任何代理身份验证，则为 null。 |
| bool isProxyRequest | 如果此请求是以获取代理身份验证的凭据，则为 true。 如果实现对获取代理凭据无效，则应返回 null。 |
| bool isRetry | 如果凭据已以前请求过此 uri，但提供的凭据不允许授权的访问，则为 true。 |
| 非交互式 bool | 如果为 true，则凭据提供程序必须取消所有用户提示，并改为使用默认值。 |
| CancellationToken cancellationToken | 此取消标记应检查以确定操作要求输入凭据已被取消。 |

**返回值**： 凭据对象实现[`System.Net.ICredentials`接口](/dotnet/api/system.net.icredentials?view=netstandard-2.0)。
