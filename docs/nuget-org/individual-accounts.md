---
title: 个人帐户 - NuGet.org
description: 需要 NuGet.org 上的个人帐户以发布包
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 7951b3db0cdcaee0a1eb955a5bf6fedce24c79c9
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428629"
---
# <a name="individual-accounts-on-nugetorg"></a><span data-ttu-id="16b4a-103">NuGet.org 上的个人帐户</span><span class="sxs-lookup"><span data-stu-id="16b4a-103">Individual accounts on NuGet.org</span></span>

<span data-ttu-id="16b4a-104">必须创建个人帐户才能在 NuGet.org 上发布和管理包。</span><span class="sxs-lookup"><span data-stu-id="16b4a-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="16b4a-105">个人帐户与组织帐户</span><span class="sxs-lookup"><span data-stu-id="16b4a-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="16b4a-106">个人（用户）帐户是你在 NuGet.org 上的标识，可以是任意数量的组织的成员。</span><span class="sxs-lookup"><span data-stu-id="16b4a-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="16b4a-107">包可以属于组织帐户，也可以属于个人帐户。</span><span class="sxs-lookup"><span data-stu-id="16b4a-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="16b4a-108">包使用者看不到个人帐户或组织帐户之间的任何差异：两者都显示为包 `owners`。</span><span class="sxs-lookup"><span data-stu-id="16b4a-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="16b4a-109">组织帐户具有一个或多个个人帐户作为其成员。</span><span class="sxs-lookup"><span data-stu-id="16b4a-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="16b4a-110">这些成员可以管理一组包，同时保持所有权的单一标识。</span><span class="sxs-lookup"><span data-stu-id="16b4a-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="16b4a-111">添加新的个人帐户</span><span class="sxs-lookup"><span data-stu-id="16b4a-111">Add a new individual account</span></span>

<span data-ttu-id="16b4a-112">要创建 NuGet.org 帐户，需要具备 Microsoft 个人帐户 (MSA) 或 Azure Active Directory (AAD) 帐户。</span><span class="sxs-lookup"><span data-stu-id="16b4a-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="16b4a-113">如果没有帐户，请[创建](https://signup.live.com)帐户。</span><span class="sxs-lookup"><span data-stu-id="16b4a-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="16b4a-114">如果拥有 MSA 或 AAD 帐户，请执行以下步骤。</span><span class="sxs-lookup"><span data-stu-id="16b4a-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="16b4a-115">转到 [NuGet.org 登录页](https://www.nuget.org/users/account/LogOn)。</span><span class="sxs-lookup"><span data-stu-id="16b4a-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="16b4a-116">单击“Microsoft 登录”按钮  。</span><span class="sxs-lookup"><span data-stu-id="16b4a-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="16b4a-117">输入 Microsoft 帐户或 Azure Active Directory 帐户详细信息。</span><span class="sxs-lookup"><span data-stu-id="16b4a-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="16b4a-118">请单击“是”以接受要授予 NuGet.org 应用程序的权限   。</span><span class="sxs-lookup"><span data-stu-id="16b4a-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![授予 NuGet.org 权限](media/nuget-org-permissions.png)

1. <span data-ttu-id="16b4a-120">此时系统将重定向至 nuget.org 并要求注册用户名  。</span><span class="sxs-lookup"><span data-stu-id="16b4a-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="16b4a-121">在输入框中指定用户名。</span><span class="sxs-lookup"><span data-stu-id="16b4a-121">Specify the username in the input box.</span></span> <span data-ttu-id="16b4a-122">请注意，用户名需区分大小写，并且以后无法更改或重命名  。</span><span class="sxs-lookup"><span data-stu-id="16b4a-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![在 NuGet.org 上指定用户名](media/nuget-org-register.png) 

1. <span data-ttu-id="16b4a-124">单击“注册”按钮  。</span><span class="sxs-lookup"><span data-stu-id="16b4a-124">Click the **Register** button.</span></span>

<span data-ttu-id="16b4a-125">现在 NuGet.org 帐户已成功创建。</span><span class="sxs-lookup"><span data-stu-id="16b4a-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="16b4a-126">可以在[帐户设置](https://www.nuget.org/account)页面执行帐户管理。</span><span class="sxs-lookup"><span data-stu-id="16b4a-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>

## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="16b4a-127">启用双因素身份验证 (2FA)</span><span class="sxs-lookup"><span data-stu-id="16b4a-127">Enable two-factor authentication (2FA)</span></span>

<span data-ttu-id="16b4a-128">双因素身份验证 (2FA) 是登录网站或应用时采用的额外安全保障。</span><span class="sxs-lookup"><span data-stu-id="16b4a-128">Two-factor authentication, or 2FA, is an extra layer of security used when logging into websites or apps.</span></span> <span data-ttu-id="16b4a-129">由于 2FA，你必须使用 Microsoft 帐户 (MSA) 进行登录，并另外提供一种只有你知道或有权访问的身份验证形式。</span><span class="sxs-lookup"><span data-stu-id="16b4a-129">With 2FA, you have to log in with your Microsoft Account (MSA) and provide another form of authentication that only you know or have access to.</span></span> <span data-ttu-id="16b4a-130">为了更好地保护你的帐户，请启用双因素身份验证（推荐）。</span><span class="sxs-lookup"><span data-stu-id="16b4a-130">To better protect your account, enable two-factor authentication (recommended).</span></span>

1. <span data-ttu-id="16b4a-131">登录到你的帐户后，打开个人资料，然后选择“登录帐户”下的“启用”   。</span><span class="sxs-lookup"><span data-stu-id="16b4a-131">When logged into your account, open your profile and choose **Enable** under **Login Account**.</span></span>

   ![启用 2FA](media/nuget-org-register-2fa.png)

   <span data-ttu-id="16b4a-133">随即显示一条消息，提示你在下次登录 nuget.org  时，系统会要求提供其他凭据。</span><span class="sxs-lookup"><span data-stu-id="16b4a-133">You will see a message that tells you that the next time you sign in to *nuget.org*, you will be asked for additional credentials.</span></span>

2. <span data-ttu-id="16b4a-134">若要在此时完成身份验证，请先注销，然后再次登录。</span><span class="sxs-lookup"><span data-stu-id="16b4a-134">To complete the authentication at this time, sign out and then sign in again.</span></span>

3. <span data-ttu-id="16b4a-135">登录后，选择文本或电子邮件作为第二种形式的身份验证。</span><span class="sxs-lookup"><span data-stu-id="16b4a-135">When you sign in, choose either text or e-mail as a second form of authentication.</span></span>

   <span data-ttu-id="16b4a-136">验证已与 Microsoft 帐户关联的电话号码或电子邮件。</span><span class="sxs-lookup"><span data-stu-id="16b4a-136">Verify the phone number or e-mail that is already associated with your Microsoft account.</span></span> <span data-ttu-id="16b4a-137">可能需要为你的帐户输入一个新的电话号码或电子邮件。</span><span class="sxs-lookup"><span data-stu-id="16b4a-137">You may need to enter a new phone number or e-mail for your account.</span></span> <span data-ttu-id="16b4a-138">如果是这样，请按照说明输入所需信息，然后单击“下一步”  。</span><span class="sxs-lookup"><span data-stu-id="16b4a-138">If so, enter the required information as instructed, and click **Next**.</span></span>

   ![启用 2FA](media/nuget-org-sign-in-2fa.png)

4. <span data-ttu-id="16b4a-140">检查设备或电子邮件帐户，然后输入刚刚收到的代码。</span><span class="sxs-lookup"><span data-stu-id="16b4a-140">Check your device or e-mail account, and enter the code that you were just sent.</span></span>

   ![启用 2FA](media/nuget-org-enter-code-2fa.png)

5. <span data-ttu-id="16b4a-142">按照任何其他说明完成双因素身份验证。</span><span class="sxs-lookup"><span data-stu-id="16b4a-142">Follow any additional instructions to complete Two-factor authentication.</span></span>

> [!Tip]
> <span data-ttu-id="16b4a-143">对于可能链接了用于登录 NuGet.org 的 Microsoft 帐户的其他帐户或服务，为 NuGet.org 帐户启用 2FA 不会影响它们的身份验证设置。</span><span class="sxs-lookup"><span data-stu-id="16b4a-143">Enabling 2FA for your NuGet.org account does not impact authentication settings for other accounts or services that may be linked to the Microsoft account you use to login to NuGet.org.</span></span>

## <a name="delete-a-nugetorg-account"></a><span data-ttu-id="16b4a-144">删除 NuGet.org 帐户</span><span class="sxs-lookup"><span data-stu-id="16b4a-144">Delete a NuGet.org account</span></span>

<span data-ttu-id="16b4a-145">有关其他帐户相关任务（例如删除 NuGet.org 帐户）的帮助，请参阅 [NuGet.org 帐户管理](nuget-org-faq.md#nugetorg-account-management)。</span><span class="sxs-lookup"><span data-stu-id="16b4a-145">For help with additional account-related tasks, such as deleting a NuGet.org account, see [NuGet.org account management](nuget-org-faq.md#nugetorg-account-management).</span></span>
