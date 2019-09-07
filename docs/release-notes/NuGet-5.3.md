---
title: NuGet 5.3 发行说明
description: NuGet 5.3 的发行说明，包括新功能、bug 修复和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: f16bfe5481009f7924a61f03233d288d25ac618f
ms.sourcegitcommit: f4bfdbf62302c95f1f39e81ccf998f8bbc6d56b0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2019
ms.locfileid: "70774085"
---
# <a name="nuget-53-release-notes"></a>NuGet 5.3 发行说明

NuGet 分发车辆：

| NuGet 版本 | 适用于 Visual Studio 版本| 适用于 .NET SDK|
|:---|:---|:---|
| [**5.3.0-preview3**](https://nuget.org/downloads) | [Visual Studio 2019 版本16.3 预览版3](https://visualstudio.microsoft.com/vs/preview/) | [3.0.100-preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup> |

<sup>1</sup>随 Visual Studio 2019 with .NET Core 工作负载一起安装

## <a name="summary-whats-new-in-53-preview-3"></a>摘要:5.3 preview 3 中的新增功能

* [包图标可以嵌入到包中](../reference/msbuild-targets.md#packing-an-icon-image-file)，而无需使用外部 URL。 - [#352](https://github.com/NuGet/Home/issues/352)

* 提高了对包的 SHA 跟踪和强制执行的安全性- [#7281](https://github.com/NuGet/Home/issues/7281)

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

**Bug**

* VS：程序集是完全 ngen-ed，而不是部分 ngen- [#8513](https://github.com/NuGet/Home/issues/8513)

* 减少内存使用量（取消订阅事件）- [#8471](https://github.com/NuGet/Home/issues/8471)

* "Error_UnableToFindProjectInfo" 消息的语法不正确- [#8441](https://github.com/NuGet/Home/issues/8441)

* NU1403 改进-验证所有包，包括预期/实际 sha 值- [#8424](https://github.com/NuGet/Home/issues/8424)

* NuGetPackageManager. PreviewUpdatePackagesAsync 中的多个枚举- [#8401](https://github.com/NuGet/Home/issues/8401)

* 恢复 Pluginprocess.exe 中的 "公共 > 内部" 更改- [#8390](https://github.com/NuGet/Home/issues/8390)

* IVsPackageSourceProvider. GetSources （...）的异常行为定义错误- [#8383](https://github.com/NuGet/Home/issues/8383)

* 使 PluginManager 构造函数再次公开- [#8379](https://github.com/NuGet/Home/issues/8379)

* 用于跟踪 PM UI 的刷新速率的指标- [#8369](https://github.com/NuGet/Home/issues/8369)

* 通过包管理器 UI 安装时减少 UI 刷新的次数- [#8358](https://github.com/NuGet/Home/issues/8358)

* 遥测： datetime 值使用特定于区域性的格式- [#8351](https://github.com/NuGet/Home/issues/8351)

* 减少包管理器 UI 的浏览选项卡中的 UI 刷新 #6570- [#8339](https://github.com/NuGet/Home/issues/8339)

* [测试失败]"无法解析配置文件" 将提示两次[#8320](https://github.com/NuGet/Home/issues/8320)

* 向说明客户修补程序的良好文档页引发 NU5037 错误（包缺少所需的 nuspec 文件）- [#8291](https://github.com/NuGet/Home/issues/8291)

* 更改项目的 Runtimeidentifiers 时，锁定模式还原失败- [#8260](https://github.com/NuGet/Home/issues/8260)

* 在 VS 懒惰[#8156](https://github.com/NuGet/Home/issues/8156)中进行设置读取

* "Nuget 源添加" 中的回归导致 "：" 字符（十六进制值0x3A）不能包含在名称 "errors- [#7948](https://github.com/NuGet/Home/issues/7948)

* NuGet 插件凭据提供程序-隐藏进程窗口- [#7511](https://github.com/NuGet/Home/issues/7511)

* 强制 PackagePathResolver 是绝对路径[#7349](https://github.com/NuGet/Home/issues/7349)

* 减少安装和更新包管理器 UI 的选项卡中的 UI 刷新- [#6570](https://github.com/NuGet/Home/issues/6570)

**DCR：**

* 更新 Xamarin framework 以映射到 NetStandard 2.1- [#8368](https://github.com/NuGet/Home/issues/8368)

* 为安装/更新[#8324](https://github.com/NuGet/Home/issues/8324)启用包管理器 "预览窗口" 的内容复制

* 对 proj 文件启用还原- [#8212](https://github.com/NuGet/Home/issues/8212)

* 同时`NUGET_NETFX_PLUGIN_PATHS`引入`NUGET_NETCORE_PLUGIN_PATHS`和，同时支持[#8151](https://github.com/NuGet/Home/issues/8151)的配置

* 通过版本属性为 PackageDownload 启用多个版本- [#8074](https://github.com/NuGet/Home/issues/8074)

* 将-SolutionDirectory 和-PackageDirectory 选项添加到 nuget.exe 包- [#7163](https://github.com/NuGet/Home/issues/7163)

* 使 NuGet 包具有确定性[#6229](https://github.com/NuGet/Home/issues/6229)

**[此版本中已解决的所有问题的列表-5.3 预览版3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**
