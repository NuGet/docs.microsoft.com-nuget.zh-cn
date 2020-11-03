---
title: nuget.exe 凭据提供程序
description: nuget.exe 凭据提供程序使用源进行身份验证，并以遵循特定约定的命令行可执行文件的形式实现。
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 41e3e63138351bafd5e3a56080268faef10d85a3
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238109"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="f3c17-103">通过 nuget.exe 凭据提供程序对源进行身份验证</span><span class="sxs-lookup"><span data-stu-id="f3c17-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="f3c17-104">在中， `3.3` 为特定的 `nuget.exe` 凭据提供程序添加了版本支持。</span><span class="sxs-lookup"><span data-stu-id="f3c17-104">In version `3.3` support was added for `nuget.exe` specific credential providers.</span></span> <span data-ttu-id="f3c17-105">从那时起，在版本支持中， `4.8` 对于在所有命令行方案间工作的 [凭据提供程序](NuGet-Cross-Platform-Authentication-Plugin.md) ， (`nuget.exe` 、 `dotnet.exe` `msbuild.exe`) 已添加。</span><span class="sxs-lookup"><span data-stu-id="f3c17-105">Since then, in version `4.8` [support for credential providers](NuGet-Cross-Platform-Authentication-Plugin.md) that work across all command line scenarios (`nuget.exe`, `dotnet.exe`, `msbuild.exe`) was added.</span></span>

<span data-ttu-id="f3c17-106">有关的所有身份验证方法的详细信息，请参阅[使用经过身份验证的源中的包](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe)`nuget.exe`</span><span class="sxs-lookup"><span data-stu-id="f3c17-106">See [Consuming Packages from authenticated feeds](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) for more details on all authentication approaches for `nuget.exe`</span></span>

## <a name="nugetexe-credential-provider-discovery"></a><span data-ttu-id="f3c17-107">nuget.exe 凭据提供程序发现</span><span class="sxs-lookup"><span data-stu-id="f3c17-107">nuget.exe credential provider discovery</span></span>

<span data-ttu-id="f3c17-108">nuget.exe 凭据提供程序可通过3种方式使用：</span><span class="sxs-lookup"><span data-stu-id="f3c17-108">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="f3c17-109">**全局** ：若要使凭据提供程序可用于 `nuget.exe` 在当前用户的配置文件下运行的所有实例，请将其添加到中 `%LocalAppData%\NuGet\CredentialProviders` 。</span><span class="sxs-lookup"><span data-stu-id="f3c17-109">**Globally** : to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="f3c17-110">可能需要创建该 `CredentialProviders` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="f3c17-110">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="f3c17-111">凭据提供程序可以安装在文件夹的根目录 `CredentialProviders`  或子文件夹中。</span><span class="sxs-lookup"><span data-stu-id="f3c17-111">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="f3c17-112">如果凭据提供程序具有多个文件/程序集，则可以使用子文件夹来保持提供程序的组织。</span><span class="sxs-lookup"><span data-stu-id="f3c17-112">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="f3c17-113">**从环境变量中** ：凭据提供程序可以存储在任何位置，并可 `nuget.exe` 通过将 `%NUGET_CREDENTIALPROVIDERS_PATH%` 环境变量设置为提供程序位置进行访问。</span><span class="sxs-lookup"><span data-stu-id="f3c17-113">**From an environment variable** : Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="f3c17-114">此变量可以是以分号分隔的列表 (例如， `path1;path2`) 如果有多个位置，则为。</span><span class="sxs-lookup"><span data-stu-id="f3c17-114">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="f3c17-115">与 **nuget.exe** ： nuget.exe 凭据提供程序可以放在与相同的文件夹中 `nuget.exe` 。</span><span class="sxs-lookup"><span data-stu-id="f3c17-115">**Alongside nuget.exe** : nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="f3c17-116">加载凭据提供程序时， `nuget.exe` 会按顺序搜索上述位置，对于名为的任何文件 `credentialprovider*.exe` ，然后按找到的顺序加载这些文件。</span><span class="sxs-lookup"><span data-stu-id="f3c17-116">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="f3c17-117">如果同一文件夹中存在多个凭据提供程序，则按字母顺序加载它们。</span><span class="sxs-lookup"><span data-stu-id="f3c17-117">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="f3c17-118">创建 nuget.exe 凭据提供程序</span><span class="sxs-lookup"><span data-stu-id="f3c17-118">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="f3c17-119">凭据提供程序是一个命令行可执行文件，以形式命名， `CredentialProvider*.exe` 用于收集输入，根据需要获取凭据，然后返回相应的退出状态代码和标准输出。</span><span class="sxs-lookup"><span data-stu-id="f3c17-119">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="f3c17-120">提供程序必须执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="f3c17-120">A provider must do the following:</span></span>

- <span data-ttu-id="f3c17-121">确定是否可以在启动凭据获取之前为目标 URI 提供凭据。</span><span class="sxs-lookup"><span data-stu-id="f3c17-121">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="f3c17-122">如果不是，则它应返回无凭据的状态代码1。</span><span class="sxs-lookup"><span data-stu-id="f3c17-122">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="f3c17-123">不修改 `Nuget.Config` (如在) 设置凭据。</span><span class="sxs-lookup"><span data-stu-id="f3c17-123">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="f3c17-124">自行处理 HTTP 代理配置，因为 NuGet 不向插件提供代理信息。</span><span class="sxs-lookup"><span data-stu-id="f3c17-124">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="f3c17-125">`nuget.exe`使用 utf-8 编码，通过编写 JSON 响应对象将凭据或错误详细信息返回到， (参见下面) 到 stdout。</span><span class="sxs-lookup"><span data-stu-id="f3c17-125">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="f3c17-126">（可选）向 stderr 发出附加跟踪日志记录。</span><span class="sxs-lookup"><span data-stu-id="f3c17-126">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="f3c17-127">不应将任何机密写入到 stderr，因为在详细级别 "正常" 或 "详细" 时，此类跟踪会回显到控制台。</span><span class="sxs-lookup"><span data-stu-id="f3c17-127">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="f3c17-128">应忽略意外参数，以提供与 NuGet 的未来版本的向前兼容性。</span><span class="sxs-lookup"><span data-stu-id="f3c17-128">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f3c17-129">输入参数</span><span class="sxs-lookup"><span data-stu-id="f3c17-129">Input parameters</span></span>

| <span data-ttu-id="f3c17-130">参数/开关</span><span class="sxs-lookup"><span data-stu-id="f3c17-130">Parameter/Switch</span></span> |<span data-ttu-id="f3c17-131">说明</span><span class="sxs-lookup"><span data-stu-id="f3c17-131">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="f3c17-132">Uri {value}</span><span class="sxs-lookup"><span data-stu-id="f3c17-132">Uri {value}</span></span> | <span data-ttu-id="f3c17-133">需要凭据的包源 URI。</span><span class="sxs-lookup"><span data-stu-id="f3c17-133">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="f3c17-134">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f3c17-134">NonInteractive</span></span> | <span data-ttu-id="f3c17-135">如果存在，则提供程序不会发出交互式提示。</span><span class="sxs-lookup"><span data-stu-id="f3c17-135">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="f3c17-136">IsRetry</span><span class="sxs-lookup"><span data-stu-id="f3c17-136">IsRetry</span></span> | <span data-ttu-id="f3c17-137">如果存在，则指示此尝试将重试先前失败的尝试。</span><span class="sxs-lookup"><span data-stu-id="f3c17-137">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="f3c17-138">提供程序通常使用此标志来确保它们绕过任何现有缓存，并在可能的情况下提示输入新凭据。</span><span class="sxs-lookup"><span data-stu-id="f3c17-138">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="f3c17-139">详细程度 {值}</span><span class="sxs-lookup"><span data-stu-id="f3c17-139">Verbosity {value}</span></span> | <span data-ttu-id="f3c17-140">如果存在，则为以下值之一： "normal"、"quiet" 或 "详细"。</span><span class="sxs-lookup"><span data-stu-id="f3c17-140">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="f3c17-141">如果未提供任何值，则默认为 "normal"。</span><span class="sxs-lookup"><span data-stu-id="f3c17-141">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="f3c17-142">提供程序应使用此选项来指示要发出到标准错误流的可选日志记录级别。</span><span class="sxs-lookup"><span data-stu-id="f3c17-142">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="f3c17-143">退出代码</span><span class="sxs-lookup"><span data-stu-id="f3c17-143">Exit codes</span></span>

| <span data-ttu-id="f3c17-144">代码</span><span class="sxs-lookup"><span data-stu-id="f3c17-144">Code</span></span> |<span data-ttu-id="f3c17-145">结果</span><span class="sxs-lookup"><span data-stu-id="f3c17-145">Result</span></span> | <span data-ttu-id="f3c17-146">说明</span><span class="sxs-lookup"><span data-stu-id="f3c17-146">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="f3c17-147">0</span><span class="sxs-lookup"><span data-stu-id="f3c17-147">0</span></span> | <span data-ttu-id="f3c17-148">成功</span><span class="sxs-lookup"><span data-stu-id="f3c17-148">Success</span></span> | <span data-ttu-id="f3c17-149">已成功获取凭据并已将其写入 stdout。</span><span class="sxs-lookup"><span data-stu-id="f3c17-149">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="f3c17-150">1</span><span class="sxs-lookup"><span data-stu-id="f3c17-150">1</span></span> | <span data-ttu-id="f3c17-151">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="f3c17-151">ProviderNotApplicable</span></span> | <span data-ttu-id="f3c17-152">当前提供程序不提供给定 URI 的凭据。</span><span class="sxs-lookup"><span data-stu-id="f3c17-152">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="f3c17-153">2</span><span class="sxs-lookup"><span data-stu-id="f3c17-153">2</span></span> | <span data-ttu-id="f3c17-154">失败</span><span class="sxs-lookup"><span data-stu-id="f3c17-154">Failure</span></span> | <span data-ttu-id="f3c17-155">提供程序是给定 URI 的正确提供程序，但不能提供凭据。</span><span class="sxs-lookup"><span data-stu-id="f3c17-155">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="f3c17-156">在这种情况下，nuget.exe 将不会重试身份验证，并且会失败。</span><span class="sxs-lookup"><span data-stu-id="f3c17-156">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="f3c17-157">典型的示例是用户取消交互式登录时。</span><span class="sxs-lookup"><span data-stu-id="f3c17-157">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="f3c17-158">标准输出</span><span class="sxs-lookup"><span data-stu-id="f3c17-158">Standard output</span></span>

| <span data-ttu-id="f3c17-159">属性</span><span class="sxs-lookup"><span data-stu-id="f3c17-159">Property</span></span> |<span data-ttu-id="f3c17-160">注释</span><span class="sxs-lookup"><span data-stu-id="f3c17-160">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="f3c17-161">用户名</span><span class="sxs-lookup"><span data-stu-id="f3c17-161">Username</span></span> | <span data-ttu-id="f3c17-162">经过身份验证的请求的用户名。</span><span class="sxs-lookup"><span data-stu-id="f3c17-162">Username for authenticated requests.</span></span>|
| <span data-ttu-id="f3c17-163">密码</span><span class="sxs-lookup"><span data-stu-id="f3c17-163">Password</span></span> | <span data-ttu-id="f3c17-164">经过身份验证的请求的密码。</span><span class="sxs-lookup"><span data-stu-id="f3c17-164">Password for authenticated requests.</span></span>|
| <span data-ttu-id="f3c17-165">消息</span><span class="sxs-lookup"><span data-stu-id="f3c17-165">Message</span></span> | <span data-ttu-id="f3c17-166">有关响应的可选详细信息，仅用于显示故障情况下的其他详细信息。</span><span class="sxs-lookup"><span data-stu-id="f3c17-166">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="f3c17-167">示例 stdout：</span><span class="sxs-lookup"><span data-stu-id="f3c17-167">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="f3c17-168">凭据提供程序故障排除</span><span class="sxs-lookup"><span data-stu-id="f3c17-168">Troubleshooting a credential provider</span></span>

<span data-ttu-id="f3c17-169">目前，NuGet 并不能直接支持调试自定义凭据提供程序; [问题 4598](https://github.com/NuGet/Home/issues/4598) 正在跟踪此工作。</span><span class="sxs-lookup"><span data-stu-id="f3c17-169">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="f3c17-170">你还可以执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="f3c17-170">You can also do the following:</span></span>

- <span data-ttu-id="f3c17-171">运行带开关的 nuget.exe `-verbosity` 以检查详细的输出。</span><span class="sxs-lookup"><span data-stu-id="f3c17-171">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="f3c17-172">将调试消息添加到 `stdout` 适当位置。</span><span class="sxs-lookup"><span data-stu-id="f3c17-172">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="f3c17-173">请确保使用 nuget.exe 3.3 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="f3c17-173">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="f3c17-174">在启动时将调试器附加到以下代码片段：</span><span class="sxs-lookup"><span data-stu-id="f3c17-174">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
