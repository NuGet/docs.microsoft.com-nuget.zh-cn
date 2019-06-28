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
# <a name="nugetconfig-reference"></a>nuget.config 引用

通过在不同的设置控制 NuGet 行为`NuGet.Config`文件中所述[常见 NuGet 配置](../consume-packages/configuring-nuget-behavior.md)。

`nuget.config` 是包含顶级 `<configuration>` 节点的 XML 文件，而该节点包含本主题中所述的节元素。 每个部分包含零个或多个项。 请参阅[示例配置文件](#example-config-file)。 设置名称不区分大小写，并且值可以使用[环境变量](#using-environment-variables)。

本主题内容：

- [配置节](#config-section)
- [bindingRedirects 节](#bindingredirects-section)
- [packageRestore 节](#packagerestore-section)
- [解决方案节](#solution-section)
- [包源节](#package-source-sections)：
  - [packageSources](#packagesources)
  - [packageSourceCredentials](#packagesourcecredentials)
  - [apikeys](#apikeys)
  - [disabledPackageSources](#disabledpackagesources)
  - [activePackageSource](#activepackagesource)
- [trustedSigners 部分](#trustedsigners-section)
- [使用环境变量](#using-environment-variables)
- [示例配置文件](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>配置节

包含杂项配置设置，可使用 [`nuget config` 命令](../tools/cli-ref-config.md)设置。

`dependencyVersion` 并`repositoryPath`仅适用于使用的项目`packages.config`。 `globalPackagesFolder` 仅适用于使用 PackageReference 格式的项目。

| 键 | 值 |
| --- | --- |
| dependencyVersion（仅限于 `packages.config`） | 包安装、还原和更新的默认 `DependencyVersion` 值（未直接指定 `-DependencyVersion` 开关时）。 NuGet 包管理器 UI 也使用此值。 值为 `Lowest`、`HighestPatch`、`HighestMinor`、`Highest`。 |
| globalPackagesFolder （仅限使用 PackageReference 的项目） | 默认全局包文件夹的位置。 默认值为 `%userprofile%\.nuget\packages` (Windows) 或 `~/.nuget/packages` (Mac/Linux)。 相对路径可在项目特定的 `nuget.config` 文件中使用。 由 nuget_packages 重写环境变量优先替代此设置。 |
| repositoryPath（仅限于 `packages.config`） | 安装 NuGet 包的位置，而非默认的 `$(Solutiondir)/packages` 文件夹。 相对路径可在项目特定的 `nuget.config` 文件中使用。 由 nuget_packages 重写环境变量优先替代此设置。 |
| defaultPushSource | 如果操作未找到任何其他包源，则会标识应用作默认值的包源 URL 或路径。 |
| http_proxy http_proxy.user http_proxy.password no_proxy | 连接到包源时要使用的代理设置；`http_proxy` 应为 `http://<username>:<password>@<domain>` 格式。 密码已加密，且不能手动添加。 对于 `no_proxy`，该值是绕过代理服务器的域的列表（以逗号分隔）。 可将 http_proxy 和 no_proxy 环境变量交替用于这些值。 有关其他详细信息，请参阅 [NuGet 代理设置](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com)。 |
| signatureValidationMode | 指定用来验证包安装的包签名和还原的验证模式。 值为`accept`， `require`。 默认为 `accept`。

**示例**：

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a>bindingRedirects 节

在安装包时，配置 NuGet 是否执行自动绑定重定向。

| 键 | 值 |
| --- | --- |
| skip | 指示是否跳过自动绑定重定向的布尔。 默认值为 false。 |

**示例**：

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>packageRestore 节

在生成期间控制包还原。

| 键 | 值 |
| --- | --- |
| enabled | 指示 NuGet 是否可执行自动还原的布尔。 还可以使用 `True` 的值设置 `EnableNuGetPackageRestore` 环境变量，而不是在配置文件中设置此密钥。 |
| 自动 | 指示 NuGet 是否应在生成期间检查缺少的包。 |

**示例**：

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>解决方案节

控制解决方案的 `packages` 文件夹是否包括在源代码管理中。 此节仅适用于解决方案文件夹中的 `nuget.config` 文件。

| 键 | 值 |
| --- | --- |
| disableSourceControlIntegration | 指示在使用源代码管理时是否忽略包文件夹的布尔。 默认值为 False。 |

**示例**：

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>包源节

`packageSources`， `packageSourceCredentials`， `apikeys`， `activePackageSource`，`disabledPackageSources`和`trustedSigners`一起协作来配置 NuGet 在安装、 还原和更新操作过程中如何使用包存储库的所有工作。

[ `nuget sources`命令](../tools/cli-ref-sources.md)通常用于管理这些设置，除`apikeys`使用管理[`nuget setapikey`命令](../tools/cli-ref-setapikey.md)，和`trustedSigners`它托管使用[`nuget trusted-signers`命令](../tools/cli-ref-trusted-signers.md)。

请注意，nuget.org 的源 URL 是 `https://api.nuget.org/v3/index.json`。

### <a name="packagesources"></a>packageSources

列出所有已知包源。 在还原操作期间，与任何项目使用 PackageReference 格式，被忽略的顺序。 NuGet 会遵守安装源的顺序和项目使用与更新操作`packages.config`。

| 键 | 值 |
| --- | --- |
| （要分配给包源的名称） | 包源的路径或 URL。 |

**示例**：

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a>packageSourceCredentials

存储源的用户名和密码，通常通过 `nuget sources` 使用 `-username` 和 `-password` 开关指定。 默认情况下密码会进行加密，除非还使用了 `-storepasswordincleartext` 选项。

| 键 | 值 |
| --- | --- |
| username | 纯文本形式的源用户名。 |
| 密码 | 源的加密密码。 |
| cleartextpassword | 源的未加密密码。 |

**示例：**

在配置文件中，`<packageSourceCredentials>` 元素包含每个适用源名称的子节点（名称中的空格被替换为 `_x0020_`）。 也就是说，对于名为“Contoso”和“测试源”的源，使用加密密码时，配置文件包含以下内容：

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

使用未加密密码时：

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

### <a name="apikeys"></a>apikeys

存储使用 API 密钥身份验证的源的密钥，如使用 [`nuget setapikey` 命令](../tools/cli-ref-setapikey.md) 设置。

| 键 | 值 |
| --- | --- |
| （源 URL） | 加密的 API 密钥。 |

**示例**：

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a>disabledPackageSources

标识当前已禁用的源。 可能为空。

| 键 | 值 |
| --- | --- |
| （源名称） | 指示源是否禁用的布尔。 |

**示例：**

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a>activePackageSource

*（仅限于 2.x；3.x+ 中已弃用）*

标识到当前活动的源或指示所有源的聚合。

| 键 | 值 |
| --- | --- |
| （源名称）或 `All` | 如果密钥是源的名称，则值为源路径或 URL。 如果为 `All`，值应为 `(Aggregate source)`，从而组合其他未禁用的所有包源。 |

**示例**：

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a>trustedSigners 部分

存储受信任的签名者用于允许同时安装或还原包。 当用户设置时，此列表不能为空`signatureValidationMode`到`require`。 

本部分中可以使用更新[`nuget trusted-signers`命令](../tools/cli-ref-trusted-signers.md)。

**架构**:

受信任的签名者具有一系列`certificate`登记标识给定签名者的所有证书的项。 受信任的签名者可以是`Author`或`Repository`。

受信任*存储库*还指定了`serviceIndex`存储库 (这必须是有效`https`uri) 和 （可选） 可以指定以分号分隔的列表`owners`限制更多谁是受信任从该特定存储库。

用于证书指纹的受支持的哈希算法`SHA256`，`SHA384`和`SHA512`。

如果`certificate`指定`allowUntrustedRoot`作为`true`给定的证书生成的签名验证一部分的证书链时允许链接到不受信任的根。

**示例**：

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

## <a name="using-environment-variables"></a>使用环境变量

可以在 `nuget.config` 值中使用环境变量 (NuGet 3.4 +) 在运行时应用设置。

例如，如果 Windows 上的 `HOME` 环境变量设置为 `c:\users\username`，则配置文件中 `%HOME%\NuGetRepository` 的值解析为 `c:\users\username\NuGetRepository`。

同样，如果 Mac/Linux 上的 `HOME` 设置为 `/home/myStuff`，则配置文件中的 `%HOME%/NuGetRepository` 解析为 `/home/myStuff/NuGetRepository`。

如果未找到环境变量，NuGet 会使用配置文件中的文本值。

## <a name="example-config-file"></a>示例配置文件

下面是示例 `nuget.config` 文件，它对一些设置进行了说明：

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
