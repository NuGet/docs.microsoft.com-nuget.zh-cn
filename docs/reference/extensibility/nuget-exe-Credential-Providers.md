---
title: nuget.exe 凭据提供程序
description: nuget.exe 凭据提供程序进行身份验证的源，并实现为遵循特定的约定的命令行可执行文件。
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 97a44c6d561f426fa50fa068a9bbf793f77a3111
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550184"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Nuget.exe 凭据提供程序使用的身份验证源

*NuGet 3.3 +*

当`nuget.exe`需要凭据进行身份验证使用源，它会查找它们按以下方式：

1. NuGet 会首先查看凭据中`Nuget.Config`文件。
1. 然后，NuGet 使用插件凭据提供程序，根据下面给出的顺序。 (示例中， [Visual Studio Team Services 凭据提供程序](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider)。)
1. 然后，NuGet 会提示用户输入凭据在命令行上。

请注意，此处所述的凭据提供程序仅在工作`nuget.exe`而不是在 dotnet restore 或 Visual Studio。 使用 Visual Studio 的凭据提供程序，请参阅[nuget.exe 凭据提供程序的 Visual Studio](nuget-credential-providers-for-visual-studio.md)

nuget.exe 凭据提供程序可以以三种方式使用：

- **全局**： 若要使凭据提供程序可用的所有实例`nuget.exe`运行当前用户的配置文件下，将其添加到`%LocalAppData%\NuGet\CredentialProviders`。 可能需要创建`CredentialProviders`文件夹。 凭据提供程序可以安装的根目录`CredentialProviders`文件夹或子文件夹中。 如果凭据提供程序具有多个文件/程序集，可以使用子文件夹以保持组织的提供程序。

- **从环境变量**： 凭据提供程序可以存储的任何位置，并可向`nuget.exe`通过设置`%NUGET_CREDENTIALPROVIDERS_PATH%`到提供程序位置的环境变量。 此变量可以是以分号分隔列表 (例如， `path1;path2`) 如果有多个位置。

- **Nuget.exe 旁边**: nuget.exe 凭据提供程序可以与同一文件夹中放置`nuget.exe`。

加载凭据提供程序时`nuget.exe`名为任何文件以便将搜索上面位置、 `credentialprovider*.exe`，然后加载这些文件在发现的顺序。 如果在同一文件夹中存在多个凭据提供程序，它们按字母顺序加载。

## <a name="creating-a-nugetexe-credential-provider"></a>创建一个 nuget.exe 凭据提供程序

凭据提供程序是一个命令行可执行文件，在窗体中名为`CredentialProvider*.exe`，收集输入、 获取凭据根据需要，，然后返回相应的退出状态代码和标准输出。

一个提供程序必须执行以下操作：

- 确定是否它可提供凭据的目标 URI 启动凭据获取之前。 如果没有，它应返回状态代码为没有凭据的 1。
- 不修改`Nuget.Config`（如那里设置凭据）。
- 在其自身的、 作为 NuGet 上的句柄 HTTP 代理配置不提供到该插件的代理信息。
- 返回凭据或错误详细信息到`nuget.exe`通过写入到 stdout，使用 utf-8 编码的 JSON 响应对象 （见下文）。
- 选择性地将发出附加的跟踪日志记录到 stderr。 由于详细程度级别"normal"或"详细"在此类跟踪将回显 nuget 到控制台，任何机密应不断将不写入到 stderr。
- 应忽略意外的参数，提供与未来版本的 NuGet 的向前兼容性。

### <a name="input-parameters"></a>输入的参数

| 参数/切换 |描述|
|----------------|-----------|
| Uri {value} | 包源 URI 需要凭据。|
| NonInteractive | 如果存在，则提供程序不会发出交互式提示。 |
| IsRetry | 如果存在，则指示此尝试进行尝试之前失败的重试。 提供程序通常使用此标志，以确保它们绕过任何现有的缓存，如有可能提示输入新凭据。|
| 详细级别 {value} | 如果存在，以下值之一:"正常"、"quiet"详细"。 如果不提供任何值，默认为"normal"。 提供程序应将它用作表示的可选日志记录级别发出到标准错误流。 |

### <a name="exit-codes"></a>退出代码

| 代码 |结果 | 描述 |
|----------------|-----------|-----------|
| 0 | 成功 | 凭据成功获取和已写入到 stdout。|
| 1 | ProviderNotApplicable | 当前提供程序不提供有关给定 URI 的凭据。|
| 2 | 失败 | 提供程序是正确的访问接口对于给定的 URI，但不能提供凭据。 在这种情况下，nuget.exe 不会重试身份验证，并且将失败。 典型示例是当用户取消交互式登录。 |

### <a name="standard-output"></a>标准输出

| 属性 |说明|
|----------------|-----------|
| 用户名 | 对于经过身份验证请求的用户名。|
| Password | 经过身份验证请求的密码。|
| 消息 | 有关响应，仅用于在故障情况下显示的其他详细信息的可选详细信息。 |

示例 stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>凭据提供程序进行故障排除

目前，NuGet 不会提供更直接的支持的调试自定义凭据提供程序;[发出 4598](https://github.com/NuGet/Home/issues/4598)跟踪这项工作。

你还可以执行以下操作：

- 运行使用 nuget.exe`-verbosity`开关可以检查详细的输出。
- 添加到调试消息`stdout`中相应的位置。
- 请确保使用 nuget.exe 3.3 或更高版本。
- 附加调试程序在启动时使用此代码片段：

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

获取更多帮助[提交支持请求 nuget.org](https://www.nuget.org/policies/Contact)。
