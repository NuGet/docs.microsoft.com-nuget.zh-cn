---
title: 用于发现 nuget.exe 版本的工具
description: 的端点
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: a186db9727bdfd1b55bf73a1f29283352555dede
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611022"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="4c34e-103">用于发现 nuget.exe 版本的工具</span><span class="sxs-lookup"><span data-stu-id="4c34e-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="4c34e-104">目前，有几种方法可以在计算机上以脚本方式获取 nuget.exe 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="4c34e-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="4c34e-105">例如，你可以从 nuget.org 下载并提取[`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/)包。这种方法有一定的复杂性，因为它要求您已经具有 nuget.exe （对于 `nuget.exe install`），或者必须使用基本解压缩工具来解压缩 nupkg，并在内部查找二进制文件。</span><span class="sxs-lookup"><span data-stu-id="4c34e-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="4c34e-106">如果你已有 nuget.exe，还可以使用 `nuget.exe update -self`，但这也需要具有 nuget.exe 的现有副本。</span><span class="sxs-lookup"><span data-stu-id="4c34e-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="4c34e-107">此方法还会更新到最新版本。</span><span class="sxs-lookup"><span data-stu-id="4c34e-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="4c34e-108">它不允许使用特定版本。</span><span class="sxs-lookup"><span data-stu-id="4c34e-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="4c34e-109">`tools.json` 终结点可用于解决启动问题，并可控制所下载的 nuget.exe 版本。</span><span class="sxs-lookup"><span data-stu-id="4c34e-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="4c34e-110">这可以用于 CI/CD 环境或自定义脚本，以发现和下载任何发布版本的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="4c34e-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="4c34e-111">可以使用未经身份验证的 HTTP 请求获取 `tools.json` 终结点（例如，在 PowerShell 中 `Invoke-WebRequest` 或 `wget`）。</span><span class="sxs-lookup"><span data-stu-id="4c34e-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="4c34e-112">使用 JSON 反序列化程序可以对其进行分析，后续 nuget.exe 下载 Url 也可以使用未经身份验证的 HTTP 请求提取。</span><span class="sxs-lookup"><span data-stu-id="4c34e-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="4c34e-113">可以使用 `GET` 方法获取终结点：</span><span class="sxs-lookup"><span data-stu-id="4c34e-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="4c34e-114">此处提供终结点的[JSON 架构](https://json-schema.org/)：</span><span class="sxs-lookup"><span data-stu-id="4c34e-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="4c34e-115">响应</span><span class="sxs-lookup"><span data-stu-id="4c34e-115">Response</span></span>

<span data-ttu-id="4c34e-116">响应是一个 JSON 文档，其中包含 nuget.exe 的所有可用版本。</span><span class="sxs-lookup"><span data-stu-id="4c34e-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="4c34e-117">根 JSON 对象具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="4c34e-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="4c34e-118">“属性”</span><span class="sxs-lookup"><span data-stu-id="4c34e-118">Name</span></span>      | <span data-ttu-id="4c34e-119">键入</span><span class="sxs-lookup"><span data-stu-id="4c34e-119">Type</span></span>             | <span data-ttu-id="4c34e-120">必需</span><span class="sxs-lookup"><span data-stu-id="4c34e-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="4c34e-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="4c34e-121">nuget.exe</span></span> | <span data-ttu-id="4c34e-122">对象数组</span><span class="sxs-lookup"><span data-stu-id="4c34e-122">array of objects</span></span> | <span data-ttu-id="4c34e-123">是</span><span class="sxs-lookup"><span data-stu-id="4c34e-123">yes</span></span>

<span data-ttu-id="4c34e-124">`nuget.exe` 数组中的每个对象具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="4c34e-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="4c34e-125">“属性”</span><span class="sxs-lookup"><span data-stu-id="4c34e-125">Name</span></span>     | <span data-ttu-id="4c34e-126">键入</span><span class="sxs-lookup"><span data-stu-id="4c34e-126">Type</span></span>   | <span data-ttu-id="4c34e-127">必需</span><span class="sxs-lookup"><span data-stu-id="4c34e-127">Required</span></span> | <span data-ttu-id="4c34e-128">注意</span><span class="sxs-lookup"><span data-stu-id="4c34e-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="4c34e-129">版本</span><span class="sxs-lookup"><span data-stu-id="4c34e-129">version</span></span>  | <span data-ttu-id="4c34e-130">string</span><span class="sxs-lookup"><span data-stu-id="4c34e-130">string</span></span> | <span data-ttu-id="4c34e-131">是</span><span class="sxs-lookup"><span data-stu-id="4c34e-131">yes</span></span>      | <span data-ttu-id="4c34e-132">SemVer 2.0.0 字符串</span><span class="sxs-lookup"><span data-stu-id="4c34e-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="4c34e-133">URL</span><span class="sxs-lookup"><span data-stu-id="4c34e-133">url</span></span>      | <span data-ttu-id="4c34e-134">string</span><span class="sxs-lookup"><span data-stu-id="4c34e-134">string</span></span> | <span data-ttu-id="4c34e-135">是</span><span class="sxs-lookup"><span data-stu-id="4c34e-135">yes</span></span>      | <span data-ttu-id="4c34e-136">下载此版本的 nuget.exe 的绝对 URL</span><span class="sxs-lookup"><span data-stu-id="4c34e-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="4c34e-137">结束</span><span class="sxs-lookup"><span data-stu-id="4c34e-137">stage</span></span>    | <span data-ttu-id="4c34e-138">string</span><span class="sxs-lookup"><span data-stu-id="4c34e-138">string</span></span> | <span data-ttu-id="4c34e-139">是</span><span class="sxs-lookup"><span data-stu-id="4c34e-139">yes</span></span>      | <span data-ttu-id="4c34e-140">枚举字符串</span><span class="sxs-lookup"><span data-stu-id="4c34e-140">An enum string</span></span>
<span data-ttu-id="4c34e-141">上载</span><span class="sxs-lookup"><span data-stu-id="4c34e-141">uploaded</span></span> | <span data-ttu-id="4c34e-142">string</span><span class="sxs-lookup"><span data-stu-id="4c34e-142">string</span></span> | <span data-ttu-id="4c34e-143">是</span><span class="sxs-lookup"><span data-stu-id="4c34e-143">yes</span></span>      | <span data-ttu-id="4c34e-144">可用版本的大约 ISO 8601 时间戳</span><span class="sxs-lookup"><span data-stu-id="4c34e-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="4c34e-145">数组中的项将按降序、SemVer 2.0.0 顺序排序。</span><span class="sxs-lookup"><span data-stu-id="4c34e-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="4c34e-146">这一保证旨在降低对最高版本号感兴趣的客户端的负担。</span><span class="sxs-lookup"><span data-stu-id="4c34e-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="4c34e-147">但这意味着列表不按时间顺序进行排序。</span><span class="sxs-lookup"><span data-stu-id="4c34e-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="4c34e-148">例如，如果在较高的主要版本之前的日期提供较低的主要版本，则此服务版本将不会显示在列表的顶部。</span><span class="sxs-lookup"><span data-stu-id="4c34e-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="4c34e-149">如果需要由*时间戳*发布的最新版本，只需按 `uploaded` 字符串对数组进行排序即可。</span><span class="sxs-lookup"><span data-stu-id="4c34e-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="4c34e-150">这是因为 `uploaded` 时间戳采用[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)格式，可以使用字典排序（即简单字符串排序）按时间顺序进行排序。</span><span class="sxs-lookup"><span data-stu-id="4c34e-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="4c34e-151">`stage` 属性指示此版本工具的审查。</span><span class="sxs-lookup"><span data-stu-id="4c34e-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="4c34e-152">阶段</span><span class="sxs-lookup"><span data-stu-id="4c34e-152">Stage</span></span>              | <span data-ttu-id="4c34e-153">含义</span><span class="sxs-lookup"><span data-stu-id="4c34e-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="4c34e-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="4c34e-154">EarlyAccessPreview</span></span> | <span data-ttu-id="4c34e-155">在[下载](https://www.nuget.org/downloads)网页上还不可见，应由合作伙伴验证</span><span class="sxs-lookup"><span data-stu-id="4c34e-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="4c34e-156">Released（已释放）</span><span class="sxs-lookup"><span data-stu-id="4c34e-156">Released</span></span>           | <span data-ttu-id="4c34e-157">在下载站点上可用，但尚不建议用于跨范围使用</span><span class="sxs-lookup"><span data-stu-id="4c34e-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="4c34e-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="4c34e-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="4c34e-159">在下载站点提供，建议用于使用</span><span class="sxs-lookup"><span data-stu-id="4c34e-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="4c34e-160">使用最新的建议版本的一种简单方法是使用列表中具有 `ReleasedAndBlessed``stage` 值的第一个版本。</span><span class="sxs-lookup"><span data-stu-id="4c34e-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="4c34e-161">这是因为版本按 SemVer 2.0.0 顺序排序。</span><span class="sxs-lookup"><span data-stu-id="4c34e-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="4c34e-162">Nuget.org 上的 `NuGet.CommandLine` 包通常仅更新 `ReleasedAndBlessed` 版本。</span><span class="sxs-lookup"><span data-stu-id="4c34e-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="4c34e-163">示例请求</span><span class="sxs-lookup"><span data-stu-id="4c34e-163">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="4c34e-164">示例响应</span><span class="sxs-lookup"><span data-stu-id="4c34e-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
