---
title: NuGet 3.0 RC2 发行说明
description: 发行说明 NuGet 3.0 RC2 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: eb8b514fa967cc6ef850483b6b2a5df3ab27a550
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819879"
---
# <a name="nuget-30-rc2-release-notes"></a>NuGet 3.0 RC2 发行说明

[NuGet 3.0 RC 发行说明](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 发行说明](../release-notes/nuget-3.0.0.md)

NuGet 3.0 RC2 于 2015 年 6 月 3 日发布为 Visual Studio 2015 扩展库中的过渡版本和[Codeplex](https://nuget.codeplex.com/releases/view/615507)。 此版本有大量的重要的 bug 修复和性能改进，我们认为重要之前已完成的 Visual Studio 2015 版本。 此 NuGet 扩展版本仅可用于 Visual Studio 2015。

我们已关闭，总共 158 问题在此版本中，并可以检查[GitHub 上的问题的完整列表](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01)。

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

下载此[更新到了 NuGet 扩展](https://nuget.codeplex.com/releases/view/615507)从 Codeplex 和请留意[我们的博客](http://blog.nuget.org)了解详细的进度和公告 NuGet 3.0 ！