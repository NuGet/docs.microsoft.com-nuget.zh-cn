---
title: NuGet.org 概述
description: NuGet.org 概述
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427012"
---
# <a name="overview-of-nugetorg"></a><span data-ttu-id="b9217-103">NuGet.org 概述</span><span class="sxs-lookup"><span data-stu-id="b9217-103">Overview of NuGet.org</span></span>

<span data-ttu-id="b9217-104">NuGet.org 是 NuGet 包的公用主机，每天都有数百万 .NET 和 .NET Core 开发人员使用它。</span><span class="sxs-lookup"><span data-stu-id="b9217-104">NuGet.org is a public host of NuGet packages that are employed by millions of .NET and .NET Core developers every day.</span></span>

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a><span data-ttu-id="b9217-105">NuGet.org 在 NuGet 生态系统中的角色</span><span class="sxs-lookup"><span data-stu-id="b9217-105">Role of NuGet.org in the NuGet ecosystem</span></span>

<span data-ttu-id="b9217-106">作为公用主机角色时，NuGet.org 自身负责在 [nuget.org](https://www.nuget.org) 中维护包含 100,000 多个唯一包的中央存储库。NuGet.org 不是唯一可能的包主机。</span><span class="sxs-lookup"><span data-stu-id="b9217-106">In its role as a public host, NuGet.org itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). NuGet.org is not the only possible host for packages.</span></span> <span data-ttu-id="b9217-107">NuGet 技术还支持在云中（如在 Azure DevOps 上）、在私有网络中或者甚至直接在本地文件系统以私密方式托管包。</span><span class="sxs-lookup"><span data-stu-id="b9217-107">The NuGet technology also enables you to host packages privately in the cloud (such as on Azure DevOps), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="b9217-108">如果对其他主机或承载选项感兴趣，请参阅[承载自己的 NuGet 源](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b9217-108">If you are interested in a different host or hosting option, see [Hosting your own NuGet feeds](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="b9217-109">与 NuGet 包的任何主机一样，NuGet.org 充当包创建者和包消费者之间的连接点   。</span><span class="sxs-lookup"><span data-stu-id="b9217-109">NuGet.org, like any host for NuGet packages, serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="b9217-110">创建者生成有用的 NuGet 包并将其发布。</span><span class="sxs-lookup"><span data-stu-id="b9217-110">Creators build useful NuGet packages and publish them.</span></span> <span data-ttu-id="b9217-111">然后，使用者可以在可访问的主机上搜索有用且兼容的包，下载包并将其包含在项目中。</span><span class="sxs-lookup"><span data-stu-id="b9217-111">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="b9217-112">在项目中安装包后，包的 API 将可用于其余项目代码。</span><span class="sxs-lookup"><span data-stu-id="b9217-112">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![包创建者、包主机和包使用者之间的关系](media/nuget-roles.png)

## <a name="accounts"></a><span data-ttu-id="b9217-114">帐户</span><span class="sxs-lookup"><span data-stu-id="b9217-114">Accounts</span></span>

<span data-ttu-id="b9217-115">要在 NuGet.org 上发布包，首先要创建一个[个人（用户）帐户](individual-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="b9217-115">To publish packages on NuGet.org, you first create an [individual (user) account](individual-accounts.md).</span></span> <span data-ttu-id="b9217-116">这将成为你在 NuGet.org 上的标识。</span><span class="sxs-lookup"><span data-stu-id="b9217-116">This becomes your identity on NuGet.org.</span></span>

<span data-ttu-id="b9217-117">通过 NuGet.org 还可创建[组织帐户](organizations-on-nuget-org.md)。</span><span class="sxs-lookup"><span data-stu-id="b9217-117">NuGet.org also allows you to create an [organization account](organizations-on-nuget-org.md).</span></span> <span data-ttu-id="b9217-118">组织帐户的成员可以是一个或多个个人帐户。</span><span class="sxs-lookup"><span data-stu-id="b9217-118">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="b9217-119">成员可以管理一组包，同时保持所有权的单一标识。</span><span class="sxs-lookup"><span data-stu-id="b9217-119">Members can manage a set of packages while maintaining a single identity for ownership.</span></span> <span data-ttu-id="b9217-120">通过你的个人帐户，你可以成为任意数量组织的成员。</span><span class="sxs-lookup"><span data-stu-id="b9217-120">Through your individual account, you can be a member of any number of organizations.</span></span>

<span data-ttu-id="b9217-121">包可以属于组织帐户，就像它可以属于个人帐户一样。</span><span class="sxs-lookup"><span data-stu-id="b9217-121">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="b9217-122">包使用者看不到个人帐户或组织帐户之间的任何差异：两者都显示为包 `owners`。</span><span class="sxs-lookup"><span data-stu-id="b9217-122">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="api-keys"></a><span data-ttu-id="b9217-123">API 密钥</span><span class="sxs-lookup"><span data-stu-id="b9217-123">API keys</span></span>

<span data-ttu-id="b9217-124">具有要发布的 NuGet 包（.nupkg 文件）后，可以使用 nuget.exe CLI 或 dotnet.exe CLI 以及从 NuGet.org 获得的 [API 密钥](scoped-api-keys.md)将其发布到 NuGet.org  。</span><span class="sxs-lookup"><span data-stu-id="b9217-124">Once you have a NuGet package (*.nupkg* file) to publish, you publish it to NuGet.org using either the nuget.exe CLI or the dotnet.exe CLI, along with an [API key](scoped-api-keys.md) acquired from NuGet.org.</span></span>

<span data-ttu-id="b9217-125">在[发布包](../create-packages/creating-a-package.md)时，请在 CLI 命令中包含 API 密钥值。</span><span class="sxs-lookup"><span data-stu-id="b9217-125">When you [publish a package](../create-packages/creating-a-package.md), you include the API key value in the CLI command.</span></span>

## <a name="id-prefixes"></a><span data-ttu-id="b9217-126">ID 前缀</span><span class="sxs-lookup"><span data-stu-id="b9217-126">ID prefixes</span></span>

<span data-ttu-id="b9217-127">发布包时，可以通过[保留 ID 前缀](id-prefix-reservation.md)来保留和保护标识。</span><span class="sxs-lookup"><span data-stu-id="b9217-127">When you publish packages, you can reserve and protect your identity by [reserving ID prefixes](id-prefix-reservation.md).</span></span> <span data-ttu-id="b9217-128">安装包时，包使用者会收到附加信息，其中指出他们使用的包在标识属性中并不具有欺骗性。</span><span class="sxs-lookup"><span data-stu-id="b9217-128">When installing a package, package consumers are provided with additional information indicating that the package they are consuming is not deceptive in its identifying properties.</span></span>

## <a name="api-endpoint-for-nugetorg"></a><span data-ttu-id="b9217-129">适用于 NuGet.org 的 API 终结点</span><span class="sxs-lookup"><span data-stu-id="b9217-129">API endpoint for NuGet.org</span></span>

<span data-ttu-id="b9217-130">若要将 NuGet.org 用作 NuGet 客户端的包存储库，应使用以下 V3 API 终结点：</span><span class="sxs-lookup"><span data-stu-id="b9217-130">To use NuGet.org as a package repository with NuGet clients, you should use the following V3 API endpoint:</span></span> 

`https://api.nuget.org/v3/index.json`

<span data-ttu-id="b9217-131">较旧版本的客户端仍然可以使用 V2 协议来访问 NuGet.org。但是，请注意，NuGet 客户端 3.0 或更高版本在使用 V2 协议时将导致服务的速度更慢且不太可靠：</span><span class="sxs-lookup"><span data-stu-id="b9217-131">Older clients can still use the V2 protocol to reach NuGet.org. However, please note, NuGet clients 3.0 or later will have slower and less reliable service using the V2 protocol:</span></span>

<span data-ttu-id="b9217-132">`https://www.nuget.org/api/v2`（**V2 prototcol 已弃用！** ）</span><span class="sxs-lookup"><span data-stu-id="b9217-132">`https://www.nuget.org/api/v2` (**The V2 prototcol is deprecated!**)</span></span>
