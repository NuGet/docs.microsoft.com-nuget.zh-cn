---
ms.openlocfilehash: 5acdc54726e4cb07794f8ee07d5e0d357ff622a3
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842056"
---
1. <span data-ttu-id="61e41-101">[登录你的 nuget.org 帐户](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)，或创建一个帐户（如果你还没有帐户）。</span><span class="sxs-lookup"><span data-stu-id="61e41-101">[Sign into your nuget.org account](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) or create an account if you don't have one already.</span></span>

1. <span data-ttu-id="61e41-102">选择用户名（在右上角），然后选择“API 密钥”。 </span><span class="sxs-lookup"><span data-stu-id="61e41-102">Select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="61e41-103">选择“创建”  ，提供密钥名称，选择“选择范围”>“推送”  。</span><span class="sxs-lookup"><span data-stu-id="61e41-103">Select **Create**, provide a name for your key, select **Select Scopes > Push**.</span></span> <span data-ttu-id="61e41-104">输入“Glob 模式”  \*，然后选择“创建”  。</span><span class="sxs-lookup"><span data-stu-id="61e41-104">Enter \* for **Glob pattern**, then select **Create**.</span></span> <span data-ttu-id="61e41-105">（请参阅下面有关范围的详细信息。）</span><span class="sxs-lookup"><span data-stu-id="61e41-105">(See below for more about scopes.)</span></span>

1. <span data-ttu-id="61e41-106">创建密钥后，选择“复制”，检索需要在 CLI 中使用的访问密钥  ：</span><span class="sxs-lookup"><span data-stu-id="61e41-106">Once the key is created, select **Copy** to retrieve the access key you need in the CLI:</span></span>

    ![将 API 密钥复制到剪贴板](../media/QS_Create-02-APIKey.png)

1. <span data-ttu-id="61e41-108">**重要说明**：将密钥保存在安全位置，因为以后无法再次复制密钥。</span><span class="sxs-lookup"><span data-stu-id="61e41-108">**Important**: Save your key in a secure location because you cannot copy the key again later on.</span></span> <span data-ttu-id="61e41-109">如果返回到 API 密钥页，则需要重新生成密钥以对其进行复制。</span><span class="sxs-lookup"><span data-stu-id="61e41-109">If you return to the API key page, you need to regenerate the key to copy it.</span></span> <span data-ttu-id="61e41-110">如果不再希望通过 CLI 推送包，还可以删除 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="61e41-110">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>

<span data-ttu-id="61e41-111">范围允许创建针对不同用途的单独 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="61e41-111">Scoping allows you to create separate API keys for different purposes.</span></span> <span data-ttu-id="61e41-112">每个密钥都有其过期时间，并且可以将范围限定为特定包（或 glob 模式）。</span><span class="sxs-lookup"><span data-stu-id="61e41-112">Each key has its expiration timeframe and can be scoped to specific packages (or glob patterns).</span></span> <span data-ttu-id="61e41-113">每个密钥还将范围限定为特定操作：新包和更新推送、仅更新推送，或者从列表中删除。</span><span class="sxs-lookup"><span data-stu-id="61e41-113">Each key is also scoped to specific operations: push of new packages and updates, push of updates only, or delisting.</span></span> <span data-ttu-id="61e41-114">通过范围限定，可以为管理组织不同包的不同人员创建 API 密钥，这样他们就只有所需的权限。</span><span class="sxs-lookup"><span data-stu-id="61e41-114">Through scoping, you can create API keys for different people who manage packages for your organization such that they have only the permissions they need.</span></span> <span data-ttu-id="61e41-115">有关详细信息，请参阅[限定范围的 API 密钥简介](https://blog.nuget.org/20170202/introducing-scoped-api-keys.html) (blogs.nuget.org)。</span><span class="sxs-lookup"><span data-stu-id="61e41-115">For more information, see [Introducing scoped API keys](https://blog.nuget.org/20170202/introducing-scoped-api-keys.html) (blogs.nuget.org).</span></span>