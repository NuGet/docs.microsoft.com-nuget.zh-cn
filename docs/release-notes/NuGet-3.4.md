---
title: NuGet 3.4 发行说明
description: NuGet 3.4 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776411"
---
# <a name="nuget-34-release-notes"></a>NuGet 3.4 发行说明

[NuGet 3.4-RC 发行说明](../release-notes/nuget-3.4-RC.md)  | [NuGet 3.4.1 发行说明](../release-notes/nuget-3.4.1.md)

在 Visual Studio 2015 更新2和 Visual Studio 15 预览版中，NuGet 3.4 发布了3月 30 2016 日，并使用了一些思想原则构建：

* 跨平台支持
* 性能改进
* 细微的 UI 改进

以下功能以前已添加到 RC 中，并已在3.4 版本中更新或完成：

## <a name="new-features"></a>新功能

* NuGet 客户端现在支持存储库中的 gzip 内容编码
* Xproj 项目中的包支持 Pdb
* 在 contentFiles 元素中支持 iOS 和 Android 生成操作
* 支持 netstandard 和 netstandardapp framework 名字对象

## <a name="new-user-interface-features"></a>新的用户界面功能

* 显著提高性能，尤其是在已安装、更新和合并选项卡上
* 聚合 "所有包源" 源可用于正确的搜索结果合并
* "已安装" 和 "更新" 选项卡现在按字母顺序排序
* 添加了允许刷新搜索的刷新按钮
* 版本列表顶部的最新生成选项

## <a name="updates-and-improvements"></a>更新和改进

* 在中引用 `project.json` 的包含浮动版本的包在每次生成时都不会更新。 相反，它们仅在强制还原、清理、重新生成或修改时才进行更新 `project.json` 。
* 使用 NuGet 配置 UI 时，不再将 nuget.org 存储库源强制转换为项目配置。
* NuGet 不再还原共享项目中的包，也不写入锁定文件。
* 我们已改进网络故障并重试处理，使其无法访问或响应缓慢服务器。
* 在 Visual Studio 包管理器 UI 中，键盘和鼠标的行为得到了改善。
* 现在，我们支持 DNX 中的最新 `project.json` 架构。

## <a name="breaking-changes"></a>重大更改

* 包的版本号现在规范化为格式的 *主要* 版本号。*次要*。*修补程序* -*预发行*  每个主要、次要和修补程序都被视为整数并删除任何前导零。  预发布信息被视为字符串，不会应用任何更改。 NuGet 客户端和 nuget.org 服务提供的搜索将在查询中使用这些数字。  有关更多详细信息，请参阅 [预发行版本](../create-packages/prerelease-packages.md)下的 NuGet 文档。

## <a name="known-issues"></a>已知问题

* **问题：** 在以下情况下，Windows 10 v1511 用户可能会遇到问题，甚至在 Visual Studio 中使用 Powershell 时出现 Visual Studio 崩溃：
    * 安装/卸载具有 install.ps1/uninstall.ps1 脚本的包
    * 加载具有 init.ps1 脚本的项目 (例如 EntityFramework) 
    * 发布 web 内容

* **解决方法：** 确保 Windows 10 安装已应用最新修补程序，专用 2016 (KB 3124263) 或更高版本的更新。  有关更多详细信息，请访问 [GitHub 问题 #1638](http://github.com/nuget/home/issues/1638)

* **问题：** NuGet v2 协议重定向已断开。
将请求重定向到备用主机的自定义 NuGet 存储库不接受重定向请求。
* **解决方法：**  若要解决此问题，请在 "设置" 中将包存储库 URI 配置为指向重定向的服务器位置。
有关详细信息，请参阅 [GitHub 拉取请求 #387](https://github.com/NuGet/NuGet.Client/pull/387)。

我们继续跟踪 GitHub 问题列表中的问题，可在以下位置找到： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)