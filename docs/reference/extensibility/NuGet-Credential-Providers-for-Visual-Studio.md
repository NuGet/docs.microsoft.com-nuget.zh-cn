---
title: 用于 Visual Studio 的 NuGet 凭据提供程序
description: NuGet 凭据提供程序通过在 Visual Studio 扩展中实现 IVsCredentialProvider 接口馈送进行身份验证。
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: abe009fee5863c55a188f4d7c71ed0924dd067ff
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547949"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="dd71c-103">在 Visual Studio 中使用 NuGet 凭据提供程序的源进行身份验证</span><span class="sxs-lookup"><span data-stu-id="dd71c-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="dd71c-104">NuGet Visual Studio 扩展 3.6 + 支持可以使 NuGet 能够使用已验证的源的凭据提供程序。</span><span class="sxs-lookup"><span data-stu-id="dd71c-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="dd71c-105">安装 Visual Studio 的 NuGet 凭据提供程序后，NuGet Visual Studio 扩展将自动获取和刷新用于根据需要已验证的源的凭据。</span><span class="sxs-lookup"><span data-stu-id="dd71c-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="dd71c-106">示例实现可在[VsCredentialProvider 示例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)。</span><span class="sxs-lookup"><span data-stu-id="dd71c-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="dd71c-107">从开始 4.8 + 在 Visual Studio 中的 NuGet 支持，新的跨平台身份验证插件，但它们不是出于性能原因，建议的方法。</span><span class="sxs-lookup"><span data-stu-id="dd71c-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="dd71c-108">用于 Visual Studio 的 NuGet 凭据提供程序必须作为常规的 Visual Studio 扩展安装，并且需要[Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe)或更高版本。</span><span class="sxs-lookup"><span data-stu-id="dd71c-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="dd71c-109">用于 Visual Studio 的 NuGet 凭据提供程序仅适用于 Visual Studio 中 （不在 dotnet 还原或 nuget.exe）。</span><span class="sxs-lookup"><span data-stu-id="dd71c-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="dd71c-110">Nuget.exe 凭据提供程序，请参阅[nuget.exe 凭据提供程序](nuget-exe-Credential-providers.md)。</span><span class="sxs-lookup"><span data-stu-id="dd71c-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="dd71c-111">有关凭据 dotnet 和 msbuild 中的提供程序请参阅[NuGet 跨平台插件](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="dd71c-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="dd71c-112">Visual Studio 的可用 NuGet 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="dd71c-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="dd71c-113">没有内置于 Visual Studio NuGet 扩展的凭据提供程序以支持 Visual Studio Team Services。</span><span class="sxs-lookup"><span data-stu-id="dd71c-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="dd71c-114">NuGet Visual Studio 扩展使用内部`VsCredentialProviderImporter`这还扫描插件凭据提供程序。</span><span class="sxs-lookup"><span data-stu-id="dd71c-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="dd71c-115">这些插件凭据提供程序必须能够发现作为导出类型的 MEF `IVsCredentialProvider`。</span><span class="sxs-lookup"><span data-stu-id="dd71c-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="dd71c-116">可用的插件凭据提供程序包括：</span><span class="sxs-lookup"><span data-stu-id="dd71c-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="dd71c-117">适用于 Visual Studio 2017 的 MyGet 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="dd71c-117">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="dd71c-118">创建 Visual Studio 的 NuGet 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="dd71c-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="dd71c-119">NuGet Visual Studio 扩展 3.6 + 实现内部 CredentialService 用来获取凭据。</span><span class="sxs-lookup"><span data-stu-id="dd71c-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="dd71c-120">CredentialService 具有内置和插件凭据提供程序的列表。</span><span class="sxs-lookup"><span data-stu-id="dd71c-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="dd71c-121">获取凭据之前，将按顺序尝试每个提供程序。</span><span class="sxs-lookup"><span data-stu-id="dd71c-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="dd71c-122">在凭据获取凭据服务将尝试按以下顺序停止立即获取凭据的凭据提供程序：</span><span class="sxs-lookup"><span data-stu-id="dd71c-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="dd71c-123">NuGet 配置文件中提取的凭据 (使用内置`SettingsCredentialProvider`)。</span><span class="sxs-lookup"><span data-stu-id="dd71c-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="dd71c-124">如果包源是在 Visual Studio Team Services`VisualStudioAccountProvider`将使用。</span><span class="sxs-lookup"><span data-stu-id="dd71c-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="dd71c-125">将按顺序尝试所有其他插件 Visual Studio 的凭据提供程序。</span><span class="sxs-lookup"><span data-stu-id="dd71c-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="dd71c-126">尝试按顺序使用跨平台的凭据提供程序的所有 NuGet。</span><span class="sxs-lookup"><span data-stu-id="dd71c-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="dd71c-127">如果已获取不使用凭据，将凭据使用标准的基本身份验证对话框提示用户。</span><span class="sxs-lookup"><span data-stu-id="dd71c-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="dd71c-128">实现 IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="dd71c-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="dd71c-129">若要创建 Visual Studio 的 NuGet 凭据提供程序，创建一个 Visual Studio 扩展，公开公共 MEF 导出实现`IVsCredentialProvider`类型，并遵循下面所述的原则。</span><span class="sxs-lookup"><span data-stu-id="dd71c-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="dd71c-130">示例实现可在[VsCredentialProvider 示例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)。</span><span class="sxs-lookup"><span data-stu-id="dd71c-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="dd71c-131">Visual Studio 的每个 NuGet 凭据提供程序必须：</span><span class="sxs-lookup"><span data-stu-id="dd71c-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="dd71c-132">确定是否它可提供凭据的目标 URI 启动凭据获取之前。</span><span class="sxs-lookup"><span data-stu-id="dd71c-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="dd71c-133">如果提供商无法提供凭据的目标的源，则它应返回`null`。</span><span class="sxs-lookup"><span data-stu-id="dd71c-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="dd71c-134">如果提供程序无法处理请求的目标 URI，但不能提供的凭据，则应引发异常。</span><span class="sxs-lookup"><span data-stu-id="dd71c-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="dd71c-135">Visual Studio 的自定义 NuGet 凭据提供程序必须实现`IVsCredentialProvider`中提供的接口[NuGet.VisualStudio 包](https://www.nuget.org/packages/NuGet.VisualStudio/)。</span><span class="sxs-lookup"><span data-stu-id="dd71c-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="dd71c-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="dd71c-136">GetCredentialAsync</span></span>

| <span data-ttu-id="dd71c-137">输入的参数</span><span class="sxs-lookup"><span data-stu-id="dd71c-137">Input Parameter</span></span> |<span data-ttu-id="dd71c-138">描述</span><span class="sxs-lookup"><span data-stu-id="dd71c-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="dd71c-139">Uri uri</span><span class="sxs-lookup"><span data-stu-id="dd71c-139">Uri uri</span></span> | <span data-ttu-id="dd71c-140">正在为其请求凭据包源 Uri。</span><span class="sxs-lookup"><span data-stu-id="dd71c-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="dd71c-141">IWebProxy 代理</span><span class="sxs-lookup"><span data-stu-id="dd71c-141">IWebProxy proxy</span></span> | <span data-ttu-id="dd71c-142">若要在网络上通信时使用的 web 代理。</span><span class="sxs-lookup"><span data-stu-id="dd71c-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="dd71c-143">如果不没有配置任何代理身份验证，则为 null。</span><span class="sxs-lookup"><span data-stu-id="dd71c-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="dd71c-144">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="dd71c-144">bool isProxyRequest</span></span> | <span data-ttu-id="dd71c-145">如果此请求获取代理身份验证凭据，则为 true。</span><span class="sxs-lookup"><span data-stu-id="dd71c-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="dd71c-146">如果实现用于获取代理凭据无效，应返回 null。</span><span class="sxs-lookup"><span data-stu-id="dd71c-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="dd71c-147">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="dd71c-147">bool isRetry</span></span> | <span data-ttu-id="dd71c-148">如果凭据以前请求过，此 Uri，但提供的凭据不允许经授权的访问权限，则为 true。</span><span class="sxs-lookup"><span data-stu-id="dd71c-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="dd71c-149">非交互式 bool</span><span class="sxs-lookup"><span data-stu-id="dd71c-149">bool nonInteractive</span></span> | <span data-ttu-id="dd71c-150">如果为 true，则必须取消所有用户提示的凭据提供程序并将其改为使用默认值。</span><span class="sxs-lookup"><span data-stu-id="dd71c-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="dd71c-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="dd71c-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="dd71c-152">应检查此取消标记，以确定操作要求凭据已被取消。</span><span class="sxs-lookup"><span data-stu-id="dd71c-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="dd71c-153">**返回值**： 凭据对象实现[`System.Net.ICredentials`接口](/dotnet/api/system.net.icredentials?view=netstandard-2.0)。</span><span class="sxs-lookup"><span data-stu-id="dd71c-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
