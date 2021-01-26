---
title: NuGet 1.0 和1.1 发行说明
description: NuGet 1.1 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cdd4bad54b08d956dbfdaf54220971492fd3ab02
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777214"
---
# <a name="nuget-10-and-11-release-notes"></a>NuGet 1.0 和1.1 发行说明

[NuGet 1.2 发行说明](../release-notes/nuget-1.2.md)

NuGet 1.0 于2011年1月13日发布。  NuGet 1.1 于2011年2月12日发布。

## <a name="overview"></a>概述

本文档包含根据主要预览版进行分组的各种版本的 NuGet 1.0 发行说明。

NuGet 包含以下组件：

* *NuGet. .vsix* *，其中包括：
  * 在 Visual Studio 中的 "**添加库包" 对话框** 中，用于浏览和安装包。
  * Visual Studio 中的 **包管理器控制台*** 基于 Powershell 的控制台。
* *NuGet 命令行工具* * 工具，用于创建 (，并最终发布) 包。

NuGet 工具 Visual Studio *扩展 ()* 需要：

* Visual Studio 2010 或 Visual Web Developer 2010 Express。

NuGet 命令行工具需要：

* .NET Framework 版本4

## <a name="installation"></a>安装

使用此 [最新版本](http://nuget.codeplex.com/releases/view/52018)：

* 首先卸载旧版本。 需要以管理员身份运行 VS 才能执行此操作。
* 删除所有现有源。
* 添加指向的新源 <https://go.microsoft.com/fwlink/?LinkId=206669> 。

## <a name="nuget-11"></a>NuGet 1.1

[可在此处找到](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)此版本中已修复问题的列表

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

自 RC 以来，为 RTM 修复了一个问题。

* [问题474：删除包会影响解决方案中的所有项目](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>候选发布版本

自 CTP 2 起，此候选发布版中的更改如下所述。 请访问问题跟踪程序，查看完整的错误列表。

* [从控制台更新包不会更新依赖项。](http://nuget.codeplex.com/workitem/443)
* [添加包提取 bin not (CTP1) 的包引用 ](http://nuget.codeplex.com/workitem/442)
* [更新包会保留损坏的引用](http://nuget.codeplex.com/workitem/440)
* [获取包-对话框中的更新失败，或在控制台中选择 "全部" 聚合源时失败](http://nuget.codeplex.com/workitem/439)
* [获取包验证错误](http://nuget.codeplex.com/workitem/426)
* [当无法通过 "添加包" 对话框安装包时警告用户](http://nuget.codeplex.com/workitem/425)
* [获取包-更新大量包时引发更新](http://nuget.codeplex.com/workitem/424)
* [当错误编写 nuspec 文件时改进错误处理](http://nuget.codeplex.com/workitem/423)
* [Nuget 包忽略指定文件](http://nuget.codeplex.com/workitem/422)
* [删除第二个到最后一个包源，然后单击 "下移" 崩溃与](http://nuget.codeplex.com/workitem/418)
* [安装包时删除程序集引用](http://nuget.codeplex.com/workitem/413)
* [打开设置对话框时的 InvalidOperationException](http://nuget.codeplex.com/workitem/411)
* [包源在包管理器控制台中的访问密钥无效](http://nuget.codeplex.com/workitem/410)
* [NuGet VS 设置对话框访问键将焦点放在错误字段上](http://nuget.codeplex.com/workitem/409)
* [包 ID intellisense 不应查询太多项目](http://nuget.codeplex.com/workitem/404)
* [将包添加到项目名称中包含点字符的项目失败](http://nuget.codeplex.com/workitem/403)
* [Nuspec 中指定文件的问题](http://nuget.codeplex.com/workitem/400)
* [使用较新版本时应注册正确的官方源](http://nuget.codeplex.com/workitem/399)
* [标记应使用空格而不是#](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata 缺少某些有用信息](http://nuget.codeplex.com/workitem/388)
* [向对话添加 "报告滥用行为" 链接](http://nuget.codeplex.com/workitem/386)
* [在 Visual Studio 中使用 App_Data 解压缩包中断](http://nuget.codeplex.com/workitem/380)
* [实现标记](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder 允许没有要创建的依赖项的空包](http://nuget.codeplex.com/workitem/373)
* [为包添加所有者字段](http://nuget.codeplex.com/workitem/365)
* [更新 VSIX 清单以表示 NuGet 包管理器，而不是 VSIX 工具](http://nuget.codeplex.com/workitem/364)
* [选择 "所有源" 时，"获取包" 命令会引发错误](http://nuget.codeplex.com/workitem/359)
* [允许在 "选项" 对话框中排序包源](http://nuget.codeplex.com/workitem/356)
* [更新-包不会删除较旧的版本](http://nuget.codeplex.com/workitem/352)
* [实现依赖项的版本范围规范](http://nuget.codeplex.com/workitem/347)
* [单击 "添加新包" 时 Visual Studio 崩溃](http://nuget.codeplex.com/workitem/346)
* [显示 "添加包" 对话框中的下载和分级](http://nuget.codeplex.com/workitem/345)
* [对话框中的包源之间的更改不会更新活动源](http://nuget.codeplex.com/workitem/344)
* [删除程序包管理器控制台窗口的键绑定](http://nuget.codeplex.com/workitem/339)
* [安装包未被识别为 cmdlet 的名称 .。。](http://nuget.codeplex.com/workitem/338)
* [从本地源安装包未解析常规源上的依赖项](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies 应跳过仍在使用的依赖项](http://nuget.codeplex.com/workitem/331)
* [如果取消页面导航，则当原始页面请求返回时，用户无法导航到其他页面](http://nuget.codeplex.com/workitem/325)
* [调查 NuPack 的性能，以便为具有大量包的源提供服务。](http://nuget.codeplex.com/workitem/324)
* [第二次筛选包时，它将使用 "新" 包源，而不是以前选择的源。](http://nuget.codeplex.com/workitem/321)
* [选择对话框上的 "联机" 选项卡时，应选择默认的包源。](http://nuget.codeplex.com/workitem/320)
* [默认情况下，列表包应显示已安装的包](http://nuget.codeplex.com/workitem/309)
* [程序集引用 HintPaths](http://nuget.codeplex.com/workitem/294)
* [打开程序包管理器控制台时出现异常](http://nuget.codeplex.com/workitem/268)
* [控制台 intellisense 下载整个源](http://nuget.codeplex.com/workitem/259)
* ["Default" 包源应重命名为 "Active"](http://nuget.codeplex.com/workitem/258)
* [包源 UI：如果名称/源字段非空，请按 "确定" 以添加新源](http://nuget.codeplex.com/workitem/257)
* [当已安装的包的数量较大时，对话框变慢](http://nuget.codeplex.com/workitem/243)
* [支持强名称程序集的绑定重定向](http://nuget.codeplex.com/workitem/238)
* [添加包引用 .。。用于包含包源的下拉的 UI](http://nuget.codeplex.com/workitem/226)
* [NuPack 需要支持配置文件名称的配置转换 agnostically](http://nuget.codeplex.com/workitem/224)
* [允许在 NuPack.exe中重写 BasePath ](http://nuget.codeplex.com/workitem/222)
* [包源回退行为](http://nuget.codeplex.com/workitem/204)
* [GUI 崩溃](http://nuget.codeplex.com/workitem/201)
* [添加排序选项以添加包对话框](http://nuget.codeplex.com/workitem/179)
* [用于清除程序包管理器控制台的快捷键](http://nuget.codeplex.com/workitem/174)
* [PowerConsole 导致 NuPack 控制台失败](http://nuget.codeplex.com/workitem/166)
* [控制台和 "添加包" 对话框应在请求中设置用户代理](http://nuget.codeplex.com/workitem/141)
* [在生成中设置 VSIX 和 NuPack.exe 的版本号。](http://nuget.codeplex.com/workitem/134)
* [从-？隐藏公共 PowerShell 参数](http://nuget.codeplex.com/workitem/118)
* [为控制台命令添加详细帮助](http://nuget.codeplex.com/workitem/110)
* ["添加包" 对话框应该允许选择当前包源](http://nuget.codeplex.com/workitem/88)
* [将 NuPack 类移到不同的命名空间](http://nuget.codeplex.com/workitem/50)
* [向 cmdlet 添加帮助](http://nuget.codeplex.com/workitem/23)
* [下载包后验证源中的哈希](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

下面是 CTP 2 中最重要的更改：

* 将包源从 ATOM 切换到 OData 服务终结点：如果升级到 CTP2 版本的 NuGet，请确保将以下 URL 作为包源添加： `https://feed.nuget.org/ctp2/odata/v1/` 。
* 将 Add-Package 命令重命名为 *安装包*。
* 已更新 `.nuspec` 格式。 `.nuspec`现在，格式包括用于指定 32x32 png 图标的 *iconUrl* 字段，该图标将显示在 "添加包" 对话框中。 因此，请确保将其设置为区分包。 此 `.nuspec` 格式还包含新的 *projectUrl* 字段，可用于指向提供有关包的详细信息的网页。

此生成不适用于旧 `.nupkg` 文件。 如果收到空引用异常，则使用的是旧 `.nupkg` 文件，需要使用更新后的 [NuGet 命令行工具](http://nuget.codeplex.com/releases/52017/download/165468)重新生成它。

下面列出了针对 NuGet CTP 2 修复的功能和 bug， (不包括次代码清理等的 bug ) 。

* [为程序集指定 TargetFramework 时，解压缩包程序集时出错。](http://nuget.codeplex.com/workitem/10)
* [使 NuPack 控制台窗口更易发现](http://nuget.codeplex.com/workitem/14)
* [ILMerge nupack.exe 版本](http://nuget.codeplex.com/workitem/19)
* [更好的错误/异常处理](http://nuget.codeplex.com/workitem/24)
* [[Nupack]： PackageManager 应适当处理与源相关的错误](http://nuget.codeplex.com/workitem/28)
* [需要控制台的新图标](http://nuget.codeplex.com/workitem/29)
* [在对话框中本地化字符串](http://nuget.codeplex.com/workitem/38)
* [NuPack 在内存中缓存下载的 NuPack 文件](http://nuget.codeplex.com/workitem/40)
* [NuPack 控制台：更改显示控制台的默认快捷方式](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem 应支持通用属性的默认值](http://nuget.codeplex.com/workitem/49)
* [仅使用一个 nuspec 文件在文件夹中运行 nupack.exe 应使用该 nuspec](http://nuget.codeplex.com/workitem/52)
* [即使没有加载任何项目/解决方案，"项目" 菜单也会显示](http://nuget.codeplex.com/workitem/54)
* [在基本代码的干净克隆上生成 .cmd 失败](http://nuget.codeplex.com/workitem/56)
* [更新可用功能](http://nuget.codeplex.com/workitem/57)
* [对话框：通过对话框添加包将删除控制台中的提示](http://nuget.codeplex.com/workitem/73)
* [通过单击 "安装" 添加包的速度通常较慢，无可视反馈](http://nuget.codeplex.com/workitem/80)
* [无法发现哪些已安装的包有更新。](http://nuget.codeplex.com/workitem/82)
* [无法在对话框中更新已安装的包。](http://nuget.codeplex.com/workitem/83)
* [无法在对话框中卸载已安装的包](http://nuget.codeplex.com/workitem/84)
* [&ldquo;添加包引用 &hellip; &rdquo; 出现在已安装的引用的上下文菜单上](http://nuget.codeplex.com/workitem/85)
* [从控制台更新包后，它会将旧版本和新版本显示为已安装](http://nuget.codeplex.com/workitem/86)
* [使用对话框时，控制台中的活动会在使用后消失](http://nuget.codeplex.com/workitem/87)
* [清理 nupack.exe中的命令行分析 ](http://nuget.codeplex.com/workitem/89)
* [将友好名称添加到包源](http://nuget.codeplex.com/workitem/98)
* [要支持包括包图标的 nuspec](http://nuget.codeplex.com/workitem/103)
* [源 UI 不允许复制 URL](http://nuget.codeplex.com/workitem/105)
* [更好的删除包错误处理。](http://nuget.codeplex.com/workitem/107)
* [在控制台窗口中键入依赖于游标焦点](http://nuget.codeplex.com/workitem/112)
* [错误消息的外观](http://nuget.codeplex.com/workitem/116)
* [未安装的包的 Remove-Package 性能不佳](http://nuget.codeplex.com/workitem/117)
* [如果没有包源，则删除包会失败](http://nuget.codeplex.com/workitem/119)
* [当包源不可用时，删除包失败](http://nuget.codeplex.com/workitem/120)
* [将标题添加到包元数据和源。](http://nuget.codeplex.com/workitem/125)
* [将-Source 参数添加回添加包](http://nuget.codeplex.com/workitem/127)
* [列表-包应具有-Source 参数](http://nuget.codeplex.com/workitem/128)
* [更新 NuPack 以要求 NuPack 用户代理下载包](http://nuget.codeplex.com/workitem/142)
* ["许可证接受" 对话框必须列出所有需要接受的依赖项的许可证](http://nuget.codeplex.com/workitem/145)
* [在源中引发包时记录错误](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe 不应允许空的 &lt; licenseurl &gt; 元素](http://nuget.codeplex.com/workitem/152)
* [将 List-Package 重命名为获取包，Add-Package 安装包，并将 Remove-Package 为卸载包](http://nuget.codeplex.com/workitem/155)
* [使用解决方案导航器中的 "添加包引用" 菜单项导致 Visual Studio 崩溃](http://nuget.codeplex.com/workitem/158)
* ["可用的包源" 标签缺少冒号](http://nuget.codeplex.com/workitem/160)
* [使. nuspec xml 元素大小写一致大小写](http://nuget.codeplex.com/workitem/161)
* [NuPack VSIX 的清单需要启用 "admin" 位](http://nuget.codeplex.com/workitem/162)
* [如果运行不带源的 List-Package，则会出现 null 引用错误](http://nuget.codeplex.com/workitem/164)
* [nuget.exe：指定目标路径](http://nuget.codeplex.com/workitem/171)
* [在 WinXP 上打开包管理控制台时出现 Powershell 错误](http://nuget.codeplex.com/workitem/175)
* [尝试加载包列表时 VS 崩溃](http://nuget.codeplex.com/workitem/176)
* [允许元包不 (文件，仅) 依赖项 ](http://nuget.codeplex.com/workitem/180)
* [将 Powershell 脚本转换为 Powershell 2.0 模块](http://nuget.codeplex.com/workitem/181)
* [指定 target 后，PathResolver 应丢弃前面的通配符字符的路径部分](http://nuget.codeplex.com/workitem/183)
* [无依赖项](http://nuget.codeplex.com/workitem/186)
* [安装 Elmah 时出错](http://nuget.codeplex.com/workitem/192)
* [使用 configsections 无法正常使用配置转换 &lt;&gt;](http://nuget.codeplex.com/workitem/194)
* [无法检索变量 "$global:p rojectCache"，因为它尚未设置](http://nuget.codeplex.com/workitem/203)
* [添加用于创建 NuPack 包的 MSBuild 任务](http://nuget.codeplex.com/workitem/205)
* [列表-包需要支持搜索/筛选](http://nuget.codeplex.com/workitem/206)
* [如果包作者提供许可证 URL，则始终显示许可证的链接](http://nuget.codeplex.com/workitem/208)
* [使用删除包偶尔出现 "拒绝访问" 异常](http://nuget.codeplex.com/workitem/213)
* [失败的单元测试： InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [如果找不到针对特定 framework 版本，则允许使用回退/默认文件集](http://nuget.codeplex.com/workitem/223)
* [添加包引用 .。。UI 无法删除包](http://nuget.codeplex.com/workitem/225)
* [卸载一个或多个项目时添加包引用崩溃 studio](http://nuget.codeplex.com/workitem/228)
* [配置转换似乎不适用于 web.debug.config 文件](http://nuget.codeplex.com/workitem/229)
* [ 不会在自定义包上触发init.ps1](http://nuget.codeplex.com/workitem/237)
* [将路径添加到 feedlist 时，默认按钮设置为 "确定"，因此，如果我按 ENTER 自动关闭](http://nuget.codeplex.com/workitem/240)
* [尝试卸载依赖项将崩溃，并在行中尝试2次](http://nuget.codeplex.com/workitem/241)
* [在 "添加包" 对话框中显示项目 URL](http://nuget.codeplex.com/workitem/253)
* [默认情况下，Add-Package 对话框安装到已安装的包](http://nuget.codeplex.com/workitem/254)
* [更改 "添加包" 对话框菜单项。](http://nuget.codeplex.com/workitem/261)
* [重命名命名空间和程序集](http://nuget.codeplex.com/workitem/274)
* [将 NuPack 项目重命名为 NuGet](http://nuget.codeplex.com/workitem/282)
* [将以下文本添加到依赖项列表下](http://nuget.codeplex.com/workitem/288)
* [在 "许可证接受" 对话框中更改许可证接受文本](http://nuget.codeplex.com/workitem/291)
* [更改包列表上方的 "许可证接受" 对话框中的文本](http://nuget.codeplex.com/workitem/292)
* [OData 不适用于 fwlink URL](http://nuget.codeplex.com/workitem/304)
* [包管理器 UI：通过积极缓存用于分页的包计数](http://nuget.codeplex.com/workitem/317)
* [NuPack/NuGet- &gt; 程序包管理器控制台错误](http://nuget.codeplex.com/workitem/335)
* ["添加包" 对话框显示已安装包的许可证接受情况](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

下面列出了针对 NuGet CTP 1 修复的功能和 bug。

* [包扩展应重命名为。 nupack](http://nuget.codeplex.com/workitem/1)
* [将包文件移动到文件夹](http://nuget.codeplex.com/workitem/2)
* [合并安装 &amp; 添加 PS 命令](http://nuget.codeplex.com/workitem/3)
* [为 Verb-Noun cmdlet 创建别名](http://nuget.codeplex.com/workitem/4)
* [在 VS 中切换解决方案时，NuPack 混淆](http://nuget.codeplex.com/workitem/6)
* [默认情况下，应隐藏 "包" 解决方案文件夹](http://nuget.codeplex.com/workitem/11)
* [添加对内容项中的标记替换的支持。](http://nuget.codeplex.com/workitem/12)
* [NuPack 应使用 Register-packagesource API](http://nuget.codeplex.com/workitem/26)
* [[Nupack]： PackageManager 在安装包之前将它们标记为已安装](http://nuget.codeplex.com/workitem/27)
* [从解决方案中删除默认项目仍会将已删除的项目显示为默认项目](http://nuget.codeplex.com/workitem/30)
* [新包失败，出现 "无法为指定的 URI 添加部分，因为它已在包中"。](http://nuget.codeplex.com/workitem/32)
* [从 Visual Studio GUI 中删除 "NuPack" 字符串](http://nuget.codeplex.com/workitem/35)
* [将 Apache 标头添加到 COPYRIGHT.txt 文件](http://nuget.codeplex.com/workitem/36)
* [删除 Update-PackageSource 命令](http://nuget.codeplex.com/workitem/37)
* [加载配置文件时程序包管理器不可用引发异常](http://nuget.codeplex.com/workitem/39)
* [init.ps1，install.ps1 和 uninstall.ps1 需要接收附加状态](http://nuget.codeplex.com/workitem/41)
* [将控制台和 GUI 包合并到一个包中](http://nuget.codeplex.com/workitem/42)
* [如果应用于不在根位置的 XML，则 Xml 转换逻辑不起作用](http://nuget.codeplex.com/workitem/43)
* [管理包源设置对话框未更新 NuPack 控制台](http://nuget.codeplex.com/workitem/44)
* [NuPack 控制台 UI：将 "包源" 下拉列表重命名为 "包源"](http://nuget.codeplex.com/workitem/45)
* [NuPack 控制台选项：将 "存储库 UI" 重命名为与 NuPack 控制台一致](http://nuget.codeplex.com/workitem/46)
* [对于从 IIS 或 URL 打开的网站，添加包失败](http://nuget.codeplex.com/workitem/53)
* [程序包管理器源不适用于 FwLink](http://nuget.codeplex.com/workitem/55)
* [设置默认包源](http://nuget.codeplex.com/workitem/59)
* [如果在选项中添加包源，则仅提供一个源时，假定它是默认值。](http://nuget.codeplex.com/workitem/60)
* [对话框 UI 显示虚假的 "最近的" 包](http://nuget.codeplex.com/workitem/62)
* [选项：单击 "取消" 不会取消更改](http://nuget.codeplex.com/workitem/63)
* [添加包引用对话框搜索应该不区分大小写](http://nuget.codeplex.com/workitem/65)
* [修复 AssemblyInfo.cs 文件中的公司元数据](http://nuget.codeplex.com/workitem/67)
* [VSIX 的版本号](http://nuget.codeplex.com/workitem/71)
* [删除包：使用-？显示帮助两次](http://nuget.codeplex.com/workitem/72)
* [执行项目级包的安装/卸载包](http://nuget.codeplex.com/workitem/74)
* [服务器无法在验证失败时创建源 nupack](http://nuget.codeplex.com/workitem/90)
* [需要替换 NuPack 图标](http://nuget.codeplex.com/workitem/94)
* [NTLM http 代理不对包源进行身份验证。](http://nuget.codeplex.com/workitem/96)
* [对话框并不总是在 VS 窗口中居中](http://nuget.codeplex.com/workitem/100)
* [包中的许多字段未在对话框中填充](http://nuget.codeplex.com/workitem/102)
* [对话框 UI 不显示作者姓名](http://nuget.codeplex.com/workitem/108)
* [原因-删除包的版本](http://nuget.codeplex.com/workitem/113)
* [删除对话框 UI 上的 "最近" 选项卡](http://nuget.codeplex.com/workitem/115)
* [当在对话框 UI 至少打开一次后右键单击解决方案文件夹时，VS 崩溃。](http://nuget.codeplex.com/workitem/126)
* [将 List-Package 的本地参数更改为-已安装](http://nuget.codeplex.com/workitem/129)
* [将 packages.xml 重命名为 NuPack.config](http://nuget.codeplex.com/workitem/132)
* [控制台强制将光标移到行尾](http://nuget.codeplex.com/workitem/135)
* [删除-包 intellisense 已中断](http://nuget.codeplex.com/workitem/136)
* [向 nuspec 和源添加 RequireLicenseAcceptance 标志](http://nuget.codeplex.com/workitem/137)
* [将 LicenseUrl 添加到 nuspec 格式和包源](http://nuget.codeplex.com/workitem/138)
* [单击 "安装" 需要接受的包应显示 "接受" 对话框](http://nuget.codeplex.com/workitem/139)
* [将免责声明文本添加到 "添加包" 对话框](http://nuget.codeplex.com/workitem/140)
* [首次运行包控制台时添加声明](http://nuget.codeplex.com/workitem/143)
* [在控制台中安装包后显示声明](http://nuget.codeplex.com/workitem/144)
* [将 nupack 扩展名重命名为 nupkg。](http://nuget.codeplex.com/workitem/146)