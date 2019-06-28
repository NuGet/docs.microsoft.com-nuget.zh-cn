---
title: nuget.config 文件引用
description: NuGet.Config 文件引用，包括配置、bindingRedirects、packageRestore、解决方案和 packageSource 节。
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: 2eceb6e94a353cb29b83aea114c6cea2acbac266
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426149"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="14ba0-103">nuget.config 引用</span><span class="sxs-lookup"><span data-stu-id="14ba0-103">nuget.config reference</span></span>

<span data-ttu-id="14ba0-104">通过在不同的设置控制 NuGet 行为`NuGet.Config`文件中所述[常见 NuGet 配置](../consume-packages/configuring-nuget-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="14ba0-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="14ba0-105">`nuget.config` 是包含顶级 `<configuration>` 节点的 XML 文件，而该节点包含本主题中所述的节元素。</span><span class="sxs-lookup"><span data-stu-id="14ba0-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="14ba0-106">每个部分包含零个或多个项。</span><span class="sxs-lookup"><span data-stu-id="14ba0-106">Each section contains zero or more items.</span></span> <span data-ttu-id="14ba0-107">请参阅[示例配置文件](#example-config-file)。</span><span class="sxs-lookup"><span data-stu-id="14ba0-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="14ba0-108">设置名称不区分大小写，并且值可以使用[环境变量](#using-environment-variables)。</span><span class="sxs-lookup"><span data-stu-id="14ba0-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="14ba0-109">本主题内容：</span><span class="sxs-lookup"><span data-stu-id="14ba0-109">In this topic:</span></span>

- [<span data-ttu-id="14ba0-110">配置节</span><span class="sxs-lookup"><span data-stu-id="14ba0-110">config section</span></span>](#config-section)
- [<span data-ttu-id="14ba0-111">bindingRedirects 节</span><span class="sxs-lookup"><span data-stu-id="14ba0-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="14ba0-112">packageRestore 节</span><span class="sxs-lookup"><span data-stu-id="14ba0-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="14ba0-113">解决方案节</span><span class="sxs-lookup"><span data-stu-id="14ba0-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="14ba0-114">[包源节](#package-source-sections)：</span><span class="sxs-lookup"><span data-stu-id="14ba0-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="14ba0-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="14ba0-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="14ba0-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="14ba0-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="14ba0-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="14ba0-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="14ba0-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="14ba0-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="14ba0-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="14ba0-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="14ba0-120">trustedSigners 部分</span><span class="sxs-lookup"><span data-stu-id="14ba0-120">trustedSigners section</span></span>](#trustedsigners-section)
- [<span data-ttu-id="14ba0-121">使用环境变量</span><span class="sxs-lookup"><span data-stu-id="14ba0-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="14ba0-122">示例配置文件</span><span class="sxs-lookup"><span data-stu-id="14ba0-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="14ba0-123">配置节</span><span class="sxs-lookup"><span data-stu-id="14ba0-123">config section</span></span>

<span data-ttu-id="14ba0-124">包含杂项配置设置，可使用 [`nuget config` 命令](../tools/cli-ref-config.md)设置。</span><span class="sxs-lookup"><span data-stu-id="14ba0-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="14ba0-125">`dependencyVersion` 并`repositoryPath`仅适用于使用的项目`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="14ba0-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="14ba0-126">`globalPackagesFolder` 仅适用于使用 PackageReference 格式的项目。</span><span class="sxs-lookup"><span data-stu-id="14ba0-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="14ba0-127">键</span><span class="sxs-lookup"><span data-stu-id="14ba0-127">Key</span></span> | <span data-ttu-id="14ba0-128">值</span><span class="sxs-lookup"><span data-stu-id="14ba0-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="14ba0-129">dependencyVersion（仅限于 `packages.config`）</span><span class="sxs-lookup"><span data-stu-id="14ba0-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="14ba0-130">包安装、还原和更新的默认 `DependencyVersion` 值（未直接指定 `-DependencyVersion` 开关时）。</span><span class="sxs-lookup"><span data-stu-id="14ba0-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="14ba0-131">NuGet 包管理器 UI 也使用此值。</span><span class="sxs-lookup"><span data-stu-id="14ba0-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="14ba0-132">值为 `Lowest`、`HighestPatch`、`HighestMinor`、`Highest`。</span><span class="sxs-lookup"><span data-stu-id="14ba0-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="14ba0-133">globalPackagesFolder （仅限使用 PackageReference 的项目）</span><span class="sxs-lookup"><span data-stu-id="14ba0-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="14ba0-134">默认全局包文件夹的位置。</span><span class="sxs-lookup"><span data-stu-id="14ba0-134">The location of the default global packages folder.</span></span> <span data-ttu-id="14ba0-135">默认值为 `%userprofile%\.nuget\packages` (Windows) 或 `~/.nuget/packages` (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="14ba0-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="14ba0-136">相对路径可在项目特定的 `nuget.config` 文件中使用。</span><span class="sxs-lookup"><span data-stu-id="14ba0-136">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="14ba0-137">由 nuget_packages 重写环境变量优先替代此设置。</span><span class="sxs-lookup"><span data-stu-id="14ba0-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="14ba0-138">repositoryPath（仅限于 `packages.config`）</span><span class="sxs-lookup"><span data-stu-id="14ba0-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="14ba0-139">安装 NuGet 包的位置，而非默认的 `$(Solutiondir)/packages` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="14ba0-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="14ba0-140">相对路径可在项目特定的 `nuget.config` 文件中使用。</span><span class="sxs-lookup"><span data-stu-id="14ba0-140">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="14ba0-141">由 nuget_packages 重写环境变量优先替代此设置。</span><span class="sxs-lookup"><span data-stu-id="14ba0-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="14ba0-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="14ba0-142">defaultPushSource</span></span> | <span data-ttu-id="14ba0-143">如果操作未找到任何其他包源，则会标识应用作默认值的包源 URL 或路径。</span><span class="sxs-lookup"><span data-stu-id="14ba0-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="14ba0-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="14ba0-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="14ba0-145">连接到包源时要使用的代理设置；`http_proxy` 应为 `http://<username>:<password>@<domain>` 格式。</span><span class="sxs-lookup"><span data-stu-id="14ba0-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="14ba0-146">密码已加密，且不能手动添加。</span><span class="sxs-lookup"><span data-stu-id="14ba0-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="14ba0-147">对于 `no_proxy`，该值是绕过代理服务器的域的列表（以逗号分隔）。</span><span class="sxs-lookup"><span data-stu-id="14ba0-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="14ba0-148">可将 http_proxy 和 no_proxy 环境变量交替用于这些值。</span><span class="sxs-lookup"><span data-stu-id="14ba0-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="14ba0-149">有关其他详细信息，请参阅 [NuGet 代理设置](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com)。</span><span class="sxs-lookup"><span data-stu-id="14ba0-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="14ba0-150">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="14ba0-150">signatureValidationMode</span></span> | <span data-ttu-id="14ba0-151">指定用来验证包安装的包签名和还原的验证模式。</span><span class="sxs-lookup"><span data-stu-id="14ba0-151">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="14ba0-152">值为`accept`， `require`。</span><span class="sxs-lookup"><span data-stu-id="14ba0-152">Values are `accept`, `require`.</span></span> <span data-ttu-id="14ba0-153">默认为 `accept`。</span><span class="sxs-lookup"><span data-stu-id="14ba0-153">Defaults to `accept`.</span></span>

<span data-ttu-id="14ba0-154">**示例**：</span><span class="sxs-lookup"><span data-stu-id="14ba0-154">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="14ba0-155">bindingRedirects 节</span><span class="sxs-lookup"><span data-stu-id="14ba0-155">bindingRedirects section</span></span>

<span data-ttu-id="14ba0-156">在安装包时，配置 NuGet 是否执行自动绑定重定向。</span><span class="sxs-lookup"><span data-stu-id="14ba0-156">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="14ba0-157">键</span><span class="sxs-lookup"><span data-stu-id="14ba0-157">Key</span></span> | <span data-ttu-id="14ba0-158">值</span><span class="sxs-lookup"><span data-stu-id="14ba0-158">Value</span></span> |
| --- | --- |
| <span data-ttu-id="14ba0-159">skip</span><span class="sxs-lookup"><span data-stu-id="14ba0-159">skip</span></span> | <span data-ttu-id="14ba0-160">指示是否跳过自动绑定重定向的布尔。</span><span class="sxs-lookup"><span data-stu-id="14ba0-160">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="14ba0-161">默认值为 false。</span><span class="sxs-lookup"><span data-stu-id="14ba0-161">The default is false.</span></span> |

<span data-ttu-id="14ba0-162">**示例**：</span><span class="sxs-lookup"><span data-stu-id="14ba0-162">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="14ba0-163">packageRestore 节</span><span class="sxs-lookup"><span data-stu-id="14ba0-163">packageRestore section</span></span>

<span data-ttu-id="14ba0-164">在生成期间控制包还原。</span><span class="sxs-lookup"><span data-stu-id="14ba0-164">Controls package restore during builds.</span></span>

| <span data-ttu-id="14ba0-165">键</span><span class="sxs-lookup"><span data-stu-id="14ba0-165">Key</span></span> | <span data-ttu-id="14ba0-166">值</span><span class="sxs-lookup"><span data-stu-id="14ba0-166">Value</span></span> |
| --- | --- |
| <span data-ttu-id="14ba0-167">enabled</span><span class="sxs-lookup"><span data-stu-id="14ba0-167">enabled</span></span> | <span data-ttu-id="14ba0-168">指示 NuGet 是否可执行自动还原的布尔。</span><span class="sxs-lookup"><span data-stu-id="14ba0-168">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="14ba0-169">还可以使用 `True` 的值设置 `EnableNuGetPackageRestore` 环境变量，而不是在配置文件中设置此密钥。</span><span class="sxs-lookup"><span data-stu-id="14ba0-169">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="14ba0-170">自动</span><span class="sxs-lookup"><span data-stu-id="14ba0-170">automatic</span></span> | <span data-ttu-id="14ba0-171">指示 NuGet 是否应在生成期间检查缺少的包。</span><span class="sxs-lookup"><span data-stu-id="14ba0-171">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="14ba0-172">**示例**：</span><span class="sxs-lookup"><span data-stu-id="14ba0-172">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="14ba0-173">解决方案节</span><span class="sxs-lookup"><span data-stu-id="14ba0-173">solution section</span></span>

<span data-ttu-id="14ba0-174">控制解决方案的 `packages` 文件夹是否包括在源代码管理中。</span><span class="sxs-lookup"><span data-stu-id="14ba0-174">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="14ba0-175">此节仅适用于解决方案文件夹中的 `nuget.config` 文件。</span><span class="sxs-lookup"><span data-stu-id="14ba0-175">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="14ba0-176">键</span><span class="sxs-lookup"><span data-stu-id="14ba0-176">Key</span></span> | <span data-ttu-id="14ba0-177">值</span><span class="sxs-lookup"><span data-stu-id="14ba0-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="14ba0-178">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="14ba0-178">disableSourceControlIntegration</span></span> | <span data-ttu-id="14ba0-179">指示在使用源代码管理时是否忽略包文件夹的布尔。</span><span class="sxs-lookup"><span data-stu-id="14ba0-179">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="14ba0-180">默认值为 False。</span><span class="sxs-lookup"><span data-stu-id="14ba0-180">The default value is false.</span></span> |

<span data-ttu-id="14ba0-181">**示例**：</span><span class="sxs-lookup"><span data-stu-id="14ba0-181">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="14ba0-182">包源节</span><span class="sxs-lookup"><span data-stu-id="14ba0-182">Package source sections</span></span>

<span data-ttu-id="14ba0-183">`packageSources`， `packageSourceCredentials`， `apikeys`， `activePackageSource`，`disabledPackageSources`和`trustedSigners`一起协作来配置 NuGet 在安装、 还原和更新操作过程中如何使用包存储库的所有工作。</span><span class="sxs-lookup"><span data-stu-id="14ba0-183">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="14ba0-184">[ `nuget sources`命令](../tools/cli-ref-sources.md)通常用于管理这些设置，除`apikeys`使用管理[`nuget setapikey`命令](../tools/cli-ref-setapikey.md)，和`trustedSigners`它托管使用[`nuget trusted-signers`命令](../tools/cli-ref-trusted-signers.md)。</span><span class="sxs-lookup"><span data-stu-id="14ba0-184">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="14ba0-185">请注意，nuget.org 的源 URL 是 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="14ba0-185">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="14ba0-186">packageSources</span><span class="sxs-lookup"><span data-stu-id="14ba0-186">packageSources</span></span>

<span data-ttu-id="14ba0-187">列出所有已知包源。</span><span class="sxs-lookup"><span data-stu-id="14ba0-187">Lists all known package sources.</span></span> <span data-ttu-id="14ba0-188">在还原操作期间，与任何项目使用 PackageReference 格式，被忽略的顺序。</span><span class="sxs-lookup"><span data-stu-id="14ba0-188">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="14ba0-189">NuGet 会遵守安装源的顺序和项目使用与更新操作`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="14ba0-189">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="14ba0-190">键</span><span class="sxs-lookup"><span data-stu-id="14ba0-190">Key</span></span> | <span data-ttu-id="14ba0-191">值</span><span class="sxs-lookup"><span data-stu-id="14ba0-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="14ba0-192">（要分配给包源的名称）</span><span class="sxs-lookup"><span data-stu-id="14ba0-192">(name to assign to the package source)</span></span> | <span data-ttu-id="14ba0-193">包源的路径或 URL。</span><span class="sxs-lookup"><span data-stu-id="14ba0-193">The path or URL of the package source.</span></span> |

<span data-ttu-id="14ba0-194">**示例**：</span><span class="sxs-lookup"><span data-stu-id="14ba0-194">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="14ba0-195">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="14ba0-195">packageSourceCredentials</span></span>

<span data-ttu-id="14ba0-196">存储源的用户名和密码，通常通过 `nuget sources` 使用 `-username` 和 `-password` 开关指定。</span><span class="sxs-lookup"><span data-stu-id="14ba0-196">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="14ba0-197">默认情况下密码会进行加密，除非还使用了 `-storepasswordincleartext` 选项。</span><span class="sxs-lookup"><span data-stu-id="14ba0-197">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="14ba0-198">键</span><span class="sxs-lookup"><span data-stu-id="14ba0-198">Key</span></span> | <span data-ttu-id="14ba0-199">值</span><span class="sxs-lookup"><span data-stu-id="14ba0-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="14ba0-200">username</span><span class="sxs-lookup"><span data-stu-id="14ba0-200">username</span></span> | <span data-ttu-id="14ba0-201">纯文本形式的源用户名。</span><span class="sxs-lookup"><span data-stu-id="14ba0-201">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="14ba0-202">密码</span><span class="sxs-lookup"><span data-stu-id="14ba0-202">password</span></span> | <span data-ttu-id="14ba0-203">源的加密密码。</span><span class="sxs-lookup"><span data-stu-id="14ba0-203">The encrypted password for the source.</span></span> |
| <span data-ttu-id="14ba0-204">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="14ba0-204">cleartextpassword</span></span> | <span data-ttu-id="14ba0-205">源的未加密密码。</span><span class="sxs-lookup"><span data-stu-id="14ba0-205">The unencrypted password for the source.</span></span> |

<span data-ttu-id="14ba0-206">**示例：**</span><span class="sxs-lookup"><span data-stu-id="14ba0-206">**Example:**</span></span>

<span data-ttu-id="14ba0-207">在配置文件中，`<packageSourceCredentials>` 元素包含每个适用源名称的子节点（名称中的空格被替换为 `_x0020_`）。</span><span class="sxs-lookup"><span data-stu-id="14ba0-207">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="14ba0-208">也就是说，对于名为“Contoso”和“测试源”的源，使用加密密码时，配置文件包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="14ba0-208">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="Password" value="..." />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="14ba0-209">使用未加密密码时：</span><span class="sxs-lookup"><span data-stu-id="14ba0-209">When using unencrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="33f!!lloppa" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="14ba0-210">apikeys</span><span class="sxs-lookup"><span data-stu-id="14ba0-210">apikeys</span></span>

<span data-ttu-id="14ba0-211">存储使用 API 密钥身份验证的源的密钥，如使用 [`nuget setapikey` 命令](../tools/cli-ref-setapikey.md) 设置。</span><span class="sxs-lookup"><span data-stu-id="14ba0-211">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="14ba0-212">键</span><span class="sxs-lookup"><span data-stu-id="14ba0-212">Key</span></span> | <span data-ttu-id="14ba0-213">值</span><span class="sxs-lookup"><span data-stu-id="14ba0-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="14ba0-214">（源 URL）</span><span class="sxs-lookup"><span data-stu-id="14ba0-214">(source URL)</span></span> | <span data-ttu-id="14ba0-215">加密的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="14ba0-215">The encrypted API key.</span></span> |

<span data-ttu-id="14ba0-216">**示例**：</span><span class="sxs-lookup"><span data-stu-id="14ba0-216">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="14ba0-217">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="14ba0-217">disabledPackageSources</span></span>

<span data-ttu-id="14ba0-218">标识当前已禁用的源。</span><span class="sxs-lookup"><span data-stu-id="14ba0-218">Identified currently disabled sources.</span></span> <span data-ttu-id="14ba0-219">可能为空。</span><span class="sxs-lookup"><span data-stu-id="14ba0-219">May be empty.</span></span>

| <span data-ttu-id="14ba0-220">键</span><span class="sxs-lookup"><span data-stu-id="14ba0-220">Key</span></span> | <span data-ttu-id="14ba0-221">值</span><span class="sxs-lookup"><span data-stu-id="14ba0-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="14ba0-222">（源名称）</span><span class="sxs-lookup"><span data-stu-id="14ba0-222">(name of source)</span></span> | <span data-ttu-id="14ba0-223">指示源是否禁用的布尔。</span><span class="sxs-lookup"><span data-stu-id="14ba0-223">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="14ba0-224">**示例：**</span><span class="sxs-lookup"><span data-stu-id="14ba0-224">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="14ba0-225">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="14ba0-225">activePackageSource</span></span>

<span data-ttu-id="14ba0-226">*（仅限于 2.x；3.x+ 中已弃用）*</span><span class="sxs-lookup"><span data-stu-id="14ba0-226">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="14ba0-227">标识到当前活动的源或指示所有源的聚合。</span><span class="sxs-lookup"><span data-stu-id="14ba0-227">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="14ba0-228">键</span><span class="sxs-lookup"><span data-stu-id="14ba0-228">Key</span></span> | <span data-ttu-id="14ba0-229">值</span><span class="sxs-lookup"><span data-stu-id="14ba0-229">Value</span></span> |
| --- | --- |
| <span data-ttu-id="14ba0-230">（源名称）或 `All`</span><span class="sxs-lookup"><span data-stu-id="14ba0-230">(name of source) or `All`</span></span> | <span data-ttu-id="14ba0-231">如果密钥是源的名称，则值为源路径或 URL。</span><span class="sxs-lookup"><span data-stu-id="14ba0-231">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="14ba0-232">如果为 `All`，值应为 `(Aggregate source)`，从而组合其他未禁用的所有包源。</span><span class="sxs-lookup"><span data-stu-id="14ba0-232">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="14ba0-233">**示例**：</span><span class="sxs-lookup"><span data-stu-id="14ba0-233">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a><span data-ttu-id="14ba0-234">trustedSigners 部分</span><span class="sxs-lookup"><span data-stu-id="14ba0-234">trustedSigners section</span></span>

<span data-ttu-id="14ba0-235">存储受信任的签名者用于允许同时安装或还原包。</span><span class="sxs-lookup"><span data-stu-id="14ba0-235">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="14ba0-236">当用户设置时，此列表不能为空`signatureValidationMode`到`require`。</span><span class="sxs-lookup"><span data-stu-id="14ba0-236">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="14ba0-237">本部分中可以使用更新[`nuget trusted-signers`命令](../tools/cli-ref-trusted-signers.md)。</span><span class="sxs-lookup"><span data-stu-id="14ba0-237">This section can be updated with the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="14ba0-238">**架构**:</span><span class="sxs-lookup"><span data-stu-id="14ba0-238">**Schema**:</span></span>

<span data-ttu-id="14ba0-239">受信任的签名者具有一系列`certificate`登记标识给定签名者的所有证书的项。</span><span class="sxs-lookup"><span data-stu-id="14ba0-239">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="14ba0-240">受信任的签名者可以是`Author`或`Repository`。</span><span class="sxs-lookup"><span data-stu-id="14ba0-240">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="14ba0-241">受信任*存储库*还指定了`serviceIndex`存储库 (这必须是有效`https`uri) 和 （可选） 可以指定以分号分隔的列表`owners`限制更多谁是受信任从该特定存储库。</span><span class="sxs-lookup"><span data-stu-id="14ba0-241">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="14ba0-242">用于证书指纹的受支持的哈希算法`SHA256`，`SHA384`和`SHA512`。</span><span class="sxs-lookup"><span data-stu-id="14ba0-242">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="14ba0-243">如果`certificate`指定`allowUntrustedRoot`作为`true`给定的证书生成的签名验证一部分的证书链时允许链接到不受信任的根。</span><span class="sxs-lookup"><span data-stu-id="14ba0-243">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="14ba0-244">**示例**：</span><span class="sxs-lookup"><span data-stu-id="14ba0-244">**Example**:</span></span>

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="using-environment-variables"></a><span data-ttu-id="14ba0-245">使用环境变量</span><span class="sxs-lookup"><span data-stu-id="14ba0-245">Using environment variables</span></span>

<span data-ttu-id="14ba0-246">可以在 `nuget.config` 值中使用环境变量 (NuGet 3.4 +) 在运行时应用设置。</span><span class="sxs-lookup"><span data-stu-id="14ba0-246">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="14ba0-247">例如，如果 Windows 上的 `HOME` 环境变量设置为 `c:\users\username`，则配置文件中 `%HOME%\NuGetRepository` 的值解析为 `c:\users\username\NuGetRepository`。</span><span class="sxs-lookup"><span data-stu-id="14ba0-247">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="14ba0-248">同样，如果 Mac/Linux 上的 `HOME` 设置为 `/home/myStuff`，则配置文件中的 `%HOME%/NuGetRepository` 解析为 `/home/myStuff/NuGetRepository`。</span><span class="sxs-lookup"><span data-stu-id="14ba0-248">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="14ba0-249">如果未找到环境变量，NuGet 会使用配置文件中的文本值。</span><span class="sxs-lookup"><span data-stu-id="14ba0-249">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="14ba0-250">示例配置文件</span><span class="sxs-lookup"><span data-stu-id="14ba0-250">Example config file</span></span>

<span data-ttu-id="14ba0-251">下面是示例 `nuget.config` 文件，它对一些设置进行了说明：</span><span class="sxs-lookup"><span data-stu-id="14ba0-251">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable. On Mac/Linux,
            use $PACKAGE_HOME/External as the value.
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%\External" />

        <!--
            Used to specify default source for the push command.
            See: nuget.exe help push
        -->

        <add key="defaultPushSource" value="https://MyRepo/ES/api/v2/package" />

        <!-- Proxy settings -->
        <add key="http_proxy" value="host" />
        <add key="http_proxy.user" value="username" />
        <add key="http_proxy.password" value="encrypted_password" />
    </config>

    <packageRestore>
        <!-- Allow NuGet to download missing packages -->
        <add key="enabled" value="True" />

        <!-- Automatically check for missing packages during build in Visual Studio -->
        <add key="automatic" value="True" />
    </packageRestore>

    <!--
        Used to specify the default Sources for list, install and update.
        See: nuget.exe help list
        See: nuget.exe help install
        See: nuget.exe help update
    -->
    <packageSources>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
        <add key="MyRepo - ES" value="https://MyRepo/ES/nuget" />
    </packageSources>

    <!-- Used to store credentials -->
    <packageSourceCredentials />

    <!-- Used to disable package sources  -->
    <disabledPackageSources />

    <!--
        Used to specify default API key associated with sources.
        See: nuget.exe help setApiKey
        See: nuget.exe help push
        See: nuget.exe help mirror
    -->
    <apikeys>
        <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
    </apikeys>

    <!--
        Used to specify trusted signers to allow during signature verification.
        See: nuget.exe help trusted-signers
    -->
    <trustedSigners>
        <author name="microsoft">
            <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
