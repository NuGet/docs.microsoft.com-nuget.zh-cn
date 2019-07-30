---
ms.openlocfilehash: 20851cd71cc5eb6735fe5e0cd8b0f314f9100be4
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419917"
---
1. <span data-ttu-id="b33a5-101">[登录你的 nuget.org 帐户](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)，或创建一个帐户（如果你还没有帐户）。</span><span class="sxs-lookup"><span data-stu-id="b33a5-101">[Sign into your nuget.org account](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) or create an account if you don't have one already.</span></span>

   <span data-ttu-id="b33a5-102">有关创建帐户的详细信息，请参阅[个人帐户](../../nuget-org/individual-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="b33a5-102">For more information on creating your account, see [Individual accounts](../../nuget-org/individual-accounts.md).</span></span>

1. <span data-ttu-id="b33a5-103">选择用户名（在右上角），然后选择“API 密钥”。 </span><span class="sxs-lookup"><span data-stu-id="b33a5-103">Select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="b33a5-104">选择“创建”  ，提供密钥名称，选择“选择范围”>“推送”  。</span><span class="sxs-lookup"><span data-stu-id="b33a5-104">Select **Create**, provide a name for your key, select **Select Scopes > Push**.</span></span> <span data-ttu-id="b33a5-105">输入“Glob 模式”  \*，然后选择“创建”  。</span><span class="sxs-lookup"><span data-stu-id="b33a5-105">Enter \* for **Glob pattern**, then select **Create**.</span></span> <span data-ttu-id="b33a5-106">（请参阅下面有关范围的详细信息。）</span><span class="sxs-lookup"><span data-stu-id="b33a5-106">(See below for more about scopes.)</span></span>

1. <span data-ttu-id="b33a5-107">创建密钥后，选择“复制”，检索需要在 CLI 中使用的访问密钥  ：</span><span class="sxs-lookup"><span data-stu-id="b33a5-107">Once the key is created, select **Copy** to retrieve the access key you need in the CLI:</span></span>

    ![将 API 密钥复制到剪贴板](../media/QS_Create-02-APIKey.png)

1. <span data-ttu-id="b33a5-109">**重要说明**：将密钥保存在安全位置，因为以后无法再次复制密钥。</span><span class="sxs-lookup"><span data-stu-id="b33a5-109">**Important**: Save your key in a secure location because you cannot copy the key again later on.</span></span> <span data-ttu-id="b33a5-110">如果返回到 API 密钥页，则需要重新生成密钥以对其进行复制。</span><span class="sxs-lookup"><span data-stu-id="b33a5-110">If you return to the API key page, you need to regenerate the key to copy it.</span></span> <span data-ttu-id="b33a5-111">如果不再希望通过 CLI 推送包，还可以删除 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="b33a5-111">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>

<span data-ttu-id="b33a5-112">范围允许创建针对不同用途的单独 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="b33a5-112">Scoping allows you to create separate API keys for different purposes.</span></span> <span data-ttu-id="b33a5-113">每个密钥都有其过期时间，并且可以将范围限定为特定包（或 glob 模式）。</span><span class="sxs-lookup"><span data-stu-id="b33a5-113">Each key has its expiration timeframe and can be scoped to specific packages (or glob patterns).</span></span> <span data-ttu-id="b33a5-114">每个密钥还将范围限定为特定操作：新包和更新推送、仅更新推送，或者从列表中删除。</span><span class="sxs-lookup"><span data-stu-id="b33a5-114">Each key is also scoped to specific operations: push of new packages and updates, push of updates only, or delisting.</span></span> <span data-ttu-id="b33a5-115">通过范围限定，可以为管理组织不同包的不同人员创建 API 密钥，这样他们就只有所需的权限。</span><span class="sxs-lookup"><span data-stu-id="b33a5-115">Through scoping, you can create API keys for different people who manage packages for your organization such that they have only the permissions they need.</span></span> <span data-ttu-id="b33a5-116">有关详细信息，请参阅[范围内的 API 密钥](../../nuget-org/scoped-api-keys.md)。</span><span class="sxs-lookup"><span data-stu-id="b33a5-116">For more information, see [scoped API keys](../../nuget-org/scoped-api-keys.md).</span></span>