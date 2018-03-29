---
title: NuGet 3.0 发行说明 |Microsoft 文档
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 发行说明，了解 NuGet 3.0.0 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。
keywords: NuGet 3.0.0 发行说明，bug 修复的已知问题，添加了一些功能，DCRs
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: fc669e4a8440c295f08eef461186eef5f505df42
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-30-release-notes"></a>NuGet 3.0 发行说明

[NuGet 3.0 RC2 发行说明](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 发行说明](../release-notes/nuget-3.1.md)

NuGet 3.0 于 2015 年 7 月 20 日发布为 Visual Studio 2015 的捆绑扩展。 我们推送以提供使用 Visual Studio 的此版本，以便完成更新的 NuGet 3.0 体验将可用于新的 Visual Studio 用户。 此 NuGet 扩展版本仅可用于 Visual Studio 2015。

我们建议这些开发人员有权访问不可用，因为我们要包含适用于 Windows 10 开发支持的 Visual Studio 2015 的发布后，将很快发布更新的最新版本的 Visual Studio 库更新。

我们已关闭，总共 240 问题在 3.0 版本中，并可以检查[GitHub 上的问题的完整列表](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)。

## <a name="known-issues"></a>已知问题

有大量的时候附带此版本的已知问题，我们计划的 3.1 版本，以便在年 7 月 29 上保持一致随着 Windows 10 的发布中修复所有这些项。  你就能够更新你从库该日期以解决这些已知的问题或之后的 Visual Studio 扩展。

*  在预览窗口上的"不再显示此对话框"标签和包描述窗口中的"作者"标签不提供转换。
*  当你通过使用 TFS 处理项目源代码管理时，NuGet 不能显示包管理器用户界面如果 Nuget.Config 文件标记为只读的。
   * **解决方法**签出该文件从 TFS。
*  当你使用 Visual Studio 深色主题时，黄色 NuGet Powershell 窗口中的"重新启动栏"中的文本不可见。
   * **解决方法**使用 Visual Studio 浅色主题。


## <a name="summary-of-top-issues-resolved"></a>已解决的最主要问题的摘要

* [包管理器窗口刷新一次时，将调用频繁网络更新](https://github.com/NuGet/Home/issues/515)
* [将更改为安装在程序包管理器中的视图时延迟滚动](https://github.com/NuGet/Home/issues/519)
* [应在后台线程上运行网络调用](https://github.com/NuGet/Home/issues/516)
* [添加不显示预览窗口复选框](https://github.com/NuGet/Home/issues/566)
* [添加的进程限制以减少处理器使用率](https://github.com/NuGet/Home/issues/356)
* 改进了可移植类库引用处理
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [记忆式键入功能服务不区分大小写](https://github.com/NuGet/Home/issues/198)
* [更新，以重新引入基本身份验证凭据](https://github.com/NuGet/Home/issues/456)
* [改进的错误日志记录](https://github.com/NuGet/Home/issues/407)
* [改进了的 powershell 调用更新包时的错误消息](https://github.com/NuGet/Home/issues/5)
* [固定的了解有关选项的信息链接，以防止在 Windows 10 上发生故障](https://github.com/NuGet/Home/issues/822)
* [请记住预发行版复选框设置](https://github.com/NuGet/Home/issues/732)
* [通过跨解决方案中的项目中缓存结果的改进的收集性能](https://github.com/NuGet/Home/issues/721)
* [可以并行收集多个包](https://github.com/NuGet/Home/issues/713)
* [删除安装包的强制命令](https://github.com/NuGet/Home/issues/697)

请留意[我们的博客](http://blog.nuget.org)了解详细的进度和公告如我们准备好为 Windows 10 开发提供支持。