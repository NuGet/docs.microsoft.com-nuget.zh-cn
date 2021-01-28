---
title: 用户数据请求
description: 请求用户数据导出和删除的策略
author: JonDouglas
ms.author: jodou
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: e0ec429469a992c9558d1635890fd568398206a1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775719"
---
# <a name="user-data-requests"></a><span data-ttu-id="562a7-103">用户数据请求</span><span class="sxs-lookup"><span data-stu-id="562a7-103">User Data Requests</span></span>

<span data-ttu-id="562a7-104">nuget.org 用户可通过 [nuget.org](https://www.nuget.org) 提交信息删除请求和信息导出请求。这两种类型均以支持请求的形式提交，并由 nuget.org 管理员在 30 天内执行。</span><span class="sxs-lookup"><span data-stu-id="562a7-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="562a7-105">可通过 nuget.org 直接访问以下用户数据：</span><span class="sxs-lookup"><span data-stu-id="562a7-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="562a7-106">与电子邮件地址、登录帐户、个人资料图片、电子邮件通知设置等数据相关的帐户</span><span class="sxs-lookup"><span data-stu-id="562a7-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="562a7-107">拥有的 API 密钥</span><span class="sxs-lookup"><span data-stu-id="562a7-107">Owned API Keys</span></span>
* <span data-ttu-id="562a7-108">拥有包列表</span><span class="sxs-lookup"><span data-stu-id="562a7-108">List of owned packages</span></span>

<span data-ttu-id="562a7-109">此数据不包含在通过支持请求导出的数据中。</span><span class="sxs-lookup"><span data-stu-id="562a7-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="562a7-110">标识客户数据</span><span class="sxs-lookup"><span data-stu-id="562a7-110">Identifying customer data</span></span>

<span data-ttu-id="562a7-111">可以将客户数据标识为 nuget.org 用户帐户名。</span><span class="sxs-lookup"><span data-stu-id="562a7-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="562a7-112">删除客户数据</span><span class="sxs-lookup"><span data-stu-id="562a7-112">Deleting customer data</span></span>

<span data-ttu-id="562a7-113">请求从 nuget.org 删除用户数据：</span><span class="sxs-lookup"><span data-stu-id="562a7-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="562a7-114">用户必须登录到 [nuget.org](https://www.nuget.org)</span><span class="sxs-lookup"><span data-stu-id="562a7-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="562a7-115">用户必须通过 [nuget.org/account/delete](https://www.nuget.org/account/delete) 提交请求，才能删除帐户</span><span class="sxs-lookup"><span data-stu-id="562a7-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="562a7-116">若用户为包的唯一所有者，建议其在请求删除帐户前找到新的所有者。</span><span class="sxs-lookup"><span data-stu-id="562a7-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="562a7-117">如果不转移包所有权，则不会列出 NuGet 包，因此，它不会再显示在 Visual Studio 的搜索查询中或 nuget.org 网站上。</span><span class="sxs-lookup"><span data-stu-id="562a7-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="562a7-118">删除帐户前，nuget.org 管理员需与用户协作，为其所拥有的包寻找新的所有者。</span><span class="sxs-lookup"><span data-stu-id="562a7-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="562a7-119">nuget.org 管理员将在请求提交后 30 天内完成帐户删除操作。</span><span class="sxs-lookup"><span data-stu-id="562a7-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="562a7-120">帐户删除后，所有用户数据都将从 nuget.org 系统中删除，并会执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="562a7-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="562a7-121">从 nuget.org 中注销已删除的帐户</span><span class="sxs-lookup"><span data-stu-id="562a7-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="562a7-122">删除所有拥有的 API 密钥</span><span class="sxs-lookup"><span data-stu-id="562a7-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="562a7-123">释放所有保留命名空间</span><span class="sxs-lookup"><span data-stu-id="562a7-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="562a7-124">删除所有包所有权</span><span class="sxs-lookup"><span data-stu-id="562a7-124">Any package ownership are removed</span></span>

<span data-ttu-id="562a7-125">不会删除拥有包  。</span><span class="sxs-lookup"><span data-stu-id="562a7-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="562a7-126">虽然搜索结果中未列出这些包，但依赖于它们的项目仍可通过包还原进行使用。</span><span class="sxs-lookup"><span data-stu-id="562a7-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="562a7-127">导出客户数据</span><span class="sxs-lookup"><span data-stu-id="562a7-127">Exporting customer data</span></span>

<span data-ttu-id="562a7-128">登录到 nuget.org 后，用户可通过 [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact) 提交导出请求</span><span class="sxs-lookup"><span data-stu-id="562a7-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="562a7-129">用户可以通过 Azure Blob 在 48 小时内下载导出的数据。</span><span class="sxs-lookup"><span data-stu-id="562a7-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="562a7-130">48 小时后，访问过期，用户必须根据需要提交新的导出请求。</span><span class="sxs-lookup"><span data-stu-id="562a7-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="562a7-131">导出的数据包括：</span><span class="sxs-lookup"><span data-stu-id="562a7-131">The exported data includes:</span></span>

* <span data-ttu-id="562a7-132">用户的支持请求</span><span class="sxs-lookup"><span data-stu-id="562a7-132">The user's support requests</span></span>
* <span data-ttu-id="562a7-133">审核日志中保存的用户操作（发布包、创建帐户）</span><span class="sxs-lookup"><span data-stu-id="562a7-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="562a7-134">IIS 日志中保存的任何用户信息</span><span class="sxs-lookup"><span data-stu-id="562a7-134">Any user information as persisted in the IIS logs</span></span>
