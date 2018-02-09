1. <span data-ttu-id="b7c28-101">[登录你的 nuget.org 帐户](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)，或创建一个帐户（如果你还没有帐户）。</span><span class="sxs-lookup"><span data-stu-id="b7c28-101">[Sign into your nuget.org account](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) or create an account if you don't have one already.</span></span>

1. <span data-ttu-id="b7c28-102">选择用户名（在右上角），然后选择“API 密钥”。</span><span class="sxs-lookup"><span data-stu-id="b7c28-102">Select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="b7c28-103">选择“创建”，提供密钥的名称，在“API 密钥”下，选择“作用域”>“推送”，为“Glob 模式”输入“\*”，然后选择“创建”。</span><span class="sxs-lookup"><span data-stu-id="b7c28-103">Select **Create**, provide a name for your key, select **Select Scopes > Push**Under **API Key**, enter \* for **Glob pattern**, then select **Create**.</span></span>

1. <span data-ttu-id="b7c28-104">创建密钥后，选择“复制”，检索需要在 CLI 中使用的访问密钥：</span><span class="sxs-lookup"><span data-stu-id="b7c28-104">Once the key is created, select **Copy** to retrieve the access key you need in the CLI:</span></span>

    ![将 API 密钥复制到剪贴板](../media/QS_Create-02-APIKey.png)

1. <span data-ttu-id="b7c28-106">**重要事项**：将你的密钥保存在安全位置，因为以后无法再次复制密钥。</span><span class="sxs-lookup"><span data-stu-id="b7c28-106">**Important**: Save your key in a secure location because you cannot copy the key again later on.</span></span> <span data-ttu-id="b7c28-107">如果返回到 API 密钥页，则需要重新生成密钥以对其进行复制。</span><span class="sxs-lookup"><span data-stu-id="b7c28-107">If you return to the API key page, you need to regenerate the key to copy it.</span></span> <span data-ttu-id="b7c28-108">如果不再希望通过 CLI 推送包，还可以删除 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="b7c28-108">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>