---
title: "NuGet 4.6 RTM 发行说明 | Microsoft Docs"
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 3/7/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 4.6.0 的发行说明，包括已知问题、bug 修复、新增功能和 DCR。"
keywords: "NuGet 4.6.0 发行说明, bug 修复, 已知问题, 新增功能, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 32bfe8a7d5d60a0ad24444749beff64edcaab305
ms.sourcegitcommit: fa31ae10b5a5add7184bf7420554aade8adce6ed
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2018
---
# <a name="nuget-46-rtm-release-notes"></a>NuGet 4.6 RTM 发行说明

[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 附带 [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe)。

## <a name="summary-whats-new-in-this-release"></a>摘要：此版本中的新增功能
* 添加了对[给包签名](https://docs.microsoft.com/en-us/nuget/create-packages/sign-a-package)的支持。  
* Visual Studio 2017 和 nuget.exe 现将在安装包、为[已签名包](https://docs.microsoft.com/en-us/nuget/reference/signed-packages-reference)还原包之前，验证包的完整性。
* 改进了连续还原的性能。

## <a name="known-issues"></a>已知问题
### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>使用 .NET Framework 和 NuGet 的 .NET Standard 2.0 的问题 

.NET Standard 及其工具旨在使面向 .NET Framework 4.6.1 的项目可使用面向 .NET Standard 2.0 或更早版本的 NuGet 包和项目。 [本文档](https://github.com/dotnet/standard/issues/481)总结了该方案相关问题、解决问题的计划以及可使用当前工具状态部署的变通方法。

## <a name="top-issues-fixed-in-this-release"></a>此版本中已修复的主要问题

**性能修复**
* 没有更改时，无法写入资产文件 - [#6491](https://github.com/NuGet/Home/issues/6491)
* 当子项目的 TFM 与父项目的 TFM 不匹配时，还原会导致额外的 MSBuild 计算 - [#6311](https://github.com/NuGet/Home/issues/6311)
* 通过优化依赖项关系图创建规范来提高 NoOp 还原性能 - [#6252](https://github.com/NuGet/Home/issues/6252)

**Bug**
* 推送到本地文件夹导致 nupkg 锁定 - [#6325](https://github.com/NuGet/Home/issues/6325)
* NuGet 插件实现：多个问题 - [#6149](https://github.com/NuGet/Home/issues/6149)
* UIHang - 从 VSSolutionManager 的 MEF 初始化中删除查询服务调用 - [#6110](https://github.com/NuGet/Home/issues/6110)
* 错误报告已取消的包下载任务发生异常 - [#6096](https://github.com/NuGet/Home/issues/6096)
* NuGet.exe 在程序集名称中用“%2B”替换“+”- [#5956](https://github.com/NuGet/Home/issues/5956)
* Fn+F1 无法转到 PM UI 和控制台的正确帮助页面 - [#5912](https://github.com/NuGet/Home/issues/5912)
* VS NuGet 在特定情况下会将绝对路径写入项目文件 - [#5888](https://github.com/NuGet/Home/issues/5888)
* 修复 4.3 回归 - 无法通过转换在内容文件中替换占位符 $product$ 和 $AssemblyGuid$ - [#5880](https://github.com/NuGet/Home/issues/5880)
* dotnet 还原出现多个源故障 - [#5817](https://github.com/NuGet/Home/issues/5817)
* 包应重新评估项目版本以允许 git 版本控制 - [#4790](https://github.com/NuGet/Home/issues/4790)
* 改善在安装不兼容包时出现的难以理解的错误 - [#4555](https://github.com/NuGet/Home/issues/4555)
* TemplateWizard 需要将包安装为 PackageReferences 的选项 - [#4549](https://github.com/NuGet/Home/issues/4549)
* 从开发人员命令提示符以外运行 MSBuild.exe 时，包传递的属性文件被忽略 - [#4530](https://github.com/NuGet/Home/issues/4530)
* 修复在引用不适用于项目的 .NET Standard 库时出现的不当错误消息 - [#4423](https://github.com/NuGet/Home/issues/4423)
* dotnet add package 无法为面向可移植配置文件的包提供指导 - [#4349](https://github.com/NuGet/Home/issues/4349)
* dotnet 包 - ProjectReference 缺少版本后缀 - [#4337](https://github.com/NuGet/Home/issues/4337)
* 有关 .NET Core 模板的生成错误和 VS 崩溃 - [#3973](https://github.com/NuGet/Home/issues/3973)
* 无法加载源 https:* 的服务索引 - [#3681](https://github.com/NuGet/Home/issues/3681)
* nuget.exe list -allversions 无法正常工作 - [#3441](https://github.com/NuGet/Home/issues/3441)
* 误导性的依赖项解析错误信息 - [#2984](https://github.com/NuGet/Home/issues/2984)
* nuget.exe 还原不会为 .msbuildproj 生成 .props 和 .targets 文件（在 v3.3.0-3.4.4 升级中回归） - [#2921](https://github.com/NuGet/Home/issues/2921)
* 更新打开了 XAML 文件的 NuGet 包时出现 UI 延迟 - [#2878](https://github.com/NuGet/Home/issues/2878)
* 来自 IIS 的 WebSite 项目失败，路径中包含非法字符 - [#2798](https://github.com/NuGet/Home/issues/2798)
* Nuget 添加在 CentOS 上挂起 - [#2708](https://github.com/NuGet/Home/issues/2708)
* 使用 packagesavemode -nupkg 还原 json.net 失败 - [#2706](https://github.com/NuGet/Home/issues/2706)
* 包管理器筛选器在 vs 输出窗口中不可用于还原命令 - [#2704](https://github.com/NuGet/Home/issues/2704)


[此版本中所有已修复问题的列表](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
