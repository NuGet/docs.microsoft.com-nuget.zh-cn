---
title: NuGet 3.4 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 3.4 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551186"
---
# <a name="nuget-34-release-notes"></a>NuGet 3.4 发行说明

[NuGet 3.4 RC 发行说明](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 发行说明](../release-notes/nuget-3.4.1.md)

NuGet 3.4 已于 2016 年 3 月 30 日发布的 Visual Studio 2015 Update 2 和 Visual Studio 15 预览版的一部分，并且已生成具有几项基本原则在脑海中：

* 跨平台支持
* 性能改进
* 次要 UI 改进

以下功能以前在 RC 中添加和已更新或完成 3.4 版：

## <a name="new-features"></a>新增功能

* NuGet 客户端现在支持 gzip 内容编码从存储库
* 从 xproj 项目包中支持 Pdb
* 支持 iOS 和 Android 生成 contentFiles 元素中的操作
* 支持 netstandard 和 netstandardapp 框架名字对象

## <a name="new-user-interface-features"></a>新用户界面功能

* 尤其是在已安装、 更新和合并选项卡上的显著的性能改进
* 聚合的所有包源源，同时提供正确的搜索结果合并
* 安装和更新选项卡现在按字母顺序排序
* 添加允许搜索要刷新的刷新按钮
* 在版本列表顶部的最新生成选项

## <a name="updates-and-improvements"></a>更新和改进

* 中引用的包`project.json`具有浮点版本将不会更新在每次生成。 相反，它们将在其中更新仅当强制还原、 清理、 重新生成或修改时`project.json`。
* 使用 NuGet 配置 UI 时，不能再强制 nuget.org 存储库源到项目配置。
* NuGet 不能再还原在共享项目中的包，也不写入锁定文件。
* 我们改进了网络故障，然后重试处理无法访问或为响应速度缓慢的服务器。
* 键盘和鼠标行为是改进了 Visual Studio 包管理器 UI 中。
* 我们现在支持最新`project.json`DNX 中的架构。

## <a name="breaking-changes"></a>重大更改

* 包的版本号现在规范化为格式*主要*。*次要*。*修补程序*-*预发行版*每个主要版本号、 次要版本号和补丁都被视为整数并删除任何前导零。  作为字符串处理的预发布信息并向其应用任何更改。 通过 NuGet 客户端并由 nuget.org 服务提供的搜索查询中使用的这些数字。  可以在 NuGet 文档中找到更多详细信息[预发行版版本](../create-packages/prerelease-packages.md)。

## <a name="known-issues"></a>已知问题

* **问题：** Windows 10 v1511 用户可能会遇到问题或甚至在 Visual Studio 系统崩溃时 Visual Studio 中的 Powershell 在以下方案中：
    * 安装 / 卸载包具有 install.ps1 / uninstall.ps1 脚本
    * 正在加载具有 init.ps1 脚本 （如 EntityFramework) 的项目
    * 发布的 web 内容

* **解决方法：** 确保 Windows 10 安装有最新的修补程序应用、 专用 (KB 3124263) 的 2016 年 1 月或更高版本的更新。  更多详细信息位于[GitHub 问题 # 1638年](http://github.com/nuget/home/issues/1638)

* **问题：** NuGet v2 协议重定向已断开。
将请求重定向到备用主机的自定义 NuGet 存储库不接受重定向请求。
* **解决方法：** 若要解决此问题，请包存储库 URI 配置设置来重定向的服务器位置中。
有关详细信息，请参阅[GitHub 拉取请求 #387](https://github.com/NuGet/NuGet.Client/pull/387)。

我们继续来跟踪我们的 GitHub 问题中，可以在中找到的问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)