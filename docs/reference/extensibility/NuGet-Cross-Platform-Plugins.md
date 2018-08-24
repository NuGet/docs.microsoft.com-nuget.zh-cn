---
title: 跨平台插件的 NuGet
description: NuGet 的 NuGet.exe、 dotnet.exe、 msbuild.exe 和 Visual Studio 跨平台插件
author: nkolev92
ms.author: nikolev
manager: rrelyea
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: cf2c4fb484703b034a8569d053f2417fe58e41ff
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794166"
---
# <a name="nuget-cross-platform-plugins"></a>跨平台插件的 NuGet

在 NuGet 4.8 + 中添加了对跨平台插件的支持。
这是通过生成新的插件可扩展性模型，必须符合一组严格的规则的操作的使用来实现。
插件是自包含的可执行文件 （可运行对象在.NET Core 世界中），NuGet 客户端在一个单独的进程中启动。
这是 true 一次编写，随处运行插件。 它会使用所有 NuGet 客户端工具。
插件可以是.NET Framework （NuGet.exe、 MSBuild.exe 和 Visual Studio） 或.NET Core (dotnet.exe)。
NuGet 客户端和插件之间的版本控制的通信协议定义。 启动握手期间 2 进程协商的协议版本。

要覆盖所有 NuGet 客户端工具方案，其中一个需要.NET Framework 和.NET 核心插件。
下面介绍了插件的客户端/框架组合。

| 客户端工具  | 框架 |
| ------------ | --------- |
| Visual Studio | .NET Framework |
| dotnet.exe | .NET Core |
| NuGet.exe | .NET Framework |
| MSBuild.exe | .NET Framework |
| Mono 上的 NuGet.exe | .NET Framework |

## <a name="how-does-it-work"></a>它是如何工作的

高级工作流如下所述：

1. NuGet 发现可用插件。
1. 如果适用，NuGet 将循环访问的优先级顺序并开始逐个进行中的插件。
1. NuGet 将使用第一个插件，可以处理该请求。
1. 在不再需要时，将关闭插件。

## <a name="general-plugin-requirements"></a>常规插件要求

当前的协议版本是*2.0.0*。
在此版本中，要求如下所示：

- 具有有效的、 受信任的验证码签名程序集将在 Windows 和 Mono 上运行。 没有任何特殊信任要求尚未运行 Linux 和 Mac 上的程序集。 [相关的问题](https://github.com/NuGet/Home/issues/6702)
- 支持的 NuGet 客户端工具的当前安全上下文的无状态启动。 例如，NuGet 客户端工具将执行提升或更高版本所述的插件协议之外的其他初始化。
- 除非显式指定，则为非交互式。
- 遵守协商的插件协议版本。
- 在合理时间段内响应的所有请求。
- 接受任何正在进行中操作的取消请求。

技术规范都进行了以下规范中的更多详细信息：

- [NuGet 包下载插件](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [跨平台身份验证插件的 NuGet](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>客户端-插件交互

NuGet 客户端工具和插件通过进行通信使用 JSON 标准流 （stdin、 stdout、 stderr）。 所有数据必须都是 utf-8 编码。
插件启动具有参数"的插件"。 如果用户直接启动可执行文件而不使用此参数的插件，该插件可以提供信息性消息而不是等待协议握手。
协议握手超时值为 5 秒。 插件应完成作为缺乏尽可能的金额中设置。
NuGet 客户端工具将通过传入的 NuGet 源的服务索引查询插件的支持的操作。 插件可能使用的服务索引检查支持的服务类型存在。

NuGet 客户端工具和插件之间的通信是双向的。 每个请求已超时设置为 5 秒。 如果需要更长时间操作都认为各自的进程应发送进度消息以防止请求超时。处于非活动状态的 1 分钟之后插件被视为空闲和关闭的情况下。

## <a name="plugin-installation-and-discovery"></a>插件安装和发现

插件会发现通过基于约定的目录结构。
CI/CD 方案和高级用户可以使用环境变量重写的行为。

- `NUGET_PLUGIN_PATHS` -定义将用于该 NuGet 过程中，保留的优先级的插件。 如果设置此环境变量，它将替代约定，其发现。
-  用户位置、 中的 NuGet 主页位置`%UserProfile%/.nuget/plugins`。 此位置不能重写。 不同的根目录将用于.NET Core 和.NET Framework 的插件。

| 框架 | 根发现位置  |
| ------- | ------------------------ |
| .NET Core |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

应在其自己的文件夹中安装的每个插件。
插件的入口点将是使用.NET Core 的.dll 扩展和.exe 适用于.NET Framework 的扩展的安装文件夹的名称。

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
> 目前存在的插件安装没有用户情景。 它是将所需的文件移动到预先确定的位置一样简单。

## <a name="supported-operations"></a>支持的操作

在新的插件协议下支持两个操作。

| 操作名称 | 最低协议版本 | 最低 NuGet 客户端版本 |
| -------------- | ----------------------- | --------------------- |
| 下载包 | 1.0.0 | 4.3.0 |
| [身份验证](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>运行插件下正确运行时

适用于 NuGet dotnet.exe 方案中，插件需要能够执行的 dotnet.exe 该特定运行时。
它是插件提供商和使用者，以确保兼容 dotnet.exe/plugin 结合使用。
使用用户位置插件时例如时出现潜在问题，dotnet.exe 下 2.0 运行时尝试使用针对 2.1 运行时编写的插件。

## <a name="capabilities-caching"></a>缓存的功能

安全验证和实例化的插件是代价高昂。 但是一般 NuGet 用户才可能具有一个身份验证插件，下载操作比身份验证操作，更频繁地发生。
若要改进的体验，NuGet 将缓存给定请求的操作声明。 此缓存是每个插件使用的插件路径中，插件键，此功能缓存的到期时间为 30 天。 

缓存位于`%LocalAppData%/NuGet/plugins-cache`和环境变量替代`NUGET_PLUGINS_CACHE_PATH`。 若要清除这[缓存](../../consume-packages/managing-the-global-packages-and-cache-folders.md)，其中一个可以运行局部变量命令和`plugins-cache`选项。
`all`局部变量选项也会立即删除插件缓存。 

## <a name="protocol-messages-index"></a>协议消息索引

协议版本*1.0.0*消息：

1.  关闭
    * 请求方向： NuGet-> 插件
    * 该请求将包含无有效负载
    * 预期无响应。  正确的响应是插件进程立即退出。

2.  将包中复制文件
    * 请求方向： NuGet-> 插件
    * 该请求将包含：
        * 包 ID 和版本
        * 包源存储库位置
        * 目标目录路径
        * 可枚举的包复制到目标目录路径中的文件
    * 响应将包含：
        * 指示操作结果的响应代码
        * 如果操作成功的目标目录中复制文件的完整路径的可枚举值

3.  将包文件 (.nupkg) 复制
    * 请求方向： NuGet-> 插件
    * 该请求将包含：
        * 包 ID 和版本
        * 包源存储库位置
        * 目标文件路径
    * 响应将包含：
        * 指示操作结果的响应代码

4.  获取凭据
    * 请求方向： 插件-> NuGet
    * 该请求将包含：
        * 包源存储库位置
        * 从包源存储库使用当前凭据获取 HTTP 状态代码
    * 响应将包含：
        * 指示操作结果的响应代码
        * 用户名，如果可用
        * 密码，如果可用

5.  获取包中的文件
    * 请求方向： NuGet-> 插件
    * 该请求将包含：
        * 包 ID 和版本
        * 包源存储库位置
    * 响应将包含：
        * 指示操作结果的响应代码
        * 如果操作已成功在包中的文件路径的可枚举值

6.  获取操作声明 
    * 请求方向： NuGet-> 插件
    * 该请求将包含：
        * 包源服务 index.json
        * 包源存储库位置
    * 响应将包含：
        * 指示操作结果的响应代码
        * 可枚举的支持的操作 (例如： 包下载) 如果操作成功。  如果提供的插件不支持包源，该插件必须返回空集支持的操作。

> [!Note]
> 此消息已更新版本中*2.0.0*。 它是在客户端可以保持向后兼容性。

7.  获取包哈希
    * 请求方向： NuGet-> 插件
    * 该请求将包含：
        * 包 ID 和版本
        * 包源存储库位置
        * 哈希算法
    * 响应将包含：
        * 指示操作结果的响应代码
        * 包文件哈希使用请求的哈希算法，如果操作成功

8.  获取包的版本
    * 请求方向： NuGet-> 插件
    * 该请求将包含：
        * 包 ID
        * 包源存储库位置
    * 响应将包含：
        * 指示操作结果的响应代码
        * 可枚举的包版本，如果操作成功

9.  获取服务索引
    * 请求方向： 插件-> NuGet
    * 该请求将包含：
        * 包源存储库位置
    * 响应将包含：
        * 指示操作结果的响应代码
        * 服务索引，如果操作成功

10.  握手
     * 请求方向： NuGet <>-插件
     * 该请求将包含：
         * 当前的插件协议版本
         * 支持的最低插件协议版本
     * 响应将包含：
         * 指示操作结果的响应代码
         * 如果操作成功协商的协议的版本。  失败将导致终止的插件。

11.  初始化
     * 请求方向： NuGet-> 插件
     * 该请求将包含：
         * NuGet 客户端工具版本
         * NuGet 客户端工具有效语言。  这将考虑 ForceEnglishOutput 设置中，如果使用。
         * 默认请求超时，取代了协议的默认值。
     * 响应将包含：
         * 指示操作结果的响应代码。  失败将导致终止的插件。

12.  日志
     * 请求方向： 插件-> NuGet
     * 该请求将包含：
         * 请求日志级别
         * 要记录的消息
     * 响应将包含：
         * 指示操作结果的响应代码。

13.  监视 NuGet 进程退出
     * 请求方向： NuGet-> 插件
     * 该请求将包含：
         * NuGet 进程 ID
     * 响应将包含：
         * 指示操作结果的响应代码。

14.  预提取的包
     * 请求方向： NuGet-> 插件
     * 该请求将包含：
         * 包 ID 和版本
         * 包源存储库位置
     * 响应将包含：
         * 指示操作结果的响应代码

15.  设置凭据
     * 请求方向： NuGet-> 插件
     * 该请求将包含：
         * 包源存储库位置
         * 最后一个已知的包源用户名，如果可用
         * 最后一个已知的包源密码，如果可用
         * 最后一个已知的代理用户名，如果可用
         * 最后一个已知的代理密码，如果可用
     * 响应将包含：
         * 指示操作结果的响应代码

16.  将日志级别设置
     * 请求方向： NuGet-> 插件
     * 该请求将包含：
         * 默认日志级别
     * 响应将包含：
         * 指示操作结果的响应代码

协议版本*2.0.0*消息

17. 获取操作声明

* 请求方向： NuGet-> 插件
    * 该请求将包含：
        * 包源服务 index.json
        * 包源存储库位置
    * 响应将包含：
        * 指示操作结果的响应代码
        * 可枚举的支持的操作如果操作成功。  如果提供的插件不支持包源，该插件必须返回空集支持的操作。

    如果服务索引和包源为 null，则该插件可以回答与身份验证。

18. 获取身份验证凭据

* 请求方向： NuGet-> 插件
* 该请求将包含：
    * URI
    * isRetry
    * NonInteractive
    * CanShowDialog
* 响应将包含
    * 用户名
    * Password
    * 消息
    * 身份验证类型的列表
    * MessageResponseCode