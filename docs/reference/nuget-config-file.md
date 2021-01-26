---
title: nuget.config 文件引用
description: NuGet.Config 文件引用，包括配置、bindingRedirects、packageRestore、解决方案和 packageSource 节。
author: JonDouglas
ms.author: jodou
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 9b15550d0e6e8aec4d526391d77c654a756f343e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777660"
---
# <a name="nugetconfig-reference"></a>nuget.config 引用

NuGet 行为由不同或文件中的设置控制 `NuGet.Config` `nuget.config` ，如 [常见 NuGet 配置](../consume-packages/configuring-nuget-behavior.md)中所述。

`nuget.config` 是包含顶级 `<configuration>` 节点的 XML 文件，而该节点包含本主题中所述的节元素。 每节都包含零个或多个项。 请参阅[示例配置文件](#example-config-file)。 设置名称不区分大小写，并且值可以使用[环境变量](#using-environment-variables)。

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>配置节

包含可使用[ `nuget config` 命令](../reference/cli-reference/cli-ref-config.md)设置的其他配置设置。

`dependencyVersion` 和 `repositoryPath` 仅适用于使用 `packages.config` 的项目。 `globalPackagesFolder` 仅适用于使用 PackageReference 格式的项目。

| Key | 值 |
| --- | --- |
| dependencyVersion（仅限于 `packages.config`） | 包安装、还原和更新的默认 `DependencyVersion` 值（未直接指定 `-DependencyVersion` 开关时）。 NuGet 包管理器 UI 也使用此值。 值为 `Lowest`、`HighestPatch`、`HighestMinor`、`Highest`。 |
| 仅使用 PackageReference (项目的 globalPackagesFolder)  | 默认全局包文件夹的位置。 默认值为 `%userprofile%\.nuget\packages` (Windows) 或 `~/.nuget/packages` (Mac/Linux)。 相对路径可在项目特定的 `nuget.config` 文件中使用。 此设置由 NUGET_PACKAGES 环境变量重写，该变量优先。 |
| repositoryPath（仅限于 `packages.config`） | 安装 NuGet 包的位置，而非默认的 `$(Solutiondir)/packages` 文件夹。 相对路径可在项目特定的 `nuget.config` 文件中使用。 此设置由 NUGET_PACKAGES 环境变量重写，该变量优先。 |
| defaultPushSource | 如果操作未找到任何其他包源，则会标识应用作默认值的包源 URL 或路径。 |
| http_proxy http_proxy.user http_proxy.password no_proxy | 连接到包源时要使用的代理设置；`http_proxy` 应为 `http://<username>:<password>@<domain>` 格式。 密码已加密，且不能手动添加。 对于 `no_proxy`，该值是绕过代理服务器的域的列表（以逗号分隔）。 可将 http_proxy 和 no_proxy 环境变量交替用于这些值。 有关其他详细信息，请参阅 [NuGet 代理设置](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com)。 |
| signatureValidationMode | 指定用于验证包签名以便安装和还原的验证模式。 值为 `accept` 、 `require` 。 默认为 `accept`。

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

| Key | 值 |
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

| Key | 值 |
| --- | --- |
| enabled | 指示 NuGet 是否可执行自动还原的布尔。 还可以使用 `True` 的值设置 `EnableNuGetPackageRestore` 环境变量，而不是在配置文件中设置此密钥。 |
| automatic | 指示 NuGet 是否应在生成期间检查缺少的包。 |

**示例**：

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>解决方案节

控制解决方案的 `packages` 文件夹是否包括在源代码管理中。 此节仅适用于解决方案文件夹中的 `nuget.config` 文件。

| Key | 值 |
| --- | --- |
| disableSourceControlIntegration | 指示在使用源代码管理时是否忽略包文件夹的布尔。 默认值为 false。 |

**示例**：

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>包源节

`packageSources`、、 `packageSourceCredentials` 、 `apikeys` `activePackageSource` `disabledPackageSources` 和 `trustedSigners` 都一起使用，以配置在安装、还原和更新操作过程中 NuGet 如何处理包存储库。

[ `nuget sources` 命令](../reference/cli-reference/cli-ref-sources.md)通常用于管理这些设置，但 `apikeys` 使用[ `nuget setapikey` 命令](../reference/cli-reference/cli-ref-setapikey.md)管理的和 `trustedSigners` 使用[ `nuget trusted-signers` 命令](../reference/cli-reference/cli-ref-trusted-signers.md)管理的设置除外。

请注意，nuget.org 的源 URL 是 `https://api.nuget.org/v3/index.json`。

### <a name="packagesources"></a>packageSources

列出所有已知包源。 在还原操作和任何使用 PackageReference 格式的项目中，将忽略此顺序。 NuGet 遵循使用的项目进行安装和更新操作的源顺序 `packages.config` 。

| Key | 值 |
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

> [!Tip]
> 当给定节点中存在 `<clear />` 时，NuGet 将忽略之前为该节点定义的配置值。 [阅读有关如何应用设置的详细信息](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。

### <a name="packagesourcecredentials"></a>packageSourceCredentials

存储源的用户名和密码，通常通过 `nuget sources` 使用 `-username` 和 `-password` 开关指定。 默认情况下密码会进行加密，除非还使用了 `-storepasswordincleartext` 选项。
或者，可以在开关中指定有效的身份验证类型 `-validauthenticationtypes` 。

| Key | 值 |
| --- | --- |
| username | 纯文本形式的源用户名。 |
| password | 源的加密密码。 仅在 Windows 上支持加密密码，并且仅当在同一台计算机上使用加密密码时，才可以对其进行解密。 |
| cleartextpassword | 源的未加密密码。 注意：环境变量可用于提高安全性。 |
| validauthenticationtypes | 此源的有效身份验证类型的逗号分隔列表。 如果服务器公布 NTLM 或协商，并且你必须使用基本机制发送凭据（例如，在本地 Azure DevOps Server 中使用 PAT 时），则将此项设置为 `basic`。 其他有效值包括 `negotiate`、`kerberos`、`ntlm` 和 `digest`，但这些值不太可能有用。 |

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

使用环境变量中存储的未加密密码时：

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="%ContosoPassword%" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="%TestSourcePassword%" />
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

此外，还可以提供有效的身份验证方法：

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
        <add key="ValidAuthenticationTypes" value="basic" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
        <add key="ValidAuthenticationTypes" value="basic, negotiate" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a>apikeys

存储使用 API 密钥身份验证的源的密钥，使用[ `nuget setapikey` 命令](../reference/cli-reference/cli-ref-setapikey.md)进行设置。

| Key | 值 |
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

| Key | 值 |
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

| Key | 值 |
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

存储用于在安装或还原时允许包的可信签名者。 当用户将设置为时，此列表不能为空 `signatureValidationMode` `require` 。 

可以通过[ `nuget trusted-signers` 命令](../reference/cli-reference/cli-ref-trusted-signers.md)更新此部分。

**架构**：

受信任的签名者具有一个 `certificate` 项的集合，这些项将登记标识给定签名者的所有证书。 受信任的签名者可以是 `Author` 或 `Repository` 。

受信任的 *存储库* 还指定了 `serviceIndex` 存储库 (的，该存储库必须是有效的 `https` uri) 并且可以选择指定一个以分号分隔的列表， `owners` 以限制更多受此特定存储库信任的用户。

用于证书指纹的受支持的哈希算法为 `SHA256` 、 `SHA384` 和 `SHA512` 。

如果为，则在将 `certificate` `allowUntrustedRoot` `true` 证书链作为签名验证的一部分生成时，允许将指定的证书链接到不受信任的根。

**示例**：

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="fallbackpackagefolders-section"></a>fallbackPackageFolders 部分

*(3.5 +)* 提供了一种预安装包的方法，以便在回退文件夹中发现包时无需执行任何操作。 回退包文件夹与全局包文件夹具有完全相同的文件夹和文件结构： *。 nupkg* 存在，并提取所有文件。

此配置的查找逻辑为：

- 查看全局包文件夹，查看是否已下载包/版本。

- 查看后备文件夹中是否有包/版本匹配。

如果查找成功，则无需下载。

如果找不到匹配项，NuGet 将检查文件源，然后检查 http 源，然后下载包。

| Key | 值 |
| --- | --- |
| 后备文件夹 (名称)  | 回退文件夹的路径。 |

**示例**：

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a>packageManagement 部分

设置默认包管理格式， *packages.config* 或 PackageReference。 SDK 样式项目始终使用 PackageReference。

| Key | 值 |
| --- | --- |
| format | 指示默认包管理格式的布尔值。 如果 `1` 为，则格式为 PackageReference。 如果 `0` 为，则 *packages.config* 格式。 |
| disabled | 指示是否在第一次安装包时显示提示选择默认包格式的布尔值。 `False` 隐藏提示。 |

**示例**：

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a>使用环境变量

可以在 `nuget.config` 值中使用环境变量 (NuGet 3.4 +) 在运行时应用设置。

例如，如果 Windows 上的 `HOME` 环境变量设置为 `c:\users\username`，则配置文件中 `%HOME%\NuGetRepository` 的值解析为 `c:\users\username\NuGetRepository`。

请注意，必须使用 Windows 样式的环境变量 (以% ) 开头和结尾，即使在 Mac/Linux 上也是如此。 `$HOME/NuGetRepository`配置文件中的不会解析。 在 Mac/Linux 上，的值 `%HOME%/NuGetRepository` 将解析为 `/home/myStuff/NuGetRepository` 。

如果未找到环境变量，NuGet 会使用配置文件中的文本值。 例如， `%MY_UNDEFINED_VAR%/NuGetRepository` 将解析为 `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`

下表显示了环境变量语法和 NuGet.Config 文件的路径分隔符支持。

### <a name="nugetconfig-environment-variable-support"></a>NuGet.Config 环境变量支持

| 语法 | Dir 分隔符 | Windows nuget.exe | Windows dotnet.exe | Mono) 的 Mac nuget.exe ( | Mac dotnet.exe |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | 是 | 是 | 是 | 是 |
| `%MY_VAR%` | `\`  | 是 | 是 | 否 | 否 |
| `$MY_VAR` | `/`  | 否 | 否 | 否 | 否 |
| `$MY_VAR` | `\`  | 否 | 否 | 否 | 否 |


## <a name="example-config-file"></a>示例配置文件

下面是一个示例 `nuget.config` 文件，演示了一些设置，包括可选的设置：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable.
            This syntax works on Windows/Mac/Linux
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%/External" />

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
            <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
