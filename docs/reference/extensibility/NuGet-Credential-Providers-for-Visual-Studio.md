---
title: 用于 Visual Studio 的 NuGet 凭据提供程序
description: 通过在 Visual Studio 扩展中实现 IVsCredentialProvider 接口，NuGet 凭据提供程序对源进行身份验证。
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 906d07eb22599eb423b00300954ff2601dd33369
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383546"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="5f90c-103">在 Visual Studio 中通过 NuGet 凭据提供程序对源进行身份验证</span><span class="sxs-lookup"><span data-stu-id="5f90c-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="5f90c-104">NuGet Visual Studio 扩展 3.6 + 支持凭据提供程序，这些提供程序允许 NuGet 使用经过身份验证的源。</span><span class="sxs-lookup"><span data-stu-id="5f90c-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="5f90c-105">安装适用于 Visual Studio 的 NuGet 凭据提供程序后，NuGet Visual Studio 扩展会根据需要自动获取和刷新经过身份验证的源的凭据。</span><span class="sxs-lookup"><span data-stu-id="5f90c-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="5f90c-106">可在[VsCredentialProvider 示例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)中找到示例实现。</span><span class="sxs-lookup"><span data-stu-id="5f90c-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="5f90c-107">从 Visual Studio 中的 4.8 + NuGet 开始，还支持新的跨平台身份验证插件，但出于性能方面的原因，不建议采用这些方法。</span><span class="sxs-lookup"><span data-stu-id="5f90c-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="5f90c-108">用于 Visual Studio 的 NuGet 凭据提供程序必须安装为常规 Visual Studio 扩展，并需要[Visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe)或更高版本。</span><span class="sxs-lookup"><span data-stu-id="5f90c-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="5f90c-109">用于 Visual Studio 的 NuGet 凭据提供程序仅适用于 Visual Studio （不在 dotnet restore 或 nuget.exe 中）。</span><span class="sxs-lookup"><span data-stu-id="5f90c-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="5f90c-110">有关 nuget.exe 的凭据提供程序，请参阅[Nuget.exe 凭据提供程序](nuget-exe-Credential-providers.md)。</span><span class="sxs-lookup"><span data-stu-id="5f90c-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="5f90c-111">对于 dotnet 和 msbuild 中的凭据提供程序，请参阅[NuGet 跨平台插件](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="5f90c-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="5f90c-112">适用于 Visual Studio 的 NuGet 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="5f90c-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="5f90c-113">Visual Studio NuGet 扩展中内置了一个凭据提供程序，可支持 Visual Studio Team Services。</span><span class="sxs-lookup"><span data-stu-id="5f90c-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="5f90c-114">NuGet Visual Studio 扩展使用内部 `VsCredentialProviderImporter`，这也会扫描插件凭据提供程序。</span><span class="sxs-lookup"><span data-stu-id="5f90c-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="5f90c-115">这些插件凭据提供程序必须可被视为 `IVsCredentialProvider`类型的 MEF 导出。</span><span class="sxs-lookup"><span data-stu-id="5f90c-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="5f90c-116">可用插件凭据提供程序包括：</span><span class="sxs-lookup"><span data-stu-id="5f90c-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="5f90c-117">适用于 Visual Studio 的 MyGet 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="5f90c-117">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="5f90c-118">为 Visual Studio 创建 NuGet 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="5f90c-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="5f90c-119">NuGet Visual Studio 扩展 3.6 + 实现了用于获取凭据的内部 CredentialService。</span><span class="sxs-lookup"><span data-stu-id="5f90c-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="5f90c-120">CredentialService 包含内置和插件凭据提供程序的列表。</span><span class="sxs-lookup"><span data-stu-id="5f90c-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="5f90c-121">每个提供程序按顺序尝试，直到获取凭据。</span><span class="sxs-lookup"><span data-stu-id="5f90c-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="5f90c-122">获取凭据时，凭据服务将按以下顺序尝试凭据提供程序，获取凭据后立即停止：</span><span class="sxs-lookup"><span data-stu-id="5f90c-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="5f90c-123">将从 NuGet 配置文件（使用内置 `SettingsCredentialProvider`）中提取凭据。</span><span class="sxs-lookup"><span data-stu-id="5f90c-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="5f90c-124">如果包源位于 Visual Studio Team Services 上，则将使用 `VisualStudioAccountProvider`。</span><span class="sxs-lookup"><span data-stu-id="5f90c-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="5f90c-125">将按顺序尝试所有其他插件 Visual Studio 凭据提供程序。</span><span class="sxs-lookup"><span data-stu-id="5f90c-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="5f90c-126">尝试按顺序使用所有 NuGet 跨平台凭据提供程序。</span><span class="sxs-lookup"><span data-stu-id="5f90c-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="5f90c-127">如果尚未获取任何凭据，则系统会提示用户使用标准的基本身份验证对话框来输入凭据。</span><span class="sxs-lookup"><span data-stu-id="5f90c-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="5f90c-128">实现 IVsCredentialProvider. GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="5f90c-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="5f90c-129">若要为 Visual Studio 创建 NuGet 凭据提供程序，请创建一个 Visual Studio 扩展，该扩展公开实现 `IVsCredentialProvider` 类型的公共 MEF 导出，并遵循下面所述的原则。</span><span class="sxs-lookup"><span data-stu-id="5f90c-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="5f90c-130">可在[VsCredentialProvider 示例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)中找到示例实现。</span><span class="sxs-lookup"><span data-stu-id="5f90c-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="5f90c-131">适用于 Visual Studio 的每个 NuGet 凭据提供程序必须：</span><span class="sxs-lookup"><span data-stu-id="5f90c-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="5f90c-132">确定是否可以在启动凭据获取之前为目标 URI 提供凭据。</span><span class="sxs-lookup"><span data-stu-id="5f90c-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="5f90c-133">如果提供程序无法为目标源提供凭据，则它应返回 `null`。</span><span class="sxs-lookup"><span data-stu-id="5f90c-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="5f90c-134">如果提供程序处理目标 URI 的请求，但无法提供凭据，则应引发异常。</span><span class="sxs-lookup"><span data-stu-id="5f90c-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="5f90c-135">Visual Studio 的自定义 NuGet 凭据提供程序必须实现[VisualStudio 包](https://www.nuget.org/packages/NuGet.VisualStudio/)中提供的 `IVsCredentialProvider` 接口。</span><span class="sxs-lookup"><span data-stu-id="5f90c-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="5f90c-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="5f90c-136">GetCredentialAsync</span></span>

| <span data-ttu-id="5f90c-137">输入参数</span><span class="sxs-lookup"><span data-stu-id="5f90c-137">Input Parameter</span></span> |<span data-ttu-id="5f90c-138">描述</span><span class="sxs-lookup"><span data-stu-id="5f90c-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="5f90c-139">Uri uri</span><span class="sxs-lookup"><span data-stu-id="5f90c-139">Uri uri</span></span> | <span data-ttu-id="5f90c-140">正在为其请求凭据的包源 Uri。</span><span class="sxs-lookup"><span data-stu-id="5f90c-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="5f90c-141">IWebProxy 代理</span><span class="sxs-lookup"><span data-stu-id="5f90c-141">IWebProxy proxy</span></span> | <span data-ttu-id="5f90c-142">网络上通信时要使用的 Web 代理。</span><span class="sxs-lookup"><span data-stu-id="5f90c-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="5f90c-143">如果未配置代理身份验证，则为 Null。</span><span class="sxs-lookup"><span data-stu-id="5f90c-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="5f90c-144">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="5f90c-144">bool isProxyRequest</span></span> | <span data-ttu-id="5f90c-145">如果此请求将获取代理身份验证凭据，则为 True。</span><span class="sxs-lookup"><span data-stu-id="5f90c-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="5f90c-146">如果实现对于获取代理凭据无效，则应返回 null。</span><span class="sxs-lookup"><span data-stu-id="5f90c-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="5f90c-147">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="5f90c-147">bool isRetry</span></span> | <span data-ttu-id="5f90c-148">如果以前已为此 Uri 请求凭据，但提供的凭据不允许授权访问，则为 True。</span><span class="sxs-lookup"><span data-stu-id="5f90c-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="5f90c-149">bool 非交互式</span><span class="sxs-lookup"><span data-stu-id="5f90c-149">bool nonInteractive</span></span> | <span data-ttu-id="5f90c-150">如果为 true，则凭据提供程序必须禁止显示所有用户提示并改用默认值。</span><span class="sxs-lookup"><span data-stu-id="5f90c-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="5f90c-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="5f90c-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="5f90c-152">应检查此取消标记以确定请求凭据的操作是否已取消。</span><span class="sxs-lookup"><span data-stu-id="5f90c-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="5f90c-153">**返回值**：实现[`System.Net.ICredentials` 接口](/dotnet/api/system.net.icredentials?view=netstandard-2.0)的凭据对象。</span><span class="sxs-lookup"><span data-stu-id="5f90c-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
