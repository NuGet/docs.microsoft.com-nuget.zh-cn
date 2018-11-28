---
title: NuGet 跨平台身份验证插件
description: NuGet 的 NuGet.exe、 dotnet.exe、 msbuild.exe 和 Visual Studio 跨平台身份验证插件
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: b76fab1028ec9a4172d2390083fbf9adb4290a6c
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453502"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>NuGet 跨平台身份验证插件

在版本 4.8 +，客户端 (NuGet.exe，Visual Studio、 dotnet.exe 和 MSBuild.exe) 可使用身份验证插件构建的所有 NuGet[跨平台插件 NuGet](NuGet-Cross-Platform-Plugins.md)模型。

## <a name="authentication-in-dotnetexe"></a>Dotnet.exe 中的身份验证

Visual Studio 和 NuGet.exe 是交互式的默认情况下。 NuGet.exe 包含一个开关，它使得[非交互式](../../tools/nuget-exe-CLI-Reference.md)。
此外，NuGet.exe 和 Visual Studio 插件提示用户输入。
Dotnet.exe 中没有任何提示，默认值为非交互式。

Dotnet.exe 中的身份验证机制是设备流。 当还原或添加操作块和用户如何向完成身份验证将提供命令行的说明，以交互方式运行包操作。
当用户完成身份验证将继续操作。

若要使该操作具有交互性，一个应传递`--interactive`。
当前仅显式`dotnet restore`和`dotnet add package`命令支持交互式切换。
在没有交互式开关`dotnet build`和`dotnet publish`。

## <a name="authentication-in-msbuild"></a>在 MSBuild 中的身份验证

类似于 dotnet.exe，MSBuild.exe 默认为非交互式 MSBuild.exe 身份验证机制是设备流。
若要允许还原后，若要暂停并等待身份验证，请调用使用还原`msbuild -t:restore -p:NuGetInteractive="true"`。

## <a name="creating-a-cross-platform-authentication-plugin"></a>创建跨平台身份验证插件

示例实现可在[Microsoft 凭据提供程序插件](https://github.com/Microsoft/artifacts-credprovider)。

它是非常重要的插件，符合所提出的 NuGet 客户端工具的安全要求。
所需的最低版本为插件以进行身份验证插件*2.0.0*。
NuGet 将执行与插件和查询握手的受支持的操作声明。
跨平台插件 NuGet，请参阅[协议消息](NuGet-Cross-Platform-Plugins.md#protocol-messages-index)有关特定消息的详细信息。

NuGet 会将日志级别设置和代理服务器信息提供给插件时适用。
记录到 NuGet 控制台可接受后才 NuGet 已将日志级别设置为该插件。

- .NET framework 插件的身份验证行为

在.NET Framework 中，插件可以提示用户提供输入，在对话框的窗体中。

- .NET core 插件的身份验证行为

在.NET Core 中，不能显示一个对话框。 插件应使用设备流身份验证。
该插件可将日志消息发送到 NuGet，向用户说明。
请注意，日志记录可用后的日志级别已设置为该插件。
NuGet 不会从命令行的任何交互式输入。

当客户端调用时获得获取身份验证凭据的插件时，插件需要符合交互性开关并遵循对话框开关。 

下表总结了该插件的所有组合的行为方式。

| IsNonInteractive | CanShowDialog | 插件行为 |
| ---------------- | ------------- | --------------- |
| true | true | IsNonInteractive 开关将优先于对话框开关。 该插件不能弹出一个对话框。 此组合所适用的.NET Framework 插件 |
| true | False | IsNonInteractive 开关将优先于对话框开关。 该插件不能阻止。 这种组合时才有效.NET 核心插件 |
| False | true | 插件应显示一个对话框。 此组合所适用的.NET Framework 插件 |
| False | False | 插件应可以显示一个对话框。 插件应使用设备流的日志记录通过记录器的指令消息进行身份验证。 这种组合时才有效.NET 核心插件 |

请参阅以下规范在编写一个插件之前。

- [NuGet 包下载插件](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [跨平台身份验证插件的 NuGet](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
