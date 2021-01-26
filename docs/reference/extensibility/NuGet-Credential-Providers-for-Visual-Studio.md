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
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="c9244-103">在 Visual Studio 中通过 NuGet 凭据提供程序对源进行身份验证</span><span class="sxs-lookup"><span data-stu-id="c9244-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="c9244-104">NuGet Visual Studio 扩展 3.6 + 支持凭据提供程序，这些提供程序允许 NuGet 使用经过身份验证的源。</span><span class="sxs-lookup"><span data-stu-id="c9244-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="c9244-105">安装适用于 Visual Studio 的 NuGet 凭据提供程序后，NuGet Visual Studio 扩展会根据需要自动获取和刷新经过身份验证的源的凭据。</span><span class="sxs-lookup"><span data-stu-id="c9244-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="c9244-106">可在 [VsCredentialProvider 示例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)中找到示例实现。</span><span class="sxs-lookup"><span data-stu-id="c9244-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="c9244-107">在 Visual Studio 中，NuGet 使用内部， `VsCredentialProviderImporter` 后者还会扫描插件凭据提供程序。</span><span class="sxs-lookup"><span data-stu-id="c9244-107">Within Visual Studio, NuGet uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="c9244-108">这些插件凭据提供程序必须可被发现为类型的 MEF 导出 `IVsCredentialProvider` 。</span><span class="sxs-lookup"><span data-stu-id="c9244-108">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="c9244-109">从 Visual Studio 中的 4.8 + NuGet 开始，还支持新的跨平台身份验证插件，但出于性能方面的原因，不建议采用这些方法。</span><span class="sxs-lookup"><span data-stu-id="c9244-109">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="c9244-110">用于 Visual Studio 的 NuGet 凭据提供程序必须安装为常规 Visual Studio 扩展，并需要 [Visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="c9244-110">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="c9244-111">用于 Visual Studio 的 NuGet 凭据提供程序仅适用于 Visual Studio 中 (dotnet restore 或 nuget.exe) 。</span><span class="sxs-lookup"><span data-stu-id="c9244-111">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="c9244-112">有关 nuget.exe 的凭据提供程序，请参阅 [nuget.exe 凭据提供程序](nuget-exe-Credential-providers.md)。</span><span class="sxs-lookup"><span data-stu-id="c9244-112">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="c9244-113">对于 dotnet 和 msbuild 中的凭据提供程序，请参阅 [NuGet 跨平台插件](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="c9244-113">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="c9244-114">为 Visual Studio 创建 NuGet 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="c9244-114">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="c9244-115">NuGet Visual Studio 扩展 3.6 + 实现了用于获取凭据的内部 CredentialService。</span><span class="sxs-lookup"><span data-stu-id="c9244-115">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="c9244-116">CredentialService 包含内置和插件凭据提供程序的列表。</span><span class="sxs-lookup"><span data-stu-id="c9244-116">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="c9244-117">每个提供程序按顺序尝试，直到获取凭据。</span><span class="sxs-lookup"><span data-stu-id="c9244-117">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="c9244-118">获取凭据时，凭据服务将按以下顺序尝试凭据提供程序，获取凭据后立即停止：</span><span class="sxs-lookup"><span data-stu-id="c9244-118">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="c9244-119">将使用内置)  (从 NuGet 配置文件中提取凭据 `SettingsCredentialProvider` 。</span><span class="sxs-lookup"><span data-stu-id="c9244-119">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="c9244-120">如果包源位于 Visual Studio Team Services 上，则 `VisualStudioAccountProvider` 将使用。</span><span class="sxs-lookup"><span data-stu-id="c9244-120">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="c9244-121">将按顺序尝试所有其他插件 Visual Studio 凭据提供程序。</span><span class="sxs-lookup"><span data-stu-id="c9244-121">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="c9244-122">尝试按顺序使用所有 NuGet 跨平台凭据提供程序。</span><span class="sxs-lookup"><span data-stu-id="c9244-122">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="c9244-123">如果尚未获取任何凭据，则系统会提示用户使用标准的基本身份验证对话框来输入凭据。</span><span class="sxs-lookup"><span data-stu-id="c9244-123">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="c9244-124">实现 IVsCredentialProvider. GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="c9244-124">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="c9244-125">若要为 Visual Studio 创建 NuGet 凭据提供程序，请创建一个 Visual Studio 扩展，该扩展公开实现该类型的公共 MEF 导出 `IVsCredentialProvider` ，并遵循下面所述的原则。</span><span class="sxs-lookup"><span data-stu-id="c9244-125">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="c9244-126">可在 [VsCredentialProvider 示例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)中找到示例实现。</span><span class="sxs-lookup"><span data-stu-id="c9244-126">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="c9244-127">适用于 Visual Studio 的每个 NuGet 凭据提供程序必须：</span><span class="sxs-lookup"><span data-stu-id="c9244-127">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="c9244-128">确定是否可以在启动凭据获取之前为目标 URI 提供凭据。</span><span class="sxs-lookup"><span data-stu-id="c9244-128">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="c9244-129">如果提供程序无法为目标源提供凭据，则它应返回 `null` 。</span><span class="sxs-lookup"><span data-stu-id="c9244-129">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="c9244-130">如果提供程序处理目标 URI 的请求，但无法提供凭据，则应引发异常。</span><span class="sxs-lookup"><span data-stu-id="c9244-130">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="c9244-131">Visual Studio 的自定义 NuGet 凭据提供程序必须实现 `IVsCredentialProvider` [VisualStudio 包](https://www.nuget.org/packages/NuGet.VisualStudio/)中提供的接口。</span><span class="sxs-lookup"><span data-stu-id="c9244-131">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="c9244-132">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="c9244-132">GetCredentialAsync</span></span>

| <span data-ttu-id="c9244-133">输入参数</span><span class="sxs-lookup"><span data-stu-id="c9244-133">Input Parameter</span></span> |<span data-ttu-id="c9244-134">说明</span><span class="sxs-lookup"><span data-stu-id="c9244-134">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="c9244-135">Uri uri</span><span class="sxs-lookup"><span data-stu-id="c9244-135">Uri uri</span></span> | <span data-ttu-id="c9244-136">正在为其请求凭据的包源 Uri。</span><span class="sxs-lookup"><span data-stu-id="c9244-136">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="c9244-137">IWebProxy 代理</span><span class="sxs-lookup"><span data-stu-id="c9244-137">IWebProxy proxy</span></span> | <span data-ttu-id="c9244-138">网络上通信时要使用的 Web 代理。</span><span class="sxs-lookup"><span data-stu-id="c9244-138">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="c9244-139">如果未配置代理身份验证，则为 Null。</span><span class="sxs-lookup"><span data-stu-id="c9244-139">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="c9244-140">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="c9244-140">bool isProxyRequest</span></span> | <span data-ttu-id="c9244-141">如果此请求将获取代理身份验证凭据，则为 True。</span><span class="sxs-lookup"><span data-stu-id="c9244-141">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="c9244-142">如果实现对于获取代理凭据无效，则应返回 null。</span><span class="sxs-lookup"><span data-stu-id="c9244-142">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="c9244-143">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="c9244-143">bool isRetry</span></span> | <span data-ttu-id="c9244-144">如果以前已为此 Uri 请求凭据，但提供的凭据不允许授权访问，则为 True。</span><span class="sxs-lookup"><span data-stu-id="c9244-144">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="c9244-145">bool 非交互式</span><span class="sxs-lookup"><span data-stu-id="c9244-145">bool nonInteractive</span></span> | <span data-ttu-id="c9244-146">如果为 true，则凭据提供程序必须禁止显示所有用户提示并改用默认值。</span><span class="sxs-lookup"><span data-stu-id="c9244-146">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="c9244-147">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="c9244-147">CancellationToken cancellationToken</span></span> | <span data-ttu-id="c9244-148">应检查此取消标记以确定请求凭据的操作是否已取消。</span><span class="sxs-lookup"><span data-stu-id="c9244-148">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="c9244-149">**返回值**：实现 [ `System.Net.ICredentials` 接口](/dotnet/api/system.net.icredentials?view=netstandard-2.0)的凭据对象。</span><span class="sxs-lookup"><span data-stu-id="c9244-149">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
