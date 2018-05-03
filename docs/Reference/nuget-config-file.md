---
title: nuget.config 文件引用
description: NuGet.Config 文件引用，包括配置、bindingRedirects、packageRestore、解决方案和 packageSource 节。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: 871cd05ed010d2a31348151de6b7e225ed2dc915
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="6fa1c-103">nuget.config 引用</span><span class="sxs-lookup"><span data-stu-id="6fa1c-103">nuget.config reference</span></span>

<span data-ttu-id="6fa1c-104">NuGet 行为由不同 `NuGet.Config` 文件中的设置控制，如[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="6fa1c-105">`nuget.config` 是包含顶级 `<configuration>` 节点的 XML 文件，而该节点包含本主题中所述的节元素。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="6fa1c-106">每个节包含零个或多个具有 `key` 和 `value` 属性的 `<add>` 元素 。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-106">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="6fa1c-107">请参阅[示例配置文件](#example-config-file)。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="6fa1c-108">设置名称不区分大小写，并且值可以使用[环境变量](#using-environment-variables)。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="6fa1c-109">本主题内容：</span><span class="sxs-lookup"><span data-stu-id="6fa1c-109">In this topic:</span></span>

- [<span data-ttu-id="6fa1c-110">配置节</span><span class="sxs-lookup"><span data-stu-id="6fa1c-110">config section</span></span>](#config-section)
- [<span data-ttu-id="6fa1c-111">bindingRedirects 节</span><span class="sxs-lookup"><span data-stu-id="6fa1c-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="6fa1c-112">packageRestore 节</span><span class="sxs-lookup"><span data-stu-id="6fa1c-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="6fa1c-113">解决方案节</span><span class="sxs-lookup"><span data-stu-id="6fa1c-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="6fa1c-114">[包源节](#package-source-sections)：</span><span class="sxs-lookup"><span data-stu-id="6fa1c-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="6fa1c-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="6fa1c-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="6fa1c-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="6fa1c-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="6fa1c-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="6fa1c-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="6fa1c-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="6fa1c-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="6fa1c-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="6fa1c-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="6fa1c-120">使用环境变量</span><span class="sxs-lookup"><span data-stu-id="6fa1c-120">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="6fa1c-121">示例配置文件</span><span class="sxs-lookup"><span data-stu-id="6fa1c-121">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="6fa1c-122">配置节</span><span class="sxs-lookup"><span data-stu-id="6fa1c-122">config section</span></span>

<span data-ttu-id="6fa1c-123">包含杂项配置设置，可使用 [`nuget config` 命令](../tools/cli-ref-config.md)设置。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-123">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="6fa1c-124">`dependencyVersion` 和`repositoryPath`仅适用于使用的项目`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-124">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="6fa1c-125">`globalPackagesFolder` 仅适用于使用 PackageReference 格式的项目。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-125">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="6fa1c-126">键</span><span class="sxs-lookup"><span data-stu-id="6fa1c-126">Key</span></span> | <span data-ttu-id="6fa1c-127">值</span><span class="sxs-lookup"><span data-stu-id="6fa1c-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6fa1c-128">dependencyVersion（仅限于 `packages.config`）</span><span class="sxs-lookup"><span data-stu-id="6fa1c-128">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="6fa1c-129">包安装、还原和更新的默认 `DependencyVersion` 值（未直接指定 `-DependencyVersion` 开关时）。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-129">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="6fa1c-130">NuGet 包管理器 UI 也使用此值。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-130">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="6fa1c-131">值为 `Lowest`、`HighestPatch`、`HighestMinor`、`Highest`。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-131">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="6fa1c-132">globalPackagesFolder （仅限使用 PackageReference 项目）</span><span class="sxs-lookup"><span data-stu-id="6fa1c-132">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="6fa1c-133">默认全局包文件夹的位置。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-133">The location of the default global packages folder.</span></span> <span data-ttu-id="6fa1c-134">默认值为 `%userprofile%\.nuget\packages` (Windows) 或 `~/.nuget/packages` (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-134">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="6fa1c-135">相对路径可在项目特定的 `nuget.config` 文件中使用。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-135">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="6fa1c-136">此设置被重写通过 NUGET_PACKAGES 环境变量将优先。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-136">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="6fa1c-137">repositoryPath（仅限于 `packages.config`）</span><span class="sxs-lookup"><span data-stu-id="6fa1c-137">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="6fa1c-138">安装 NuGet 包的位置，而非默认的 `$(Solutiondir)/packages` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-138">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="6fa1c-139">相对路径可在项目特定的 `nuget.config` 文件中使用。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-139">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="6fa1c-140">此设置被重写通过 NUGET_PACKAGES 环境变量将优先。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-140">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="6fa1c-141">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="6fa1c-141">defaultPushSource</span></span> | <span data-ttu-id="6fa1c-142">如果操作未找到任何其他包源，则会标识应用作默认值的包源 URL 或路径。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-142">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="6fa1c-143">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="6fa1c-143">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="6fa1c-144">连接到包源时要使用的代理设置；`http_proxy` 应为 `http://<username>:<password>@<domain>` 格式。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-144">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="6fa1c-145">密码已加密，且不能手动添加。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-145">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="6fa1c-146">对于 `no_proxy`，该值是绕过代理服务器的域的列表（以逗号分隔）。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-146">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="6fa1c-147">可将 http_proxy 和 no_proxy 环境变量交替用于这些值。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-147">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="6fa1c-148">有关其他详细信息，请参阅 [NuGet 代理设置](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com)。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-148">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="6fa1c-149">**示例**：</span><span class="sxs-lookup"><span data-stu-id="6fa1c-149">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="6fa1c-150">bindingRedirects 节</span><span class="sxs-lookup"><span data-stu-id="6fa1c-150">bindingRedirects section</span></span>

<span data-ttu-id="6fa1c-151">在安装包时，配置 NuGet 是否执行自动绑定重定向。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-151">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="6fa1c-152">键</span><span class="sxs-lookup"><span data-stu-id="6fa1c-152">Key</span></span> | <span data-ttu-id="6fa1c-153">值</span><span class="sxs-lookup"><span data-stu-id="6fa1c-153">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6fa1c-154">skip</span><span class="sxs-lookup"><span data-stu-id="6fa1c-154">skip</span></span> | <span data-ttu-id="6fa1c-155">指示是否跳过自动绑定重定向的布尔。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-155">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="6fa1c-156">默认值为 false。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-156">The default is false.</span></span> |

<span data-ttu-id="6fa1c-157">**示例**：</span><span class="sxs-lookup"><span data-stu-id="6fa1c-157">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="6fa1c-158">packageRestore 节</span><span class="sxs-lookup"><span data-stu-id="6fa1c-158">packageRestore section</span></span>

<span data-ttu-id="6fa1c-159">在生成期间控制包还原。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-159">Controls package restore during builds.</span></span>

| <span data-ttu-id="6fa1c-160">键</span><span class="sxs-lookup"><span data-stu-id="6fa1c-160">Key</span></span> | <span data-ttu-id="6fa1c-161">值</span><span class="sxs-lookup"><span data-stu-id="6fa1c-161">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6fa1c-162">enabled</span><span class="sxs-lookup"><span data-stu-id="6fa1c-162">enabled</span></span> | <span data-ttu-id="6fa1c-163">指示 NuGet 是否可执行自动还原的布尔。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-163">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="6fa1c-164">还可以使用 `True` 的值设置 `EnableNuGetPackageRestore` 环境变量，而不是在配置文件中设置此密钥。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-164">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="6fa1c-165">自动</span><span class="sxs-lookup"><span data-stu-id="6fa1c-165">automatic</span></span> | <span data-ttu-id="6fa1c-166">指示 NuGet 是否应在生成期间检查缺少的包。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-166">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="6fa1c-167">**示例**：</span><span class="sxs-lookup"><span data-stu-id="6fa1c-167">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="6fa1c-168">解决方案节</span><span class="sxs-lookup"><span data-stu-id="6fa1c-168">solution section</span></span>

<span data-ttu-id="6fa1c-169">控制解决方案的 `packages` 文件夹是否包括在源代码管理中。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-169">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="6fa1c-170">此节仅适用于解决方案文件夹中的 `nuget.config` 文件。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-170">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="6fa1c-171">键</span><span class="sxs-lookup"><span data-stu-id="6fa1c-171">Key</span></span> | <span data-ttu-id="6fa1c-172">值</span><span class="sxs-lookup"><span data-stu-id="6fa1c-172">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6fa1c-173">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="6fa1c-173">disableSourceControlIntegration</span></span> | <span data-ttu-id="6fa1c-174">指示在使用源代码管理时是否忽略包文件夹的布尔。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-174">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="6fa1c-175">默认值为 False。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-175">The default value is false.</span></span> |

<span data-ttu-id="6fa1c-176">**示例**：</span><span class="sxs-lookup"><span data-stu-id="6fa1c-176">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="6fa1c-177">包源节</span><span class="sxs-lookup"><span data-stu-id="6fa1c-177">Package source sections</span></span>

<span data-ttu-id="6fa1c-178">在进行安装、还原和更新操作期间，`packageSources`、`packageSourceCredentials`、`apikeys`、`activePackageSource` 和 `disabledPackageSources` 全部一起协作来配置 NuGet 与包存储库协作的方式。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-178">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="6fa1c-179">[`nuget sources` 命令](../tools/cli-ref-sources.md)通常用于管理这些设置，但 `apikeys` 使用 [`nuget setapikey` 命令](../tools/cli-ref-setapikey.md)进行管理。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-179">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="6fa1c-180">请注意，nuget.org 的源 URL 是 `https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-180">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="6fa1c-181">packageSources</span><span class="sxs-lookup"><span data-stu-id="6fa1c-181">packageSources</span></span>

<span data-ttu-id="6fa1c-182">列出所有已知包源。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-182">Lists all known package sources.</span></span> <span data-ttu-id="6fa1c-183">在还原操作期间和与使用 PackageReference 格式任何项目，将忽略顺序。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-183">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="6fa1c-184">NuGet 遵循的顺序的源安装和使用的项目与更新操作`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-184">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="6fa1c-185">键</span><span class="sxs-lookup"><span data-stu-id="6fa1c-185">Key</span></span> | <span data-ttu-id="6fa1c-186">值</span><span class="sxs-lookup"><span data-stu-id="6fa1c-186">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6fa1c-187">（要分配给包源的名称）</span><span class="sxs-lookup"><span data-stu-id="6fa1c-187">(name to assign to the package source)</span></span> | <span data-ttu-id="6fa1c-188">包源的路径或 URL。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-188">The path or URL of the package source.</span></span> |

<span data-ttu-id="6fa1c-189">**示例**：</span><span class="sxs-lookup"><span data-stu-id="6fa1c-189">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="6fa1c-190">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="6fa1c-190">packageSourceCredentials</span></span>

<span data-ttu-id="6fa1c-191">存储源的用户名和密码，通常通过 `nuget sources` 使用 `-username` 和 `-password` 开关指定。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-191">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="6fa1c-192">默认情况下密码会进行加密，除非还使用了 `-storepasswordincleartext` 选项。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-192">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="6fa1c-193">键</span><span class="sxs-lookup"><span data-stu-id="6fa1c-193">Key</span></span> | <span data-ttu-id="6fa1c-194">值</span><span class="sxs-lookup"><span data-stu-id="6fa1c-194">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6fa1c-195">username</span><span class="sxs-lookup"><span data-stu-id="6fa1c-195">username</span></span> | <span data-ttu-id="6fa1c-196">纯文本形式的源用户名。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-196">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="6fa1c-197">密码</span><span class="sxs-lookup"><span data-stu-id="6fa1c-197">password</span></span> | <span data-ttu-id="6fa1c-198">源的加密密码。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-198">The encrypted password for the source.</span></span> |
| <span data-ttu-id="6fa1c-199">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="6fa1c-199">cleartextpassword</span></span> | <span data-ttu-id="6fa1c-200">源的未加密密码。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-200">The unencrypted password for the source.</span></span> |

<span data-ttu-id="6fa1c-201">**示例：**</span><span class="sxs-lookup"><span data-stu-id="6fa1c-201">**Example:**</span></span>

<span data-ttu-id="6fa1c-202">在配置文件中，`<packageSourceCredentials>` 元素包含每个适用源名称的子节点（名称中的空格被替换为 `_x0020_`）。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="6fa1c-203">也就是说，对于名为“Contoso”和“测试源”的源，使用加密密码时，配置文件包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="6fa1c-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="6fa1c-204">使用未加密密码时：</span><span class="sxs-lookup"><span data-stu-id="6fa1c-204">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="6fa1c-205">apikeys</span><span class="sxs-lookup"><span data-stu-id="6fa1c-205">apikeys</span></span>

<span data-ttu-id="6fa1c-206">存储使用 API 密钥身份验证的源的密钥，如使用 [`nuget setapikey` 命令](../tools/cli-ref-setapikey.md) 设置。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-206">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="6fa1c-207">键</span><span class="sxs-lookup"><span data-stu-id="6fa1c-207">Key</span></span> | <span data-ttu-id="6fa1c-208">值</span><span class="sxs-lookup"><span data-stu-id="6fa1c-208">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6fa1c-209">（源 URL）</span><span class="sxs-lookup"><span data-stu-id="6fa1c-209">(source URL)</span></span> | <span data-ttu-id="6fa1c-210">加密的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-210">The encrypted API key.</span></span> |

<span data-ttu-id="6fa1c-211">**示例**：</span><span class="sxs-lookup"><span data-stu-id="6fa1c-211">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="6fa1c-212">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="6fa1c-212">disabledPackageSources</span></span>

<span data-ttu-id="6fa1c-213">标识当前已禁用的源。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-213">Identified currently disabled sources.</span></span> <span data-ttu-id="6fa1c-214">可能为空。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-214">May be empty.</span></span>

| <span data-ttu-id="6fa1c-215">键</span><span class="sxs-lookup"><span data-stu-id="6fa1c-215">Key</span></span> | <span data-ttu-id="6fa1c-216">值</span><span class="sxs-lookup"><span data-stu-id="6fa1c-216">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6fa1c-217">（源名称）</span><span class="sxs-lookup"><span data-stu-id="6fa1c-217">(name of source)</span></span> | <span data-ttu-id="6fa1c-218">指示源是否禁用的布尔。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-218">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="6fa1c-219">**示例：**</span><span class="sxs-lookup"><span data-stu-id="6fa1c-219">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="6fa1c-220">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="6fa1c-220">activePackageSource</span></span>

<span data-ttu-id="6fa1c-221">*（仅限于 2.x；3.x+ 中已弃用）*</span><span class="sxs-lookup"><span data-stu-id="6fa1c-221">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="6fa1c-222">标识到当前活动的源或指示所有源的聚合。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-222">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="6fa1c-223">键</span><span class="sxs-lookup"><span data-stu-id="6fa1c-223">Key</span></span> | <span data-ttu-id="6fa1c-224">值</span><span class="sxs-lookup"><span data-stu-id="6fa1c-224">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6fa1c-225">（源名称）或 `All`</span><span class="sxs-lookup"><span data-stu-id="6fa1c-225">(name of source) or `All`</span></span> | <span data-ttu-id="6fa1c-226">如果密钥是源的名称，则值为源路径或 URL。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-226">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="6fa1c-227">如果为 `All`，值应为 `(Aggregate source)`，从而组合其他未禁用的所有包源。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-227">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="6fa1c-228">**示例**：</span><span class="sxs-lookup"><span data-stu-id="6fa1c-228">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="6fa1c-229">使用环境变量</span><span class="sxs-lookup"><span data-stu-id="6fa1c-229">Using environment variables</span></span>

<span data-ttu-id="6fa1c-230">可以在 `nuget.config` 值中使用环境变量 (NuGet 3.4 +) 在运行时应用设置。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-230">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="6fa1c-231">例如，如果 Windows 上的 `HOME` 环境变量设置为 `c:\users\username`，则配置文件中 `%HOME%\NuGetRepository` 的值解析为 `c:\users\username\NuGetRepository`。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-231">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="6fa1c-232">同样，如果 Mac/Linux 上的 `HOME` 设置为 `/home/myStuff`，则配置文件中的 `$HOME/NuGetRepository` 解析为 `/home/myStuff/NuGetRepository`。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-232">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="6fa1c-233">如果未找到环境变量，NuGet 会使用配置文件中的文本值。</span><span class="sxs-lookup"><span data-stu-id="6fa1c-233">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="6fa1c-234">示例配置文件</span><span class="sxs-lookup"><span data-stu-id="6fa1c-234">Example config file</span></span>

<span data-ttu-id="6fa1c-235">下面是示例 `nuget.config` 文件，它对一些设置进行了说明：</span><span class="sxs-lookup"><span data-stu-id="6fa1c-235">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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
