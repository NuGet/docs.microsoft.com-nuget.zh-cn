---
title: NuGet.Config 文件引用 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet.Config 文件引用，包括配置、bindingRedirects、packageRestore、解决方案和 packageSource 节。
keywords: NuGet.Config 文件, NuGet 配置引用, NuGet 配置选项
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e2a9d4f10ac6af4e5bc7386d4f78e18c2a5752c4
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="0e242-104">NuGet.Config 引用</span><span class="sxs-lookup"><span data-stu-id="0e242-104">NuGet.Config reference</span></span>

<span data-ttu-id="0e242-105">NuGet 行为由不同 `NuGet.Config` 文件中的设置控制，如[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="0e242-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="0e242-106">`NuGet.Config` 是包含顶级 `<configuration>` 节点的 XML 文件，而该节点包含本主题中所述的节元素。</span><span class="sxs-lookup"><span data-stu-id="0e242-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="0e242-107">每个节包含零个或多个具有 `key` 和 `value` 属性的 `<add>` 元素 。</span><span class="sxs-lookup"><span data-stu-id="0e242-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="0e242-108">请参阅[示例配置文件](#example-config-file)。</span><span class="sxs-lookup"><span data-stu-id="0e242-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="0e242-109">设置名称不区分大小写，并且值可以使用[环境变量](#using-environment-variables)。</span><span class="sxs-lookup"><span data-stu-id="0e242-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="0e242-110">本主题内容：</span><span class="sxs-lookup"><span data-stu-id="0e242-110">In this topic:</span></span>

- [<span data-ttu-id="0e242-111">配置节</span><span class="sxs-lookup"><span data-stu-id="0e242-111">config section</span></span>](#config-section)
- [<span data-ttu-id="0e242-112">bindingRedirects 节</span><span class="sxs-lookup"><span data-stu-id="0e242-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="0e242-113">packageRestore 节</span><span class="sxs-lookup"><span data-stu-id="0e242-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="0e242-114">解决方案节</span><span class="sxs-lookup"><span data-stu-id="0e242-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="0e242-115">[包源节](#package-source-sections)：</span><span class="sxs-lookup"><span data-stu-id="0e242-115">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="0e242-116">packageSources</span><span class="sxs-lookup"><span data-stu-id="0e242-116">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="0e242-117">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="0e242-117">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="0e242-118">apikeys</span><span class="sxs-lookup"><span data-stu-id="0e242-118">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="0e242-119">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="0e242-119">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="0e242-120">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="0e242-120">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="0e242-121">使用环境变量</span><span class="sxs-lookup"><span data-stu-id="0e242-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="0e242-122">示例配置文件</span><span class="sxs-lookup"><span data-stu-id="0e242-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="0e242-123">配置节</span><span class="sxs-lookup"><span data-stu-id="0e242-123">config section</span></span>

<span data-ttu-id="0e242-124">包含杂项配置设置，可使用 [`nuget config` 命令](../tools/cli-ref-config.md)设置。</span><span class="sxs-lookup"><span data-stu-id="0e242-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="0e242-125">`dependencyVersion` 和`repositoryPath`仅适用于使用的项目`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="0e242-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="0e242-126">`globalPackagesFolder` 仅适用于使用 PackageReference 格式的项目。</span><span class="sxs-lookup"><span data-stu-id="0e242-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="0e242-127">键</span><span class="sxs-lookup"><span data-stu-id="0e242-127">Key</span></span> | <span data-ttu-id="0e242-128">值</span><span class="sxs-lookup"><span data-stu-id="0e242-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0e242-129">dependencyVersion（仅限于 `packages.config`）</span><span class="sxs-lookup"><span data-stu-id="0e242-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="0e242-130">包安装、还原和更新的默认 `DependencyVersion` 值（未直接指定 `-DependencyVersion` 开关时）。</span><span class="sxs-lookup"><span data-stu-id="0e242-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="0e242-131">NuGet 包管理器 UI 也使用此值。</span><span class="sxs-lookup"><span data-stu-id="0e242-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="0e242-132">值为 `Lowest`、`HighestPatch`、`HighestMinor`、`Highest`。</span><span class="sxs-lookup"><span data-stu-id="0e242-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="0e242-133">globalPackagesFolder （仅限使用 PackageReference 项目）</span><span class="sxs-lookup"><span data-stu-id="0e242-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="0e242-134">默认全局包文件夹的位置。</span><span class="sxs-lookup"><span data-stu-id="0e242-134">The location of the default global packages folder.</span></span> <span data-ttu-id="0e242-135">默认值为 `%userprofile%\.nuget\packages` (Windows) 或 `~/.nuget/packages` (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="0e242-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="0e242-136">相对路径可在项目特定的 `Nuget.Config` 文件中使用。</span><span class="sxs-lookup"><span data-stu-id="0e242-136">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="0e242-137">此设置被重写通过 NUGET_PACKAGES 环境变量将优先。</span><span class="sxs-lookup"><span data-stu-id="0e242-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="0e242-138">repositoryPath（仅限于 `packages.config`）</span><span class="sxs-lookup"><span data-stu-id="0e242-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="0e242-139">安装 NuGet 包的位置，而非默认的 `$(Solutiondir)/packages` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="0e242-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="0e242-140">相对路径可在项目特定的 `Nuget.Config` 文件中使用。</span><span class="sxs-lookup"><span data-stu-id="0e242-140">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="0e242-141">此设置被重写通过 NUGET_PACKAGES 环境变量将优先。</span><span class="sxs-lookup"><span data-stu-id="0e242-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="0e242-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="0e242-142">defaultPushSource</span></span> | <span data-ttu-id="0e242-143">如果操作未找到任何其他包源，则会标识应用作默认值的包源 URL 或路径。</span><span class="sxs-lookup"><span data-stu-id="0e242-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="0e242-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="0e242-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="0e242-145">连接到包源时要使用的代理设置；`http_proxy` 应为 `http://<username>:<password>@<domain>` 格式。</span><span class="sxs-lookup"><span data-stu-id="0e242-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="0e242-146">密码已加密，且不能手动添加。</span><span class="sxs-lookup"><span data-stu-id="0e242-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="0e242-147">对于 `no_proxy`，该值是绕过代理服务器的域的列表（以逗号分隔）。</span><span class="sxs-lookup"><span data-stu-id="0e242-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="0e242-148">可将 http_proxy 和 no_proxy 环境变量交替用于这些值。</span><span class="sxs-lookup"><span data-stu-id="0e242-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="0e242-149">有关其他详细信息，请参阅 [NuGet 代理设置](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com)。</span><span class="sxs-lookup"><span data-stu-id="0e242-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="0e242-150">**示例**：</span><span class="sxs-lookup"><span data-stu-id="0e242-150">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="0e242-151">bindingRedirects 节</span><span class="sxs-lookup"><span data-stu-id="0e242-151">bindingRedirects section</span></span>

<span data-ttu-id="0e242-152">在安装包时，配置 NuGet 是否执行自动绑定重定向。</span><span class="sxs-lookup"><span data-stu-id="0e242-152">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="0e242-153">键</span><span class="sxs-lookup"><span data-stu-id="0e242-153">Key</span></span> | <span data-ttu-id="0e242-154">值</span><span class="sxs-lookup"><span data-stu-id="0e242-154">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0e242-155">skip</span><span class="sxs-lookup"><span data-stu-id="0e242-155">skip</span></span> | <span data-ttu-id="0e242-156">指示是否跳过自动绑定重定向的布尔。</span><span class="sxs-lookup"><span data-stu-id="0e242-156">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="0e242-157">默认值为 false。</span><span class="sxs-lookup"><span data-stu-id="0e242-157">The default is false.</span></span> |

<span data-ttu-id="0e242-158">**示例**：</span><span class="sxs-lookup"><span data-stu-id="0e242-158">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="0e242-159">packageRestore 节</span><span class="sxs-lookup"><span data-stu-id="0e242-159">packageRestore section</span></span>

<span data-ttu-id="0e242-160">在生成期间控制包还原。</span><span class="sxs-lookup"><span data-stu-id="0e242-160">Controls package restore during builds.</span></span>

| <span data-ttu-id="0e242-161">键</span><span class="sxs-lookup"><span data-stu-id="0e242-161">Key</span></span> | <span data-ttu-id="0e242-162">值</span><span class="sxs-lookup"><span data-stu-id="0e242-162">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0e242-163">enabled</span><span class="sxs-lookup"><span data-stu-id="0e242-163">enabled</span></span> | <span data-ttu-id="0e242-164">指示 NuGet 是否可执行自动还原的布尔。</span><span class="sxs-lookup"><span data-stu-id="0e242-164">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="0e242-165">还可以使用 `True` 的值设置 `EnableNuGetPackageRestore` 环境变量，而不是在配置文件中设置此密钥。</span><span class="sxs-lookup"><span data-stu-id="0e242-165">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="0e242-166">自动</span><span class="sxs-lookup"><span data-stu-id="0e242-166">automatic</span></span> | <span data-ttu-id="0e242-167">指示 NuGet 是否应在生成期间检查缺少的包。</span><span class="sxs-lookup"><span data-stu-id="0e242-167">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="0e242-168">**示例**：</span><span class="sxs-lookup"><span data-stu-id="0e242-168">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="0e242-169">解决方案节</span><span class="sxs-lookup"><span data-stu-id="0e242-169">solution section</span></span>

<span data-ttu-id="0e242-170">控制解决方案的 `packages` 文件夹是否包括在源代码管理中。</span><span class="sxs-lookup"><span data-stu-id="0e242-170">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="0e242-171">此节仅适用于解决方案文件夹中的 `Nuget.Config` 文件。</span><span class="sxs-lookup"><span data-stu-id="0e242-171">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="0e242-172">键</span><span class="sxs-lookup"><span data-stu-id="0e242-172">Key</span></span> | <span data-ttu-id="0e242-173">值</span><span class="sxs-lookup"><span data-stu-id="0e242-173">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0e242-174">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="0e242-174">disableSourceControlIntegration</span></span> | <span data-ttu-id="0e242-175">指示在使用源代码管理时是否忽略包文件夹的布尔。</span><span class="sxs-lookup"><span data-stu-id="0e242-175">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="0e242-176">默认值为 False。</span><span class="sxs-lookup"><span data-stu-id="0e242-176">The default value is false.</span></span> |

<span data-ttu-id="0e242-177">**示例**：</span><span class="sxs-lookup"><span data-stu-id="0e242-177">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="0e242-178">包源节</span><span class="sxs-lookup"><span data-stu-id="0e242-178">Package source sections</span></span>

<span data-ttu-id="0e242-179">在进行安装、还原和更新操作期间，`packageSources`、`packageSourceCredentials`、`apikeys`、`activePackageSource` 和 `disabledPackageSources` 全部一起协作来配置 NuGet 与包存储库协作的方式。</span><span class="sxs-lookup"><span data-stu-id="0e242-179">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="0e242-180">[`nuget sources` 命令](../tools/cli-ref-sources.md)通常用于管理这些设置，但 `apikeys` 使用 [`nuget setapikey` 命令](../tools/cli-ref-setapikey.md)进行管理。</span><span class="sxs-lookup"><span data-stu-id="0e242-180">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="0e242-181">请注意，nuget.org 的源 URL 是 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="0e242-181">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="0e242-182">packageSources</span><span class="sxs-lookup"><span data-stu-id="0e242-182">packageSources</span></span>

<span data-ttu-id="0e242-183">列出所有已知包源。</span><span class="sxs-lookup"><span data-stu-id="0e242-183">Lists all known package sources.</span></span> <span data-ttu-id="0e242-184">在还原操作期间和与使用 PackageReference 格式任何项目，将忽略顺序。</span><span class="sxs-lookup"><span data-stu-id="0e242-184">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="0e242-185">NuGet 遵循的顺序的源安装和使用的项目与更新操作`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="0e242-185">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="0e242-186">键</span><span class="sxs-lookup"><span data-stu-id="0e242-186">Key</span></span> | <span data-ttu-id="0e242-187">值</span><span class="sxs-lookup"><span data-stu-id="0e242-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0e242-188">（要分配给包源的名称）</span><span class="sxs-lookup"><span data-stu-id="0e242-188">(name to assign to the package source)</span></span> | <span data-ttu-id="0e242-189">包源的路径或 URL。</span><span class="sxs-lookup"><span data-stu-id="0e242-189">The path or URL of the package source.</span></span> |

<span data-ttu-id="0e242-190">**示例**：</span><span class="sxs-lookup"><span data-stu-id="0e242-190">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="0e242-191">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="0e242-191">packageSourceCredentials</span></span>

<span data-ttu-id="0e242-192">存储源的用户名和密码，通常通过 `nuget sources` 使用 `-username` 和 `-password` 开关指定。</span><span class="sxs-lookup"><span data-stu-id="0e242-192">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="0e242-193">默认情况下密码会进行加密，除非还使用了 `-storepasswordincleartext` 选项。</span><span class="sxs-lookup"><span data-stu-id="0e242-193">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="0e242-194">键</span><span class="sxs-lookup"><span data-stu-id="0e242-194">Key</span></span> | <span data-ttu-id="0e242-195">值</span><span class="sxs-lookup"><span data-stu-id="0e242-195">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0e242-196">username</span><span class="sxs-lookup"><span data-stu-id="0e242-196">username</span></span> | <span data-ttu-id="0e242-197">纯文本形式的源用户名。</span><span class="sxs-lookup"><span data-stu-id="0e242-197">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="0e242-198">密码</span><span class="sxs-lookup"><span data-stu-id="0e242-198">password</span></span> | <span data-ttu-id="0e242-199">源的加密密码。</span><span class="sxs-lookup"><span data-stu-id="0e242-199">The encrypted password for the source.</span></span> |
| <span data-ttu-id="0e242-200">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="0e242-200">cleartextpassword</span></span> | <span data-ttu-id="0e242-201">源的未加密密码。</span><span class="sxs-lookup"><span data-stu-id="0e242-201">The unencrypted password for the source.</span></span> |

<span data-ttu-id="0e242-202">**示例：**</span><span class="sxs-lookup"><span data-stu-id="0e242-202">**Example:**</span></span>

<span data-ttu-id="0e242-203">在配置文件中，`<packageSourceCredentials>` 元素包含每个适用源名称的子节点（名称中的空格被替换为 `_x0020_`）。</span><span class="sxs-lookup"><span data-stu-id="0e242-203">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="0e242-204">也就是说，对于名为“Contoso”和“测试源”的源，使用加密密码时，配置文件包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="0e242-204">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="0e242-205">使用未加密密码时：</span><span class="sxs-lookup"><span data-stu-id="0e242-205">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="0e242-206">apikeys</span><span class="sxs-lookup"><span data-stu-id="0e242-206">apikeys</span></span>

<span data-ttu-id="0e242-207">存储使用 API 密钥身份验证的源的密钥，如使用 [`nuget setapikey` 命令](../tools/cli-ref-setapikey.md) 设置。</span><span class="sxs-lookup"><span data-stu-id="0e242-207">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="0e242-208">键</span><span class="sxs-lookup"><span data-stu-id="0e242-208">Key</span></span> | <span data-ttu-id="0e242-209">值</span><span class="sxs-lookup"><span data-stu-id="0e242-209">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0e242-210">（源 URL）</span><span class="sxs-lookup"><span data-stu-id="0e242-210">(source URL)</span></span> | <span data-ttu-id="0e242-211">加密的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="0e242-211">The encrypted API key.</span></span> |

<span data-ttu-id="0e242-212">**示例**：</span><span class="sxs-lookup"><span data-stu-id="0e242-212">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="0e242-213">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="0e242-213">disabledPackageSources</span></span>

<span data-ttu-id="0e242-214">标识当前已禁用的源。</span><span class="sxs-lookup"><span data-stu-id="0e242-214">Identified currently disabled sources.</span></span> <span data-ttu-id="0e242-215">可能为空。</span><span class="sxs-lookup"><span data-stu-id="0e242-215">May be empty.</span></span>

| <span data-ttu-id="0e242-216">键</span><span class="sxs-lookup"><span data-stu-id="0e242-216">Key</span></span> | <span data-ttu-id="0e242-217">值</span><span class="sxs-lookup"><span data-stu-id="0e242-217">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0e242-218">（源名称）</span><span class="sxs-lookup"><span data-stu-id="0e242-218">(name of source)</span></span> | <span data-ttu-id="0e242-219">指示源是否禁用的布尔。</span><span class="sxs-lookup"><span data-stu-id="0e242-219">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="0e242-220">**示例：**</span><span class="sxs-lookup"><span data-stu-id="0e242-220">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="0e242-221">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="0e242-221">activePackageSource</span></span>

<span data-ttu-id="0e242-222">*（仅限于 2.x；3.x+ 中已弃用）*</span><span class="sxs-lookup"><span data-stu-id="0e242-222">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="0e242-223">标识到当前活动的源或指示所有源的聚合。</span><span class="sxs-lookup"><span data-stu-id="0e242-223">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="0e242-224">键</span><span class="sxs-lookup"><span data-stu-id="0e242-224">Key</span></span> | <span data-ttu-id="0e242-225">值</span><span class="sxs-lookup"><span data-stu-id="0e242-225">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0e242-226">（源名称）或 `All`</span><span class="sxs-lookup"><span data-stu-id="0e242-226">(name of source) or `All`</span></span> | <span data-ttu-id="0e242-227">如果密钥是源的名称，则值为源路径或 URL。</span><span class="sxs-lookup"><span data-stu-id="0e242-227">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="0e242-228">如果为 `All`，值应为 `(Aggregate source)`，从而组合其他未禁用的所有包源。</span><span class="sxs-lookup"><span data-stu-id="0e242-228">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="0e242-229">**示例**：</span><span class="sxs-lookup"><span data-stu-id="0e242-229">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="0e242-230">使用环境变量</span><span class="sxs-lookup"><span data-stu-id="0e242-230">Using environment variables</span></span>

<span data-ttu-id="0e242-231">可以在 `NuGet.Config` 值中使用环境变量 (NuGet 3.4 +) 在运行时应用设置。</span><span class="sxs-lookup"><span data-stu-id="0e242-231">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="0e242-232">例如，如果 Windows 上的 `HOME` 环境变量设置为 `c:\users\username`，则配置文件中 `%HOME%\NuGetRepository` 的值解析为 `c:\users\username\NuGetRepository`。</span><span class="sxs-lookup"><span data-stu-id="0e242-232">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="0e242-233">同样，如果 Mac/Linux 上的 `HOME` 设置为 `/home/myStuff`，则配置文件中的 `$HOME/NuGetRepository` 解析为 `/home/myStuff/NuGetRepository`。</span><span class="sxs-lookup"><span data-stu-id="0e242-233">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="0e242-234">如果未找到环境变量，NuGet 会使用配置文件中的文本值。</span><span class="sxs-lookup"><span data-stu-id="0e242-234">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="0e242-235">示例配置文件</span><span class="sxs-lookup"><span data-stu-id="0e242-235">Example config file</span></span>

<span data-ttu-id="0e242-236">下面是示例 `NuGet.Config` 文件，它对一些设置进行了说明：</span><span class="sxs-lookup"><span data-stu-id="0e242-236">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
