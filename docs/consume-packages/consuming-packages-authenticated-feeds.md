---
title: 使用经过身份验证的源中的包
description: 在所有 NuGet 客户端方案中使用经过身份验证的源中的包
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: e76fefaf4d3c86aa15cf279090c0adb8ed779aab
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901507"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="3be3e-103">使用经过身份验证的源中的包</span><span class="sxs-lookup"><span data-stu-id="3be3e-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="3be3e-104">除了 nuget.org [公共源](https://api.nuget.org/v3/index.json)外，NuGet 客户端能够与文件源和专用 http 源交互。</span><span class="sxs-lookup"><span data-stu-id="3be3e-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="3be3e-105">要向专用 http 源进行身份验证，可以使用以下两种方式：</span><span class="sxs-lookup"><span data-stu-id="3be3e-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="3be3e-106">在 [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials) 中添加凭据</span><span class="sxs-lookup"><span data-stu-id="3be3e-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="3be3e-107">根据所用的客户端，使用一种扩展性模型进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="3be3e-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="3be3e-108">NuGet 客户端的身份验证扩展性</span><span class="sxs-lookup"><span data-stu-id="3be3e-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="3be3e-109">对于各种 NuGet 客户端，专用源提供程序本身负责进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="3be3e-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="3be3e-110">所有 NuGet 客户端都具有支持此方式的扩展性方法。</span><span class="sxs-lookup"><span data-stu-id="3be3e-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="3be3e-111">这些方法包括 Visual Studio 扩展或可与 NuGet 通信以检索凭据的插件。</span><span class="sxs-lookup"><span data-stu-id="3be3e-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="3be3e-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3be3e-112">Visual Studio</span></span>

<span data-ttu-id="3be3e-113">在 Visual Studio 中，NuGet 公开了一个源提供程序可以实现并向其客户提供的接口。</span><span class="sxs-lookup"><span data-stu-id="3be3e-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="3be3e-114">如需了解详情，请参阅介绍[如何创建 Visual Studio 凭据提供程序](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)的文档。</span><span class="sxs-lookup"><span data-stu-id="3be3e-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="3be3e-115">Visual Studio 的可用 NuGet 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="3be3e-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="3be3e-116">Visual Studio 中有一个支持 Azure DevOps 的内置凭据提供程序。</span><span class="sxs-lookup"><span data-stu-id="3be3e-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="3be3e-117">可用的插件凭据提供程序包括：</span><span class="sxs-lookup"><span data-stu-id="3be3e-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="3be3e-118">适用于 Visual Studio 的 MyGet 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="3be3e-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="3be3e-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="3be3e-119">nuget.exe</span></span>

<span data-ttu-id="3be3e-120">当 `nuget.exe` 需要凭据来向源进行身份验证时，它会采用以下方式查找凭据：</span><span class="sxs-lookup"><span data-stu-id="3be3e-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="3be3e-121">在 `NuGet.config` 文件中查找凭据。</span><span class="sxs-lookup"><span data-stu-id="3be3e-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="3be3e-122">使用 V2 插件凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="3be3e-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="3be3e-123">使用 V1 插件凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="3be3e-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="3be3e-124">然后，NuGet 会提示用户在命令行上提供凭据。</span><span class="sxs-lookup"><span data-stu-id="3be3e-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="3be3e-125">nuget.exe 和 V2 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="3be3e-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="3be3e-126">在 `4.8` 版中，NuGet 定义了一种新的身份验证插件机制（以下称为 V2 凭据提供程序）。</span><span class="sxs-lookup"><span data-stu-id="3be3e-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="3be3e-127">若要发现和安装这些提供程序，请参阅 [NuGet 跨平台插件](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。</span><span class="sxs-lookup"><span data-stu-id="3be3e-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="3be3e-128">nuget.exe 和 V1 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="3be3e-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="3be3e-129">在 `3.3` 版本中，NuGet 引入了首版身份验证插件。</span><span class="sxs-lookup"><span data-stu-id="3be3e-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="3be3e-130">若要发现和安装这些提供程序，请参阅 [nuget.exe 凭据提供程序](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span><span class="sxs-lookup"><span data-stu-id="3be3e-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="3be3e-131">nuget.exe 的可用凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="3be3e-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="3be3e-132">[Azure DevOps V2 凭据提供程序](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later)或 [Azure Artifacts 凭据提供程序](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="3be3e-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="3be3e-133">对于 Visual Studio 2017 15.9 及更高版本，Azure DevOps 凭据提供程序捆绑在 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="3be3e-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="3be3e-134">如果 `nuget.exe` 使用来自该特定 Visual Studio 工具集的 MSBuild，则系统会自动发现该插件。</span><span class="sxs-lookup"><span data-stu-id="3be3e-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="3be3e-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="3be3e-135">dotnet.exe</span></span>

<span data-ttu-id="3be3e-136">当 `dotnet.exe` 需要凭据来向源进行身份验证时，它会采用以下方式查找凭据：</span><span class="sxs-lookup"><span data-stu-id="3be3e-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="3be3e-137">在 `NuGet.config` 文件中查找凭据。</span><span class="sxs-lookup"><span data-stu-id="3be3e-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="3be3e-138">使用 V2 插件凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="3be3e-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="3be3e-139">默认情况下，`dotnet.exe` 不是交互式的，因此可能需要传递 `--interactive` 标志，将工具指向用于身份验证的程序块。</span><span class="sxs-lookup"><span data-stu-id="3be3e-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="3be3e-140">dotnet.exe 和 V2 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="3be3e-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="3be3e-141">在 SDK `2.2.100` 版本中，NuGet 定义了一种适用于所有客户端的身份验证插件机制。</span><span class="sxs-lookup"><span data-stu-id="3be3e-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="3be3e-142">若要发现和安装这些提供程序，请参阅 [NuGet 跨平台插件](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。</span><span class="sxs-lookup"><span data-stu-id="3be3e-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="3be3e-143">dotnet.exe 的可用凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="3be3e-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="3be3e-144">Azure Artifacts 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="3be3e-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="3be3e-145">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="3be3e-145">MSBuild.exe</span></span>

<span data-ttu-id="3be3e-146">当 `MSBuild.exe` 需要凭据来向源进行身份验证时，它会采用以下方式查找凭据：</span><span class="sxs-lookup"><span data-stu-id="3be3e-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="3be3e-147">在 `NuGet.config` 文件中查找凭据</span><span class="sxs-lookup"><span data-stu-id="3be3e-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="3be3e-148">使用 V2 插件凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="3be3e-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="3be3e-149">默认情况下，`MSBuild.exe` 不是交互式的，因此你可能需要设置 `/p:NuGetInteractive=true` 属性，将工具指向用于身份验证的程序块。</span><span class="sxs-lookup"><span data-stu-id="3be3e-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="3be3e-150">MSBuild.exe 和 V2 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="3be3e-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="3be3e-151">在 Visual Studio 2019 Update 9 中，NuGet 定义了一种适用于所有客户端的身份验证插件机制。</span><span class="sxs-lookup"><span data-stu-id="3be3e-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="3be3e-152">若要发现和安装这些提供程序，请参阅 [NuGet 跨平台插件](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)。</span><span class="sxs-lookup"><span data-stu-id="3be3e-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="3be3e-153">MSBuild.exe 的可用凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="3be3e-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="3be3e-154">Azure Artifacts 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="3be3e-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="3be3e-155">对于 Visual Studio 2017 Update 9 及更高版本，Azure DevOps 凭据提供程序捆绑在 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="3be3e-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="3be3e-156">无需执行其他步骤。</span><span class="sxs-lookup"><span data-stu-id="3be3e-156">No additional steps are required.</span></span>
