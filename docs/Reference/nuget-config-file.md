---
title: "NuGet.Config 文件引用 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "NuGet.Config 文件引用，包括配置、bindingRedirects、packageRestore、解决方案和 packageSource 节。"
keywords: "NuGet.Config 文件, NuGet 配置引用, NuGet 配置选项"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9a183b67ae18f4fa5c042f1806f8abcc9b799b77
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="19ddf-104">NuGet.Config 引用</span><span class="sxs-lookup"><span data-stu-id="19ddf-104">NuGet.Config reference</span></span>

<span data-ttu-id="19ddf-105">NuGet 行为由不同 `NuGet.Config` 文件中的设置控制，如[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="19ddf-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="19ddf-106">`NuGet.Config` 是包含顶级 `<configuration>` 节点的 XML 文件，而该节点包含本主题中所述的节元素。</span><span class="sxs-lookup"><span data-stu-id="19ddf-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="19ddf-107">每个节包含零个或多个具有 `key` 和 `value` 属性的 `<add>` 元素 。</span><span class="sxs-lookup"><span data-stu-id="19ddf-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="19ddf-108">请参阅[示例配置文件](#example-config-file)。</span><span class="sxs-lookup"><span data-stu-id="19ddf-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="19ddf-109">设置名称不区分大小写，并且值可以使用[环境变量](#using-environment-variables)。</span><span class="sxs-lookup"><span data-stu-id="19ddf-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="19ddf-110">本主题内容：</span><span class="sxs-lookup"><span data-stu-id="19ddf-110">In this topic:</span></span>

- [<span data-ttu-id="19ddf-111">配置节</span><span class="sxs-lookup"><span data-stu-id="19ddf-111">config section</span></span>](#config-section)
- [<span data-ttu-id="19ddf-112">bindingRedirects 节</span><span class="sxs-lookup"><span data-stu-id="19ddf-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="19ddf-113">packageRestore 节</span><span class="sxs-lookup"><span data-stu-id="19ddf-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="19ddf-114">解决方案节</span><span class="sxs-lookup"><span data-stu-id="19ddf-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="19ddf-115">[包源节](#package-source-sections)：</span><span class="sxs-lookup"><span data-stu-id="19ddf-115">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="19ddf-116">packageSources</span><span class="sxs-lookup"><span data-stu-id="19ddf-116">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="19ddf-117">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="19ddf-117">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="19ddf-118">apikeys</span><span class="sxs-lookup"><span data-stu-id="19ddf-118">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="19ddf-119">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="19ddf-119">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="19ddf-120">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="19ddf-120">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="19ddf-121">使用环境变量</span><span class="sxs-lookup"><span data-stu-id="19ddf-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="19ddf-122">示例配置文件</span><span class="sxs-lookup"><span data-stu-id="19ddf-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="19ddf-123">配置节</span><span class="sxs-lookup"><span data-stu-id="19ddf-123">config section</span></span>

<span data-ttu-id="19ddf-124">包含杂项配置设置，可使用 [`nuget config` 命令](../tools/cli-ref-config.md)设置。</span><span class="sxs-lookup"><span data-stu-id="19ddf-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="19ddf-125">注意：`dependencyVersion` 和 `repositoryPath` 仅适用于使用 `packages.config` 的项目。</span><span class="sxs-lookup"><span data-stu-id="19ddf-125">Note: `dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="19ddf-126">`globalPackagesFolder`仅适用于使用 PackageReference 格式的项目。</span><span class="sxs-lookup"><span data-stu-id="19ddf-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="19ddf-127">键</span><span class="sxs-lookup"><span data-stu-id="19ddf-127">Key</span></span> | <span data-ttu-id="19ddf-128">“值”</span><span class="sxs-lookup"><span data-stu-id="19ddf-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="19ddf-129">dependencyVersion（仅限于 `packages.config`）</span><span class="sxs-lookup"><span data-stu-id="19ddf-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="19ddf-130">包安装、还原和更新的默认 `DependencyVersion` 值（未直接指定 `-DependencyVersion` 开关时）。</span><span class="sxs-lookup"><span data-stu-id="19ddf-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="19ddf-131">NuGet 包管理器 UI 也使用此值。</span><span class="sxs-lookup"><span data-stu-id="19ddf-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="19ddf-132">值为 `Lowest`、`HighestPatch`、`HighestMinor`、`Highest`。</span><span class="sxs-lookup"><span data-stu-id="19ddf-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="19ddf-133">globalPackagesFolder（未使用 `packages.config` 的项目）</span><span class="sxs-lookup"><span data-stu-id="19ddf-133">globalPackagesFolder (projects not using `packages.config`)</span></span> | <span data-ttu-id="19ddf-134">默认全局包文件夹的位置。</span><span class="sxs-lookup"><span data-stu-id="19ddf-134">The location of the default global packages folder.</span></span> <span data-ttu-id="19ddf-135">默认值为 `%USERPROFILE%\.nuget\packages` (Windows) 或 `~/.nuget/packages` (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="19ddf-135">The default is `%USERPROFILE%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="19ddf-136">相对路径可在项目特定的 `Nuget.Config` 文件中使用。</span><span class="sxs-lookup"><span data-stu-id="19ddf-136">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="19ddf-137">repositoryPath（仅限于 `packages.config`）</span><span class="sxs-lookup"><span data-stu-id="19ddf-137">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="19ddf-138">安装 NuGet 包的位置，而非默认的 `$(Solutiondir)/packages` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="19ddf-138">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="19ddf-139">相对路径可在项目特定的 `Nuget.Config` 文件中使用。</span><span class="sxs-lookup"><span data-stu-id="19ddf-139">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="19ddf-140">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="19ddf-140">defaultPushSource</span></span> | <span data-ttu-id="19ddf-141">如果操作未找到任何其他包源，则会标识应用作默认值的包源 URL 或路径。</span><span class="sxs-lookup"><span data-stu-id="19ddf-141">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="19ddf-142">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="19ddf-142">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="19ddf-143">连接到包源时要使用的代理设置；`http_proxy` 应为 `http://<username>:<password>@<domain>` 格式。</span><span class="sxs-lookup"><span data-stu-id="19ddf-143">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="19ddf-144">密码已加密，且不能手动添加。</span><span class="sxs-lookup"><span data-stu-id="19ddf-144">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="19ddf-145">对于 `no_proxy`，该值是绕过代理服务器的域的列表（以逗号分隔）。</span><span class="sxs-lookup"><span data-stu-id="19ddf-145">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="19ddf-146">可将 http_proxy 和 no_proxy 环境变量交替用于这些值。</span><span class="sxs-lookup"><span data-stu-id="19ddf-146">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="19ddf-147">有关其他详细信息，请参阅 [NuGet 代理设置](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com)。</span><span class="sxs-lookup"><span data-stu-id="19ddf-147">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="19ddf-148">**示例**：</span><span class="sxs-lookup"><span data-stu-id="19ddf-148">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="19ddf-149">bindingRedirects 节</span><span class="sxs-lookup"><span data-stu-id="19ddf-149">bindingRedirects section</span></span>

<span data-ttu-id="19ddf-150">在安装包时，配置 NuGet 是否执行自动绑定重定向。</span><span class="sxs-lookup"><span data-stu-id="19ddf-150">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="19ddf-151">键</span><span class="sxs-lookup"><span data-stu-id="19ddf-151">Key</span></span> | <span data-ttu-id="19ddf-152">“值”</span><span class="sxs-lookup"><span data-stu-id="19ddf-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="19ddf-153">skip</span><span class="sxs-lookup"><span data-stu-id="19ddf-153">skip</span></span> | <span data-ttu-id="19ddf-154">指示是否跳过自动绑定重定向的布尔。</span><span class="sxs-lookup"><span data-stu-id="19ddf-154">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="19ddf-155">默认值为 false。</span><span class="sxs-lookup"><span data-stu-id="19ddf-155">The default is false.</span></span> |

<span data-ttu-id="19ddf-156">**示例**：</span><span class="sxs-lookup"><span data-stu-id="19ddf-156">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="19ddf-157">packageRestore 节</span><span class="sxs-lookup"><span data-stu-id="19ddf-157">packageRestore section</span></span>

<span data-ttu-id="19ddf-158">*2.7+ 中已忽略*</span><span class="sxs-lookup"><span data-stu-id="19ddf-158">*Ignored in 2.7+*</span></span>

<span data-ttu-id="19ddf-159">在生成期间控制包还原。</span><span class="sxs-lookup"><span data-stu-id="19ddf-159">Controls package restore during builds.</span></span>

| <span data-ttu-id="19ddf-160">键</span><span class="sxs-lookup"><span data-stu-id="19ddf-160">Key</span></span> | <span data-ttu-id="19ddf-161">“值”</span><span class="sxs-lookup"><span data-stu-id="19ddf-161">Value</span></span> |
| --- | --- |
| <span data-ttu-id="19ddf-162">enabled</span><span class="sxs-lookup"><span data-stu-id="19ddf-162">enabled</span></span> | <span data-ttu-id="19ddf-163">指示 NuGet 是否可执行自动还原的布尔。</span><span class="sxs-lookup"><span data-stu-id="19ddf-163">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="19ddf-164">还可以使用 `True` 的值设置 `EnableNuGetPackageRestore` 环境变量，而不是在配置文件中设置此密钥。</span><span class="sxs-lookup"><span data-stu-id="19ddf-164">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="19ddf-165">自动</span><span class="sxs-lookup"><span data-stu-id="19ddf-165">automatic</span></span> | <span data-ttu-id="19ddf-166">指示 NuGet 是否应在生成期间检查缺少的包。</span><span class="sxs-lookup"><span data-stu-id="19ddf-166">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="19ddf-167">**示例**：</span><span class="sxs-lookup"><span data-stu-id="19ddf-167">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="19ddf-168">解决方案节</span><span class="sxs-lookup"><span data-stu-id="19ddf-168">solution section</span></span>

<span data-ttu-id="19ddf-169">控制解决方案的 `packages` 文件夹是否包括在源代码管理中。</span><span class="sxs-lookup"><span data-stu-id="19ddf-169">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="19ddf-170">此节仅适用于解决方案文件夹中的 `Nuget.Config` 文件。</span><span class="sxs-lookup"><span data-stu-id="19ddf-170">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="19ddf-171">键</span><span class="sxs-lookup"><span data-stu-id="19ddf-171">Key</span></span> | <span data-ttu-id="19ddf-172">“值”</span><span class="sxs-lookup"><span data-stu-id="19ddf-172">Value</span></span> |
| --- | --- |
| <span data-ttu-id="19ddf-173">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="19ddf-173">disableSourceControlIntegration</span></span> | <span data-ttu-id="19ddf-174">指示在使用源代码管理时是否忽略包文件夹的布尔。</span><span class="sxs-lookup"><span data-stu-id="19ddf-174">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="19ddf-175">默认值为 False。</span><span class="sxs-lookup"><span data-stu-id="19ddf-175">The default value is false.</span></span> |

<span data-ttu-id="19ddf-176">**示例**：</span><span class="sxs-lookup"><span data-stu-id="19ddf-176">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="19ddf-177">包源节</span><span class="sxs-lookup"><span data-stu-id="19ddf-177">Package source sections</span></span>

<span data-ttu-id="19ddf-178">在进行安装、还原和更新操作期间，`packageSources`、`packageSourceCredentials`、`apikeys`、`activePackageSource` 和 `disabledPackageSources` 全部一起协作来配置 NuGet 与包存储库协作的方式。</span><span class="sxs-lookup"><span data-stu-id="19ddf-178">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="19ddf-179">[`nuget sources` 命令](../tools/cli-ref-sources.md)通常用于管理这些设置，但 `apikeys` 使用 [`nuget setapikey` 命令](../tools/cli-ref-setapikey.md)进行管理。</span><span class="sxs-lookup"><span data-stu-id="19ddf-179">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="19ddf-180">请注意，nuget.org 的源 URL 是 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="19ddf-180">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="19ddf-181">packageSources</span><span class="sxs-lookup"><span data-stu-id="19ddf-181">packageSources</span></span>

<span data-ttu-id="19ddf-182">列出所有已知包源。</span><span class="sxs-lookup"><span data-stu-id="19ddf-182">Lists all known package sources.</span></span>

| <span data-ttu-id="19ddf-183">键</span><span class="sxs-lookup"><span data-stu-id="19ddf-183">Key</span></span> | <span data-ttu-id="19ddf-184">“值”</span><span class="sxs-lookup"><span data-stu-id="19ddf-184">Value</span></span> |
| --- | --- |
| <span data-ttu-id="19ddf-185">（要分配给包源的名称）</span><span class="sxs-lookup"><span data-stu-id="19ddf-185">(name to assign to the package source)</span></span> | <span data-ttu-id="19ddf-186">包源的路径或 URL。</span><span class="sxs-lookup"><span data-stu-id="19ddf-186">The path or URL of the package source.</span></span> |

<span data-ttu-id="19ddf-187">**示例**：</span><span class="sxs-lookup"><span data-stu-id="19ddf-187">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="19ddf-188">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="19ddf-188">packageSourceCredentials</span></span>

<span data-ttu-id="19ddf-189">存储源的用户名和密码，通常通过 `nuget sources` 使用 `-username` 和 `-password` 开关指定。</span><span class="sxs-lookup"><span data-stu-id="19ddf-189">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="19ddf-190">默认情况下密码会进行加密，除非还使用了 `-storepasswordincleartext` 选项。</span><span class="sxs-lookup"><span data-stu-id="19ddf-190">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="19ddf-191">键</span><span class="sxs-lookup"><span data-stu-id="19ddf-191">Key</span></span> | <span data-ttu-id="19ddf-192">“值”</span><span class="sxs-lookup"><span data-stu-id="19ddf-192">Value</span></span> |
| --- | --- |
| <span data-ttu-id="19ddf-193">username</span><span class="sxs-lookup"><span data-stu-id="19ddf-193">username</span></span> | <span data-ttu-id="19ddf-194">纯文本形式的源用户名。</span><span class="sxs-lookup"><span data-stu-id="19ddf-194">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="19ddf-195">密码</span><span class="sxs-lookup"><span data-stu-id="19ddf-195">password</span></span> | <span data-ttu-id="19ddf-196">源的加密密码。</span><span class="sxs-lookup"><span data-stu-id="19ddf-196">The encrypted password for the source.</span></span> |
| <span data-ttu-id="19ddf-197">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="19ddf-197">cleartextpassword</span></span> | <span data-ttu-id="19ddf-198">源的未加密密码。</span><span class="sxs-lookup"><span data-stu-id="19ddf-198">The unencrypted password for the source.</span></span> |

<span data-ttu-id="19ddf-199">**示例：**</span><span class="sxs-lookup"><span data-stu-id="19ddf-199">**Example:**</span></span>

<span data-ttu-id="19ddf-200">在配置文件中，`<packageSourceCredentials>` 元素包含每个适用源名称的子节点（名称中的空格被替换为 `_x0020+`）。</span><span class="sxs-lookup"><span data-stu-id="19ddf-200">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020+`).</span></span> <span data-ttu-id="19ddf-201">也就是说，对于名为“Contoso”和“测试源”的源，使用加密密码时，配置文件包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="19ddf-201">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="19ddf-202">使用未加密密码时：</span><span class="sxs-lookup"><span data-stu-id="19ddf-202">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="19ddf-203">apikeys</span><span class="sxs-lookup"><span data-stu-id="19ddf-203">apikeys</span></span>

<span data-ttu-id="19ddf-204">存储使用 API 密钥身份验证的源的密钥，如使用 [`nuget setapikey` 命令](../tools/cli-ref-setapikey.md) 设置。</span><span class="sxs-lookup"><span data-stu-id="19ddf-204">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="19ddf-205">键</span><span class="sxs-lookup"><span data-stu-id="19ddf-205">Key</span></span> | <span data-ttu-id="19ddf-206">“值”</span><span class="sxs-lookup"><span data-stu-id="19ddf-206">Value</span></span> |
| --- | --- |
| <span data-ttu-id="19ddf-207">（源 URL）</span><span class="sxs-lookup"><span data-stu-id="19ddf-207">(source URL)</span></span> | <span data-ttu-id="19ddf-208">加密的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="19ddf-208">The encrypted API key.</span></span> |

<span data-ttu-id="19ddf-209">**示例**：</span><span class="sxs-lookup"><span data-stu-id="19ddf-209">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="19ddf-210">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="19ddf-210">disabledPackageSources</span></span>

<span data-ttu-id="19ddf-211">标识当前已禁用的源。</span><span class="sxs-lookup"><span data-stu-id="19ddf-211">Identified currently disabled sources.</span></span> <span data-ttu-id="19ddf-212">可能为空。</span><span class="sxs-lookup"><span data-stu-id="19ddf-212">May be empty.</span></span>

| <span data-ttu-id="19ddf-213">键</span><span class="sxs-lookup"><span data-stu-id="19ddf-213">Key</span></span> | <span data-ttu-id="19ddf-214">“值”</span><span class="sxs-lookup"><span data-stu-id="19ddf-214">Value</span></span> |
| --- | --- |
| <span data-ttu-id="19ddf-215">（源名称）</span><span class="sxs-lookup"><span data-stu-id="19ddf-215">(name of source)</span></span> | <span data-ttu-id="19ddf-216">指示源是否禁用的布尔。</span><span class="sxs-lookup"><span data-stu-id="19ddf-216">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="19ddf-217">**示例：**</span><span class="sxs-lookup"><span data-stu-id="19ddf-217">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="19ddf-218">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="19ddf-218">activePackageSource</span></span>

<span data-ttu-id="19ddf-219">*（仅限于 2.x；3.x+ 中已弃用）*</span><span class="sxs-lookup"><span data-stu-id="19ddf-219">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="19ddf-220">标识到当前活动的源或指示所有源的聚合。</span><span class="sxs-lookup"><span data-stu-id="19ddf-220">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="19ddf-221">键</span><span class="sxs-lookup"><span data-stu-id="19ddf-221">Key</span></span> | <span data-ttu-id="19ddf-222">“值”</span><span class="sxs-lookup"><span data-stu-id="19ddf-222">Value</span></span> |
| --- | --- |
| <span data-ttu-id="19ddf-223">（源名称）或 `All`</span><span class="sxs-lookup"><span data-stu-id="19ddf-223">(name of source) or `All`</span></span> | <span data-ttu-id="19ddf-224">如果密钥是源的名称，则值为源路径或 URL。</span><span class="sxs-lookup"><span data-stu-id="19ddf-224">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="19ddf-225">如果为 `All`，值应为 `(Aggregate source)`，从而组合其他未禁用的所有包源。</span><span class="sxs-lookup"><span data-stu-id="19ddf-225">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="19ddf-226">**示例**：</span><span class="sxs-lookup"><span data-stu-id="19ddf-226">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="19ddf-227">使用环境变量</span><span class="sxs-lookup"><span data-stu-id="19ddf-227">Using environment variables</span></span>

<span data-ttu-id="19ddf-228">可以在 `NuGet.Config` 值中使用环境变量 (NuGet 3.4 +) 在运行时应用设置。</span><span class="sxs-lookup"><span data-stu-id="19ddf-228">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="19ddf-229">例如，如果 Windows 上的 `HOME` 环境变量设置为 `c:\users\username`，则配置文件中 `%HOME%\NuGetRepository` 的值解析为 `c:\users\username\NuGetRepository`。</span><span class="sxs-lookup"><span data-stu-id="19ddf-229">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="19ddf-230">同样，如果 Mac/Linux 上的 `HOME` 设置为 `/home/myStuff`，则配置文件中的 `$HOME/NuGetRepository` 解析为 `/home/myStuff/NuGetRepository`。</span><span class="sxs-lookup"><span data-stu-id="19ddf-230">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="19ddf-231">如果未找到环境变量，NuGet 会使用配置文件中的文本值。</span><span class="sxs-lookup"><span data-stu-id="19ddf-231">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="19ddf-232">示例配置文件</span><span class="sxs-lookup"><span data-stu-id="19ddf-232">Example config file</span></span>

<span data-ttu-id="19ddf-233">下面是示例 `NuGet.Config` 文件，它对一些设置进行了说明：</span><span class="sxs-lookup"><span data-stu-id="19ddf-233">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
</configuration>
```
