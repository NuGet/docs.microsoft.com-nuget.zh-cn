---
title: 用于发现 nuget.exe 版本 tools.json
description: 为终结点
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 003139abac7808dbdaef4aa66119e09772db2b4f
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852528"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="add10-103">用于发现 nuget.exe 版本 tools.json</span><span class="sxs-lookup"><span data-stu-id="add10-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="add10-104">如今，有几种方法获取 nuget.exe 的最新版本以可编写脚本的方式在计算机上。</span><span class="sxs-lookup"><span data-stu-id="add10-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="add10-105">例如，可以下载并提取[ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/)从 nuget.org 的包。这具有某种程度的复杂性，因为它也需要已有 nuget.exe (对于`nuget.exe install`) 或您必须将使用基本解压缩工具.nupkg 解压缩并查找二进制的内部。</span><span class="sxs-lookup"><span data-stu-id="add10-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="add10-106">如果已有 nuget.exe，还可以使用`nuget.exe update -self`，但此操作还需要具有 nuget.exe 的现有副本。</span><span class="sxs-lookup"><span data-stu-id="add10-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="add10-107">这种方法也更新到最新版本。</span><span class="sxs-lookup"><span data-stu-id="add10-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="add10-108">它不允许使用特定版本。</span><span class="sxs-lookup"><span data-stu-id="add10-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="add10-109">`tools.json`终结点可供同时解决启动问题并使你下载的 nuget.exe 的版本控制。</span><span class="sxs-lookup"><span data-stu-id="add10-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="add10-110">这可以用于 CI/CD 环境或自定义脚本中发现和下载 nuget.exe 任何已发布的版本。</span><span class="sxs-lookup"><span data-stu-id="add10-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="add10-111">`tools.json`可以使用未经身份验证的 HTTP 请求获取终结点 (例如`Invoke-WebRequest`在 PowerShell 中或`wget`)。</span><span class="sxs-lookup"><span data-stu-id="add10-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="add10-112">可以分析使用 JSON 反序列化程序，还可以使用提取 Url 的后续 nuget.exe 下载未经身份验证的 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="add10-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="add10-113">终结点可以使用提取`GET`方法：</span><span class="sxs-lookup"><span data-stu-id="add10-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="add10-114">[JSON 架构](http://json-schema.org/)为此处提供了终结点：</span><span class="sxs-lookup"><span data-stu-id="add10-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="add10-115">响应</span><span class="sxs-lookup"><span data-stu-id="add10-115">Response</span></span>

<span data-ttu-id="add10-116">响应是 nuget.exe 的包含所有可用版本的 JSON 文档。</span><span class="sxs-lookup"><span data-stu-id="add10-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="add10-117">根 JSON 对象具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="add10-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="add10-118">name</span><span class="sxs-lookup"><span data-stu-id="add10-118">Name</span></span>      | <span data-ttu-id="add10-119">类型</span><span class="sxs-lookup"><span data-stu-id="add10-119">Type</span></span>             | <span data-ttu-id="add10-120">必需</span><span class="sxs-lookup"><span data-stu-id="add10-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="add10-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="add10-121">nuget.exe</span></span> | <span data-ttu-id="add10-122">对象的数组</span><span class="sxs-lookup"><span data-stu-id="add10-122">array of objects</span></span> | <span data-ttu-id="add10-123">是</span><span class="sxs-lookup"><span data-stu-id="add10-123">yes</span></span>

<span data-ttu-id="add10-124">在每个对象`nuget.exe`数组具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="add10-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="add10-125">name</span><span class="sxs-lookup"><span data-stu-id="add10-125">Name</span></span>     | <span data-ttu-id="add10-126">类型</span><span class="sxs-lookup"><span data-stu-id="add10-126">Type</span></span>   | <span data-ttu-id="add10-127">必需</span><span class="sxs-lookup"><span data-stu-id="add10-127">Required</span></span> | <span data-ttu-id="add10-128">说明</span><span class="sxs-lookup"><span data-stu-id="add10-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="add10-129">version</span><span class="sxs-lookup"><span data-stu-id="add10-129">version</span></span>  | <span data-ttu-id="add10-130">string</span><span class="sxs-lookup"><span data-stu-id="add10-130">string</span></span> | <span data-ttu-id="add10-131">是</span><span class="sxs-lookup"><span data-stu-id="add10-131">yes</span></span>      | <span data-ttu-id="add10-132">SemVer 2.0.0 字符串</span><span class="sxs-lookup"><span data-stu-id="add10-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="add10-133">URL</span><span class="sxs-lookup"><span data-stu-id="add10-133">url</span></span>      | <span data-ttu-id="add10-134">string</span><span class="sxs-lookup"><span data-stu-id="add10-134">string</span></span> | <span data-ttu-id="add10-135">是</span><span class="sxs-lookup"><span data-stu-id="add10-135">yes</span></span>      | <span data-ttu-id="add10-136">下载此版本的 nuget.exe 绝对 URL</span><span class="sxs-lookup"><span data-stu-id="add10-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="add10-137">阶段</span><span class="sxs-lookup"><span data-stu-id="add10-137">stage</span></span>    | <span data-ttu-id="add10-138">string</span><span class="sxs-lookup"><span data-stu-id="add10-138">string</span></span> | <span data-ttu-id="add10-139">是</span><span class="sxs-lookup"><span data-stu-id="add10-139">yes</span></span>      | <span data-ttu-id="add10-140">枚举字符串</span><span class="sxs-lookup"><span data-stu-id="add10-140">An enum string</span></span>
<span data-ttu-id="add10-141">上传</span><span class="sxs-lookup"><span data-stu-id="add10-141">uploaded</span></span> | <span data-ttu-id="add10-142">string</span><span class="sxs-lookup"><span data-stu-id="add10-142">string</span></span> | <span data-ttu-id="add10-143">是</span><span class="sxs-lookup"><span data-stu-id="add10-143">yes</span></span>      | <span data-ttu-id="add10-144">版本何时进行可用一个近似的 ISO 8601 时间戳</span><span class="sxs-lookup"><span data-stu-id="add10-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="add10-145">将按降序，SemVer 2.0.0 排序数组中的项。</span><span class="sxs-lookup"><span data-stu-id="add10-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="add10-146">这一保证旨在减少客户端感兴趣的最高版本号的负担。</span><span class="sxs-lookup"><span data-stu-id="add10-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="add10-147">但是这意味着列表不按时间顺序排序。</span><span class="sxs-lookup"><span data-stu-id="add10-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="add10-148">例如，如果在某个日期晚于更高版本的主版本，较低的主版本已得到处理，此服务的版本将不出现在列表顶部。</span><span class="sxs-lookup"><span data-stu-id="add10-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="add10-149">如果想要发布的最新版本*时间戳*，只需对数组进行排序`uploaded`字符串。</span><span class="sxs-lookup"><span data-stu-id="add10-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="add10-150">这样做的原因`uploaded`时间戳处于[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)格式，它可以通过使用按字典编辑顺序排序 （即简单的字符串排序） 按时间顺序排序。</span><span class="sxs-lookup"><span data-stu-id="add10-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="add10-151">`stage`属性指示如何审查该版本的工具是。</span><span class="sxs-lookup"><span data-stu-id="add10-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="add10-152">阶段</span><span class="sxs-lookup"><span data-stu-id="add10-152">Stage</span></span>              | <span data-ttu-id="add10-153">含义</span><span class="sxs-lookup"><span data-stu-id="add10-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="add10-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="add10-154">EarlyAccessPreview</span></span> | <span data-ttu-id="add10-155">在上尚不可见[下载网页](https://www.nuget.org/downloads)和应由合作伙伴验证</span><span class="sxs-lookup"><span data-stu-id="add10-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="add10-156">Released（已释放）</span><span class="sxs-lookup"><span data-stu-id="add10-156">Released</span></span>           | <span data-ttu-id="add10-157">下载站点上的可用但尚未广泛使用建议</span><span class="sxs-lookup"><span data-stu-id="add10-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="add10-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="add10-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="add10-159">下载站点上可用，建议使用</span><span class="sxs-lookup"><span data-stu-id="add10-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="add10-160">具有最新的一个简单的方法，建议的版本是所要采取的第一个版本列表，其中包含`stage`的值`ReleasedAndBlessed`。</span><span class="sxs-lookup"><span data-stu-id="add10-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="add10-161">这有效，因为版本 SemVer 2.0.0 顺序进行排序。</span><span class="sxs-lookup"><span data-stu-id="add10-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="add10-162">`NuGet.CommandLine` Nuget.org 上的包通常只会更新与`ReleasedAndBlessed`版本。</span><span class="sxs-lookup"><span data-stu-id="add10-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="add10-163">示例请求</span><span class="sxs-lookup"><span data-stu-id="add10-163">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="add10-164">示例响应</span><span class="sxs-lookup"><span data-stu-id="add10-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
