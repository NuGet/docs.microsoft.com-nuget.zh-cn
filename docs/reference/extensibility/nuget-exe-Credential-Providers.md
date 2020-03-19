---
title: nuget.exe 凭据提供程序
description: nuget.exe 凭据提供程序使用源进行身份验证，并以遵循特定约定的命令行可执行文件的形式实现。
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 41e3e63138351bafd5e3a56080268faef10d85a3
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428299"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="2530f-103">用 nuget.exe 凭据提供程序对源进行身份验证</span><span class="sxs-lookup"><span data-stu-id="2530f-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="2530f-104">在版本 `3.3` 为 `nuget.exe` 特定凭据提供程序添加了支持。</span><span class="sxs-lookup"><span data-stu-id="2530f-104">In version `3.3` support was added for `nuget.exe` specific credential providers.</span></span> <span data-ttu-id="2530f-105">自那时起，在版本 `4.8` 支持跨所有命令行方案（`nuget.exe`、`dotnet.exe``msbuild.exe`）的[凭据提供程序](NuGet-Cross-Platform-Authentication-Plugin.md)。</span><span class="sxs-lookup"><span data-stu-id="2530f-105">Since then, in version `4.8` [support for credential providers](NuGet-Cross-Platform-Authentication-Plugin.md) that work across all command line scenarios (`nuget.exe`, `dotnet.exe`, `msbuild.exe`) was added.</span></span>

<span data-ttu-id="2530f-106">有关 `nuget.exe` 的所有身份验证方法的详细信息，请参阅[使用已通过身份验证的源中的包](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe)</span><span class="sxs-lookup"><span data-stu-id="2530f-106">See [Consuming Packages from authenticated feeds](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) for more details on all authentication approaches for `nuget.exe`</span></span>

## <a name="nugetexe-credential-provider-discovery"></a><span data-ttu-id="2530f-107">nuget.exe 凭据提供程序发现</span><span class="sxs-lookup"><span data-stu-id="2530f-107">nuget.exe credential provider discovery</span></span>

<span data-ttu-id="2530f-108">可以通过3种方式使用 nuget.exe 凭据提供程序：</span><span class="sxs-lookup"><span data-stu-id="2530f-108">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="2530f-109">**全局**：若要使凭据提供程序可用于在当前用户的配置文件下运行 `nuget.exe` 的所有实例，请将其添加到 `%LocalAppData%\NuGet\CredentialProviders`中。</span><span class="sxs-lookup"><span data-stu-id="2530f-109">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="2530f-110">可能需要创建 `CredentialProviders` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="2530f-110">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="2530f-111">凭据提供程序可以安装在 `CredentialProviders` 文件夹的根目录或子文件夹中。</span><span class="sxs-lookup"><span data-stu-id="2530f-111">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="2530f-112">如果凭据提供程序具有多个文件/程序集，则可以使用子文件夹来保持提供程序的组织。</span><span class="sxs-lookup"><span data-stu-id="2530f-112">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="2530f-113">**从环境变量中**：凭据提供程序可以存储在任何位置，并可通过将 `%NUGET_CREDENTIALPROVIDERS_PATH%` 环境变量设置为提供程序位置来访问 `nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="2530f-113">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="2530f-114">如果有多个位置，则此变量可以是以分号分隔的列表（例如 `path1;path2`）。</span><span class="sxs-lookup"><span data-stu-id="2530f-114">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="2530f-115">除了**nuget.exe，还**可以将 nuget.exe 凭据提供程序放在与 `nuget.exe`相同的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="2530f-115">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="2530f-116">加载凭据提供程序时，`nuget.exe` 会按顺序搜索前面的任何名为 `credentialprovider*.exe`的文件，然后按找到的顺序加载这些文件。</span><span class="sxs-lookup"><span data-stu-id="2530f-116">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="2530f-117">如果同一文件夹中存在多个凭据提供程序，则按字母顺序加载它们。</span><span class="sxs-lookup"><span data-stu-id="2530f-117">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="2530f-118">创建 nuget.exe 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="2530f-118">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="2530f-119">凭据提供程序是一个命令行可执行文件，它以 `CredentialProvider*.exe`格式指定，可收集输入，根据需要获取凭据，然后返回相应的退出状态代码和标准输出。</span><span class="sxs-lookup"><span data-stu-id="2530f-119">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="2530f-120">提供程序必须执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="2530f-120">A provider must do the following:</span></span>

- <span data-ttu-id="2530f-121">确定是否可以在启动凭据获取之前为目标 URI 提供凭据。</span><span class="sxs-lookup"><span data-stu-id="2530f-121">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="2530f-122">如果不是，则它应返回无凭据的状态代码1。</span><span class="sxs-lookup"><span data-stu-id="2530f-122">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="2530f-123">不修改 `Nuget.Config` （例如在此处设置凭据）。</span><span class="sxs-lookup"><span data-stu-id="2530f-123">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="2530f-124">自行处理 HTTP 代理配置，因为 NuGet 不向插件提供代理信息。</span><span class="sxs-lookup"><span data-stu-id="2530f-124">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="2530f-125">使用 UTF-8 编码将 JSON 响应对象（见下文）写入 stdout，从而将凭据或错误详细信息返回给 `nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="2530f-125">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="2530f-126">（可选）向 stderr 发出附加跟踪日志记录。</span><span class="sxs-lookup"><span data-stu-id="2530f-126">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="2530f-127">不应将任何机密写入到 stderr，因为在详细级别 "正常" 或 "详细" 时，此类跟踪会回显到控制台。</span><span class="sxs-lookup"><span data-stu-id="2530f-127">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="2530f-128">应忽略意外参数，以提供与 NuGet 的未来版本的向前兼容性。</span><span class="sxs-lookup"><span data-stu-id="2530f-128">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2530f-129">输入参数</span><span class="sxs-lookup"><span data-stu-id="2530f-129">Input parameters</span></span>

| <span data-ttu-id="2530f-130">参数/开关</span><span class="sxs-lookup"><span data-stu-id="2530f-130">Parameter/Switch</span></span> |<span data-ttu-id="2530f-131">说明</span><span class="sxs-lookup"><span data-stu-id="2530f-131">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="2530f-132">Uri {value}</span><span class="sxs-lookup"><span data-stu-id="2530f-132">Uri {value}</span></span> | <span data-ttu-id="2530f-133">需要凭据的包源 URI。</span><span class="sxs-lookup"><span data-stu-id="2530f-133">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="2530f-134">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2530f-134">NonInteractive</span></span> | <span data-ttu-id="2530f-135">如果存在，则提供程序不会发出交互式提示。</span><span class="sxs-lookup"><span data-stu-id="2530f-135">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="2530f-136">IsRetry</span><span class="sxs-lookup"><span data-stu-id="2530f-136">IsRetry</span></span> | <span data-ttu-id="2530f-137">如果存在，则指示此尝试将重试先前失败的尝试。</span><span class="sxs-lookup"><span data-stu-id="2530f-137">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="2530f-138">提供程序通常使用此标志来确保它们绕过任何现有缓存，并在可能的情况下提示输入新凭据。</span><span class="sxs-lookup"><span data-stu-id="2530f-138">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="2530f-139">详细程度 {值}</span><span class="sxs-lookup"><span data-stu-id="2530f-139">Verbosity {value}</span></span> | <span data-ttu-id="2530f-140">如果存在，则为以下值之一： "normal"、"quiet" 或 "详细"。</span><span class="sxs-lookup"><span data-stu-id="2530f-140">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="2530f-141">如果未提供任何值，则默认为 "normal"。</span><span class="sxs-lookup"><span data-stu-id="2530f-141">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="2530f-142">提供程序应使用此选项来指示要发出到标准错误流的可选日志记录级别。</span><span class="sxs-lookup"><span data-stu-id="2530f-142">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="2530f-143">退出代码</span><span class="sxs-lookup"><span data-stu-id="2530f-143">Exit codes</span></span>

| <span data-ttu-id="2530f-144">代码</span><span class="sxs-lookup"><span data-stu-id="2530f-144">Code</span></span> |<span data-ttu-id="2530f-145">结果</span><span class="sxs-lookup"><span data-stu-id="2530f-145">Result</span></span> | <span data-ttu-id="2530f-146">说明</span><span class="sxs-lookup"><span data-stu-id="2530f-146">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="2530f-147">0</span><span class="sxs-lookup"><span data-stu-id="2530f-147">0</span></span> | <span data-ttu-id="2530f-148">成功</span><span class="sxs-lookup"><span data-stu-id="2530f-148">Success</span></span> | <span data-ttu-id="2530f-149">已成功获取凭据并已将其写入 stdout。</span><span class="sxs-lookup"><span data-stu-id="2530f-149">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="2530f-150">1</span><span class="sxs-lookup"><span data-stu-id="2530f-150">1</span></span> | <span data-ttu-id="2530f-151">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="2530f-151">ProviderNotApplicable</span></span> | <span data-ttu-id="2530f-152">当前提供程序不提供给定 URI 的凭据。</span><span class="sxs-lookup"><span data-stu-id="2530f-152">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="2530f-153">2</span><span class="sxs-lookup"><span data-stu-id="2530f-153">2</span></span> | <span data-ttu-id="2530f-154">失败</span><span class="sxs-lookup"><span data-stu-id="2530f-154">Failure</span></span> | <span data-ttu-id="2530f-155">提供程序是给定 URI 的正确提供程序，但不能提供凭据。</span><span class="sxs-lookup"><span data-stu-id="2530f-155">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="2530f-156">在这种情况下，nuget.exe 不会重试身份验证，并且会失败。</span><span class="sxs-lookup"><span data-stu-id="2530f-156">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="2530f-157">典型的示例是用户取消交互式登录时。</span><span class="sxs-lookup"><span data-stu-id="2530f-157">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="2530f-158">标准输出</span><span class="sxs-lookup"><span data-stu-id="2530f-158">Standard output</span></span>

| <span data-ttu-id="2530f-159">属性</span><span class="sxs-lookup"><span data-stu-id="2530f-159">Property</span></span> |<span data-ttu-id="2530f-160">注意</span><span class="sxs-lookup"><span data-stu-id="2530f-160">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="2530f-161">用户名</span><span class="sxs-lookup"><span data-stu-id="2530f-161">Username</span></span> | <span data-ttu-id="2530f-162">经过身份验证的请求的用户名。</span><span class="sxs-lookup"><span data-stu-id="2530f-162">Username for authenticated requests.</span></span>|
| <span data-ttu-id="2530f-163">Password</span><span class="sxs-lookup"><span data-stu-id="2530f-163">Password</span></span> | <span data-ttu-id="2530f-164">经过身份验证的请求的密码。</span><span class="sxs-lookup"><span data-stu-id="2530f-164">Password for authenticated requests.</span></span>|
| <span data-ttu-id="2530f-165">Message</span><span class="sxs-lookup"><span data-stu-id="2530f-165">Message</span></span> | <span data-ttu-id="2530f-166">有关响应的可选详细信息，仅用于显示故障情况下的其他详细信息。</span><span class="sxs-lookup"><span data-stu-id="2530f-166">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="2530f-167">示例 stdout：</span><span class="sxs-lookup"><span data-stu-id="2530f-167">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="2530f-168">凭据提供程序故障排除</span><span class="sxs-lookup"><span data-stu-id="2530f-168">Troubleshooting a credential provider</span></span>

<span data-ttu-id="2530f-169">目前，NuGet 并不能直接支持调试自定义凭据提供程序;[问题 4598](https://github.com/NuGet/Home/issues/4598)正在跟踪此工作。</span><span class="sxs-lookup"><span data-stu-id="2530f-169">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="2530f-170">也可以执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="2530f-170">You can also do the following:</span></span>

- <span data-ttu-id="2530f-171">运行带有 `-verbosity` 开关的 nuget.exe 以检查详细的输出。</span><span class="sxs-lookup"><span data-stu-id="2530f-171">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="2530f-172">将调试消息添加到 `stdout` 在适当的位置。</span><span class="sxs-lookup"><span data-stu-id="2530f-172">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="2530f-173">请确保使用的是 nuget.exe 3.3 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="2530f-173">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="2530f-174">在启动时将调试器附加到以下代码片段：</span><span class="sxs-lookup"><span data-stu-id="2530f-174">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
