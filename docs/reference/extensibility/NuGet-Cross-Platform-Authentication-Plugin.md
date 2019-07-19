---
title: NuGet 跨平台身份验证插件
description: Nuget、dotnet、msbuild.exe 和 Visual Studio 的 NuGet 跨平台身份验证插件
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: a716737343ea826d28da6de46c32ca73aef590bd
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317283"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>NuGet 跨平台身份验证插件

在版本 4.8 + 中, 所有 NuGet 客户端 (Nuget.exe、Visual Studio、dotnet 和 Msbuild.exe) 都可以使用在[NuGet 跨平台插件](NuGet-Cross-Platform-Plugins.md)模型之上构建的身份验证插件。

## <a name="authentication-in-dotnetexe"></a>Dotnet 中的身份验证

默认情况下, Visual Studio 和 Nuget.exe 是交互式的。 Nuget.exe 包含用于使其成为[非交互式](../nuget-exe-CLI-Reference.md)的开关。
此外, Nuget.exe 和 Visual Studio 插件会提示用户输入。
在 dotnet 中没有提示, 默认值为非交互式。

Dotnet 中的身份验证机制是设备流。 如果 "还原" 或 "添加包" 操作以交互方式运行, 则在命令行上将会阻止操作并向用户提供如何完成身份验证的说明。
用户完成身份验证后, 操作将继续。

若要使操作具有交互性, 应通过`--interactive`一个。
目前只有显式`dotnet restore`和`dotnet add package`命令支持交互式切换。
`dotnet build` 和`dotnet publish`上没有交互式开关。

## <a name="authentication-in-msbuild"></a>MSBuild 中的身份验证

与 dotnet 类似, Msbuild.exe 默认情况下不交互, msbuild.exe 身份验证机制是设备流。
若要允许还原暂停并等待身份验证, 请调用 restore with `msbuild -t:restore -p:NuGetInteractive="true"`。

## <a name="creating-a-cross-platform-authentication-plugin"></a>创建跨平台身份验证插件

可以在[Microsoft 凭据提供程序插件](https://github.com/Microsoft/artifacts-credprovider)中找到示例实现。

插件必须符合 NuGet 客户端工具所规定的安全要求, 这一点非常重要。
作为身份验证插件的插件所需的最低版本为*2.0.0*。
NuGet 将通过插件执行握手, 并查询支持的操作声明。
有关特定消息的详细信息, 请参阅 NuGet 跨平台插件[协议消息](NuGet-Cross-Platform-Plugins.md#protocol-messages-index)。

NuGet 会将日志级别设置为 "可用", 并向该插件提供代理信息。
仅在 NuGet 将日志级别设置为插件后, 才可以接受日志记录到 NuGet 控制台。

- .NET Framework 插件身份验证行为

在 .NET Framework 中, 允许插件以对话框的形式提示用户输入。

- .NET Core 插件身份验证行为

在 .NET Core 中, 无法显示对话框。 插件应该使用设备流进行身份验证。
该插件可以向 NuGet 发送日志消息, 并向用户发送说明。
请注意, 在日志级别设置为插件后, 日志记录可用。
NuGet 不会从命令行获取任何交互式输入。

当客户端使用获取身份验证凭据调用插件时, 插件需要符合交互交换机, 并遵循对话开关。 

下表总结了插件对于所有组合的行为方式。

| IsNonInteractive | CanShowDialog | 插件行为 |
| ---------------- | ------------- | --------------- |
| true | true | IsNonInteractive 开关优先于对话框开关。 不允许插件弹出对话框。 此组合仅对 .NET Framework 插件有效 |
| true | False | IsNonInteractive 开关优先于对话框开关。 不允许插件阻止。 此组合仅适用于 .NET Core 插件 |
| False | true | 插件应该会显示一个对话框。 此组合仅对 .NET Framework 插件有效 |
| False | False | 插件应/不能显示对话框。 该插件应该使用设备流通过日志记录指令消息进行身份验证。 此组合仅适用于 .NET Core 插件 |

请参阅以下规范, 然后再编写插件。

- [NuGet 包下载插件](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet 跨 x-plat 身份验证插件](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
