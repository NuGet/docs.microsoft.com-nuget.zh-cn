---
title: "NuGet 对 Visual Studio 的凭据提供程序 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 的凭据提供程序进行身份验证源通过在 Visual Studio 扩展中实现该 IVsCredentialProvider 接口。"
keywords: "NuGet 的凭据提供程序，使用的源进行身份验证，使用 NuGet visual studio 扩展库进行身份验证"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ff143526c814c69f1a133a62c1ad1a8f5fbedd60
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2018
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="77e61-104">NuGet 的凭据提供程序与 Visual Studio 中的源进行身份验证</span><span class="sxs-lookup"><span data-stu-id="77e61-104">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="77e61-105">NuGet Visual Studio 扩展中 3.6 + 支持启用 NuGet 用于经过身份验证的源的凭据提供程序。</span><span class="sxs-lookup"><span data-stu-id="77e61-105">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="77e61-106">安装 Visual Studio 的 NuGet 凭据提供程序后，NuGet Visual Studio 扩展将自动获取并刷新根据需要经过身份验证源的凭据。</span><span class="sxs-lookup"><span data-stu-id="77e61-106">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="77e61-107">在找不到示例实现[VsCredentialProvider 示例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)。</span><span class="sxs-lookup"><span data-stu-id="77e61-107">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

> [!Note]
> <span data-ttu-id="77e61-108">NuGet 对 Visual Studio 的凭据提供程序必须安装为正则 Visual Studio 扩展，将需要[Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) （当前为预览版） 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="77e61-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (currently in preview) or above.</span></span>
>
> <span data-ttu-id="77e61-109">NuGet 对 Visual Studio 的凭据提供程序仅适用于 Visual Studio 中 （不在 dotnet 还原或 nuget.exe）。</span><span class="sxs-lookup"><span data-stu-id="77e61-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="77e61-110">有关通过 nuget.exe 使用凭据提供程序，请参阅[nuget.exe 凭据提供程序](nuget-exe-Credential-providers.md)。</span><span class="sxs-lookup"><span data-stu-id="77e61-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="77e61-111">Visual Studio 的可用 NuGet 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="77e61-111">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="77e61-112">没有内置于 Visual Studio NuGet 扩展凭据提供程序以支持 Visual Studio Team Services。</span><span class="sxs-lookup"><span data-stu-id="77e61-112">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="77e61-113">NuGet Visual Studio 扩展使用内部`VsCredentialProviderImporter`这还扫描插件凭据提供程序。</span><span class="sxs-lookup"><span data-stu-id="77e61-113">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="77e61-114">这些插件的凭据提供程序必须能够发现作为类型 MEF 导出`IVsCredentialProvider`。</span><span class="sxs-lookup"><span data-stu-id="77e61-114">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="77e61-115">可用的插件凭据提供程序包括：</span><span class="sxs-lookup"><span data-stu-id="77e61-115">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="77e61-116">适用于 Visual Studio 2017 的 MyGet 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="77e61-116">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="77e61-117">创建 Visual Studio 的 NuGet 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="77e61-117">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="77e61-118">NuGet Visual Studio 扩展中 3.6 + 实现内部 CredentialService 用于获取凭据。</span><span class="sxs-lookup"><span data-stu-id="77e61-118">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="77e61-119">CredentialService 具有内置和插件的凭据提供程序的列表。</span><span class="sxs-lookup"><span data-stu-id="77e61-119">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="77e61-120">每个提供程序是按顺序尝试，直到获取凭据。</span><span class="sxs-lookup"><span data-stu-id="77e61-120">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="77e61-121">在凭据获取凭据服务将尝试按以下顺序，停止就会立即获取凭据的凭据提供程序：</span><span class="sxs-lookup"><span data-stu-id="77e61-121">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="77e61-122">凭据将提取从 NuGet 配置文件 (使用内置`SettingsCredentialProvider`)。</span><span class="sxs-lookup"><span data-stu-id="77e61-122">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="77e61-123">如果包源位于 Visual Studio Team Services，`VisualStudioAccountProvider`将使用。</span><span class="sxs-lookup"><span data-stu-id="77e61-123">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="77e61-124">将按顺序尝试所有其他插件的凭据提供程序。</span><span class="sxs-lookup"><span data-stu-id="77e61-124">All other plug-in credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="77e61-125">如果已不获取任何凭据，用户将提示输入凭据使用标准的基本身份验证对话框。</span><span class="sxs-lookup"><span data-stu-id="77e61-125">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="77e61-126">实现 IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="77e61-126">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="77e61-127">若要创建 Visual Studio 的 NuGet 凭据提供程序，创建一个公开公共 MEF 导出实现的 Visual Studio 扩展`IVsCredentialProvider`键入，并遵循下面所述的原则。</span><span class="sxs-lookup"><span data-stu-id="77e61-127">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="77e61-128">在找不到示例实现[VsCredentialProvider 示例](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)。</span><span class="sxs-lookup"><span data-stu-id="77e61-128">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="77e61-129">Visual Studio 的每个 NuGet 凭据提供程序必须：</span><span class="sxs-lookup"><span data-stu-id="77e61-129">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="77e61-130">确定是否可以在启动凭据获取之前目标 uri 提供凭据。</span><span class="sxs-lookup"><span data-stu-id="77e61-130">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="77e61-131">如果提供程序无法提供凭据的目标的源，则它应返回`null`。</span><span class="sxs-lookup"><span data-stu-id="77e61-131">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="77e61-132">如果提供程序对目标 uri，无法处理请求，但不能提供的凭据，则应引发异常。</span><span class="sxs-lookup"><span data-stu-id="77e61-132">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="77e61-133">用于 Visual Studio 的自定义 NuGet 凭据提供程序必须实现`IVsCredentialProvider`中提供界面[NuGet.VisualStudio 包](https://www.nuget.org/packages/NuGet.VisualStudio/)。</span><span class="sxs-lookup"><span data-stu-id="77e61-133">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="77e61-134">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="77e61-134">GetCredentialAsync</span></span>

| <span data-ttu-id="77e61-135">输入的参数</span><span class="sxs-lookup"><span data-stu-id="77e61-135">Input Parameter</span></span> |<span data-ttu-id="77e61-136">描述</span><span class="sxs-lookup"><span data-stu-id="77e61-136">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="77e61-137">Uri uri</span><span class="sxs-lookup"><span data-stu-id="77e61-137">Uri uri</span></span> | <span data-ttu-id="77e61-138">正在为其请求凭据是包源 Uri。</span><span class="sxs-lookup"><span data-stu-id="77e61-138">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="77e61-139">IWebProxy 代理</span><span class="sxs-lookup"><span data-stu-id="77e61-139">IWebProxy proxy</span></span> | <span data-ttu-id="77e61-140">在网络上进行通信时要使用的 web 代理。</span><span class="sxs-lookup"><span data-stu-id="77e61-140">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="77e61-141">如果不没有配置任何代理身份验证，则为 null。</span><span class="sxs-lookup"><span data-stu-id="77e61-141">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="77e61-142">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="77e61-142">bool isProxyRequest</span></span> | <span data-ttu-id="77e61-143">如果此请求是以获取代理身份验证的凭据，则为 true。</span><span class="sxs-lookup"><span data-stu-id="77e61-143">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="77e61-144">如果实现对获取代理凭据无效，则应返回 null。</span><span class="sxs-lookup"><span data-stu-id="77e61-144">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="77e61-145">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="77e61-145">bool isRetry</span></span> | <span data-ttu-id="77e61-146">如果凭据已以前请求过此 uri，但提供的凭据不允许授权的访问，则为 true。</span><span class="sxs-lookup"><span data-stu-id="77e61-146">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="77e61-147">非交互式 bool</span><span class="sxs-lookup"><span data-stu-id="77e61-147">bool nonInteractive</span></span> | <span data-ttu-id="77e61-148">如果为 true，则凭据提供程序必须取消所有用户提示，并改为使用默认值。</span><span class="sxs-lookup"><span data-stu-id="77e61-148">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="77e61-149">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="77e61-149">CancellationToken cancellationToken</span></span> | <span data-ttu-id="77e61-150">此取消标记应检查以确定操作要求输入凭据已被取消。</span><span class="sxs-lookup"><span data-stu-id="77e61-150">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="77e61-151">**返回值**： 凭据对象实现[`System.Net.ICredentials`接口](/dotnet/api/system.net.icredentials?view=netstandard-2.0)。</span><span class="sxs-lookup"><span data-stu-id="77e61-151">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
