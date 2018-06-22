---
title: NuGet 3.4 发行说明
description: 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 3.4 的发行说明。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f2a945b628022bdcc6e69a7a4b1be6c53b65626
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820467"
---
# <a name="nuget-34-release-notes"></a>NuGet 3.4 发行说明

[NuGet 3.4 RC 发行说明](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 发行说明](../release-notes/nuget-3.4.1.md)

NuGet 3.4 2016 年 3 月 30 日发布为 Visual Studio 2015 Update 2 和 Visual Studio 15 预览版的一部分，并且已生成与几项基本原则思想中：

* 跨平台支持
* 性能改进
* 小的 UI 改进

以下功能之前添加 RC 中和已更新或完成 3.4 版本：

## <a name="new-features"></a>新增功能

* NuGet 客户端现在支持 gzip 内容编码从存储库
* 对 Pdb 的 xproj 项目中的包的支持
* 支持 iOS 和 Android 生成在 contentFiles 元素中的操作
* 支持 netstandard 和 netstandardapp 框架名字对象

## <a name="new-user-interface-features"></a>新的用户界面功能

* 特别是在已安装、 更新和合并选项卡上的显著的性能改进
* 聚合的所有包源源可用与正确的搜索结果合并
* 安装和更新选项卡现在按字母顺序排序
* 添加允许搜索要刷新的刷新按钮
* 在版本列表顶部的最新生成选项

## <a name="updates-and-improvements"></a>更新和改进

* 包中引用`project.json`具有浮点版本将不在每次生成上更新。 相反，它们将在其中更新仅当强制还原、 清理、 重新生成，或修改`project.json`。
* 当你使用 NuGet 配置 UI，无法再强制 nuget.org 存储库源到项目配置。
* NuGet 无法再还原在共享项目中的包也不写入锁定文件。
* 我们改进了网络故障，然后重试处理无法访问或到响应速度缓慢的服务器。
* 在 Visual Studio 包管理器 UI 中改进了键盘和鼠标的行为。
* 我们现在支持最新`project.json`DNX 中的架构。

## <a name="breaking-changes"></a>重大更改

* 包版本号现在规范化为格式*主要*。*次要*。*修补程序*-*预发布*每个主版本号、 次版本、 和修补程序被视为整数并删除任何前导零。  预发布信息视为一个字符串，并向其应用任何更改。 将这些数用在查询中通过 NuGet 客户端和 nuget.org 服务提供的搜索。  在 NuGet 文档中找不到更多详细信息[预发行版本](../create-packages/prerelease-packages.md)。

## <a name="known-issues"></a>已知问题

* **问题：** Windows 10 v1511 用户可能会遇到问题或甚至在 Visual Studio 系统崩溃时 Visual Studio 中的 Powershell 在以下方案：
    * 安装 / 卸载具有 install.ps1 的包 / uninstall.ps1 脚本
    * 加载具有 （如 EntityFramework) 的 init.ps1 脚本的项目
    * 发布的 web 内容

* **解决方法：** 确保 Windows 10 安装已应用最新修补程序、 expecially 2016 年 1 月 (KB 3124263) 或更高版本的更新。  更多详细信息位于[GitHub 问题 # 1638年](http://github.com/nuget/home/issues/1638)

* **问题：** NuGet v2 协议重定向已断开。
将请求重定向到备用主机的自定义 NuGet 存储库不接受重定向请求。
* **解决方法：** 若要解决此问题，将程序包存储库 URI 在设置配置为指向重定向的服务器的位置。
有关详细信息，请参阅[GitHub 拉取请求 #387](https://github.com/NuGet/NuGet.Client/pull/387)。

我们将继续在我们的 GitHub 问题列表，可在上跟踪问题： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)