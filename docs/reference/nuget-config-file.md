---
title: nuget .config 文件引用
description: NuGet.Config 文件引用，包括配置、bindingRedirects、packageRestore、解决方案和 packageSource 节。
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: cd321084c46709e3d1d22872c37485edacd33afa
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230521"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="18c09-103">nuget.exe 引用</span><span class="sxs-lookup"><span data-stu-id="18c09-103">nuget.config reference</span></span>

<span data-ttu-id="18c09-104">NuGet 行为由不同 `NuGet.Config` 或 `nuget.config` 文件中的设置控制，如[常见 NuGet 配置](../consume-packages/configuring-nuget-behavior.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="18c09-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="18c09-105">`nuget.config` 是包含顶级 `<configuration>` 节点的 XML 文件，而该节点包含本主题中所述的节元素。</span><span class="sxs-lookup"><span data-stu-id="18c09-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="18c09-106">每节都包含零个或多个项。</span><span class="sxs-lookup"><span data-stu-id="18c09-106">Each section contains zero or more items.</span></span> <span data-ttu-id="18c09-107">请参阅[示例配置文件](#example-config-file)。</span><span class="sxs-lookup"><span data-stu-id="18c09-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="18c09-108">设置名称不区分大小写，并且值可以使用[环境变量](#using-environment-variables)。</span><span class="sxs-lookup"><span data-stu-id="18c09-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="18c09-109">配置节</span><span class="sxs-lookup"><span data-stu-id="18c09-109">config section</span></span>

<span data-ttu-id="18c09-110">包含杂项配置设置，可使用 [`nuget config` 命令](../reference/cli-reference/cli-ref-config.md)设置。</span><span class="sxs-lookup"><span data-stu-id="18c09-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="18c09-111">`dependencyVersion` 和 `repositoryPath` 仅适用于使用 `packages.config`的项目。</span><span class="sxs-lookup"><span data-stu-id="18c09-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="18c09-112">`globalPackagesFolder` 仅适用于使用 PackageReference 格式的项目。</span><span class="sxs-lookup"><span data-stu-id="18c09-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="18c09-113">密钥</span><span class="sxs-lookup"><span data-stu-id="18c09-113">Key</span></span> | <span data-ttu-id="18c09-114">值</span><span class="sxs-lookup"><span data-stu-id="18c09-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="18c09-115">dependencyVersion（仅限于 `packages.config`）</span><span class="sxs-lookup"><span data-stu-id="18c09-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="18c09-116">包安装、还原和更新的默认 `DependencyVersion` 值（未直接指定 `-DependencyVersion` 开关时）。</span><span class="sxs-lookup"><span data-stu-id="18c09-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="18c09-117">NuGet 包管理器 UI 也使用此值。</span><span class="sxs-lookup"><span data-stu-id="18c09-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="18c09-118">值为 `Lowest`、`HighestPatch`、`HighestMinor`、`Highest`。</span><span class="sxs-lookup"><span data-stu-id="18c09-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="18c09-119">globalPackagesFolder （仅限使用 PackageReference 的项目）</span><span class="sxs-lookup"><span data-stu-id="18c09-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="18c09-120">默认全局包文件夹的位置。</span><span class="sxs-lookup"><span data-stu-id="18c09-120">The location of the default global packages folder.</span></span> <span data-ttu-id="18c09-121">默认值为 `%userprofile%\.nuget\packages` (Windows) 或 `~/.nuget/packages` (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="18c09-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="18c09-122">相对路径可在项目特定的 `nuget.config` 文件中使用。</span><span class="sxs-lookup"><span data-stu-id="18c09-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="18c09-123">此设置由 NUGET_PACKAGES 环境变量重写，该变量优先。</span><span class="sxs-lookup"><span data-stu-id="18c09-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="18c09-124">repositoryPath（仅限于 `packages.config`）</span><span class="sxs-lookup"><span data-stu-id="18c09-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="18c09-125">安装 NuGet 包的位置，而非默认的 `$(Solutiondir)/packages` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="18c09-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="18c09-126">相对路径可在项目特定的 `nuget.config` 文件中使用。</span><span class="sxs-lookup"><span data-stu-id="18c09-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="18c09-127">此设置由 NUGET_PACKAGES 环境变量重写，该变量优先。</span><span class="sxs-lookup"><span data-stu-id="18c09-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="18c09-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="18c09-128">defaultPushSource</span></span> | <span data-ttu-id="18c09-129">如果操作未找到任何其他包源，则会标识应用作默认值的包源 URL 或路径。</span><span class="sxs-lookup"><span data-stu-id="18c09-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="18c09-130">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="18c09-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="18c09-131">连接到包源时要使用的代理设置；`http_proxy` 应为 `http://<username>:<password>@<domain>` 格式。</span><span class="sxs-lookup"><span data-stu-id="18c09-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="18c09-132">密码已加密，且不能手动添加。</span><span class="sxs-lookup"><span data-stu-id="18c09-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="18c09-133">对于 `no_proxy`，该值是绕过代理服务器的域的列表（以逗号分隔）。</span><span class="sxs-lookup"><span data-stu-id="18c09-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="18c09-134">可将 http_proxy 和 no_proxy 环境变量交替用于这些值。</span><span class="sxs-lookup"><span data-stu-id="18c09-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="18c09-135">有关其他详细信息，请参阅 [NuGet 代理设置](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com)。</span><span class="sxs-lookup"><span data-stu-id="18c09-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="18c09-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="18c09-136">signatureValidationMode</span></span> | <span data-ttu-id="18c09-137">指定用于验证包签名以便安装和还原的验证模式。</span><span class="sxs-lookup"><span data-stu-id="18c09-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="18c09-138">值为 `accept`，`require`。</span><span class="sxs-lookup"><span data-stu-id="18c09-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="18c09-139">默认为 `accept`。</span><span class="sxs-lookup"><span data-stu-id="18c09-139">Defaults to `accept`.</span></span>

<span data-ttu-id="18c09-140">**示例**：</span><span class="sxs-lookup"><span data-stu-id="18c09-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="18c09-141">bindingRedirects 节</span><span class="sxs-lookup"><span data-stu-id="18c09-141">bindingRedirects section</span></span>

<span data-ttu-id="18c09-142">在安装包时，配置 NuGet 是否执行自动绑定重定向。</span><span class="sxs-lookup"><span data-stu-id="18c09-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="18c09-143">密钥</span><span class="sxs-lookup"><span data-stu-id="18c09-143">Key</span></span> | <span data-ttu-id="18c09-144">值</span><span class="sxs-lookup"><span data-stu-id="18c09-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="18c09-145">skip</span><span class="sxs-lookup"><span data-stu-id="18c09-145">skip</span></span> | <span data-ttu-id="18c09-146">指示是否跳过自动绑定重定向的布尔。</span><span class="sxs-lookup"><span data-stu-id="18c09-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="18c09-147">默认值为 false。</span><span class="sxs-lookup"><span data-stu-id="18c09-147">The default is false.</span></span> |

<span data-ttu-id="18c09-148">**示例**：</span><span class="sxs-lookup"><span data-stu-id="18c09-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="18c09-149">packageRestore 节</span><span class="sxs-lookup"><span data-stu-id="18c09-149">packageRestore section</span></span>

<span data-ttu-id="18c09-150">在生成期间控制包还原。</span><span class="sxs-lookup"><span data-stu-id="18c09-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="18c09-151">密钥</span><span class="sxs-lookup"><span data-stu-id="18c09-151">Key</span></span> | <span data-ttu-id="18c09-152">值</span><span class="sxs-lookup"><span data-stu-id="18c09-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="18c09-153">已启用</span><span class="sxs-lookup"><span data-stu-id="18c09-153">enabled</span></span> | <span data-ttu-id="18c09-154">指示 NuGet 是否可执行自动还原的布尔。</span><span class="sxs-lookup"><span data-stu-id="18c09-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="18c09-155">还可以使用 `EnableNuGetPackageRestore` 的值设置 `True` 环境变量，而不是在配置文件中设置此密钥。</span><span class="sxs-lookup"><span data-stu-id="18c09-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="18c09-156">automatic</span><span class="sxs-lookup"><span data-stu-id="18c09-156">automatic</span></span> | <span data-ttu-id="18c09-157">指示 NuGet 是否应在生成期间检查缺少的包。</span><span class="sxs-lookup"><span data-stu-id="18c09-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="18c09-158">**示例**：</span><span class="sxs-lookup"><span data-stu-id="18c09-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="18c09-159">解决方案节</span><span class="sxs-lookup"><span data-stu-id="18c09-159">solution section</span></span>

<span data-ttu-id="18c09-160">控制解决方案的 `packages` 文件夹是否包括在源代码管理中。</span><span class="sxs-lookup"><span data-stu-id="18c09-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="18c09-161">此节仅适用于解决方案文件夹中的 `nuget.config` 文件。</span><span class="sxs-lookup"><span data-stu-id="18c09-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="18c09-162">密钥</span><span class="sxs-lookup"><span data-stu-id="18c09-162">Key</span></span> | <span data-ttu-id="18c09-163">值</span><span class="sxs-lookup"><span data-stu-id="18c09-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="18c09-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="18c09-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="18c09-165">指示在使用源代码管理时是否忽略包文件夹的布尔。</span><span class="sxs-lookup"><span data-stu-id="18c09-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="18c09-166">默认值是 False。</span><span class="sxs-lookup"><span data-stu-id="18c09-166">The default value is false.</span></span> |

<span data-ttu-id="18c09-167">**示例**：</span><span class="sxs-lookup"><span data-stu-id="18c09-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="18c09-168">包源节</span><span class="sxs-lookup"><span data-stu-id="18c09-168">Package source sections</span></span>

<span data-ttu-id="18c09-169">`packageSources`、`packageSourceCredentials`、`apikeys`、`activePackageSource`、`disabledPackageSources` 和 `trustedSigners` 一起使用，以配置在安装、还原和更新操作过程中 NuGet 如何与包存储库一起工作。</span><span class="sxs-lookup"><span data-stu-id="18c09-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="18c09-170">[`nuget sources` 命令](../reference/cli-reference/cli-ref-sources.md)通常用于管理这些设置，但使用[`nuget setapikey` 命令](../reference/cli-reference/cli-ref-setapikey.md)管理的 `apikeys` 和使用[`nuget trusted-signers` 命令](../reference/cli-reference/cli-ref-trusted-signers.md)管理的 `trustedSigners` 除外。</span><span class="sxs-lookup"><span data-stu-id="18c09-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="18c09-171">请注意，nuget.org 的源 URL 是 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="18c09-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="18c09-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="18c09-172">packageSources</span></span>

<span data-ttu-id="18c09-173">列出所有已知包源。</span><span class="sxs-lookup"><span data-stu-id="18c09-173">Lists all known package sources.</span></span> <span data-ttu-id="18c09-174">在还原操作和任何使用 PackageReference 格式的项目中，将忽略此顺序。</span><span class="sxs-lookup"><span data-stu-id="18c09-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="18c09-175">NuGet 遵循使用 `packages.config`的项目进行安装和更新操作的源顺序。</span><span class="sxs-lookup"><span data-stu-id="18c09-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="18c09-176">密钥</span><span class="sxs-lookup"><span data-stu-id="18c09-176">Key</span></span> | <span data-ttu-id="18c09-177">值</span><span class="sxs-lookup"><span data-stu-id="18c09-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="18c09-178">（要分配给包源的名称）</span><span class="sxs-lookup"><span data-stu-id="18c09-178">(name to assign to the package source)</span></span> | <span data-ttu-id="18c09-179">包源的路径或 URL。</span><span class="sxs-lookup"><span data-stu-id="18c09-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="18c09-180">**示例**：</span><span class="sxs-lookup"><span data-stu-id="18c09-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="18c09-181">当给定节点中存在 `<clear />` 时，NuGet 将忽略之前为该节点定义的配置值。</span><span class="sxs-lookup"><span data-stu-id="18c09-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="18c09-182">[阅读有关如何应用设置的详细信息](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。</span><span class="sxs-lookup"><span data-stu-id="18c09-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="18c09-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="18c09-183">packageSourceCredentials</span></span>

<span data-ttu-id="18c09-184">存储源的用户名和密码，通常通过 `-username` 使用 `-password` 和 `nuget sources` 开关指定。</span><span class="sxs-lookup"><span data-stu-id="18c09-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="18c09-185">默认情况下密码会进行加密，除非还使用了 `-storepasswordincleartext` 选项。</span><span class="sxs-lookup"><span data-stu-id="18c09-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="18c09-186">密钥</span><span class="sxs-lookup"><span data-stu-id="18c09-186">Key</span></span> | <span data-ttu-id="18c09-187">值</span><span class="sxs-lookup"><span data-stu-id="18c09-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="18c09-188">username</span><span class="sxs-lookup"><span data-stu-id="18c09-188">username</span></span> | <span data-ttu-id="18c09-189">纯文本形式的源用户名。</span><span class="sxs-lookup"><span data-stu-id="18c09-189">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="18c09-190">password</span><span class="sxs-lookup"><span data-stu-id="18c09-190">password</span></span> | <span data-ttu-id="18c09-191">源的加密密码。</span><span class="sxs-lookup"><span data-stu-id="18c09-191">The encrypted password for the source.</span></span> |
| <span data-ttu-id="18c09-192">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="18c09-192">cleartextpassword</span></span> | <span data-ttu-id="18c09-193">源的未加密密码。</span><span class="sxs-lookup"><span data-stu-id="18c09-193">The unencrypted password for the source.</span></span> |

<span data-ttu-id="18c09-194">**示例：**</span><span class="sxs-lookup"><span data-stu-id="18c09-194">**Example:**</span></span>

<span data-ttu-id="18c09-195">在配置文件中，`<packageSourceCredentials>` 元素包含每个适用源名称的子节点（名称中的空格被替换为 `_x0020_`）。</span><span class="sxs-lookup"><span data-stu-id="18c09-195">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="18c09-196">也就是说，对于名为“Contoso”和“测试源”的源，使用加密密码时，配置文件包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="18c09-196">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="18c09-197">使用未加密密码时：</span><span class="sxs-lookup"><span data-stu-id="18c09-197">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="18c09-198">apikeys</span><span class="sxs-lookup"><span data-stu-id="18c09-198">apikeys</span></span>

<span data-ttu-id="18c09-199">存储使用 API 密钥身份验证的源的密钥，如使用 [`nuget setapikey` 命令](../reference/cli-reference/cli-ref-setapikey.md) 设置。</span><span class="sxs-lookup"><span data-stu-id="18c09-199">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="18c09-200">密钥</span><span class="sxs-lookup"><span data-stu-id="18c09-200">Key</span></span> | <span data-ttu-id="18c09-201">值</span><span class="sxs-lookup"><span data-stu-id="18c09-201">Value</span></span> |
| --- | --- |
| <span data-ttu-id="18c09-202">（源 URL）</span><span class="sxs-lookup"><span data-stu-id="18c09-202">(source URL)</span></span> | <span data-ttu-id="18c09-203">加密的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="18c09-203">The encrypted API key.</span></span> |

<span data-ttu-id="18c09-204">**示例**：</span><span class="sxs-lookup"><span data-stu-id="18c09-204">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="18c09-205">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="18c09-205">disabledPackageSources</span></span>

<span data-ttu-id="18c09-206">标识当前已禁用的源。</span><span class="sxs-lookup"><span data-stu-id="18c09-206">Identified currently disabled sources.</span></span> <span data-ttu-id="18c09-207">可能为空。</span><span class="sxs-lookup"><span data-stu-id="18c09-207">May be empty.</span></span>

| <span data-ttu-id="18c09-208">密钥</span><span class="sxs-lookup"><span data-stu-id="18c09-208">Key</span></span> | <span data-ttu-id="18c09-209">值</span><span class="sxs-lookup"><span data-stu-id="18c09-209">Value</span></span> |
| --- | --- |
| <span data-ttu-id="18c09-210">（源名称）</span><span class="sxs-lookup"><span data-stu-id="18c09-210">(name of source)</span></span> | <span data-ttu-id="18c09-211">指示源是否禁用的布尔。</span><span class="sxs-lookup"><span data-stu-id="18c09-211">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="18c09-212">**示例：**</span><span class="sxs-lookup"><span data-stu-id="18c09-212">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="18c09-213">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="18c09-213">activePackageSource</span></span>

<span data-ttu-id="18c09-214">*（仅限于 2.x；3.x+ 中已弃用）*</span><span class="sxs-lookup"><span data-stu-id="18c09-214">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="18c09-215">标识到当前活动的源或指示所有源的聚合。</span><span class="sxs-lookup"><span data-stu-id="18c09-215">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="18c09-216">密钥</span><span class="sxs-lookup"><span data-stu-id="18c09-216">Key</span></span> | <span data-ttu-id="18c09-217">值</span><span class="sxs-lookup"><span data-stu-id="18c09-217">Value</span></span> |
| --- | --- |
| <span data-ttu-id="18c09-218">（源名称）或 `All`</span><span class="sxs-lookup"><span data-stu-id="18c09-218">(name of source) or `All`</span></span> | <span data-ttu-id="18c09-219">如果密钥是源的名称，则值为源路径或 URL。</span><span class="sxs-lookup"><span data-stu-id="18c09-219">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="18c09-220">如果为 `All`，值应为 `(Aggregate source)`，从而组合其他未禁用的所有包源。</span><span class="sxs-lookup"><span data-stu-id="18c09-220">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="18c09-221">**示例**：</span><span class="sxs-lookup"><span data-stu-id="18c09-221">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="18c09-222">trustedSigners 部分</span><span class="sxs-lookup"><span data-stu-id="18c09-222">trustedSigners section</span></span>

<span data-ttu-id="18c09-223">存储用于在安装或还原时允许包的可信签名者。</span><span class="sxs-lookup"><span data-stu-id="18c09-223">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="18c09-224">当用户将 `signatureValidationMode` 设置为 `require`时，此列表不能为空。</span><span class="sxs-lookup"><span data-stu-id="18c09-224">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="18c09-225">可以通过[`nuget trusted-signers` 命令](../reference/cli-reference/cli-ref-trusted-signers.md)更新此部分。</span><span class="sxs-lookup"><span data-stu-id="18c09-225">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="18c09-226">**架构**：</span><span class="sxs-lookup"><span data-stu-id="18c09-226">**Schema**:</span></span>

<span data-ttu-id="18c09-227">受信任的签名者具有 `certificate` 项的集合，这些项将登记标识给定签名者的所有证书。</span><span class="sxs-lookup"><span data-stu-id="18c09-227">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="18c09-228">受信任的签名者可以是 `Author` 或 `Repository`。</span><span class="sxs-lookup"><span data-stu-id="18c09-228">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="18c09-229">受信任的*存储库*还指定存储库的 `serviceIndex` （必须是有效的 `https` uri），并可以选择指定以分号分隔的 `owners` 列表，以限制更多的受信任的用户。</span><span class="sxs-lookup"><span data-stu-id="18c09-229">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="18c09-230">用于证书指纹的受支持的哈希算法 `SHA256`、`SHA384` 和 `SHA512`。</span><span class="sxs-lookup"><span data-stu-id="18c09-230">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="18c09-231">如果 `certificate` 指定 `allowUntrustedRoot` `true`，则在将证书链作为签名验证的一部分生成时，允许给定的证书链接到不受信任的根。</span><span class="sxs-lookup"><span data-stu-id="18c09-231">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="18c09-232">**示例**：</span><span class="sxs-lookup"><span data-stu-id="18c09-232">**Example**:</span></span>

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

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="18c09-233">fallbackPackageFolders 部分</span><span class="sxs-lookup"><span data-stu-id="18c09-233">fallbackPackageFolders section</span></span>

<span data-ttu-id="18c09-234">*（3.5 +）* 提供了一种预安装包的方法，以便在回退文件夹中发现包时无需执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="18c09-234">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="18c09-235">回退包文件夹与全局包文件夹具有完全相同的文件夹和文件结构： *。 nupkg*存在，并提取所有文件。</span><span class="sxs-lookup"><span data-stu-id="18c09-235">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="18c09-236">此配置的查找逻辑为：</span><span class="sxs-lookup"><span data-stu-id="18c09-236">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="18c09-237">查看全局包文件夹，查看是否已下载包/版本。</span><span class="sxs-lookup"><span data-stu-id="18c09-237">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="18c09-238">查看后备文件夹中是否有包/版本匹配。</span><span class="sxs-lookup"><span data-stu-id="18c09-238">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="18c09-239">如果查找成功，则无需下载。</span><span class="sxs-lookup"><span data-stu-id="18c09-239">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="18c09-240">如果找不到匹配项，NuGet 将检查文件源，然后检查 http 源，然后下载包。</span><span class="sxs-lookup"><span data-stu-id="18c09-240">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="18c09-241">密钥</span><span class="sxs-lookup"><span data-stu-id="18c09-241">Key</span></span> | <span data-ttu-id="18c09-242">值</span><span class="sxs-lookup"><span data-stu-id="18c09-242">Value</span></span> |
| --- | --- |
| <span data-ttu-id="18c09-243">（后备文件夹的名称）</span><span class="sxs-lookup"><span data-stu-id="18c09-243">(name of fallback folder)</span></span> | <span data-ttu-id="18c09-244">回退文件夹的路径。</span><span class="sxs-lookup"><span data-stu-id="18c09-244">Path to fallback folder.</span></span> |

<span data-ttu-id="18c09-245">**示例**：</span><span class="sxs-lookup"><span data-stu-id="18c09-245">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="18c09-246">packageManagement 部分</span><span class="sxs-lookup"><span data-stu-id="18c09-246">packageManagement section</span></span>

<span data-ttu-id="18c09-247">设置默认包管理格式 *，即 package 或 PackageReference* 。</span><span class="sxs-lookup"><span data-stu-id="18c09-247">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="18c09-248">SDK 样式项目始终使用 PackageReference。</span><span class="sxs-lookup"><span data-stu-id="18c09-248">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="18c09-249">密钥</span><span class="sxs-lookup"><span data-stu-id="18c09-249">Key</span></span> | <span data-ttu-id="18c09-250">值</span><span class="sxs-lookup"><span data-stu-id="18c09-250">Value</span></span> |
| --- | --- |
| <span data-ttu-id="18c09-251">format</span><span class="sxs-lookup"><span data-stu-id="18c09-251">format</span></span> | <span data-ttu-id="18c09-252">指示默认包管理格式的布尔值。</span><span class="sxs-lookup"><span data-stu-id="18c09-252">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="18c09-253">如果 `1`，格式为 PackageReference。</span><span class="sxs-lookup"><span data-stu-id="18c09-253">If `1`, format is PackageReference.</span></span> <span data-ttu-id="18c09-254">如果 `0`，则 format 为*包。*</span><span class="sxs-lookup"><span data-stu-id="18c09-254">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="18c09-255">disabled</span><span class="sxs-lookup"><span data-stu-id="18c09-255">disabled</span></span> | <span data-ttu-id="18c09-256">指示是否在第一次安装包时显示提示选择默认包格式的布尔值。</span><span class="sxs-lookup"><span data-stu-id="18c09-256">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="18c09-257">`False` 隐藏提示。</span><span class="sxs-lookup"><span data-stu-id="18c09-257">`False` hides the prompt.</span></span> |

<span data-ttu-id="18c09-258">**示例**：</span><span class="sxs-lookup"><span data-stu-id="18c09-258">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="18c09-259">使用环境变量</span><span class="sxs-lookup"><span data-stu-id="18c09-259">Using environment variables</span></span>

<span data-ttu-id="18c09-260">可以在 `nuget.config` 值中使用环境变量 (NuGet 3.4 +) 在运行时应用设置。</span><span class="sxs-lookup"><span data-stu-id="18c09-260">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="18c09-261">例如，如果 Windows 上的 `HOME` 环境变量设置为 `c:\users\username`，则配置文件中 `%HOME%\NuGetRepository` 的值解析为 `c:\users\username\NuGetRepository`。</span><span class="sxs-lookup"><span data-stu-id="18c09-261">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="18c09-262">请注意，必须使用 Windows 样式的环境变量（开头和结尾均为%）即使在 Mac/Linux 上也是如此。</span><span class="sxs-lookup"><span data-stu-id="18c09-262">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="18c09-263">配置文件中的 `$HOME/NuGetRepository` 将无法解析。</span><span class="sxs-lookup"><span data-stu-id="18c09-263">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="18c09-264">在 Mac/Linux 上，`%HOME%\NuGetRepository` 的值将解析为 `/home/myStuff/NuGetRepository`。</span><span class="sxs-lookup"><span data-stu-id="18c09-264">On Mac/Linux the value of `%HOME%\NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="18c09-265">如果未找到环境变量，NuGet 会使用配置文件中的文本值。</span><span class="sxs-lookup"><span data-stu-id="18c09-265">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="18c09-266">示例配置文件</span><span class="sxs-lookup"><span data-stu-id="18c09-266">Example config file</span></span>

<span data-ttu-id="18c09-267">下面是一个示例 `nuget.config` 文件示例，演示了一些设置，包括可选的设置：</span><span class="sxs-lookup"><span data-stu-id="18c09-267">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

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
