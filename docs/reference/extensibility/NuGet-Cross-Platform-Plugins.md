---
title: NuGet 跨平台插件
description: Nuget、dotnet、msbuild.exe 和 Visual Studio 的 NuGet 跨平台插件
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380497"
---
# <a name="nuget-cross-platform-plugins"></a>NuGet 跨平台插件

已添加 NuGet 4.8 + 跨平台插件支持。
这是通过生成新的插件扩展性模型实现的，该模型必须符合一组严格的操作规则。
这些插件是独立的可执行文件（.NET Core world 中的 runnables），NuGet 客户端在单独的进程中启动。
这是一次真正的写入，可在任何位置运行插件。 它将适用于所有 NuGet 客户端工具。
插件可以是 .NET Framework （Nuget.exe、Msbuild.exe 和 Visual Studio），也可以是 .NET Core （dotnet）。
定义 NuGet 客户端与插件之间的版本控制通信协议。 在启动握手期间，2个进程会协商协议版本。

为了涵盖所有 NuGet 客户端工具方案，同时需要 .NET Framework 和 .NET Core 插件。
下面介绍插件的客户端/框架组合。

| 客户端工具  | 框架 |
| ------------ | --------- |
| Visual Studio | .NET Framework |
| dotnet.exe | .NET Core |
| Nuget.exe | .NET Framework |
| Msbuild.exe | .NET Framework |
| Mono 上的 Nuget.exe | .NET Framework |

## <a name="how-does-it-work"></a>工作原理

高级别工作流的描述如下所示：

1. NuGet 发现可用插件。
1. 如果适用，NuGet 将按优先级顺序循环访问插件，并逐个启动插件。
1. NuGet 将使用第一个可为请求服务的插件。
1. 插件不再需要时将关闭。

## <a name="general-plugin-requirements"></a>一般插件要求

当前协议版本为*2.0.0*。
在此版本下，要求如下所示：

- 具有有效的受信任 Authenticode 签名程序集，将在 Windows 和 Mono 上运行。 尚无对 Linux 和 Mac 上运行的程序集的特殊信任要求。 [相关问题](https://github.com/NuGet/Home/issues/6702)
- 支持在 NuGet 客户端工具的当前安全上下文下进行无状态启动。 例如，NuGet 客户端工具不会在稍后所述的插件协议之外执行提升或其他初始化。
- 除非显式指定，否则为非交互式。
- 遵循协商插件协议版本。
- 在合理的时间段内响应所有请求。
- 处理任何正在进行的操作的取消请求。

以下规范更详细地介绍了技术规范：

- [NuGet 包下载插件](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet 跨 x-plat 身份验证插件](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>客户端-插件交互

NuGet 客户端工具和插件通过标准流（stdin、stdout、stderr）与 JSON 通信。 所有数据必须采用 UTF-8 编码。
插件用参数 "-插件" 启动。 如果用户在没有此参数的情况下直接启动了插件可执行文件，则该插件可以提供信息性消息，而不是等待协议握手。
协议握手超时值为5秒。 插件应尽可能简短地在中完成设置。
NuGet 客户端工具将通过传入 NuGet 源的服务索引来查询插件支持的操作。 插件可以使用服务索引来检查是否存在受支持的服务类型。

NuGet 客户端工具与插件之间的通信是双向的。 每个请求的超时为5秒。 如果操作需要更长的时间，则应发送进度消息，以防止请求超时。1分钟处于非活动状态后，插件将被视为空闲状态并关闭。

## <a name="plugin-installation-and-discovery"></a>插件安装和发现

插件将通过基于约定的目录结构来发现。
CI/CD 方案和超级用户可以使用环境变量来重写此行为。 使用环境变量时，只允许使用绝对路径。 请注意，`NUGET_NETFX_PLUGIN_PATHS` 和 `NUGET_NETCORE_PLUGIN_PATHS` 仅适用于 5.3 + 版本的 NuGet 工具和更高版本。

- `NUGET_NETFX_PLUGIN_PATHS`-定义将由基于 .NET Framework 的工具（Nuget.exe/Msbuild.exe/Visual Studio）使用的插件。 优先于 `NUGET_PLUGIN_PATHS`。 （仅 NuGet 版本 5.3 +）
- `NUGET_NETCORE_PLUGIN_PATHS`-定义将由基于 .NET Core 的工具（dotnet）使用的插件。 优先于 `NUGET_PLUGIN_PATHS`。 （仅 NuGet 版本 5.3 +）
- `NUGET_PLUGIN_PATHS`-定义将用于 NuGet 进程的插件，保留优先级。 如果设置了此环境变量，它将覆盖基于约定的发现。 如果指定了任何一个框架特定的变量，则忽略。
-  用户-位置，`%UserProfile%/.nuget/plugins` 中的 NuGet 主页位置。 此位置不能被重写。 .NET Core 和 .NET Framework 插件将使用不同的根目录。

| 框架 | 根发现位置  |
| ------- | ------------------------ |
| .NET Core |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

每个插件都应安装在其自己的文件夹中。
插件入口点将是已安装文件夹的名称，其扩展名为 .NET Core，.exe 扩展名用于 .NET Framework。

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> 当前没有用于安装插件的用户情景。 只需将所需文件移动到预定位置即可。

## <a name="supported-operations"></a>支持的操作

新的插件协议支持两个操作。

| 操作名称 | 最低协议版本 | 最小 NuGet 客户端版本 |
| -------------- | ----------------------- | --------------------- |
| 下载包 | 1.0.0 | 4.3.0 |
| [身份验证](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>在正确的运行时下运行插件

对于 dotnet 方案中的 NuGet，插件需要能够在 dotnet 的特定运行时执行。
它在插件提供程序和使用者上，以确保使用兼容的 dotnet/插件组合。
用户位置插件可能会出现问题，例如，2.0 运行时下的 dotnet 尝试使用为2.1 运行时编写的插件。

## <a name="capabilities-caching"></a>功能缓存

插件的安全验证和实例化成本高昂。 类似于身份验证操作，下载操作的执行频率更高，但平均 NuGet 用户只可能具有身份验证插件。
为了改进体验，NuGet 将缓存给定请求的操作声明。 此缓存是每个插件，其中插件键是插件路径，此功能缓存的过期时间为30天。 

缓存位于 `%LocalAppData%/NuGet/plugins-cache` 中，并通过环境变量 `NUGET_PLUGINS_CACHE_PATH` 进行重写。 若要清除此[缓存](../../consume-packages/managing-the-global-packages-and-cache-folders.md)，可以运行带有 `plugins-cache` 选项的局部变量命令。
现在，`all` 局部变量 "选项也将删除插件缓存。 

## <a name="protocol-messages-index"></a>协议消息索引

协议版本*1.0.0*消息：

1.  关闭
    * 请求方向： NuGet > 插件
    * 请求不包含有效负载
    * 不需要响应。  适当的响应是为了使插件进程及时退出。

2.  复制包中的文件
    * 请求方向： NuGet > 插件
    * 该请求将包含：
        * 包 ID 和版本
        * 包源存储库位置
        * 目标目录路径
        * 包中要复制到目标目录路径的文件的可枚举
    * 响应将包含：
        * 指示操作结果的响应代码
        * 如果操作成功，则为目标目录中复制的文件的完整路径的可枚举

3.  复制包文件（. nupkg）
    * 请求方向： NuGet > 插件
    * 该请求将包含：
        * 包 ID 和版本
        * 包源存储库位置
        * 目标文件路径
    * 响应将包含：
        * 指示操作结果的响应代码

4.  获取凭据
    * 请求方向：插件-> NuGet
    * 该请求将包含：
        * 包源存储库位置
        * 使用当前凭据从包源存储库获取的 HTTP 状态代码
    * 响应将包含：
        * 指示操作结果的响应代码
        * 用户名（如果可用）
        * 密码（如果可用）

5.  获取包中的文件
    * 请求方向： NuGet > 插件
    * 该请求将包含：
        * 包 ID 和版本
        * 包源存储库位置
    * 响应将包含：
        * 指示操作结果的响应代码
        * 如果操作成功，则为包中的文件路径的可枚举

6.  获取操作声明 
    * 请求方向： NuGet > 插件
    * 该请求将包含：
        * 包源的服务索引 json
        * 包源存储库位置
    * 响应将包含：
        * 指示操作结果的响应代码
        * 如果操作成功，则为支持的操作（如包下载）的可枚举。  如果插件不支持包源，则该插件必须返回一组支持操作的空集。

> [!Note]
> 此消息已在版本*2.0.0*中更新。 它在客户端上，用于保留向后兼容性。

7.  获取包哈希
    * 请求方向： NuGet > 插件
    * 该请求将包含：
        * 包 ID 和版本
        * 包源存储库位置
        * 哈希算法
    * 响应将包含：
        * 指示操作结果的响应代码
        * 如果操作成功，则使用所请求的哈希算法的包文件哈希

8.  获取包版本
    * 请求方向： NuGet > 插件
    * 该请求将包含：
        * 包 ID
        * 包源存储库位置
    * 响应将包含：
        * 指示操作结果的响应代码
        * 如果操作成功，则为包版本的可枚举

9.  获取服务索引
    * 请求方向：插件-> NuGet
    * 该请求将包含：
        * 包源存储库位置
    * 响应将包含：
        * 指示操作结果的响应代码
        * 如果操作成功，则为服务索引

10.  信号
     * 请求方向： NuGet < > 插件
     * 该请求将包含：
         * 当前插件协议版本
         * 支持的最低插件协议版本
     * 响应将包含：
         * 指示操作结果的响应代码
         * 如果操作成功，则协商协议版本。  失败将导致插件终止。

11.  Initialize
     * 请求方向： NuGet > 插件
     * 该请求将包含：
         * NuGet 客户端工具版本
         * NuGet 客户端工具的有效语言。  如果使用，此操作将考虑 ForceEnglishOutput 设置。
         * 默认请求超时值，它取代协议默认值。
     * 响应将包含：
         * 指示操作结果的响应代码。  失败将导致插件终止。

12.  日志
     * 请求方向：插件-> NuGet
     * 该请求将包含：
         * 请求的日志级别
         * 要记录的消息
     * 响应将包含：
         * 指示操作结果的响应代码。

13.  监视 NuGet 进程退出
     * 请求方向： NuGet > 插件
     * 该请求将包含：
         * NuGet 进程 ID
     * 响应将包含：
         * 指示操作结果的响应代码。

14.  预提取包
     * 请求方向： NuGet > 插件
     * 该请求将包含：
         * 包 ID 和版本
         * 包源存储库位置
     * 响应将包含：
         * 指示操作结果的响应代码

15.  设置凭据
     * 请求方向： NuGet > 插件
     * 该请求将包含：
         * 包源存储库位置
         * 最后一个已知包源用户名（如果可用）
         * 最后一个已知包源密码（如果可用）
         * 最后一个已知代理用户名（如果可用）
         * 最后一个已知代理密码（如果可用）
     * 响应将包含：
         * 指示操作结果的响应代码

16.  设置日志级别
     * 请求方向： NuGet > 插件
     * 该请求将包含：
         * 默认日志级别
     * 响应将包含：
         * 指示操作结果的响应代码

协议版本*2.0.0*消息

17. 获取操作声明

* 请求方向： NuGet > 插件
    * 该请求将包含：
        * 包源的服务索引 json
        * 包源存储库位置
    * 响应将包含：
        * 指示操作结果的响应代码
        * 如果操作成功，则为支持的操作的可枚举。  如果插件不支持包源，则该插件必须返回一组支持操作的空集。

    如果服务索引和包源为 null，则该插件可以通过身份验证进行应答。

18. 获取身份验证凭据

* 请求方向： NuGet > 插件
* 该请求将包含：
    * URI
    * isRetry
    * 交互
    * CanShowDialog
* 响应将包含
    * 用户名
    * Password
    * 消息
    * 身份验证类型列表
    * MessageResponseCode
