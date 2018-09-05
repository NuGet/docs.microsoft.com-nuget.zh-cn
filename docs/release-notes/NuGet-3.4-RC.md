---
title: NuGet 3.4 RC 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 3.4 RC 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546749"
---
# <a name="nuget-34-rc-release-notes"></a>NuGet 3.4 RC 发行说明

[NuGet 3.3 发行说明](../release-notes/nuget-3.3.md) | [NuGet 3.4 发行说明](../release-notes/nuget-3.4.md)

NuGet 3.4 RC 已发布于 2016 年 3 月 3 日与 Visual Studio 2015 Update 2 RC 一起，并且已生成具有几项基本原则在脑海中：

* 跨平台支持
* 性能改进
* 次要 UI 改进

以下功能都在此 RC 中，提供了计划 3.4 的最终版本的详细信息。

## <a name="new-features"></a>新增功能

* NuGet 客户端现在支持 gzip 内容编码从存储库
* 从 xproj 项目包中支持 Pdb
* 支持 iOS 和 Android 生成 contentFiles 元素中的操作
* 支持 netstandard 和 netstandardapp 框架名字对象

## <a name="new-user-interface-features"></a>新用户界面功能

* 尤其是在已安装、 更新和合并选项卡上的显著的性能改进
* 安装和更新选项卡现在按字母顺序排序
* 添加允许搜索要刷新的刷新按钮

## <a name="updates-and-improvements"></a>更新和改进

* 中引用的包`project.json`具有浮点版本将不会更新在每次生成。 相反，它们将在其中更新仅当强制还原、 清理、 重新生成或修改时`project.json`。
* 使用 NuGet 配置 UI 时，不能再强制 nuget.org 存储库源到项目配置。
* NuGet 不能再还原在共享项目中的包，也不写入锁定文件。
* 我们改进了网络故障，然后重试处理无法访问或为响应速度缓慢的服务器。
* 键盘和鼠标行为是改进了 Visual Studio 包管理器 UI 中。
* 我们现在支持最新`project.json`DNX 中的架构。

## <a name="known-issues"></a>已知问题

我们继续来跟踪我们的 GitHub 问题中，可以在中找到的问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)