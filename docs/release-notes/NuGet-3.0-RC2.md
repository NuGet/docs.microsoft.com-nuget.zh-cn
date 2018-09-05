---
title: NuGet 3.0 RC2 发行说明
description: 发行说明 NuGet 3.0 RC2 包括已知的问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 863e48e632387b768a43530b987683605baf6db7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545816"
---
# <a name="nuget-30-rc2-release-notes"></a>NuGet 3.0 RC2 发行说明

[NuGet 3.0 RC 发行说明](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 发行说明](../release-notes/nuget-3.0.0.md)

作为临时版本可从 Visual Studio 2015 扩展库 2015 年 6 月 3 日发布 NuGet 3.0 RC2 并[Codeplex](https://nuget.codeplex.com/releases/view/615507)。 此版本中有许多重要的 bug 修复和性能改进，我们认为已重要释放之前已完成的 Visual Studio 2015 版本。 此 NuGet 扩展版本才可用于 Visual Studio 2015。

总的来说，我们已关闭的 158 问题在此版本中，并可以检查[GitHub 上的问题的完整列表](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01)。

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

下载这[更新到 NuGet 扩展](https://nuget.codeplex.com/releases/view/615507)从 Codeplex 和请密切关注[我们的博客](http://blog.nuget.org)详细进度和 NuGet 3.0 的公告 ！