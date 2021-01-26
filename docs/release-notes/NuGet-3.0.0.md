---
title: NuGet 3.0 发行说明
description: NuGet 3.0.0 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776553"
---
# <a name="nuget-30-release-notes"></a>NuGet 3.0 发行说明

[NuGet 3.0 RC2 发行说明](../release-notes/nuget-3.0-RC2.md)  | [NuGet 3.1 发行说明](../release-notes/nuget-3.1.md)

NuGet 3.0 于年7月20日发布2015，作为 Visual Studio 2015 的捆绑扩展。 我们已推出 Visual Studio 提供此版本，以使新的 Visual Studio 用户可以使用完整的更新 NuGet 3.0 体验。 此 NuGet 扩展版本仅适用于 Visual Studio 2015。

我们建议那些有权访问 Visual Studio 库的开发人员更新到可用的最新版本，因为我们将在 Visual Studio 2015 版本中发布更新，该版本包含对 Windows 10 开发的支持。

在3.0 发行版中，我们已解决了240问题，你可以在 [GitHub 上查看问题的完整列表](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)。

## <a name="known-issues"></a>已知问题

此发行版中提供了许多已知问题，所有这些项目都在我们的计划3.1 版本中得到修复，与7月29日发布的 Windows 10 一致。  你可以从或之后的库中更新你的 Visual Studio 扩展，以解决这些已知问题。

*  对于 "预览" 窗口中的 "不再显示此项" 标签和 "包说明" 窗口中的 "作者" 标签，不提供翻译。
*  使用 TFS 源代码管理处理项目时，如果 Nuget.Config 文件标记为只读，NuGet 将无法显示包管理器用户界面。
   * **解决方法** 从 TFS 签出文件。
*  使用 Visual Studio 深色主题时，NuGet Powershell 窗口中的黄色 "重新启动栏" 中的文本将不可见。
   * **解决方法** 使用 Visual Studio 浅色主题。


## <a name="summary-of-top-issues-resolved"></a>解决的首要问题摘要

* [当程序包管理器窗口刷新时频繁进行网络更新调用](https://github.com/NuGet/Home/issues/515)
* [更改为包管理器中已安装的视图时的延迟滚动](https://github.com/NuGet/Home/issues/519)
* [应在后台线程上运行网络调用](https://github.com/NuGet/Home/issues/516)
* [添加了 "不显示预览窗口" 复选框](https://github.com/NuGet/Home/issues/566)
* [添加了进程限制以减少处理器使用率](https://github.com/NuGet/Home/issues/356)
* 改进的可移植类库引用处理
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [自动完成服务区分大小写](https://github.com/NuGet/Home/issues/198)
* [用于重新引入基本身份验证凭据的更新](https://github.com/NuGet/Home/issues/456)
* [改进了错误日志记录](https://github.com/NuGet/Home/issues/407)
* [在调用更新包时改进了 powershell 错误消息](https://github.com/NuGet/Home/issues/5)
* [修复了 "了解选项" 链接以防止在 Windows 10 上崩溃](https://github.com/NuGet/Home/issues/822)
* [记住预发布复选框设置](https://github.com/NuGet/Home/issues/732)
* [通过跨解决方案中的项目缓存结果提高了收集性能](https://github.com/NuGet/Home/issues/721)
* [可以并行收集多个包](https://github.com/NuGet/Home/issues/713)
* [已删除安装包-force 命令](https://github.com/NuGet/Home/issues/697)

请关注 [我们的博客](http://blog.nuget.org) ，了解更多进度和公告，因为我们已准备好为 Windows 10 开发提供支持。