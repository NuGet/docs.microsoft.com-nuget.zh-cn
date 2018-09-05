---
title: NuGet 3.0 发行说明
description: NuGet 3.0.0 包括的发行说明的已知问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551858"
---
# <a name="nuget-30-release-notes"></a>NuGet 3.0 发行说明

[NuGet 3.0 RC2 发行说明](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 发行说明](../release-notes/nuget-3.1.md)

NuGet 3.0 作为捆绑扩展到 Visual Studio 2015 发布于 2015 年 7 月 20 日。 我们推送来提供此版本中的使用 Visual Studio，以便完成更新后的 NuGet 3.0 体验将可用于新的 Visual Studio 用户。 此 NuGet 扩展版本才可用于 Visual Studio 2015。

我们建议有权访问不可用，因为我们要发布包含对 Windows 10 开发的支持的 Visual Studio 2015 发布更新的最新版本的 Visual Studio 库更新这些开发人员。

总的来说，我们已关闭的 240 问题在 3.0 版本中，并可以检查[GitHub 上的问题的完整列表](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)。

## <a name="known-issues"></a>已知问题

出了很多已知问题随此版本中，且所有这些项在我们计划的 3.1 版本，以便与 Windows 10 版本保持一致上年 7 月 29, 中修复。  您将能够更新你的 Visual Studio 扩展从库或之后的日期来解决这些已知的问题。

*  在预览窗口上的"不再显示此信息"标签和包描述窗口中的"作者"标签不提供翻译。
*  当你使用 TFS 处理项目源代码管理时，NuGet 不能显示包管理器用户界面如果 Nuget.Config 文件标记为只读的。
   * **解决方法**签出该文件从 TFS。
*  使用 Visual Studio 深色主题时，黄色 NuGet Powershell 窗口中的"重新启动栏"中的文本不可见。
   * **解决方法**使用 Visual Studio 浅色主题。


## <a name="summary-of-top-issues-resolved"></a>已解决的热门问题的摘要

* [刷新包管理器窗口时将调用频繁网络更新](https://github.com/NuGet/Home/issues/515)
* [更改为安装在包管理器中的视图时，延迟滚动](https://github.com/NuGet/Home/issues/519)
* [网络调用应在后台线程上运行](https://github.com/NuGet/Home/issues/516)
* [添加了不显示预览窗口复选框](https://github.com/NuGet/Home/issues/566)
* [添加了的过程限制以减少处理器使用情况](https://github.com/NuGet/Home/issues/356)
* 改进的可移植类库参考处理
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [记忆式键入功能服务是区分大小写](https://github.com/NuGet/Home/issues/198)
* [更新重新引入基本身份验证凭据](https://github.com/NuGet/Home/issues/456)
* [改进的错误日志记录](https://github.com/NuGet/Home/issues/407)
* [改进了的 powershell 调用更新包时的错误消息](https://github.com/NuGet/Home/issues/5)
* [修复了了解有关选项的信息链接，以防止在 Windows 10 上崩溃，](https://github.com/NuGet/Home/issues/822)
* [请记住预发行版复选框设置](https://github.com/NuGet/Home/issues/732)
* [改进了的收集性能的方式跨解决方案中的项目缓存结果](https://github.com/NuGet/Home/issues/721)
* [可以并行收集多个包](https://github.com/NuGet/Home/issues/713)
* [删除安装包的强制命令](https://github.com/NuGet/Home/issues/697)

请密切关注[我们的博客](http://blog.nuget.org)的更多进度和公告如我们准备好提供对 Windows 10 开发的支持。