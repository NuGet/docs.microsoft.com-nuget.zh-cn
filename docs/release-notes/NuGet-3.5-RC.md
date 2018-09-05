---
title: 3.5 RC 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 3.5 RC 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548533"
---
# <a name="nuget-35-rc-release-notes"></a>NuGet 3.5 RC 发行说明

[NuGet 3.5 Beta2 发行说明](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5 的 RTM 发行说明](../release-notes/nuget-3.5-RTM.md)

3.5 版本侧重于提高质量和性能的 NuGet 客户端。 此外，我们对发布了一些功能，例如，为支持[Fallback 文件夹](https://github.com/NuGet/Home/issues/2899)， [PackageType](https://github.com/NuGet/Home/issues/2476)中支持`.nuspec`和的详细信息。

[问题列表](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Bug 修复

* 包的安装/还原失败，出现"包包含多个`.nuspec`文件。" - [#3231](https://github.com/NuGet/Home/issues/3231)

* nuget 包添加了强制`.tt`文件复制到 content 文件夹，无论什么- [#3203](https://github.com/NuGet/Home/issues/3203)

* nuget 包 csproj (使用`project.json`) 如果没有 packOptions 和在 JSON 文件的所有者将崩溃[#3180](https://github.com/NuGet/Home/issues/3180)

* 适用于 nuget 包`project.json`将忽略摘要、 作者和所有者等-packOptions 标记[#3161](https://github.com/NuGet/Home/issues/3161)

* nuget pack 忽略输出中的依赖关系`.nuspec`有关`project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* 使用回滚更新多个包使项目处于中断状态- [#3139](https://github.com/NuGet/Home/issues/3139)

* 任何下的内容文件不会添加为 netstandard 项目- [#3118](https://github.com/NuGet/Home/issues/3118)

* 无法打包库面向.Net 标准正确- [#3108](https://github.com/NuGet/Home/issues/3108)

* 文件-> 新建项目-> 类库 （可移植） 项目失败 VS2015 和 Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* NuGet 错误-1.0.0-* 不是有效的版本字符串- [#3070](https://github.com/NuGet/Home/issues/3070)

* 查找包失败到显示，但安装包的工作原理- [#3068](https://github.com/NuGet/Home/issues/3068)

* 错误时在 dev15-上的"安装包 jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)

* 当已安装的 VS 2015 更新 3 使用的 NuGet 版本 3.5.0 错误发生的对和[#3053](https://github.com/NuGet/Home/issues/3053)

* 包管理器 UI： 在更新包后不会显示新版本- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey delete 命令行上不读取/发送中 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* 不正确的字符串： 稳定的发行版的包不应具有在预发行版的依赖关系。 - [#3030](https://github.com/NuGet/Home/issues/3030)

* 正在创建 PCL （net46 和 windows 10） 项目 get NullRef 异常。 - [#3014](https://github.com/NuGet/Home/issues/3014)

* Nuget 更新的 allowedVersions 约束的限制更高版本时应提供信息性消息[#3013](https://github.com/NuGet/Home/issues/3013)

* 凭据插件已退出，错误为-1 / 错误下载包时使用多个源的凭据提供程序[# 2885年](https://github.com/NuGet/Home/issues/2885)

* nuget 包-缺少 Newtonsoft.Json 包依赖项- [# 2876年](https://github.com/NuGet/Home/issues/2876)

* 在 Linux/MacOS + Mono-ExecuteSynchronizedCore bug [# 2860年](https://github.com/NuGet/Home/issues/2860)

* 与不支持在 repositoryPath 中环境变量 （nuget.exe 执行）- [# 2763年](https://github.com/NuGet/Home/issues/2763)

* 修复可访问性问题- [# 2745年](https://github.com/NuGet/Home/issues/2745)

* 可移植框架使用连字符的由配置文件将被拒绝。 - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet 包管理器应使它清楚该选项列表中包详细信息不适用于`project.json`  -  [# 2665年](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0 更新失败，出现...更多约束中定义 packages.config 阻止此操作。 - [#1816](https://github.com/NuGet/Home/issues/1816)

* 从本地源不存在，则会引发错误的邮件-安装包[# 1674年](https://github.com/NuGet/Home/issues/1674)

* "升级版提供"筛选器将显示与版本约束的冲突的升级[# 1094年](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>性能改进

* 性能： 改善 ContentModel 目标框架分析- [#3162](https://github.com/NuGet/Home/issues/3162)

* 性能： 避免读取`runtime.json`不具有 Rid 还原的文件[#3150](https://github.com/NuGet/Home/issues/3150)。 CI 计算机上的 ASP.NET Web 应用程序减少了超过 15 秒到 3 秒的示例中进行还原。

* 性能： 程序包管理器控制台 init.ps1 加载时间[# 2956年](https://github.com/NuGet/Home/issues/2956)。 时间才能打开 PackageManagerConsole 改进了在某些情况下从 132s年到 10 秒。

* 解决在 NuGet 更新-ReSharper 性能问题[#3044](https://github.com/NuGet/Home/issues/3044)： 上一个示例项目，安装包所花的时间减少从 140s年到 68s。

## <a name="dcrs"></a>DCR

* NuGet 需要让用户知道，在基于 dotnet tfm 升级/安装 PCL 可能会导致问题- [#3138](https://github.com/NuGet/Home/issues/3138)

* 错误安装/升级带 tfm 的项目，则发出警告 ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* 添加了 netcoreapp11 和 netstandard17 支持- [# 2998年](https://github.com/NuGet/Home/issues/2998)

* 打印 NuGet 警告标头内容，控制台中 nuget.exe- [# 2934年](https://github.com/NuGet/Home/issues/2934)

* 利用 AssemblyMetadata 属性`.nuspec`令牌替换- [# 2851年](https://github.com/NuGet/Home/issues/2851)

* 从锁定文件中的删除锁定的属性[# 2379年](https://github.com/NuGet/Home/issues/2379)

* 符号包应不曾经用于安装或更新 #2807

## <a name="features"></a>功能

* 支持回退的包文件夹- [# 2899年](https://github.com/NuGet/Home/issues/2899)

* 设计和实现包类型的概念，以支持工具的包- [# 2476年](https://github.com/NuGet/Home/issues/2476)

* 若要获取的全局包文件夹的路径的 API [# 2403年](https://github.com/NuGet/Home/issues/2403)

* 本机包更新支持- [# 1291年](https://github.com/NuGet/Home/issues/1291)
