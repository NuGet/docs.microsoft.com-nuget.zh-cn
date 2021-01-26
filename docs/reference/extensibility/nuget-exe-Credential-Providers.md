---
title: nuget.exe 凭据提供程序
description: nuget.exe 凭据提供程序使用源进行身份验证，并以遵循特定约定的命令行可执行文件的形式实现。
author: JonDouglas
ms.author: jodou
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 285504508fa88c96f5c7a23f15ef14d81ebc21e1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777767"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>通过 nuget.exe 凭据提供程序对源进行身份验证

在中， `3.3` 为特定的 `nuget.exe` 凭据提供程序添加了版本支持。 从那时起，在版本支持中， `4.8` 对于在所有命令行方案间工作的 [凭据提供程序](NuGet-Cross-Platform-Authentication-Plugin.md) ， (`nuget.exe` 、 `dotnet.exe` `msbuild.exe`) 已添加。

有关的所有身份验证方法的详细信息，请参阅[使用经过身份验证的源中的包](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe)`nuget.exe`

## <a name="nugetexe-credential-provider-discovery"></a>nuget.exe 凭据提供程序发现

nuget.exe 凭据提供程序可通过3种方式使用：

- **全局**：若要使凭据提供程序可用于 `nuget.exe` 在当前用户的配置文件下运行的所有实例，请将其添加到中 `%LocalAppData%\NuGet\CredentialProviders` 。 可能需要创建该 `CredentialProviders` 文件夹。 凭据提供程序可以安装在文件夹的根目录 `CredentialProviders`  或子文件夹中。 如果凭据提供程序具有多个文件/程序集，则可以使用子文件夹来保持提供程序的组织。

- **从环境变量中**：凭据提供程序可以存储在任何位置，并可 `nuget.exe` 通过将 `%NUGET_CREDENTIALPROVIDERS_PATH%` 环境变量设置为提供程序位置进行访问。 此变量可以是以分号分隔的列表 (例如， `path1;path2`) 如果有多个位置，则为。

- 与 **nuget.exe**： nuget.exe 凭据提供程序可以放在与相同的文件夹中 `nuget.exe` 。

加载凭据提供程序时， `nuget.exe` 会按顺序搜索上述位置，对于名为的任何文件 `credentialprovider*.exe` ，然后按找到的顺序加载这些文件。 如果同一文件夹中存在多个凭据提供程序，则按字母顺序加载它们。

## <a name="creating-a-nugetexe-credential-provider"></a>创建 nuget.exe 凭据提供程序

凭据提供程序是一个命令行可执行文件，以形式命名， `CredentialProvider*.exe` 用于收集输入，根据需要获取凭据，然后返回相应的退出状态代码和标准输出。

提供程序必须执行以下操作：

- 确定是否可以在启动凭据获取之前为目标 URI 提供凭据。 如果不是，则它应返回无凭据的状态代码1。
- 不修改 `Nuget.Config` (如在) 设置凭据。
- 自行处理 HTTP 代理配置，因为 NuGet 不向插件提供代理信息。
- `nuget.exe`使用 utf-8 编码，通过编写 JSON 响应对象将凭据或错误详细信息返回到， (参见下面) 到 stdout。
- （可选）向 stderr 发出附加跟踪日志记录。 不应将任何机密写入到 stderr，因为在详细级别 "正常" 或 "详细" 时，此类跟踪会回显到控制台。
- 应忽略意外参数，以提供与 NuGet 的未来版本的向前兼容性。

### <a name="input-parameters"></a>输入参数

| 参数/开关 |说明|
|----------------|-----------|
| Uri {value} | 需要凭据的包源 URI。|
| NonInteractive | 如果存在，则提供程序不会发出交互式提示。 |
| IsRetry | 如果存在，则指示此尝试将重试先前失败的尝试。 提供程序通常使用此标志来确保它们绕过任何现有缓存，并在可能的情况下提示输入新凭据。|
| 详细程度 {值} | 如果存在，则为以下值之一： "normal"、"quiet" 或 "详细"。 如果未提供任何值，则默认为 "normal"。 提供程序应使用此选项来指示要发出到标准错误流的可选日志记录级别。 |

### <a name="exit-codes"></a>退出代码

| 代码 |结果 | 说明 |
|----------------|-----------|-----------|
| 0 | 成功 | 已成功获取凭据并已将其写入 stdout。|
| 1 | ProviderNotApplicable | 当前提供程序不提供给定 URI 的凭据。|
| 2 | 失败 | 提供程序是给定 URI 的正确提供程序，但不能提供凭据。 在这种情况下，nuget.exe 将不会重试身份验证，并且会失败。 典型的示例是用户取消交互式登录时。 |

### <a name="standard-output"></a>标准输出

| 属性 |注释|
|----------------|-----------|
| 用户名 | 经过身份验证的请求的用户名。|
| Password | 经过身份验证的请求的密码。|
| 消息 | 有关响应的可选详细信息，仅用于显示故障情况下的其他详细信息。 |

示例 stdout：

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a>凭据提供程序故障排除

目前，NuGet 并不能直接支持调试自定义凭据提供程序; [问题 4598](https://github.com/NuGet/Home/issues/4598) 正在跟踪此工作。

你还可以执行以下操作：

- 运行带开关的 nuget.exe `-verbosity` 以检查详细的输出。
- 将调试消息添加到 `stdout` 适当位置。
- 请确保使用 nuget.exe 3.3 或更高版本。
- 在启动时将调试器附加到以下代码片段：

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
