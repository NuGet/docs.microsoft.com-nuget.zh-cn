---
title: NuGet 3.5 RTM 发行说明
description: NuGet 3.5 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776352"
---
# <a name="nuget-35-release-notes"></a>NuGet 3.5 发行说明

[NuGet 3.5-RC 发行说明](../release-notes/nuget-3.5-RC.md)  | [NuGet 4.0 RC 发行说明](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Bug 修复

* Pack 不适用于 mono [#3550](https://github.com/NuGet/Home/issues/3550)上的 MSBuild 14。1

* "更新" 选项卡未选择要更新的最新可用版本，请选择 "当前已安装的版本- [#3498](https://github.com/NuGet/Home/issues/3498)

* 修复在对私有 v2 MyGet 源进行身份验证后单击 "显示 x 个更多结果" 的故障- [#3469](https://github.com/NuGet/Home/issues/3469)

* 对于 UI [#3446](https://github.com/NuGet/Home/issues/3446) ，日志消息似乎是相反的顺序

* v 3.4.4-Nuget 还原引发 "不支持给定路径的格式"- [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet cmdLine 3.6 beta 不遵循-配置配置 = 发布- [#3432](https://github.com/NuGet/Home/issues/3432)

* 在大型项目上安装 Nuget IKVM 慢 [#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe 更新-自行继续更新 [#3395](https://github.com/NuGet/Home/issues/3395)

* 3.5 从 UNC 共享安装/还原具有3.4.4 的性能回归- [#3355](https://github.com/NuGet/Home/issues/3355)

* 从 net451 项目的包管理 UI 安装 Moq 时出错- [#3349](https://github.com/NuGet/Home/issues/3349)

* 解决方案级别的 "安装" 选项卡不显示包的版本- [#3339](https://github.com/NuGet/Home/issues/3339)

* `project.json`从安装的选项卡 xproj 更新丢失状态- [#3303](https://github.com/NuGet/Home/issues/3303)

* 上的 NuGet 包 `.csproj` 忽略文件中的空文件元素 `.nuspec` - [#3257](https://github.com/NuGet/Home/issues/3257)

* IIS 中承载的网站项目不应导致还原失败 [#3235](https://github.com/NuGet/Home/issues/3235)

* 当 v3 终结点重定向到 v2 时，不从 Nuget.Config 检索凭据- [#3179](https://github.com/NuGet/Home/issues/3179)

* 检索可移植的程序集元数据时，NuGet 包未能解析程序集- [#3128](https://github.com/NuGet/Home/issues/3128)

* `msbuild.exe`在 Mono [#3085](https://github.com/NuGet/Home/issues/3085)上找不到 Nuget

* nuget.exe pack 不允许预发行标记，以数字开头- [#1743](https://github.com/NuGet/Home/issues/1743)

* VS2015E 上的 nuget 包安装失败- [#1298](https://github.com/NuGet/Home/issues/1298)

* allowedVersions 筛选器不在解决方案级别工作- [#333](https://github.com/NuGet/Home/issues/333)

* 随机还原失败，已添加具有相同键的项。 - [#2646](https://github.com/NuGet/Home/issues/2646)

* 无法安装 Nuget。 Common in `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* 使用 UI 搜索 V2 源时，每个 ID [#2517](https://github.com/NuGet/Home/issues/2517)会调用两次 FindPackagesById

* 包不能依赖于项目- [#2490](https://github.com/NuGet/Home/issues/2490)

* 已记录 nuget.exe 包-排除项，但不支持- [#2284](https://github.com/NuGet/Home/issues/2284)

* 如果的 ' contentFiles ' 节无效，则出现错误消息的问题 `.nuspec` - [#1686](https://github.com/NuGet/Home/issues/1686)

* 推送始终向经过身份验证的包源发送整个包两次- [#1501](https://github.com/NuGet/Home/issues/1501)

* 当项目没有 #1496 时，调用 nuget.exe update * .csproj 时未提供任何信息 `packages.config`  -  [](https://github.com/NuGet/Home/issues/1496)

* `packages.config` restore 不会重试来自 V2 源的5xx 状态代码- [#1217](https://github.com/NuGet/Home/issues/1217)

* 文件 src 中的双点 `.nuspec` 不起作用- [#2947](https://github.com/NuGet/Home/issues/2947)

* CoreCLR restore 需要忽略带有加密[#2942](https://github.com/NuGet/Home/issues/2942)的源

* nuget.exe 推送403处理-错误提示输入凭据- [#2910](https://github.com/NuGet/Home/issues/2910)

* 通过程序包管理器的 NuGet 更新删除 `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)的属性

* VisualStudio 尝试加载 "TeamFoundationServer14"，但该 DLL 名称已更改为 "TeamFoundationServer"- [#2857](https://github.com/NuGet/Home/issues/2857)

* 程序包管理器 UI 不显示新更新的版本- [#2828](https://github.com/NuGet/Home/issues/2828)

* update-包尝试使用 packageid，版本而不是包。版本 [#2771](https://github.com/NuGet/Home/issues/2771)

* 如果项目未使用 nuget (`packages.config` 或) ，则 nuget 还原 .csproj 应出错 `project.json` [#2766](https://github.com/NuGet/Home/issues/2766)

* 你的工作区中找不到 TFS 错误 "[file]，或者你在将解决方案/项目绑定到 TFS 源代码管理时在升级或卸载过程中没有访问它的权限- [#2739](https://github.com/NuGet/Home/issues/2739)

* 更新包不会获取非目标包的依赖项- [#2724](https://github.com/NuGet/Home/issues/2724)

* 无法设置 Nuget 包管理器 UI 操作的日志详细级别- [#2705](https://github.com/NuGet/Home/issues/2705)

* nuget 配置无效-VS 2015 VSIX (v 3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* `NuGetDefaults.Config` () 中 `ProgramData\NuGet` 的 DefaultPushSource 不起作用- [#2653](https://github.com/NuGet/Home/issues/2653)

* nuget 3.4.3 版本-获取对包生成的值不能为 null- [#2648](https://github.com/NuGet/Home/issues/2648)

* 对于 VSTS 源，还原不使用存储的凭据 Nuget.Config [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet restore]--read-configfile 相对于项目目录而不是 cmd 目录- [#2639](https://github.com/NuGet/Home/issues/2639)

* 版本 comparsion 中过度分配的代码- [#2632](https://github.com/NuGet/Home/issues/2632)

* nuget.exe 尝试并行安装同一包的多个实例导致双写 [#2628](https://github.com/NuGet/Home/issues/2628)

* 不会缓存多项目操作的依赖项信息- [#2619](https://github.com/NuGet/Home/issues/2619)

* 安装和更新下载包，而不先检查包文件夹 [#2618](https://github.com/NuGet/Home/issues/2618)

* 如果 "包源列表" 为空，则无法通过 UI (NuGet 3.4. x) 添加包源- [#2617](https://github.com/NuGet/Home/issues/2617)

* 尝试安装依赖于设计时外观的包时出现误导性错误- [#2594](https://github.com/NuGet/Home/issues/2594)

* 通过设置为 "All" 的 PackageManager 控制台安装包仅尝试第一次源 [#2557](https://github.com/NuGet/Home/issues/2557)

* 未解压缩 ModernHttpClient 的最新 beta 版- [#2518](https://github.com/NuGet/Home/issues/2518)

* VS2015 在启动时崩溃，并提供自构建 NuGet 3.4.1- [#2419](https://github.com/NuGet/Home/issues/2419)

* 如果我要求它是，Update 命令可能会更详细一些， [#2418](https://github.com/NuGet/Home/issues/2418)

* 在本地生成的 VSIX 应该与 CI 生成具有相同的 Dll 和文件。 - [#2401](https://github.com/NuGet/Home/issues/2401)

* 在生成[#2396](https://github.com/NuGet/Home/issues/2396)中修复 NuGet 降级警告

* 未能对包源进行身份验证 (3 次) 永久阻止 [#2362](https://github.com/NuGet/Home/issues/2362)

* 当包包含文件时，使用参数-NoCache 从 nuget v 3.3 + 源安装包时，包内容无法正确还原 `.nupkg` - [#2354](https://github.com/NuGet/Home/issues/2354)

* Nuget 安装时包含所有包源，但从1源丢失包失败- [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson]UIDelay： nuget.packagemanagement.visualstudio.dll！VSMSBuildNuGetProjectSystem + & l t; VisualStudio; &gt;b__ c__DisplayClass_0 + &lt; &lt; AddReference &gt; &gt; - [#2285](https://github.com/NuGet/Home/issues/2285)

* 如果单个源未能通过身份验证，则安装块- [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` 版本范围应重写-IncludeReferencedProjects 版本 [#1983](https://github.com/NuGet/Home/issues/1983)

* Update-Package 超级慢-"正在尝试收集依赖项信息"- [#1909](https://github.com/NuGet/Home/issues/1909)

* 当批处理更新其依赖项时，NuGet 隐形降级包- [#1903](https://github.com/NuGet/Home/issues/1903)

* nuget.exe 更新删除程序集强名称和私有属性。 - [#1778](https://github.com/NuGet/Home/issues/1778)

* "DefaultPushSource" 的相对文件路径- [#1746](https://github.com/NuGet/Home/issues/1746)

* 改善解析程序失败消息- [#1373](https://github.com/NuGet/Home/issues/1373)

* v3 中的更新包失败，因为包不在指定的源中- [#1013](https://github.com/NuGet/Home/issues/1013)

* 使用包源的相对路径是使用- [#865](https://github.com/NuGet/Home/issues/865)的问题

* 如果已存在具有较低版本要求的间接依赖关系，则从项目生成的 NUPKG 中缺少依赖项- [#759](https://github.com/NuGet/Home/issues/759)

* 删除项目会关闭相应的 UI 窗口，但重命名项目不会重命名 UI 窗口。 请注意，PMC 侦听项目重命名和项目删除事件- [#670](https://github.com/NuGet/Home/issues/670)

* [Willow Web 工作负荷]创建 Razor v3 WSP 挂起- [#3241](https://github.com/NuGet/Home/issues/3241)

* 安装/还原特定包失败，并出现 "包包含多个 nuspec 文件。" - [#3231](https://github.com/NuGet/Home/issues/3231)

* 小写 Id & `packages.config` 方案- [#3209](https://github.com/NuGet/Home/issues/3209)

* [3.5-beta2]包还原无法还原 "旧版" 包- [#3208](https://github.com/NuGet/Home/issues/3208)

* 不管[#3203](https://github.com/NuGet/Home/issues/3203)如何，nuget 包都会强制将 tt 文件添加到 content 文件夹中

* ASP.NET web 应用的更新包生成与文件相关的警告：源- [#3194](https://github.com/NuGet/Home/issues/3194)

* `project.json`如果 JSON 文件中没有 packOptions 和所有者，nuget 包 .csproj () 崩溃[#3180](https://github.com/NuGet/Home/issues/3180)

* 的 nuget 包 `project.json` 忽略 packOptions 标记，如摘要、作者、所有者等 [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException via PhysicalPackageFile. System.resources.resourcemanager.getstream- [#3160](https://github.com/NuGet/Home/issues/3160)

* NuGet 包忽略 `.nuspec` `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)的输出中的依赖关系

* 使用 rollback 更新多个包会使项目处于损坏状态- [#3139](https://github.com/NuGet/Home/issues/3139)

* 不会为 netstandard 项目添加 ContentFiles 下的任何项目- [#3118](https://github.com/NuGet/Home/issues/3118)

* 无法正确打包面向 .Net Standard 的库目标- [#3108](https://github.com/NuGet/Home/issues/3108)

* 文件-> 新项目-> 类库 (可移植) 项目在 VS2015 和 Dev15 中失败- [#3094](https://github.com/NuGet/Home/issues/3094)

* nuGet 错误-1.0.0-* 不是有效的版本字符串- [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package 无法显示但 Install-Package 工作- [#3068](https://github.com/NuGet/Home/issues/3068)

* Dev15 上的 "安装包 jquery. 验证" 时出错- [#3061](https://github.com/NuGet/Home/issues/3061)

* xproj 的 nuget 包默认为无效的目标路径- [#3060](https://github.com/NuGet/Home/issues/3060)

* 在使用 NuGet 版本3.5.0 的 VS 上安装 VS 2015 update 3 时出现错误- [#3053](https://github.com/NuGet/Home/issues/3053)

*  (UWP 中的 "被 packages.config 阻止" `project.json` ，即生成集成) 项目的 [#3046](https://github.com/NuGet/Home/issues/3046)

* 将生成脚本安装的 dotnet cli 更新为 preview2-003121，这是官方 preview2 生成。 - [#3045](https://github.com/NuGet/Home/issues/3045)

* 程序包管理器 UI：更新包后不显示新版本- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey on delete 命令行在3.5.0 中未被读/发送- [#3037](https://github.com/NuGet/Home/issues/3037)

* 字符串不正确：包的稳定版本不应具有预发行依赖项。 - [#3030](https://github.com/NuGet/Home/issues/3030)

* OptimizedZipPackage 缓存保留空文件夹- [#3029](https://github.com/NuGet/Home/issues/3029)

* 创建 PCL (net46 和 windows 10) project 获取 NullRef 异常。 - [#3014](https://github.com/NuGet/Home/issues/3014)

* 当 allowedVersions 约束限制更高版本时，Nuget 更新应提供信息性消息 [#3013](https://github.com/NuGet/Home/issues/3013)

* Nuget v3 还原问题- [#2891](https://github.com/NuGet/Home/issues/2891)

* 凭据插件已退出，出现错误-1/在将凭据提供程序与多个源一起使用时下载包- [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` 当没有任何更改时，nuget 还原会导致重新编译- [#2817](https://github.com/NuGet/Home/issues/2817)

* 符号包决不会用于安装或更新- [#2807](https://github.com/NuGet/Home/issues/2807)

* VS 不支持 repositoryPath 中的环境变量 ( # A0) - [#2763](https://github.com/NuGet/Home/issues/2763)

* 在包管理器 UI 中标记未标记的 UIElements，以获取辅助功能- [#2745](https://github.com/NuGet/Home/issues/2745)

* 拒绝带有断字符配置文件的便携式框架。 - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet 包管理器应当清楚地说明包详细信息中的选项列表不适用于 `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe 推送/删除不使用 API 密钥- [#2627](https://github.com/NuGet/Home/issues/2627)

* 从锁定文件中删除锁定的属性- [#2379](https://github.com/NuGet/Home/issues/2379)

* NuGet 3.3.0 更新失败，并出现 "a 附加约束 ..."在 packages.config 中定义可防止此操作。 ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* 从不存在的本地源安装包将引发虚假消息 [#1674](https://github.com/NuGet/Home/issues/1674)

* "可用的升级" 筛选器显示违反版本约束的升级- [#1094](https://github.com/NuGet/Home/issues/1094)

* 无法更新本机包- [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>功能

* 支持将 CopyLocal 的引用设置为 false- [#329](https://github.com/NuGet/Home/issues/329)

* MSBuild 15 [#1937](https://github.com/NuGet/Home/issues/1937) nuget.exe 支持

* 包的支持。`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* 正在执行用户操作时禁用用户操作- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet 应添加对 `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)的支持

* 在 NuGet 2.x 中缺少添加框架兼容性 (已在 1.x) 中 [#2720](https://github.com/NuGet/Home/issues/2720)

* 支持备用包文件夹- [#2899](https://github.com/NuGet/Home/issues/2899)

* 设计和实现包类型的概念以支持工具包- [#2476](https://github.com/NuGet/Home/issues/2476)

* 添加 API 以获取全局包文件夹的路径- [#2403](https://github.com/NuGet/Home/issues/2403)

* 在 pack [#3356](https://github.com/NuGet/Home/issues/3356)中启用 SemVer 2.0。0

## <a name="dcrs"></a>DCR

* nuget.exe 推送超时参数不起作用- [#2785](https://github.com/NuGet/Home/issues/2785)

* 应选择包说明文本- [#1769](https://github.com/NuGet/Home/issues/1769)

* 启用 nuget.exe 以生成 `.props` `.targets` 项目的和 `.nuproj` 文件 [#2711](https://github.com/NuGet/Home/issues/2711)

* 添加扩展性 API 来比较框架和导入- [#2633](https://github.com/NuGet/Home/issues/2633)

* 使用时隐藏依赖项选项 `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* 在详细的输出中打印 nuget.exe 版本标头- [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet 需要让用户知道在基于 dotnet tfm 的 PCL 中升级/安装可能会导致问题 [#3138](https://github.com/NuGet/Home/issues/3138)

* 为 project （tfm = "dotnet"）警告安装/升级失败- [#3137](https://github.com/NuGet/Home/issues/3137)

* 解决 ReShaper 和 NuGet [#3044](https://github.com/NuGet/Home/issues/3044)的性能问题

* 添加 netcoreapp11 和 netstandard17 支持- [#2998](https://github.com/NuGet/Home/issues/2998)

* 将 AssemblyMetadata 特性用于 `.nuspec` 标记替换- [#2851](https://github.com/NuGet/Home/issues/2851)
