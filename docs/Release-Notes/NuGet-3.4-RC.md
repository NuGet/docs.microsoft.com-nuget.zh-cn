---
title: NuGet 3.4 RC 发行说明
description: 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 3.4 RC 的发行说明。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e40d685a5256fdfee818f0cc1f1bc352c698f3c2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-34-rc-release-notes"></a>NuGet 3.4 RC 发行说明

[NuGet 3.3 发行说明](../release-notes/nuget-3.3.md) | [NuGet 3.4 发行说明](../release-notes/nuget-3.4.md)

NuGet 3.4 RC 2016 年 3 月 3 日与 Visual Studio 2015 Update 2 RC 一起发布，并且用几原则思想的生成：

* 跨平台支持
* 性能改进
* 小的 UI 改进

下列功能是此 RC 中提供了更多计划 3.4 的最终版本。

## <a name="new-features"></a>新增功能

* NuGet 客户端现在支持 gzip 内容编码从存储库
* 对 Pdb 的 xproj 项目中的包的支持
* 支持 iOS 和 Android 生成在 contentFiles 元素中的操作
* 支持 netstandard 和 netstandardapp 框架名字对象

## <a name="new-user-interface-features"></a>新的用户界面功能

* 特别是在已安装、 更新和合并选项卡上的显著的性能改进
* 安装和更新选项卡现在按字母顺序排序
* 添加允许搜索要刷新的刷新按钮

## <a name="updates-and-improvements"></a>更新和改进

* 包中引用`project.json`具有浮点版本将不在每次生成上更新。 相反，它们将在其中更新仅当强制还原、 清理、 重新生成，或修改`project.json`。
* 当你使用 NuGet 配置 UI，无法再强制 nuget.org 存储库源到项目配置。
* NuGet 无法再还原在共享项目中的包也不写入锁定文件。
* 我们改进了网络故障，然后重试处理无法访问或到响应速度缓慢的服务器。
* 在 Visual Studio 包管理器 UI 中改进了键盘和鼠标的行为。
* 我们现在支持最新`project.json`DNX 中的架构。

## <a name="known-issues"></a>已知问题

我们将继续在我们的 GitHub 问题列表，可在上跟踪问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)