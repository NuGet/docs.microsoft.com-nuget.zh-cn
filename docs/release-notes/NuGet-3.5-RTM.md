---
title: NuGet 3.5 Beta 发行说明
description: 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 3.5 的发行说明。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cdb540229cae0e6e952ac2a0c00c8801ccbbb28d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822586"
---
# <a name="nuget-35-release-notes"></a>NuGet 3.5 发行说明

[NuGet 3.5 RC 发行说明](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC 发行说明](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Bug 修复

* 包不 mono-上使用 MSBuild 14.1 [#3550](https://github.com/NuGet/Home/issues/3550)

* 更新选项卡上不会选择最新可用版本更新改为选择的当前已安装的版本- [#3498](https://github.com/NuGet/Home/issues/3498)

* 对专用 v2 MyGet 源进行身份验证，并单击"显示更多结果 x"后修复崩溃的[#3469](https://github.com/NuGet/Home/issues/3469)

* 日志消息按相反的顺序可能的 UI-纳入[#3446](https://github.com/NuGet/Home/issues/3446)

* "不支持给定的路径的格式"-v3.4.4-Nuget 还原引发[#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet 命令行 3.6 beta 不会遵循-Prop Configuration = 释放- [#3432](https://github.com/NuGet/Home/issues/3432)

* 在大型项目-上安装 Nuget IKVM 慢速[#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe-自助保留在自我更新-更新[#3395](https://github.com/NuGet/Home/issues/3395)

* 从 UNC 共享的 3.5 安装/还原已从 3.4.4-性能回归[#3355](https://github.com/NuGet/Home/issues/3355)

* 错误时从包管理 UI net451 项目-安装 Moq [#3349](https://github.com/NuGet/Home/issues/3349)

* 在解决方案级别的安装选项卡不会显示包的版本- [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj`project.json`从已安装选项卡上的更新丢失状态- [#3303](https://github.com/NuGet/Home/issues/3303)

* 上的 NuGet 包`.csproj`忽略空文件中的元素`.nuspec`文件- [#3257](https://github.com/NuGet/Home/issues/3257)

* 在 IIS 中承载的网站项目不应导致还原失败- [#3235](https://github.com/NuGet/Home/issues/3235)

* 凭据未检索到从 Nuget.Config 当 v3 终结点重定向到 v2- [#3179](https://github.com/NuGet/Home/issues/3179)

* NuGet 包未能检索可移植程序集元数据的时解析程序集[#3128](https://github.com/NuGet/Home/issues/3128)

* 找不到 Nuget`msbuild.exe`上 Mono- [#3085](https://github.com/NuGet/Home/issues/3085)

* nuget.exe 包不允许的预发行标记开头号- [# 1743年](https://github.com/NuGet/Home/issues/1743)

* 在 VS2015E-上 nuget 包安装失败[# 1298年](https://github.com/NuGet/Home/issues/1298)

* allowedVersions 筛选不在解决方案级别的工作[#333](https://github.com/NuGet/Home/issues/333)

* 还原随机将失败并具有相同的项已添加了键。 - [#2646](https://github.com/NuGet/Home/issues/2646)

* 无法安装在 Nuget.Common `.csproj`  -  [# 2635年](https://github.com/NuGet/Home/issues/2635)

* 当使用 UI 搜索 V2 源，为每个 ID-两次调用 FindPackagesById [# 2517年](https://github.com/NuGet/Home/issues/2517)

* 包不能依赖于项目- [# 2490年](https://github.com/NuGet/Home/issues/2490)

* nuget.exe 包-记录排除但不是支持- [# 2284年](https://github.com/NuGet/Home/issues/2284)

* 问题的错误消息时的文件部分`.nuspec`无效- [# 1686年](https://github.com/NuGet/Home/issues/1686)

* 请求始终发送整个包两次通过身份验证包源- [# 1501年](https://github.com/NuGet/Home/issues/1501)

* 时调用 nuget.exe 更新 *.csproj 而项目没有指定任何信息`packages.config`  -  [# 1496年](https://github.com/NuGet/Home/issues/1496)

* `packages.config` 从 V2 源-5xx 状态代码，还原不重试[# 1217年](https://github.com/NuGet/Home/issues/1217)

* 在文件中的 src 双点`.nuspec`不起作用- [# 2947年](https://github.com/NuGet/Home/issues/2947)

* CoreCLR 还原需要忽略与加密-馈送[# 2942年](https://github.com/NuGet/Home/issues/2942)

* nuget.exe 推送 403 处理的错误会提示输入凭据- [# 2910年](https://github.com/NuGet/Home/issues/2910)

* 程序包管理器通过 NuGet 更新中删除属性从`project.json`  -  [# 2888年](https://github.com/NuGet/Home/issues/2888)

* 尝试加载"NuGet.TeamFoundationServer14"，但 DLL 名称更改为"NuGet.TeamFoundationServer"-NuGet.PackageManagement.VisualStudio [# 2857年](https://github.com/NuGet/Home/issues/2857)

* 程序包管理器用户界面不显示新更新版本- [# 2828年](https://github.com/NuGet/Home/issues/2828)

* 更新包尝试使用 packageid，而不是 package.version-版本[# 2771年](https://github.com/NuGet/Home/issues/2771)

* 如果项目不使用 nuget，nuget 还原 csproj 应错误 (`packages.config`或`project.json`)- [# 2766年](https://github.com/NuGet/Home/issues/2766)

* TFS 错误"[文件] 不能在工作区中，找到或您没有权限访问该"期间升级或卸载解决方案/项目绑定到 TFS 源代码管理- [# 2739年](https://github.com/NuGet/Home/issues/2739)

* 更新包不获取非目标包的依赖关系[# 2724年](https://github.com/NuGet/Home/issues/2724)

* 没有任何方法可设置为 Nuget 包管理器 UI 操作的日志详细级别[# 2705年](https://github.com/NuGet/Home/issues/2705)

* nuget 配置无效-VS 2015 VSIX (v3.4.3)- [# 2667年](https://github.com/NuGet/Home/issues/2667)

* 中的 DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) 不起作用- [# 2653年](https://github.com/NuGet/Home/issues/2653)

* nuget 3.4.3 释放-获取值不能为包生成的 null [# 2648年](https://github.com/NuGet/Home/issues/2648)

* 还原时未使用存储的凭据从 Nuget.Config VSTS 馈送- [# 2647年](https://github.com/NuGet/Home/issues/2647)

* [dotnet 还原]-configfile 是相对于项目目录，而不是 cmd 目录中- [# 2639年](https://github.com/NuGet/Home/issues/2639)

* 在版本常量代码-过度分配[# 2632年](https://github.com/NuGet/Home/issues/2632)

* Nuget.exe 尝试安装相同的多个实例中并行原因 double 的写入-打包[# 2628年](https://github.com/NuGet/Home/issues/2628)

* 依赖项信息尚未缓存的多项目操作- [# 2619年](https://github.com/NuGet/Home/issues/2619)

* 安装和更新下载包，而不首先-检查包文件夹[# 2618年](https://github.com/NuGet/Home/issues/2618)

* 如果包源列表为空，无法添加包源通过 UI (NuGet 3.4.x)- [# 2617年](https://github.com/NuGet/Home/issues/2617)

* 具有误导性错误，当试图安装包依赖于设计时外观- [# 2594年](https://github.com/NuGet/Home/issues/2594)

* 从 PackageManager 控制台中设置"全部"安装包尝试仅第一个源- [# 2557年](https://github.com/NuGet/Home/issues/2557)

* 不解压缩的最新 beta ModernHttpClient- [# 2518年](https://github.com/NuGet/Home/issues/2518)

* 在使用自生成 NuGet 3.4.1-启动 VS2015 崩溃[# 2419年](https://github.com/NuGet/Home/issues/2419)

* 更新命令可能是更详细如果 i 询问其成为...- [# 2418年](https://github.com/NuGet/Home/issues/2418)

* 本地生成的 VSIX 应作为 CI 生成具有相同的 Dll 和文件。 - [#2401](https://github.com/NuGet/Home/issues/2401)

* 在生成的修复 NuGet 降级警告[# 2396年](https://github.com/NuGet/Home/issues/2396)

* 无法进行身份验证的包源 （3 次） 永久的阻止[# 2362年](https://github.com/NuGet/Home/issues/2362)

* 从 nuget v3.3 + 安装的包源具有自变量时，不正确还原包内容-NoCache 当包包含`.nupkg`文件- [# 2354年](https://github.com/NuGet/Home/issues/2354)

* Nuget 安装的所有包源，但包缺少 1 从源失败- [# 2322年](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)

* 如果单个源失败授权-安装块[# 2034年](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` 版本范围应重写-IncludeReferencedProjects 版本- [# 1983年](https://github.com/NuGet/Home/issues/1983)

* 更新包非常缓慢-"尝试收集依赖项信息"- [# 1909年](https://github.com/NuGet/Home/issues/1909)

* NuGet 隐形降级包时批处理更新及其依赖项- [# 1903年](https://github.com/NuGet/Home/issues/1903)

* nuget.exe 更新中删除程序集强名称和私有特性。 - [#1778](https://github.com/NuGet/Home/issues/1778)

* 相对文件路径"DefaultPushSource"- [# 1746年](https://github.com/NuGet/Home/issues/1746)

* 提高冲突解决程序失败消息- [# 1373年](https://github.com/NuGet/Home/issues/1373)

* 在 v3 的更新包将失败并不在指定的源的包[# 1013年](https://github.com/NuGet/Home/issues/1013)

* 对于包源使用相对路径会产生问题，若要使用- [#865](https://github.com/NuGet/Home/issues/865)

* 缺少的 NUPKG 文件如果间接的依赖关系已存在具有较低的版本要求-生成从项目中的依赖项[#759](https://github.com/NuGet/Home/issues/759)

* 删除项目关闭相应 UI 窗口时，但是，重命名项目不是重命名用户界面窗口。 请注意 PMC 侦听项目重命名和项目删除事件数- [#670](https://github.com/NuGet/Home/issues/670)

* [Willow Web 工作负荷]创建 Razor v3 WSP 挂起- [#3241](https://github.com/NuGet/Home/issues/3241)

* 特定包的安装/还原失败，"包包含多个 nuspec 文件。" - [#3231](https://github.com/NuGet/Home/issues/3231)

* 小写 Id （& a)`packages.config`方案- [#3209](https://github.com/NuGet/Home/issues/3209)

* [3.5 beta2 之前]程序包还原失败后还原"传统"程序包- [#3208](https://github.com/NuGet/Home/issues/3208)

* nuget 包强制将.tt 文件添加到内容文件夹无论- [#3203](https://github.com/NuGet/Home/issues/3203)

* ASP.NET web 应用的更新包将生成与文件相关的警告： 源- [#3194](https://github.com/NuGet/Home/issues/3194)

* nuget 包 csproj (与`project.json`) 发生崩溃，如果没有 packOptions 和在 JSON 文件的所有者[#3180](https://github.com/NuGet/Home/issues/3180)

* 适用于的 nuget 包`project.json`忽略摘要、 作者、 所有者等-之类的 packOptions 标记[#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)

* NuGet 包将忽略输出中的依赖关系`.nuspec`为`project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* 使用回滚更新多个包使项目处于中断状态- [#3139](https://github.com/NuGet/Home/issues/3139)

* 在任何下的文件不会添加为 netstandard 项目- [#3118](https://github.com/NuGet/Home/issues/3118)

* 无法打包面向.Net 库标准正确- [#3108](https://github.com/NuGet/Home/issues/3108)

* 文件-> 新建项目-> 类库 （可移植） VS2015 和 Dev15-中的项目失败[#3094](https://github.com/NuGet/Home/issues/3094)

* nuGet 错误-1.0.0-* 不是有效的版本字符串- [#3070](https://github.com/NuGet/Home/issues/3070)

* 查找包无法显示，但安装包工作原理- [#3068](https://github.com/NuGet/Home/issues/3068)

* 错误时 dev15-上的"安装包 jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)

* nuget 包的 xproj 默认为无效的目标路径的[#3060](https://github.com/NuGet/Home/issues/3060)

* 当已安装的 VS 2015 update 3 上使用的 NuGet 版本 3.5.0 错误发生的 VS [#3053](https://github.com/NuGet/Home/issues/3053)

* 的"被 packages.config" `project.json` (UWP，即生成集成) 项目- [#3046](https://github.com/NuGet/Home/issues/3046)

* 更新安装到 preview2-003121，这是官方 preview2 生成的生成脚本的 dotnet cli。 - [#3045](https://github.com/NuGet/Home/issues/3045)

* 包管理器 UI： 在更新包后不会显示新版本- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey delete 命令行上不是读取/以发送 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* 不正确的字符串： 稳定程序包版本不应具有在预发布的依赖项。 - [#3030](https://github.com/NuGet/Home/issues/3030)

* OptimizedZipPackage 缓存离开空文件夹- [#3029](https://github.com/NuGet/Home/issues/3029)

* 创建 （net46 和 windows 10） 的 PCL 项目 get NullRef 异常。 - [#3014](https://github.com/NuGet/Home/issues/3014)

* Nuget 更新应提供信息性消息的 allowedVersions 约束的限制更高版本时[#3013](https://github.com/NuGet/Home/issues/3013)

* Nuget v3 还原问题- [# 2891年](https://github.com/NuGet/Home/issues/2891)

* 凭据插件退出，错误为-1 / 错误下载包时使用多个源的凭据提供程序[# 2885年](https://github.com/NuGet/Home/issues/2885)

* `project.json` nuget 还原会导致重新编译时执行任何操作更改- [# 2817年](https://github.com/NuGet/Home/issues/2817)

* 符号包不应在安装或更新-中使用[# 2807年](https://github.com/NuGet/Home/issues/2807)

* VS 中 repositoryPath 不支持环境变量 （nuget.exe 一样）- [# 2763年](https://github.com/NuGet/Home/issues/2763)

* 使用的辅助功能--标签在程序包管理器用户界面中未标记的 UIElements [# 2745年](https://github.com/NuGet/Home/issues/2745)

* 使用连字符连接的配置文件的可移植框架会被拒绝。 - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet 包管理器应使它清楚该详细信息不适用于的包中的选项列表`project.json`  -  [# 2665年](https://github.com/NuGet/Home/issues/2665)

* nuget.exe 推送/删除不会使用 API 密钥- [# 2627年](https://github.com/NuGet/Home/issues/2627)

* 从锁定文件的删除锁定的属性[# 2379年](https://github.com/NuGet/Home/issues/2379)

* NuGet 3.3.0 更新失败，出现...的其他约束中定义 packages.config 会阻止此操作。 - [#1816](https://github.com/NuGet/Home/issues/1816)

* 从本地源中不存在将引发错误的邮件-安装包[# 1674年](https://github.com/NuGet/Home/issues/1674)

* "可用的升级"筛选器以显示与版本约束中的冲突的升级[# 1094年](https://github.com/NuGet/Home/issues/1094)

* 无法更新本地程序包- [# 1291年](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>功能

* 引用添加的 NuGet 的支持为 false 的设置 CopyLocal [#329](https://github.com/NuGet/Home/issues/329)

* MSBuild 15-nuget.exe 支持[# 1937年](https://github.com/NuGet/Home/issues/1937)

* 包的支持。`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* 禁用用户执行任何操作，正在执行的用户操作时- [# 1440年](https://github.com/NuGet/Home/issues/1440)

* NuGet 应添加对支持`runtimes/{rid}/nativeassets/{txm}/`  -  [# 2782年](https://github.com/NuGet/Home/issues/2782)

* 添加 NuGet 中缺少的 framework 兼容性 （它们已处于 3.x） 的 2.x- [# 2720年](https://github.com/NuGet/Home/issues/2720)

* 对回退包文件夹的支持[# 2899年](https://github.com/NuGet/Home/issues/2899)

* 设计和实现包类型的概念，以支持工具包- [# 2476年](https://github.com/NuGet/Home/issues/2476)

* 将 API 来获取到的全局包文件夹的路径添加[# 2403年](https://github.com/NuGet/Home/issues/2403)

* 启用包中的 SemVer 2.0.0 [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>DCR

* nuget.exe 推送的超时参数不起作用- [# 2785年](https://github.com/NuGet/Home/issues/2785)

* 包描述文本应为可选择- [# 1769年](https://github.com/NuGet/Home/issues/1769)

* 启用 nuget.exe 生成`.props`和`.targets`文件`.nuproj`项目[# 2711年](https://github.com/NuGet/Home/issues/2711)

* 添加扩展性 API 进行比较导入的框架[# 2633年](https://github.com/NuGet/Home/issues/2633)

* 使用时隐藏依存关系选项`project.json`  -  [# 2486年](https://github.com/NuGet/Home/issues/2486)

* 打印出 nuget.exe 版本标头中详细输出- [# 1887年](https://github.com/NuGet/Home/issues/1887)

* NuGet 需要让用户知道，在基于 dotnet tfm 升级/安装 PCL 可能会导致问题- [#3138](https://github.com/NuGet/Home/issues/3138)

* 错误安装/升级带 tfm 的项目，则发出警告 ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* 为更新-使用 ReShaper 和 NuGet 修复性能问题[#3044](https://github.com/NuGet/Home/issues/3044)

* 添加 netcoreapp11 和 netstandard17 支持- [# 2998年](https://github.com/NuGet/Home/issues/2998)

* 利用 AssemblyMetadata 属性`.nuspec`令牌替换- [# 2851年](https://github.com/NuGet/Home/issues/2851)
