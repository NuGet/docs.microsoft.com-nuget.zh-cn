---
title: "nuget.exe 凭据提供程序 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "nuget.exe 凭据提供程序将具有源，身份验证，并实现为遵循特定的约定的命令行可执行文件。"
keywords: "nuget.exe 凭据提供程序，凭据提供程序 API，将具有源进行身份验证，使用库进行身份验证"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88ce0106ad4e628ba8120f94b7951c7746ab67f3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>进行身份验证与 nuget.exe 凭据提供程序的源

*NuGet 3.3 +*

当`nuget.exe`需要凭据进行身份验证将具有源，则查找它们按以下方式：

1. NuGet 首先查找中的凭据`Nuget.Config`文件。
1. NuGet 然后使用插件的凭据提供程序，根据下面列出的顺序。 (和示例是[Visual Studio Team Services 凭据提供程序](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider)。)
1. NuGet 然后会提示用户提供命令行上的凭据。

请注意，此处所述的凭据提供程序仅在工作`nuget.exe`，不能在 dotnet 还原或 Visual Studio。 有关通过 Visual Studio 使用的凭据提供程序，请参阅[nuget.exe for Visual Studio 的凭据提供程序](nuget-credential-providers-for-visual-studio.md)

nuget.exe 凭据提供程序可以采用下列 3 种方法：

- **全局**： 要提供给所有实例的凭据提供程序`nuget.exe`运行在当前用户的配置文件下，将其添加到`%LocalAppData%\NuGet\CredentialProviders`。 你可能需要创建`CredentialProviders`文件夹。 凭据提供程序可以安装的根目录`CredentialProviders`文件夹或子文件夹内。 如果凭据提供程序具有多个文件/程序集，你可以使用子文件夹需要组织的提供程序。

- **从环境变量**： 凭据提供程序可以存储任何位置，可以访问`nuget.exe`通过设置`%NUGET_CREDENTIALPROVIDERS_PATH%`到提供程序位置的环境变量。 此变量可以是以分号分隔的列表 (例如， `path1;path2`) 如果你有多个位置。

- **与 nuget.exe 一起**: nuget.exe 凭据提供程序可以与同一文件夹中放置`nuget.exe`。

在加载凭据提供程序时`nuget.exe`顺序情况下，名为任何文件将搜索上面的位置， `credentialprovider*.exe`，然后加载这些文件要找到它们的顺序。 如果在同一文件夹中存在多个凭据提供程序，它们按字母顺序加载。

## <a name="creating-a-nugetexe-credential-provider"></a>创建 nuget.exe 凭据提供程序

凭据提供程序是一个命令行可执行文件，在窗体中名为`CredentialProvider*.exe`，收集输入、 获取视情况而定的凭据，然后返回相应的退出状态代码和标准输出。

一个提供程序必须执行以下操作：

- 确定是否可以在启动凭据获取之前目标 uri 提供凭据。 如果没有，则应返回状态代码没有凭据的 1。
- 不修改`Nuget.Config`（如存在设置凭据）。
- 它本身，作为 NuGet 上的句柄 HTTP 代理配置不提供到该插件的代理信息。
- 返回凭据或错误详细信息，以便`nuget.exe`通过向 stdout，使用 utf-8 编码写入 JSON 响应对象 （见下文）。
- （可选） 发出到 stderr 的其他跟踪日志记录。 由于详细程度级别"normal"或"详细"在此类跟踪将回显 nuget 到控制台，则不断应到 stderr，不编写任何密钥。
- 应忽略意外的参数，提供与将来版本的 NuGet 的向前兼容性。

### <a name="input-parameters"></a>输入的参数

| 参数/开关 |描述|
|----------------|-----------|
| Uri {value} | 包源 URI 需要凭据。|
| NonInteractive | 如果存在，则提供程序不会颁发交互式提示。 |
| IsRetry | 如果存在，则表明此尝试是以前失败的尝试的重试。 提供程序通常使用此标志，以确保它们绕过任何现有的缓存，并尽可能提示输入新凭据。|
| 详细级别 {value} | 如果存在，以下值之一:"正常"、"静默"详细"。 如果没有提供值时，默认为"normal"。 提供程序应使用此的可选日志记录级别用于指示写入标准错误流发出。 |

### <a name="exit-codes"></a>退出代码

| 代码 |结果 | 描述 |
|----------------|-----------|-----------|
| 0 | 成功 | 凭据已成功获取和已写入到 stdout。|
| 1 | ProviderNotApplicable | 当前提供程序不提供有关给定 URI 的凭据。|
| 2 | 失败 | 提供程序是正确的提供程序的给定的 URI，但不能提供凭据。 在这种情况下，nuget.exe 不会重试身份验证，并且将失败。 一个典型示例是当用户取消交互式登录。 |

### <a name="standard-output"></a>标准输出

| 属性 |说明|
|----------------|-----------|
| 用户名 | 对于验证的请求的用户名。|
| Password | 经过身份验证请求密码。|
| 消息 | 有关响应，仅用于在故障情况下显示更多细节的可选详细信息。 |

示例 stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>故障排除凭据提供程序

目前，NuGet 不提供多直接支持针对调试自定义凭据提供程序;[发出 4598](https://github.com/NuGet/Home/issues/4598)跟踪此工作。

你还可以执行以下操作：

- 运行与 nuget.exe`-verbosity`开关来检查详细的输出。
- 添加到调试消息`stdout`在适当的位置。
- 请确保你使用的 nuget.exe 3.3 或更高版本。
- 附加调试器在启动时，此代码片段：

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

有关进一步的帮助，[提交支持请求 nuget.org](https://www.nuget.org/policies/Contact)。
