---
title: NuGet 1.0 和 1.1 版发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 1.1 发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6222a996f2fdcaaa81a1b16d1c6da2749936712a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547016"
---
# <a name="nuget-10-and-11-release-notes"></a>NuGet 1.0 和 1.1 版发行说明

[NuGet 1.2 发行说明](../release-notes/nuget-1.2.md)

NuGet 1.0 已于 2011 年 1 月 13 日发布。  NuGet 1.1 已于 2011 年 2 月 12 日发布。

## <a name="overview"></a>概述

本文档包含各种版本的 NuGet 1.0 分组根据主要预览版本的发行说明。

NuGet 包括以下组件：

* *NuGet.Tools.vsix* * 组成：
  * **添加库包对话框*** 对话框用于浏览和安装包的 Visual Studio 中。
  * **包管理器控制台*** Powershell 基于 Visual Studio 中的控制台。
* *NuGet 命令行工具** 工具用于创建 （并最终发布） 包。

NuGet 工具 Visual Studio 扩展 (*NuGet.Tools.vsix*) 要求：

* Visual Studio 2010 或 Visual Web Developer 2010 速成版。

NuGet 命令行工具需要：

* .NET framework 版本 4

## <a name="installation"></a>安装

若要使用此[最新版本](http://nuget.codeplex.com/releases/view/52018):

* 首先卸载较旧版本。 您需要以管理员身份来执行此操作运行 VS。
* 你拥有的所有现有源中删除。
* 添加新的订阅源指向[ http://go.microsoft.com/fwlink/?LinkId=206669 ](http://go.microsoft.com/fwlink/?LinkId=206669)。

## <a name="nuget-11"></a>NuGet 1.1

在此版本中修复的问题列表[可在此处找到](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

自从 RC 以来 rtm 修复一个问题。

* [问题 474： 删除包影响解决方案中的所有项目](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>候选发布版本

以下是自 CTP 2 此 Release Candidate 中所做的更改。 问题跟踪程序来查看 bug 的完整列表，请访问。

* [更新包从控制台不会更新依赖项。](http://nuget.codeplex.com/workitem/443)
* [添加包提取 bin 不包引用 (CTP1)](http://nuget.codeplex.com/workitem/442)
* [更新包离开损坏的引用](http://nuget.codeplex.com/workitem/440)
* [获取包的更新失败，在对话框中，或在控制台中选择全部聚合的源](http://nuget.codeplex.com/workitem/439)
* [获取包验证错误](http://nuget.codeplex.com/workitem/426)
* [不能从添加包对话框安装包时，用户则发出警告](http://nuget.codeplex.com/workitem/425)
* [获取包的更新，则会引发更新大量的包时](http://nuget.codeplex.com/workitem/424)
* [提高时 nuspec 文件编写错误的错误处理](http://nuget.codeplex.com/workitem/423)
* [Nuget pack 忽略指定的文件](http://nuget.codeplex.com/workitem/422)
* [删除第二个至最后一个包源，然后单击"下移"崩溃 VS](http://nuget.codeplex.com/workitem/418)
* [安装包时移除程序集引用](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException 时打开设置对话框](http://nuget.codeplex.com/workitem/411)
* [在包管理器控制台中的包源的访问键不起作用](http://nuget.codeplex.com/workitem/410)
* [NuGet VS 设置对话框的访问键将焦点移动到错误的字段](http://nuget.codeplex.com/workitem/409)
* [包 ID intellisense 不应查询项太多](http://nuget.codeplex.com/workitem/404)
* [将包添加到项目名称中的圆点字符的项目失败](http://nuget.codeplex.com/workitem/403)
* [Nuspec 中的指定文件的问题](http://nuget.codeplex.com/workitem/400)
* [使用更新版本时，应获取注册正确的官方源](http://nuget.codeplex.com/workitem/399)
* [标记应使用空格而不是 #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata 缺少某些有用的信息](http://nuget.codeplex.com/workitem/388)
* [向对话框添加报告滥用行为链接](http://nuget.codeplex.com/workitem/386)
* [使用 App_Data 来解压缩包在 Visual Studio 中的分页符](http://nuget.codeplex.com/workitem/380)
* [实现标记](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder 允许没有依赖项创建的空包](http://nuget.codeplex.com/workitem/373)
* [添加包的所有者字段](http://nuget.codeplex.com/workitem/365)
* [更新要说 NuGet 包管理器而不是 VSIX 工具的 VSIX 清单](http://nuget.codeplex.com/workitem/364)
* [获取包命令将引发错误时选中全部源](http://nuget.codeplex.com/workitem/359)
* [允许进行排序的选项对话框中的包源](http://nuget.codeplex.com/workitem/356)
* [更新包不会删除较旧版本](http://nuget.codeplex.com/workitem/352)
* [依赖项的实现版本范围规范](http://nuget.codeplex.com/workitem/347)
* [单击"添加新的包"时，visual Studio 崩溃](http://nuget.codeplex.com/workitem/346)
* [在添加包对话框中显示的下载和评级](http://nuget.codeplex.com/workitem/345)
* [在对话框中的包源之间的更改不会更新活动的源](http://nuget.codeplex.com/workitem/344)
* [删除包管理器控制台窗口的键绑定](http://nuget.codeplex.com/workitem/339)
* [安装包未被识别为 cmdlet 名称...](http://nuget.codeplex.com/workitem/338)
* [从本地上正则馈送源依赖项安装包将不解析](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies 应跳过仍在使用的依赖项](http://nuget.codeplex.com/workitem/331)
* [如果正在取消页面导航，用户无法导航到其他页面而原始页请求返回](http://nuget.codeplex.com/workitem/325)
* [调查性能 NuPack.Server 向源提供大量的包。](http://nuget.codeplex.com/workitem/324)
* [包的第二个时间筛选它使用"新建"包源，而不是以前选定的源。](http://nuget.codeplex.com/workitem/321)
* [选择对话框上的"联机"选项卡时，应选择默认包源。](http://nuget.codeplex.com/workitem/320)
* [默认情况下，列表包应显示已安装的包](http://nuget.codeplex.com/workitem/309)
* [程序集引用 HintPaths](http://nuget.codeplex.com/workitem/294)
* [打开程序包管理器控制台时出现异常](http://nuget.codeplex.com/workitem/268)
* [控制台 intellisense 下载整个源](http://nuget.codeplex.com/workitem/259)
* [Default 包源应重命名为 'Active'](http://nuget.codeplex.com/workitem/258)
* [包源 UI： 按确定应添加新的源，如果名称/源字段都为非空](http://nuget.codeplex.com/workitem/257)
* [当已安装的包很大，对话框就非常慢](http://nuget.codeplex.com/workitem/243)
* [支持的强名称程序集绑定重定向](http://nuget.codeplex.com/workitem/238)
* [添加包引用...UI 包源包括向下的下拉](http://nuget.codeplex.com/workitem/226)
* [NuPack 需要支持的配置文件名称 agnostically 配置转换](http://nuget.codeplex.com/workitem/224)
* [允许 BasePath NuPack.exe 中重写](http://nuget.codeplex.com/workitem/222)
* [包源回退行为](http://nuget.codeplex.com/workitem/204)
* [有关 GUI 崩溃](http://nuget.codeplex.com/workitem/201)
* [添加排序选项添加包对话框](http://nuget.codeplex.com/workitem/179)
* [快捷方式键以清除包管理器控制台](http://nuget.codeplex.com/workitem/174)
* [PowerConsole 导致 NuPack 控制台失败](http://nuget.codeplex.com/workitem/166)
* [控制台和添加包对话框应在请求中设置用户代理](http://nuget.codeplex.com/workitem/141)
* [设置在生成的 VSIX 和 NuPack.exe 版本号。](http://nuget.codeplex.com/workitem/134)
* [隐藏从-常见的 PowerShell 参数？](http://nuget.codeplex.com/workitem/118)
* [添加-有关控制台命令的详细的帮助](http://nuget.codeplex.com/workitem/110)
* [添加包对话框应允许选择当前的包源](http://nuget.codeplex.com/workitem/88)
* [将 NuPack.Core 类移到不同的命名空间](http://nuget.codeplex.com/workitem/50)
* [添加到 cmdlet 的帮助](http://nuget.codeplex.com/workitem/23)
* [包下载后验证哈希从数据源](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

在 CTP 2 中所做的显著更改如下：

* 切换来自 ATOM 馈送到 OData 服务终结点的包： 如果您升级到 CTP2 版本的 NuGet，请确保将以下 URL 添加为包源： `https://feed.nuget.org/ctp2/odata/v1/`。
* 重命名为添加包命令*Install-package*。
* 更新`.nuspec`格式。 `.nuspec`格式现在包括*iconUrl*字段用于指定一个 32 x 32 png 图标，它将显示在添加包对话框。 因此请确保设置，若要区分你的包。 `.nuspec`格式还包括新*projectUrl*字段可用于指向一个网页，提供了有关包的详细信息。

此生成不会使用旧`.nupkg`文件。 如果收到空引用异常，则表示使用旧`.nupkg`文件，并需要使用更新后重建[NuGet 命令行工具](http://nuget.codeplex.com/releases/52017/download/165468)。

下面是一系列功能和的 NuGet CTP 2 （不包括 bug 的细微代码清理等）。 已修复的 bug。

* [错误解包的包程序集时指定的程序集 TargetFramework。](http://nuget.codeplex.com/workitem/10)
* [使 NuPack 控制台窗口更容易地发现](http://nuget.codeplex.com/workitem/14)
* [ILMerge nupack.exe 版本](http://nuget.codeplex.com/workitem/19)
* [更好的错误/异常处理](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager 应妥善处理与源相关的错误](http://nuget.codeplex.com/workitem/28)
* [为控制台需要新图标](http://nuget.codeplex.com/workitem/29)
* [在对话框中的字符串本地化](http://nuget.codeplex.com/workitem/38)
* [NuPack 缓存在内存中的.nupack 文件下载](http://nuget.codeplex.com/workitem/40)
* [NuPack 控制台： 更改用于显示控制台的默认快捷方式](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem 应支持常见属性的默认值](http://nuget.codeplex.com/workitem/49)
* [使用一个 nuspec 文件的文件夹中运行 nupack.exe 应使用该 nuspec](http://nuget.codeplex.com/workitem/52)
* [甚至在加载任何项目/解决方案时出现项目菜单](http://nuget.codeplex.com/workitem/54)
* [build.cmd 干净代码库的克隆上失败](http://nuget.codeplex.com/workitem/56)
* [更新可用的功能](http://nuget.codeplex.com/workitem/57)
* [对话框： 添加包对话框中通过在控制台中删除提示](http://nuget.codeplex.com/workitem/73)
* [通过单击安装来添加包通常较慢，没有视觉反馈](http://nuget.codeplex.com/workitem/80)
* [没有方法来发现其中我已安装的包已更新。](http://nuget.codeplex.com/workitem/82)
* [没有方法来更新该对话框中的已安装的程序包。](http://nuget.codeplex.com/workitem/83)
* [无法卸载该对话框中的已安装的包](http://nuget.codeplex.com/workitem/84)
* [&ldquo;添加包引用&hellip;&rdquo;出现在上下文菜单中的已安装的引用](http://nuget.codeplex.com/workitem/85)
* [在更新后从控制台的包，它显示在旧版本和新版本安装](http://nuget.codeplex.com/workitem/86)
* [在控制台中，当使用对话框中，活动使用后消失](http://nuget.codeplex.com/workitem/87)
* [清除命令行中 nupack.exe 分析](http://nuget.codeplex.com/workitem/89)
* [将友好名称添加到包源](http://nuget.codeplex.com/workitem/98)
* [更新.nuspec 以支持包括包图标](http://nuget.codeplex.com/workitem/103)
* [源用户界面不允许复制 URL](http://nuget.codeplex.com/workitem/105)
* [更好的删除包错误处理。](http://nuget.codeplex.com/workitem/107)
* [在控制台窗口中键入内容取决于游标焦点](http://nuget.codeplex.com/workitem/112)
* [错误消息看起来很多次](http://nuget.codeplex.com/workitem/116)
* [未安装的包删除包的性能已损坏](http://nuget.codeplex.com/workitem/117)
* [删除包失败时没有任何包源](http://nuget.codeplex.com/workitem/119)
* [删除包失败的包源不可用时](http://nuget.codeplex.com/workitem/120)
* [添加到包元数据和源的标题。](http://nuget.codeplex.com/workitem/125)
* [添加回添加包的源参数](http://nuget.codeplex.com/workitem/127)
* [列表包都应具有的源参数](http://nuget.codeplex.com/workitem/128)
* [更新 NuPack.Server 需要 NuPack 用户代理到下载包](http://nuget.codeplex.com/workitem/142)
* [许可证接受对话框必须列出所有依赖项，需要接受许可证](http://nuget.codeplex.com/workitem/145)
* [记录错误时引发的源中的包](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe 不应该允许一个空&lt;licenseurl&gt;元素](http://nuget.codeplex.com/workitem/152)
* [列表包重命名到 Get 的包中，添加的包安装包和删除包卸载包](http://nuget.codeplex.com/workitem/155)
* [使用解决方案导航器中的添加包引用菜单项使 Visual Studio 崩溃](http://nuget.codeplex.com/workitem/158)
* ["可用的包源"标签缺少冒号](http://nuget.codeplex.com/workitem/160)
* [使.nuspec xml 元素的大小写一致地 camel 大小写](http://nuget.codeplex.com/workitem/161)
* [需要打开 admin 的位 NuPack VSIX 的清单](http://nuget.codeplex.com/workitem/162)
* [如果使用没有源运行列表包，则会为 null 引用错误](http://nuget.codeplex.com/workitem/164)
* [nuget.exe： 指定目标路径](http://nuget.codeplex.com/workitem/171)
* [打开包管理控制台上 WinXP 的 Powershell 错误](http://nuget.codeplex.com/workitem/175)
* [尝试加载包列表时 VS 崩溃](http://nuget.codeplex.com/workitem/176)
* [允许元包 （无文件，仅依赖项）](http://nuget.codeplex.com/workitem/180)
* [将 Powershell 脚本转换为 Powershell 2.0 模块](http://nuget.codeplex.com/workitem/181)
* [当指定为目标时，PathResolver 应放弃路径部分前面通配符字符](http://nuget.codeplex.com/workitem/183)
* [没有依赖关系](http://nuget.codeplex.com/workitem/186)
* [安装 Elmah 时出错](http://nuget.codeplex.com/workitem/192)
* [配置转换不正常使用&lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [变量 $global: projectCache 无法检索，因为尚未设置](http://nuget.codeplex.com/workitem/203)
* [添加用于创建 NuPack 包的 MSBuild 任务](http://nuget.codeplex.com/workitem/205)
* [列出程序包需要支持搜索/筛选](http://nuget.codeplex.com/workitem/206)
* [始终显示许可证的链接如果包的作者提供了一个许可证 URL](http://nuget.codeplex.com/workitem/208)
* [使用删除包偶尔"拒绝访问"异常](http://nuget.codeplex.com/workitem/213)
* [单元测试失败： InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [允许回退/默认组文件，如果找不到特定 framework 版本](http://nuget.codeplex.com/workitem/223)
* [添加包引用...UI 中不能删除包](http://nuget.codeplex.com/workitem/225)
* [添加包引用崩溃 studio 时一个或多个项目已卸载](http://nuget.codeplex.com/workitem/228)
* [配置转换似乎不处理 web.debug.config 文件](http://nuget.codeplex.com/workitem/229)
* [init.ps1 不触发自定义包](http://nuget.codeplex.com/workitem/237)
* [将路径添加到 feedlist 时, 的默认按钮设置为确定，因此如果我按 ENTER 会自动关闭](http://nuget.codeplex.com/workitem/240)
* [尝试卸载依赖关系会导致 VS 崩溃如果尝试在行中的 2 倍](http://nuget.codeplex.com/workitem/241)
* [在添加包对话框中显示项目 URL](http://nuget.codeplex.com/workitem/253)
* [默认为安装的程序包添加包对话框](http://nuget.codeplex.com/workitem/254)
* [更改包对话框中添加菜单项。](http://nuget.codeplex.com/workitem/261)
* [重命名命名空间和程序集](http://nuget.codeplex.com/workitem/274)
* [将 NuPack 项目重命名为 NuGet](http://nuget.codeplex.com/workitem/282)
* [添加依赖项的列表下的以下文本](http://nuget.codeplex.com/workitem/288)
* [将许可证接受对话框中的许可证接受文本](http://nuget.codeplex.com/workitem/291)
* [将上面的包的列表许可证接受对话框中的文本](http://nuget.codeplex.com/workitem/292)
* [OData 使用的 fwlink 的 URL 不起作用](http://nuget.codeplex.com/workitem/304)
* [包管理器 UI： 对包计数用于分页的主动缓存](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet-&gt;包管理器控制台错误](http://nuget.codeplex.com/workitem/335)
* [添加包对话框会显示许可接受有关已安装打包](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

下面是一系列功能和 NuGet CTP 1 已修复的 bug。

* [包扩展应重命名为.nupack](http://nuget.codeplex.com/workitem/1)
* [将包文件移动到文件夹](http://nuget.codeplex.com/workitem/2)
* [合并安装&amp;添加 PS 命令](http://nuget.codeplex.com/workitem/3)
* [为动词-名词 cmdlet 创建别名](http://nuget.codeplex.com/workitem/4)
* [在 VS 中切换解决方案时即用会混淆 NuPack](http://nuget.codeplex.com/workitem/6)
* [我们应默认情况下隐藏的包的解决方案文件夹](http://nuget.codeplex.com/workitem/11)
* [在内容项中添加支持标记替换。](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI 应使用 PackageSource API](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager 将包标记为已安装它们之前，安装](http://nuget.codeplex.com/workitem/27)
* [正在删除默认项目从解决方案仍显示为默认值已删除的项目](http://nuget.codeplex.com/workitem/30)
* [新包失败，出现"无法添加一部分为指定的 URI 因为它已在包中。"](http://nuget.codeplex.com/workitem/32)
* [从 Visual Studio GUI 中删除"NuPack"字符串](http://nuget.codeplex.com/workitem/35)
* [添加 COPYRIGHT.txt 到 Apache 标头文件](http://nuget.codeplex.com/workitem/36)
* [删除更新 PackageSource 命令](http://nuget.codeplex.com/workitem/37)
* [包管理器正在加载配置文件引发异常时不可用](http://nuget.codeplex.com/workitem/39)
* [init.ps1、 install.ps1 和 uninstall.ps1 需要接收其他状态](http://nuget.codeplex.com/workitem/41)
* [控制台和 GUI 包合并到一个包](http://nuget.codeplex.com/workitem/42)
* [如果应用到 XML 的不是根目录，Xml 转换逻辑不起作用](http://nuget.codeplex.com/workitem/43)
* [管理包源设置对话框未更新 NuPack 控制台](http://nuget.codeplex.com/workitem/44)
* [NuPack 控制台 UI： 重命名为包源的包源下拉列表](http://nuget.codeplex.com/workitem/45)
* [NuPack 控制台选项： 重命名存储库 UI，以与 NuPack 控制台保持一致](http://nuget.codeplex.com/workitem/46)
* [针对从 IIS 或 URL 打开一个网站添加包失败](http://nuget.codeplex.com/workitem/53)
* [包管理器源不使用 FwLink](http://nuget.codeplex.com/workitem/55)
* [设置默认包源](http://nuget.codeplex.com/workitem/59)
* [如果提供只有一个源时，请在选项中，添加包源，，假定它是默认值。](http://nuget.codeplex.com/workitem/60)
* [对话框用户界面显示了假"最近"的程序包](http://nuget.codeplex.com/workitem/62)
* [选项： 单击取消按钮不会取消更改](http://nuget.codeplex.com/workitem/63)
* [添加包引用对话框搜索不区分大小写](http://nuget.codeplex.com/workitem/65)
* [在 AssemblyInfo.cs 文件中修复公司元数据](http://nuget.codeplex.com/workitem/67)
* [VSIX 的版本号](http://nuget.codeplex.com/workitem/71)
* [删除包： 使用-？两次显示帮助](http://nuget.codeplex.com/workitem/72)
* [执行项目级包安装/卸载包](http://nuget.codeplex.com/workitem/74)
* [服务器无法验证一个 nupack 失败时创建源](http://nuget.codeplex.com/workitem/90)
* [需要替换 NuPack 图标](http://nuget.codeplex.com/workitem/94)
* [NTLM http 代理的身份验证不到包源。](http://nuget.codeplex.com/workitem/96)
* [该对话框不会始终居中窗口中启动 VS](http://nuget.codeplex.com/workitem/100)
* [不是在对话框中填充许多包详细信息中的字段](http://nuget.codeplex.com/workitem/102)
* [对话框 UI 不会显示作者的名称](http://nuget.codeplex.com/workitem/108)
* [为什么-删除包版本](http://nuget.codeplex.com/workitem/113)
* [删除对话框 UI 上的最近选项卡](http://nuget.codeplex.com/workitem/115)
* [VS 崩溃时正确打开对话框 UI 至少一个后单击解决方案文件夹。](http://nuget.codeplex.com/workitem/126)
* [更改列表包的本地参数到-安装](http://nuget.codeplex.com/workitem/129)
* [将 packages.xml 重命名为 NuPack.config](http://nuget.codeplex.com/workitem/132)
* [控制台强制光标到行尾](http://nuget.codeplex.com/workitem/135)
* [删除包 intellisense 会中断](http://nuget.codeplex.com/workitem/136)
* [将 RequireLicenseAcceptance 标记添加到.nuspec 和源](http://nuget.codeplex.com/workitem/137)
* [添加到.nuspec 格式和程序包的 LicenseUrl 源](http://nuget.codeplex.com/workitem/138)
* [单击安装需要接受的包应显示接受对话框](http://nuget.codeplex.com/workitem/139)
* [将免责声明文本添加到添加包对话框](http://nuget.codeplex.com/workitem/140)
* [添加免责声明时的包控制台首次运行](http://nuget.codeplex.com/workitem/143)
* [在控制台中安装包后显示的免责声明](http://nuget.codeplex.com/workitem/144)
* [将.nupack 扩展重命名为.nupkg](http://nuget.codeplex.com/workitem/146)