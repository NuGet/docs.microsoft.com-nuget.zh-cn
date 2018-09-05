---
title: 3.5 Beta2 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 3.5 Beta 2 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b47939e2fafc11823c41a849b3c58bbf0800ada
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551986"
---
# <a name="nuget-35-beta2-release-notes"></a>NuGet 3.5 Beta2 发行说明

[NuGet 3.5 测试版发行说明](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC 发行说明](../release-notes/nuget-3.5-RC.md)

NuGet 3.5 Beta 2 RTM 发布了 2016 年 6 月 27 日，Visual Studio 2013 和 nuget.exe

[完整更改日志](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[问题列表](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Bug 修复

* 更新的错误消息到不支持的已验证的源-.NET Core 中的密码 decrpytion [# 2942年](https://github.com/NuGet/Home/issues/2942)

* 如果.NET Core 项目处于打开状态的程序包管理器控制台获取的包失败[# 2932年](https://github.com/NuGet/Home/issues/2932)

* 在 NuGet push 命令中修复的 403 错误处理[# 2910年](https://github.com/NuGet/Home/issues/2910)

* 修复在卸载时 disableSourceControlIntegration 设置绑定到 TFS 源代码管理解决方案中的包的问题为 true 的[# 2739年](https://github.com/NuGet/Home/issues/2739)

* 修复包更新要考虑到帐户非目标包- [# 2724年](https://github.com/NuGet/Home/issues/2724)

* 使用 MSBuild 详细级别设置为 Nuget 程序包管理器的记录器级别 UI 操作- [# 2705年](https://github.com/NuGet/Home/issues/2705)

* 修复 NuGet 配置是在网站项目的 VS 2015 VSIX (v3.4.3)-无效的错误[# 2667年](https://github.com/NuGet/Home/issues/2667)

* 修复包期刊`.csproj`时将包含的内容文件[# 2658年](https://github.com/NuGet/Home/issues/2658)

* 在 DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) 不起作用- [# 2653年](https://github.com/NuGet/Home/issues/2653)

* 在 Nuget 3.4.3 版本中的值不能为 null 在包创建-修复问题[# 2648年](https://github.com/NuGet/Home/issues/2648)

* 还原为 VSTS 源-使用存储的凭据从 Nuget.Config [# 2647年](https://github.com/NuGet/Home/issues/2647)

* 性能-版本比较代码中修复过多分配- [# 2632年](https://github.com/NuGet/Home/issues/2632)

* Nuget.exe 的多个实例会尝试并行的安装相同包时，解决问题[# 2628年](https://github.com/NuGet/Home/issues/2628)

* 性能-缓存依赖项信息的多项目操作- [# 2619年](https://github.com/NuGet/Home/issues/2619)

* 解决问题的包源无法从设置时要从源列表为空-添加[# 2617年](https://github.com/NuGet/Home/issues/2617)

* 尝试安装包依赖于设计时外观-时修复令人误解错误[# 2594年](https://github.com/NuGet/Home/issues/2594)

* 将包安装从 PackageManager 控制台中设置"All"会尝试仅第一个源- [# 2557年](https://github.com/NuGet/Home/issues/2557)

* 修复文件写入时间在将来有 (Mono) 的包的问题[# 2518年](https://github.com/NuGet/Home/issues/2518)

* 失败时查找项目中更新命令-显示异常[# 2418年](https://github.com/NuGet/Home/issues/2418)

* 从 nuget v3.3 + 安装的包源具有参数时，不正确还原包的内容时包中包含的-NoCache`.nupkg`文件- [# 2354年](https://github.com/NuGet/Home/issues/2354)

* 修复问题，与包安装 （所有源） 时从 1 源的包缺少[# 2322年](https://github.com/NuGet/Home/issues/2322)

* 如果单个源失败授权-安装块[# 2034年](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` 版本范围应重写-IncludeReferencedProjects 版本- [# 1983年](https://github.com/NuGet/Home/issues/1983)

* NuGet 3.3.0 更新失败，出现...更多约束中定义 packages.config 阻止此操作。 - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe 更新中删除程序集强名称和专用属性。 - [#1778](https://github.com/NuGet/Home/issues/1778)

* 使用相对文件路径为"DefaultPushSource"-修复问题[# 1746年](https://github.com/NuGet/Home/issues/1746)

* 提高更新冲突解决程序失败消息- [# 1373年](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>功能及行为变化

* nuget.exe 推送-超时参数不起作用- [# 2785年](https://github.com/NuGet/Home/issues/2785)

* nuget.exe 还原不会产生`.props`并`.targets`文件，以`.nuproj`项目 （v3.4.3.855 中回归）- [# 2711年](https://github.com/NuGet/Home/issues/2711)

* 需要扩展性 API 以比较框架与导入- [# 2633年](https://github.com/NuGet/Home/issues/2633)

* 使用时隐藏依赖关系选项`project.json`  -  [# 2486年](https://github.com/NuGet/Home/issues/2486)

* 打印出 nuget.exe 版本标头中详细输出- [# 1887年](https://github.com/NuGet/Home/issues/1887)

* NuGet 应添加对 /runtimes/ {rid} /nativeassets/ {txm} 的支持 /- [# 2782年](https://github.com/NuGet/Home/issues/2782)