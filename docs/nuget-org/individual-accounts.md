---
title: 个人帐户
description: 需要 NuGet.org 上的个人帐户以发布包
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e1e31e0534706dab43f8d7b1b0db059cd6f29b80
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427132"
---
# <a name="individual-accounts"></a><span data-ttu-id="44da1-103">个人帐户</span><span class="sxs-lookup"><span data-stu-id="44da1-103">Individual accounts</span></span>

<span data-ttu-id="44da1-104">必须创建个人帐户才能在 NuGet.org 上发布和管理包。</span><span class="sxs-lookup"><span data-stu-id="44da1-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="44da1-105">个人帐户与组织帐户</span><span class="sxs-lookup"><span data-stu-id="44da1-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="44da1-106">个人（用户）帐户是你在 NuGet.org 上的标识，可以是任意数量的组织的成员。</span><span class="sxs-lookup"><span data-stu-id="44da1-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="44da1-107">包可以属于组织帐户，也可以属于个人帐户。</span><span class="sxs-lookup"><span data-stu-id="44da1-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="44da1-108">包使用者看不到个人帐户或组织帐户之间的任何差异：两者都显示为包 `owners`。</span><span class="sxs-lookup"><span data-stu-id="44da1-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="44da1-109">组织帐户具有一个或多个个人帐户作为其成员。</span><span class="sxs-lookup"><span data-stu-id="44da1-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="44da1-110">这些成员可以管理一组包，同时保持所有权的单一标识。</span><span class="sxs-lookup"><span data-stu-id="44da1-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="44da1-111">添加新的个人帐户</span><span class="sxs-lookup"><span data-stu-id="44da1-111">Add a new individual account</span></span>

<span data-ttu-id="44da1-112">要创建 NuGet.org 帐户，需要具备 Microsoft 个人帐户 (MSA) 或 Azure Active Directory (AAD) 帐户。</span><span class="sxs-lookup"><span data-stu-id="44da1-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="44da1-113">如果没有帐户，请[创建](https://signup.live.com)帐户。</span><span class="sxs-lookup"><span data-stu-id="44da1-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="44da1-114">如果拥有 MSA 或 AAD 帐户，请执行以下步骤。</span><span class="sxs-lookup"><span data-stu-id="44da1-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="44da1-115">转到 [NuGet.org 登录页](https://www.nuget.org/users/account/LogOn)。</span><span class="sxs-lookup"><span data-stu-id="44da1-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="44da1-116">单击“Microsoft 登录”按钮  。</span><span class="sxs-lookup"><span data-stu-id="44da1-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="44da1-117">输入 Microsoft 帐户或 Azure Active Directory 帐户详细信息。</span><span class="sxs-lookup"><span data-stu-id="44da1-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="44da1-118">请单击“是”以接受要授予 NuGet.org 应用程序的权限   。</span><span class="sxs-lookup"><span data-stu-id="44da1-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![授予 NuGet.org 权限](media/nuget-org-permissions.png)

1. <span data-ttu-id="44da1-120">此时系统将重定向至 nuget.org 并要求注册用户名  。</span><span class="sxs-lookup"><span data-stu-id="44da1-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="44da1-121">在输入框中指定用户名。</span><span class="sxs-lookup"><span data-stu-id="44da1-121">Specify the username in the input box.</span></span> <span data-ttu-id="44da1-122">请注意，用户名需区分大小写，并且以后无法更改或重命名  。</span><span class="sxs-lookup"><span data-stu-id="44da1-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![在 NuGet.org 上指定用户名](media/nuget-org-register.png) 

1. <span data-ttu-id="44da1-124">单击“注册”按钮  。</span><span class="sxs-lookup"><span data-stu-id="44da1-124">Click the **Register** button.</span></span>

<span data-ttu-id="44da1-125">现在 NuGet.org 帐户已成功创建。</span><span class="sxs-lookup"><span data-stu-id="44da1-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="44da1-126">可以在[帐户设置](https://www.nuget.org/account)页面执行帐户管理。</span><span class="sxs-lookup"><span data-stu-id="44da1-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>
