---
title: 用于发现 nuget.exe 版本 tools.json
description: 为终结点
author: jver
ms.author: jver
manager: skofman
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d11e79cd9109e1760189e848e35ff322be026a4d
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2018
ms.locfileid: "40247793"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="109a1-103">用于发现 nuget.exe 版本 tools.json</span><span class="sxs-lookup"><span data-stu-id="109a1-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="109a1-104">如今，有几种方法获取 nuget.exe 的最新版本以可编写脚本的方式在计算机上。</span><span class="sxs-lookup"><span data-stu-id="109a1-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="109a1-105">例如，可以下载并提取[ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/)从 nuget.org 的包。这具有某种程度的复杂性，因为它也需要已有 nuget.exe (对于`nuget.exe install`) 或您必须将使用基本解压缩工具.nupkg 解压缩并查找二进制的内部。</span><span class="sxs-lookup"><span data-stu-id="109a1-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="109a1-106">如果已有 nuget.exe，还可以使用`nuget.exe update -self`，但此操作还需要具有 nuget.exe 的现有副本。</span><span class="sxs-lookup"><span data-stu-id="109a1-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="109a1-107">这种方法也更新到最新版本。</span><span class="sxs-lookup"><span data-stu-id="109a1-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="109a1-108">它不允许使用特定版本。</span><span class="sxs-lookup"><span data-stu-id="109a1-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="109a1-109">`tools.json`终结点可供同时解决启动问题并使你下载的 nuget.exe 的版本控制。</span><span class="sxs-lookup"><span data-stu-id="109a1-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="109a1-110">这可以用于 CI/CD 环境或自定义脚本中发现和下载 nuget.exe 任何已发布的版本。</span><span class="sxs-lookup"><span data-stu-id="109a1-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="109a1-111">`tools.json`可以使用未经身份验证的 HTTP 请求获取终结点 (例如`Invoke-WebRequest`在 PowerShell 中或`wget`)。</span><span class="sxs-lookup"><span data-stu-id="109a1-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="109a1-112">可以分析使用 JSON 反序列化程序，还可以使用提取 Url 的后续 nuget.exe 下载未经身份验证的 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="109a1-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="109a1-113">终结点可以使用提取`GET`方法：</span><span class="sxs-lookup"><span data-stu-id="109a1-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="109a1-114">[JSON 架构](http://json-schema.org/)为此处提供了终结点：</span><span class="sxs-lookup"><span data-stu-id="109a1-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="109a1-115">响应</span><span class="sxs-lookup"><span data-stu-id="109a1-115">Response</span></span>

<span data-ttu-id="109a1-116">响应是 nuget.exe 的包含所有可用版本的 JSON 文档。</span><span class="sxs-lookup"><span data-stu-id="109a1-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="109a1-117">根 JSON 对象具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="109a1-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="109a1-118">name</span><span class="sxs-lookup"><span data-stu-id="109a1-118">Name</span></span>      | <span data-ttu-id="109a1-119">类型</span><span class="sxs-lookup"><span data-stu-id="109a1-119">Type</span></span>             | <span data-ttu-id="109a1-120">必需</span><span class="sxs-lookup"><span data-stu-id="109a1-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="109a1-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="109a1-121">nuget.exe</span></span> | <span data-ttu-id="109a1-122">对象的数组</span><span class="sxs-lookup"><span data-stu-id="109a1-122">array of objects</span></span> | <span data-ttu-id="109a1-123">是</span><span class="sxs-lookup"><span data-stu-id="109a1-123">yes</span></span>

<span data-ttu-id="109a1-124">在每个对象`nuget.exe`数组具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="109a1-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="109a1-125">name</span><span class="sxs-lookup"><span data-stu-id="109a1-125">Name</span></span>     | <span data-ttu-id="109a1-126">类型</span><span class="sxs-lookup"><span data-stu-id="109a1-126">Type</span></span>   | <span data-ttu-id="109a1-127">必需</span><span class="sxs-lookup"><span data-stu-id="109a1-127">Required</span></span> | <span data-ttu-id="109a1-128">说明</span><span class="sxs-lookup"><span data-stu-id="109a1-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="109a1-129">version</span><span class="sxs-lookup"><span data-stu-id="109a1-129">version</span></span>  | <span data-ttu-id="109a1-130">字符串</span><span class="sxs-lookup"><span data-stu-id="109a1-130">string</span></span> | <span data-ttu-id="109a1-131">是</span><span class="sxs-lookup"><span data-stu-id="109a1-131">yes</span></span>      | <span data-ttu-id="109a1-132">SemVer 2.0.0 字符串</span><span class="sxs-lookup"><span data-stu-id="109a1-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="109a1-133">URL</span><span class="sxs-lookup"><span data-stu-id="109a1-133">url</span></span>      | <span data-ttu-id="109a1-134">字符串</span><span class="sxs-lookup"><span data-stu-id="109a1-134">string</span></span> | <span data-ttu-id="109a1-135">是</span><span class="sxs-lookup"><span data-stu-id="109a1-135">yes</span></span>      | <span data-ttu-id="109a1-136">下载此版本的 nuget.exe 绝对 URL</span><span class="sxs-lookup"><span data-stu-id="109a1-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="109a1-137">阶段</span><span class="sxs-lookup"><span data-stu-id="109a1-137">stage</span></span>    | <span data-ttu-id="109a1-138">字符串</span><span class="sxs-lookup"><span data-stu-id="109a1-138">string</span></span> | <span data-ttu-id="109a1-139">是</span><span class="sxs-lookup"><span data-stu-id="109a1-139">yes</span></span>      | <span data-ttu-id="109a1-140">枚举字符串</span><span class="sxs-lookup"><span data-stu-id="109a1-140">An enum string</span></span>
<span data-ttu-id="109a1-141">上传</span><span class="sxs-lookup"><span data-stu-id="109a1-141">uploaded</span></span> | <span data-ttu-id="109a1-142">字符串</span><span class="sxs-lookup"><span data-stu-id="109a1-142">string</span></span> | <span data-ttu-id="109a1-143">是</span><span class="sxs-lookup"><span data-stu-id="109a1-143">yes</span></span>      | <span data-ttu-id="109a1-144">版本何时进行可用一个近似的时间戳</span><span class="sxs-lookup"><span data-stu-id="109a1-144">An approximate timestamp of when the version was made available</span></span>

<span data-ttu-id="109a1-145">将按降序，SemVer 2.0.0 排序数组中的项。</span><span class="sxs-lookup"><span data-stu-id="109a1-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="109a1-146">这一保证旨在便于在寻找最新版本的客户端上的负担。</span><span class="sxs-lookup"><span data-stu-id="109a1-146">This guarantee is meant to ease the burden on a client looking for the latest version.</span></span> 

<span data-ttu-id="109a1-147">`stage`属性指示 vettect 此版本的工具是。</span><span class="sxs-lookup"><span data-stu-id="109a1-147">The `stage` property indicates how vettect this version of the tool is.</span></span> 

<span data-ttu-id="109a1-148">阶段</span><span class="sxs-lookup"><span data-stu-id="109a1-148">Stage</span></span>              | <span data-ttu-id="109a1-149">含义</span><span class="sxs-lookup"><span data-stu-id="109a1-149">Meaning</span></span>
------------------ | ------
<span data-ttu-id="109a1-150">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="109a1-150">EarlyAccessPreview</span></span> | <span data-ttu-id="109a1-151">在上尚不可见[下载网页](https://www.nuget.org/downloads)和应由合作伙伴验证</span><span class="sxs-lookup"><span data-stu-id="109a1-151">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="109a1-152">Released（已释放）</span><span class="sxs-lookup"><span data-stu-id="109a1-152">Released</span></span>           | <span data-ttu-id="109a1-153">下载站点上的可用但尚未广泛使用建议</span><span class="sxs-lookup"><span data-stu-id="109a1-153">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="109a1-154">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="109a1-154">ReleasedAndBlessed</span></span> | <span data-ttu-id="109a1-155">下载站点上可用，建议使用</span><span class="sxs-lookup"><span data-stu-id="109a1-155">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="109a1-156">具有最新的一个简单的方法，建议的版本是所要采取的第一个版本列表，其中包含`stage`的值`ReleasedAndBlessed`。</span><span class="sxs-lookup"><span data-stu-id="109a1-156">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span>

<span data-ttu-id="109a1-157">`NuGet.CommandLine` Nuget.org 上的包通常只会更新与`ReleasedAndBlessed`版本。</span><span class="sxs-lookup"><span data-stu-id="109a1-157">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="109a1-158">示例请求</span><span class="sxs-lookup"><span data-stu-id="109a1-158">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="109a1-159">示例响应</span><span class="sxs-lookup"><span data-stu-id="109a1-159">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
