---
title: NuGet 3.4-RC 发行说明
description: NuGet 3.4 RC 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780237"
---
# <a name="nuget-34-rc-release-notes"></a>NuGet 3.4-RC 发行说明

[NuGet 3.3 发行说明](../release-notes/nuget-3.3.md)  | [NuGet 3.4 发行说明](../release-notes/nuget-3.4.md)

NuGet 3.4-RC 于3月3日发布2016，与 Visual Studio 2015 Update 2 RC 一起发布，并且是使用一些思维原则构建的：

* 跨平台支持
* 性能改进
* 细微的 UI 改进

此 RC 中提供了以下功能，并对3.4 最终版本进行了更多规划。

## <a name="new-features"></a>新功能

* NuGet 客户端现在支持存储库中的 gzip 内容编码
* Xproj 项目中的包支持 Pdb
* 在 contentFiles 元素中支持 iOS 和 Android 生成操作
* 支持 netstandard 和 netstandardapp framework 名字对象

## <a name="new-user-interface-features"></a>新的用户界面功能

* 显著提高性能，尤其是在已安装、更新和合并选项卡上
* "已安装" 和 "更新" 选项卡现在按字母顺序排序
* 添加了允许刷新搜索的刷新按钮

## <a name="updates-and-improvements"></a>更新和改进

* 在中引用 `project.json` 的包含浮动版本的包在每次生成时都不会更新。 相反，它们仅在强制还原、清理、重新生成或修改时才进行更新 `project.json` 。
* 使用 NuGet 配置 UI 时，不再将 nuget.org 存储库源强制转换为项目配置。
* NuGet 不再还原共享项目中的包，也不写入锁定文件。
* 我们已改进网络故障并重试处理，使其无法访问或响应缓慢服务器。
* 在 Visual Studio 包管理器 UI 中，键盘和鼠标的行为得到了改善。
* 现在，我们支持 DNX 中的最新 `project.json` 架构。

## <a name="known-issues"></a>已知问题

我们继续跟踪 GitHub 问题列表中的问题，可在以下位置找到： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)