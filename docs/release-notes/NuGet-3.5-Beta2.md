---
title: 3.5 Beta2 发行说明
description: NuGet 3.5 Beta 2 发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776397"
---
# <a name="nuget-35-beta2-release-notes"></a>NuGet 3.5 Beta2 发行说明

[NuGet 3.5-测试版发行说明](../release-notes/nuget-3.5-Beta.md)  | [NuGet 3.5-RC 发行说明](../release-notes/nuget-3.5-RC.md)

NuGet 3.5 Beta 2 RTM 于6月 27 2016 日发布，适用于 Visual Studio 2013 和 nuget.exe

[完整 Changelog](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[问题列表](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Bug 修复

* 更新了错误消息，导致在 .NET Core 中缺少对密码 decrpytion 的支持，以进行身份验证的源- [#2942](https://github.com/NuGet/Home/issues/2942)

* 如果 .NET Core 项目是打开的，则程序包管理器控制台 Get-Package 失败- [#2932](https://github.com/NuGet/Home/issues/2932)

* 修复 NuGet push 命令[#2910](https://github.com/NuGet/Home/issues/2910)中403的错误处理错误

* 修复在将 disableSourceControlIntegration 设置为 true 时在绑定到 TFS 源代码管理的解决方案中卸载包时出现的问题 [#2739](https://github.com/NuGet/Home/issues/2739)

* 修复包更新以考虑非目标包- [#2724](https://github.com/NuGet/Home/issues/2724)

* 使用 MSBuild 详细级别为 Nuget 包管理器 UI 操作设置记录器级别- [#2705](https://github.com/NuGet/Home/issues/2705)

* 修复 NuGet 配置在网站项目中无效错误-VS 2015 VSIX (v 3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* 修复包 `.csproj` 在包含内容文件时的问题- [#2658](https://github.com/NuGet/Home/issues/2658)

* `NuGetDefaults.Config` () 中 `ProgramData\NuGet` 的 DefaultPushSource 不起作用- [#2653](https://github.com/NuGet/Home/issues/2653)

* 在创建包时，Nuget 3.4.3 中的修复问题-值不能为 null- [#2648](https://github.com/NuGet/Home/issues/2648)

* Restore 使用存储的凭据从 Nuget.Config 获取 VSTS 源- [#2647](https://github.com/NuGet/Home/issues/2647)

* 性能-修复版本 comparsion 中过度分配的代码- [#2632](https://github.com/NuGet/Home/issues/2632)

* 修复 nuget.exe 的多个实例尝试并行安装同一包时出现的问题 [#2628](https://github.com/NuGet/Home/issues/2628)

* 针对多项目操作的性能缓存依赖关系信息- [#2619](https://github.com/NuGet/Home/issues/2619)

* 修复了源列表为空时无法从设置中添加包源的问题- [#2617](https://github.com/NuGet/Home/issues/2617)

* 解决在尝试安装依赖于设计时外观的包时出现的误导性错误 [#2594](https://github.com/NuGet/Home/issues/2594)

* 通过设置为 "All" 的 PackageManager 控制台安装包仅尝试第一次源 [#2557](https://github.com/NuGet/Home/issues/2557)

* 修复包的问题，这些包的文件在将来有写入时间 (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)

* 当在 update 命令中查找项目失败时显示异常- [#2418](https://github.com/NuGet/Home/issues/2418)

* 当包包含文件时，使用参数-NoCache 从 nuget v 3.3 + 源安装包时，包内容无法正确还原 `.nupkg` - [#2354](https://github.com/NuGet/Home/issues/2354)

* 修复了从1个源中缺少包时包安装 (所有源的问题) - [#2322](https://github.com/NuGet/Home/issues/2322)

* 如果单个源未能通过身份验证，则安装块- [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` 版本范围应重写-IncludeReferencedProjects 版本 [#1983](https://github.com/NuGet/Home/issues/1983)

* NuGet 3.3.0 更新失败，并出现 "a 附加约束 ..."在 packages.config 中定义可防止此操作。 ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe 更新删除程序集强名称和私有属性。 - [#1778](https://github.com/NuGet/Home/issues/1778)

* 解决 "DefaultPushSource" 的相对文件路径问题- [#1746](https://github.com/NuGet/Home/issues/1746)

* 改善更新解析程序失败消息- [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>功能及行为变更

* nuget.exe 推送超时参数不起作用- [#2785](https://github.com/NuGet/Home/issues/2785)

* nuget.exe 还原不会 `.props` 生成 `.targets` 项目的文件和文件 `.nuproj` (v 3.4.3.855 中的回归) - [#2711](https://github.com/NuGet/Home/issues/2711)

* 需要扩展性 API 来比较框架和导 [#2633](https://github.com/NuGet/Home/issues/2633)

* 使用时隐藏依赖项选项 `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* 在详细的输出中打印 nuget.exe 版本标头- [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet 应添加对/runtimes/{rid}/nativeassets/{txm}/的支持 [#2782](https://github.com/NuGet/Home/issues/2782)