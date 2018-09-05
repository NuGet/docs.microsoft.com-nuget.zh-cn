---
title: nuget.exe 凭据提供程序
description: nuget.exe 凭据提供程序进行身份验证的源，并实现为遵循特定的约定的命令行可执行文件。
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 97a44c6d561f426fa50fa068a9bbf793f77a3111
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550184"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="32e20-103">Nuget.exe 凭据提供程序使用的身份验证源</span><span class="sxs-lookup"><span data-stu-id="32e20-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="32e20-104">*NuGet 3.3 +*</span><span class="sxs-lookup"><span data-stu-id="32e20-104">*NuGet 3.3+*</span></span>

<span data-ttu-id="32e20-105">当`nuget.exe`需要凭据进行身份验证使用源，它会查找它们按以下方式：</span><span class="sxs-lookup"><span data-stu-id="32e20-105">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="32e20-106">NuGet 会首先查看凭据中`Nuget.Config`文件。</span><span class="sxs-lookup"><span data-stu-id="32e20-106">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="32e20-107">然后，NuGet 使用插件凭据提供程序，根据下面给出的顺序。</span><span class="sxs-lookup"><span data-stu-id="32e20-107">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="32e20-108">(示例中， [Visual Studio Team Services 凭据提供程序](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider)。)</span><span class="sxs-lookup"><span data-stu-id="32e20-108">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="32e20-109">然后，NuGet 会提示用户输入凭据在命令行上。</span><span class="sxs-lookup"><span data-stu-id="32e20-109">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="32e20-110">请注意，此处所述的凭据提供程序仅在工作`nuget.exe`而不是在 dotnet restore 或 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="32e20-110">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="32e20-111">使用 Visual Studio 的凭据提供程序，请参阅[nuget.exe 凭据提供程序的 Visual Studio](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="32e20-111">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="32e20-112">nuget.exe 凭据提供程序可以以三种方式使用：</span><span class="sxs-lookup"><span data-stu-id="32e20-112">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="32e20-113">**全局**： 若要使凭据提供程序可用的所有实例`nuget.exe`运行当前用户的配置文件下，将其添加到`%LocalAppData%\NuGet\CredentialProviders`。</span><span class="sxs-lookup"><span data-stu-id="32e20-113">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="32e20-114">可能需要创建`CredentialProviders`文件夹。</span><span class="sxs-lookup"><span data-stu-id="32e20-114">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="32e20-115">凭据提供程序可以安装的根目录`CredentialProviders`文件夹或子文件夹中。</span><span class="sxs-lookup"><span data-stu-id="32e20-115">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="32e20-116">如果凭据提供程序具有多个文件/程序集，可以使用子文件夹以保持组织的提供程序。</span><span class="sxs-lookup"><span data-stu-id="32e20-116">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="32e20-117">**从环境变量**： 凭据提供程序可以存储的任何位置，并可向`nuget.exe`通过设置`%NUGET_CREDENTIALPROVIDERS_PATH%`到提供程序位置的环境变量。</span><span class="sxs-lookup"><span data-stu-id="32e20-117">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="32e20-118">此变量可以是以分号分隔列表 (例如， `path1;path2`) 如果有多个位置。</span><span class="sxs-lookup"><span data-stu-id="32e20-118">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="32e20-119">**Nuget.exe 旁边**: nuget.exe 凭据提供程序可以与同一文件夹中放置`nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="32e20-119">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="32e20-120">加载凭据提供程序时`nuget.exe`名为任何文件以便将搜索上面位置、 `credentialprovider*.exe`，然后加载这些文件在发现的顺序。</span><span class="sxs-lookup"><span data-stu-id="32e20-120">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="32e20-121">如果在同一文件夹中存在多个凭据提供程序，它们按字母顺序加载。</span><span class="sxs-lookup"><span data-stu-id="32e20-121">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="32e20-122">创建一个 nuget.exe 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="32e20-122">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="32e20-123">凭据提供程序是一个命令行可执行文件，在窗体中名为`CredentialProvider*.exe`，收集输入、 获取凭据根据需要，，然后返回相应的退出状态代码和标准输出。</span><span class="sxs-lookup"><span data-stu-id="32e20-123">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="32e20-124">一个提供程序必须执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="32e20-124">A provider must do the following:</span></span>

- <span data-ttu-id="32e20-125">确定是否它可提供凭据的目标 URI 启动凭据获取之前。</span><span class="sxs-lookup"><span data-stu-id="32e20-125">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="32e20-126">如果没有，它应返回状态代码为没有凭据的 1。</span><span class="sxs-lookup"><span data-stu-id="32e20-126">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="32e20-127">不修改`Nuget.Config`（如那里设置凭据）。</span><span class="sxs-lookup"><span data-stu-id="32e20-127">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="32e20-128">在其自身的、 作为 NuGet 上的句柄 HTTP 代理配置不提供到该插件的代理信息。</span><span class="sxs-lookup"><span data-stu-id="32e20-128">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="32e20-129">返回凭据或错误详细信息到`nuget.exe`通过写入到 stdout，使用 utf-8 编码的 JSON 响应对象 （见下文）。</span><span class="sxs-lookup"><span data-stu-id="32e20-129">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="32e20-130">选择性地将发出附加的跟踪日志记录到 stderr。</span><span class="sxs-lookup"><span data-stu-id="32e20-130">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="32e20-131">由于详细程度级别"normal"或"详细"在此类跟踪将回显 nuget 到控制台，任何机密应不断将不写入到 stderr。</span><span class="sxs-lookup"><span data-stu-id="32e20-131">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="32e20-132">应忽略意外的参数，提供与未来版本的 NuGet 的向前兼容性。</span><span class="sxs-lookup"><span data-stu-id="32e20-132">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="32e20-133">输入的参数</span><span class="sxs-lookup"><span data-stu-id="32e20-133">Input parameters</span></span>

| <span data-ttu-id="32e20-134">参数/切换</span><span class="sxs-lookup"><span data-stu-id="32e20-134">Parameter/Switch</span></span> |<span data-ttu-id="32e20-135">描述</span><span class="sxs-lookup"><span data-stu-id="32e20-135">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="32e20-136">Uri {value}</span><span class="sxs-lookup"><span data-stu-id="32e20-136">Uri {value}</span></span> | <span data-ttu-id="32e20-137">包源 URI 需要凭据。</span><span class="sxs-lookup"><span data-stu-id="32e20-137">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="32e20-138">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="32e20-138">NonInteractive</span></span> | <span data-ttu-id="32e20-139">如果存在，则提供程序不会发出交互式提示。</span><span class="sxs-lookup"><span data-stu-id="32e20-139">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="32e20-140">IsRetry</span><span class="sxs-lookup"><span data-stu-id="32e20-140">IsRetry</span></span> | <span data-ttu-id="32e20-141">如果存在，则指示此尝试进行尝试之前失败的重试。</span><span class="sxs-lookup"><span data-stu-id="32e20-141">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="32e20-142">提供程序通常使用此标志，以确保它们绕过任何现有的缓存，如有可能提示输入新凭据。</span><span class="sxs-lookup"><span data-stu-id="32e20-142">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="32e20-143">详细级别 {value}</span><span class="sxs-lookup"><span data-stu-id="32e20-143">Verbosity {value}</span></span> | <span data-ttu-id="32e20-144">如果存在，以下值之一:"正常"、"quiet"详细"。</span><span class="sxs-lookup"><span data-stu-id="32e20-144">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="32e20-145">如果不提供任何值，默认为"normal"。</span><span class="sxs-lookup"><span data-stu-id="32e20-145">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="32e20-146">提供程序应将它用作表示的可选日志记录级别发出到标准错误流。</span><span class="sxs-lookup"><span data-stu-id="32e20-146">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="32e20-147">退出代码</span><span class="sxs-lookup"><span data-stu-id="32e20-147">Exit codes</span></span>

| <span data-ttu-id="32e20-148">代码</span><span class="sxs-lookup"><span data-stu-id="32e20-148">Code</span></span> |<span data-ttu-id="32e20-149">结果</span><span class="sxs-lookup"><span data-stu-id="32e20-149">Result</span></span> | <span data-ttu-id="32e20-150">描述</span><span class="sxs-lookup"><span data-stu-id="32e20-150">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="32e20-151">0</span><span class="sxs-lookup"><span data-stu-id="32e20-151">0</span></span> | <span data-ttu-id="32e20-152">成功</span><span class="sxs-lookup"><span data-stu-id="32e20-152">Success</span></span> | <span data-ttu-id="32e20-153">凭据成功获取和已写入到 stdout。</span><span class="sxs-lookup"><span data-stu-id="32e20-153">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="32e20-154">1</span><span class="sxs-lookup"><span data-stu-id="32e20-154">1</span></span> | <span data-ttu-id="32e20-155">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="32e20-155">ProviderNotApplicable</span></span> | <span data-ttu-id="32e20-156">当前提供程序不提供有关给定 URI 的凭据。</span><span class="sxs-lookup"><span data-stu-id="32e20-156">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="32e20-157">2</span><span class="sxs-lookup"><span data-stu-id="32e20-157">2</span></span> | <span data-ttu-id="32e20-158">失败</span><span class="sxs-lookup"><span data-stu-id="32e20-158">Failure</span></span> | <span data-ttu-id="32e20-159">提供程序是正确的访问接口对于给定的 URI，但不能提供凭据。</span><span class="sxs-lookup"><span data-stu-id="32e20-159">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="32e20-160">在这种情况下，nuget.exe 不会重试身份验证，并且将失败。</span><span class="sxs-lookup"><span data-stu-id="32e20-160">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="32e20-161">典型示例是当用户取消交互式登录。</span><span class="sxs-lookup"><span data-stu-id="32e20-161">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="32e20-162">标准输出</span><span class="sxs-lookup"><span data-stu-id="32e20-162">Standard output</span></span>

| <span data-ttu-id="32e20-163">属性</span><span class="sxs-lookup"><span data-stu-id="32e20-163">Property</span></span> |<span data-ttu-id="32e20-164">说明</span><span class="sxs-lookup"><span data-stu-id="32e20-164">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="32e20-165">用户名</span><span class="sxs-lookup"><span data-stu-id="32e20-165">Username</span></span> | <span data-ttu-id="32e20-166">对于经过身份验证请求的用户名。</span><span class="sxs-lookup"><span data-stu-id="32e20-166">Username for authenticated requests.</span></span>|
| <span data-ttu-id="32e20-167">Password</span><span class="sxs-lookup"><span data-stu-id="32e20-167">Password</span></span> | <span data-ttu-id="32e20-168">经过身份验证请求的密码。</span><span class="sxs-lookup"><span data-stu-id="32e20-168">Password for authenticated requests.</span></span>|
| <span data-ttu-id="32e20-169">消息</span><span class="sxs-lookup"><span data-stu-id="32e20-169">Message</span></span> | <span data-ttu-id="32e20-170">有关响应，仅用于在故障情况下显示的其他详细信息的可选详细信息。</span><span class="sxs-lookup"><span data-stu-id="32e20-170">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="32e20-171">示例 stdout:</span><span class="sxs-lookup"><span data-stu-id="32e20-171">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="32e20-172">凭据提供程序进行故障排除</span><span class="sxs-lookup"><span data-stu-id="32e20-172">Troubleshooting a credential provider</span></span>

<span data-ttu-id="32e20-173">目前，NuGet 不会提供更直接的支持的调试自定义凭据提供程序;[发出 4598](https://github.com/NuGet/Home/issues/4598)跟踪这项工作。</span><span class="sxs-lookup"><span data-stu-id="32e20-173">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="32e20-174">你还可以执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="32e20-174">You can also do the following:</span></span>

- <span data-ttu-id="32e20-175">运行使用 nuget.exe`-verbosity`开关可以检查详细的输出。</span><span class="sxs-lookup"><span data-stu-id="32e20-175">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="32e20-176">添加到调试消息`stdout`中相应的位置。</span><span class="sxs-lookup"><span data-stu-id="32e20-176">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="32e20-177">请确保使用 nuget.exe 3.3 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="32e20-177">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="32e20-178">附加调试程序在启动时使用此代码片段：</span><span class="sxs-lookup"><span data-stu-id="32e20-178">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="32e20-179">获取更多帮助[提交支持请求 nuget.org](https://www.nuget.org/policies/Contact)。</span><span class="sxs-lookup"><span data-stu-id="32e20-179">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
