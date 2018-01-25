---
title: "nuget.exe 凭据提供程序 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "nuget.exe 凭据提供程序将具有源，身份验证，并实现为遵循特定的约定的命令行可执行文件。"
keywords: "nuget.exe 凭据提供程序，凭据提供程序 API，将具有源进行身份验证，使用库进行身份验证"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88ce0106ad4e628ba8120f94b7951c7746ab67f3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="55a5a-104">进行身份验证与 nuget.exe 凭据提供程序的源</span><span class="sxs-lookup"><span data-stu-id="55a5a-104">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="55a5a-105">*NuGet 3.3 +*</span><span class="sxs-lookup"><span data-stu-id="55a5a-105">*NuGet 3.3+*</span></span>

<span data-ttu-id="55a5a-106">当`nuget.exe`需要凭据进行身份验证将具有源，则查找它们按以下方式：</span><span class="sxs-lookup"><span data-stu-id="55a5a-106">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="55a5a-107">NuGet 首先查找中的凭据`Nuget.Config`文件。</span><span class="sxs-lookup"><span data-stu-id="55a5a-107">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="55a5a-108">NuGet 然后使用插件的凭据提供程序，根据下面列出的顺序。</span><span class="sxs-lookup"><span data-stu-id="55a5a-108">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="55a5a-109">(和示例是[Visual Studio Team Services 凭据提供程序](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider)。)</span><span class="sxs-lookup"><span data-stu-id="55a5a-109">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="55a5a-110">NuGet 然后会提示用户提供命令行上的凭据。</span><span class="sxs-lookup"><span data-stu-id="55a5a-110">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="55a5a-111">请注意，此处所述的凭据提供程序仅在工作`nuget.exe`，不能在 dotnet 还原或 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="55a5a-111">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="55a5a-112">有关通过 Visual Studio 使用的凭据提供程序，请参阅[nuget.exe for Visual Studio 的凭据提供程序](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="55a5a-112">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="55a5a-113">nuget.exe 凭据提供程序可以采用下列 3 种方法：</span><span class="sxs-lookup"><span data-stu-id="55a5a-113">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="55a5a-114">**全局**： 要提供给所有实例的凭据提供程序`nuget.exe`运行在当前用户的配置文件下，将其添加到`%LocalAppData%\NuGet\CredentialProviders`。</span><span class="sxs-lookup"><span data-stu-id="55a5a-114">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="55a5a-115">你可能需要创建`CredentialProviders`文件夹。</span><span class="sxs-lookup"><span data-stu-id="55a5a-115">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="55a5a-116">凭据提供程序可以安装的根目录`CredentialProviders`文件夹或子文件夹内。</span><span class="sxs-lookup"><span data-stu-id="55a5a-116">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="55a5a-117">如果凭据提供程序具有多个文件/程序集，你可以使用子文件夹需要组织的提供程序。</span><span class="sxs-lookup"><span data-stu-id="55a5a-117">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="55a5a-118">**从环境变量**： 凭据提供程序可以存储任何位置，可以访问`nuget.exe`通过设置`%NUGET_CREDENTIALPROVIDERS_PATH%`到提供程序位置的环境变量。</span><span class="sxs-lookup"><span data-stu-id="55a5a-118">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="55a5a-119">此变量可以是以分号分隔的列表 (例如， `path1;path2`) 如果你有多个位置。</span><span class="sxs-lookup"><span data-stu-id="55a5a-119">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="55a5a-120">**与 nuget.exe 一起**: nuget.exe 凭据提供程序可以与同一文件夹中放置`nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="55a5a-120">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="55a5a-121">在加载凭据提供程序时`nuget.exe`顺序情况下，名为任何文件将搜索上面的位置， `credentialprovider*.exe`，然后加载这些文件要找到它们的顺序。</span><span class="sxs-lookup"><span data-stu-id="55a5a-121">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="55a5a-122">如果在同一文件夹中存在多个凭据提供程序，它们按字母顺序加载。</span><span class="sxs-lookup"><span data-stu-id="55a5a-122">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="55a5a-123">创建 nuget.exe 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="55a5a-123">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="55a5a-124">凭据提供程序是一个命令行可执行文件，在窗体中名为`CredentialProvider*.exe`，收集输入、 获取视情况而定的凭据，然后返回相应的退出状态代码和标准输出。</span><span class="sxs-lookup"><span data-stu-id="55a5a-124">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="55a5a-125">一个提供程序必须执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="55a5a-125">A provider must do the following:</span></span>

- <span data-ttu-id="55a5a-126">确定是否可以在启动凭据获取之前目标 uri 提供凭据。</span><span class="sxs-lookup"><span data-stu-id="55a5a-126">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="55a5a-127">如果没有，则应返回状态代码没有凭据的 1。</span><span class="sxs-lookup"><span data-stu-id="55a5a-127">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="55a5a-128">不修改`Nuget.Config`（如存在设置凭据）。</span><span class="sxs-lookup"><span data-stu-id="55a5a-128">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="55a5a-129">它本身，作为 NuGet 上的句柄 HTTP 代理配置不提供到该插件的代理信息。</span><span class="sxs-lookup"><span data-stu-id="55a5a-129">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="55a5a-130">返回凭据或错误详细信息，以便`nuget.exe`通过向 stdout，使用 utf-8 编码写入 JSON 响应对象 （见下文）。</span><span class="sxs-lookup"><span data-stu-id="55a5a-130">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="55a5a-131">（可选） 发出到 stderr 的其他跟踪日志记录。</span><span class="sxs-lookup"><span data-stu-id="55a5a-131">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="55a5a-132">由于详细程度级别"normal"或"详细"在此类跟踪将回显 nuget 到控制台，则不断应到 stderr，不编写任何密钥。</span><span class="sxs-lookup"><span data-stu-id="55a5a-132">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="55a5a-133">应忽略意外的参数，提供与将来版本的 NuGet 的向前兼容性。</span><span class="sxs-lookup"><span data-stu-id="55a5a-133">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="55a5a-134">输入的参数</span><span class="sxs-lookup"><span data-stu-id="55a5a-134">Input parameters</span></span>

| <span data-ttu-id="55a5a-135">参数/开关</span><span class="sxs-lookup"><span data-stu-id="55a5a-135">Parameter/Switch</span></span> |<span data-ttu-id="55a5a-136">描述</span><span class="sxs-lookup"><span data-stu-id="55a5a-136">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="55a5a-137">Uri {value}</span><span class="sxs-lookup"><span data-stu-id="55a5a-137">Uri {value}</span></span> | <span data-ttu-id="55a5a-138">包源 URI 需要凭据。</span><span class="sxs-lookup"><span data-stu-id="55a5a-138">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="55a5a-139">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="55a5a-139">NonInteractive</span></span> | <span data-ttu-id="55a5a-140">如果存在，则提供程序不会颁发交互式提示。</span><span class="sxs-lookup"><span data-stu-id="55a5a-140">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="55a5a-141">IsRetry</span><span class="sxs-lookup"><span data-stu-id="55a5a-141">IsRetry</span></span> | <span data-ttu-id="55a5a-142">如果存在，则表明此尝试是以前失败的尝试的重试。</span><span class="sxs-lookup"><span data-stu-id="55a5a-142">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="55a5a-143">提供程序通常使用此标志，以确保它们绕过任何现有的缓存，并尽可能提示输入新凭据。</span><span class="sxs-lookup"><span data-stu-id="55a5a-143">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="55a5a-144">详细级别 {value}</span><span class="sxs-lookup"><span data-stu-id="55a5a-144">Verbosity {value}</span></span> | <span data-ttu-id="55a5a-145">如果存在，以下值之一:"正常"、"静默"详细"。</span><span class="sxs-lookup"><span data-stu-id="55a5a-145">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="55a5a-146">如果没有提供值时，默认为"normal"。</span><span class="sxs-lookup"><span data-stu-id="55a5a-146">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="55a5a-147">提供程序应使用此的可选日志记录级别用于指示写入标准错误流发出。</span><span class="sxs-lookup"><span data-stu-id="55a5a-147">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="55a5a-148">退出代码</span><span class="sxs-lookup"><span data-stu-id="55a5a-148">Exit codes</span></span>

| <span data-ttu-id="55a5a-149">代码</span><span class="sxs-lookup"><span data-stu-id="55a5a-149">Code</span></span> |<span data-ttu-id="55a5a-150">结果</span><span class="sxs-lookup"><span data-stu-id="55a5a-150">Result</span></span> | <span data-ttu-id="55a5a-151">描述</span><span class="sxs-lookup"><span data-stu-id="55a5a-151">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="55a5a-152">0</span><span class="sxs-lookup"><span data-stu-id="55a5a-152">0</span></span> | <span data-ttu-id="55a5a-153">成功</span><span class="sxs-lookup"><span data-stu-id="55a5a-153">Success</span></span> | <span data-ttu-id="55a5a-154">凭据已成功获取和已写入到 stdout。</span><span class="sxs-lookup"><span data-stu-id="55a5a-154">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="55a5a-155">1</span><span class="sxs-lookup"><span data-stu-id="55a5a-155">1</span></span> | <span data-ttu-id="55a5a-156">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="55a5a-156">ProviderNotApplicable</span></span> | <span data-ttu-id="55a5a-157">当前提供程序不提供有关给定 URI 的凭据。</span><span class="sxs-lookup"><span data-stu-id="55a5a-157">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="55a5a-158">2</span><span class="sxs-lookup"><span data-stu-id="55a5a-158">2</span></span> | <span data-ttu-id="55a5a-159">失败</span><span class="sxs-lookup"><span data-stu-id="55a5a-159">Failure</span></span> | <span data-ttu-id="55a5a-160">提供程序是正确的提供程序的给定的 URI，但不能提供凭据。</span><span class="sxs-lookup"><span data-stu-id="55a5a-160">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="55a5a-161">在这种情况下，nuget.exe 不会重试身份验证，并且将失败。</span><span class="sxs-lookup"><span data-stu-id="55a5a-161">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="55a5a-162">一个典型示例是当用户取消交互式登录。</span><span class="sxs-lookup"><span data-stu-id="55a5a-162">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="55a5a-163">标准输出</span><span class="sxs-lookup"><span data-stu-id="55a5a-163">Standard output</span></span>

| <span data-ttu-id="55a5a-164">属性</span><span class="sxs-lookup"><span data-stu-id="55a5a-164">Property</span></span> |<span data-ttu-id="55a5a-165">说明</span><span class="sxs-lookup"><span data-stu-id="55a5a-165">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="55a5a-166">用户名</span><span class="sxs-lookup"><span data-stu-id="55a5a-166">Username</span></span> | <span data-ttu-id="55a5a-167">对于验证的请求的用户名。</span><span class="sxs-lookup"><span data-stu-id="55a5a-167">Username for authenticated requests.</span></span>|
| <span data-ttu-id="55a5a-168">Password</span><span class="sxs-lookup"><span data-stu-id="55a5a-168">Password</span></span> | <span data-ttu-id="55a5a-169">经过身份验证请求密码。</span><span class="sxs-lookup"><span data-stu-id="55a5a-169">Password for authenticated requests.</span></span>|
| <span data-ttu-id="55a5a-170">消息</span><span class="sxs-lookup"><span data-stu-id="55a5a-170">Message</span></span> | <span data-ttu-id="55a5a-171">有关响应，仅用于在故障情况下显示更多细节的可选详细信息。</span><span class="sxs-lookup"><span data-stu-id="55a5a-171">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="55a5a-172">示例 stdout:</span><span class="sxs-lookup"><span data-stu-id="55a5a-172">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="55a5a-173">故障排除凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="55a5a-173">Troubleshooting a credential provider</span></span>

<span data-ttu-id="55a5a-174">目前，NuGet 不提供多直接支持针对调试自定义凭据提供程序;[发出 4598](https://github.com/NuGet/Home/issues/4598)跟踪此工作。</span><span class="sxs-lookup"><span data-stu-id="55a5a-174">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="55a5a-175">你还可以执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="55a5a-175">You can also do the following:</span></span>

- <span data-ttu-id="55a5a-176">运行与 nuget.exe`-verbosity`开关来检查详细的输出。</span><span class="sxs-lookup"><span data-stu-id="55a5a-176">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="55a5a-177">添加到调试消息`stdout`在适当的位置。</span><span class="sxs-lookup"><span data-stu-id="55a5a-177">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="55a5a-178">请确保你使用的 nuget.exe 3.3 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="55a5a-178">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="55a5a-179">附加调试器在启动时，此代码片段：</span><span class="sxs-lookup"><span data-stu-id="55a5a-179">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="55a5a-180">有关进一步的帮助，[提交支持请求 nuget.org](https://www.nuget.org/policies/Contact)。</span><span class="sxs-lookup"><span data-stu-id="55a5a-180">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
