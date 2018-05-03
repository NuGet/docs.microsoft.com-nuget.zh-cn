---
title: NuGet 1.0 和 1.1 发行说明
description: 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 1.1 的发行说明。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a11248a96109c879946e7e28a50e7753b644f042
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-10-and-11-release-notes"></a>NuGet 1.0 和 1.1 发行说明

[NuGet 1.2 发行说明](../release-notes/nuget-1.2.md)

NuGet 1.0 已于 2011 年 1 月 13 日发布。  NuGet 1.1 已于 2011 年 2 月 12 日发布。

## <a name="overview"></a>概述

本文档包含 NuGet 1.0 可根据主要预览版本进行分组的各种版本的发行说明。

NuGet 包括以下组件：

* *NuGet.Tools.vsix* * 组成：
  * **添加库包对话框*** 用来浏览和安装包的 Visual Studio 中的对话框。
  * **程序包管理器控制台*** Powershell 基于 Visual Studio 中的控制台。
* *NuGet 命令行工具** 工具用于创建 （和最终发布） 包。

NuGet 工具的 Visual Studio 扩展 (*NuGet.Tools.vsix*) 要求：

* Visual Studio 2010 或 Visual Web Developer 2010 Express。

NuGet 命令行工具需要：

* .NET framework 版本 4

## <a name="installation"></a>安装

若要使用此[最新版本](http://nuget.codeplex.com/releases/view/52018):

* 先卸载较旧生成。 你需要以管理员身份为此运行 VS。
* 删除你具有的所有现有馈送。
* 添加新的订阅源指向[ http://go.microsoft.com/fwlink/?LinkId=206669 ](http://go.microsoft.com/fwlink/?LinkId=206669)。

## <a name="nuget-11"></a>NuGet 1.1

此版本中修复的问题列表[可在此处找到](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

一个问题已修复 RTM 以来 RC。

* [问题 474： 删除包影响解决方案中的所有项目](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>候选发布版

以下是以来 CTP 2 此候选发布版本中所做的更改。 问题跟踪程序，以查看 bug 的完整列表，请访问。

* [更新包从控制台不会更新依赖关系。](http://nuget.codeplex.com/workitem/443)
* [添加包选取 bin 不包参考 (CTP1)](http://nuget.codeplex.com/workitem/442)
* [更新程序包离开损坏的引用](http://nuget.codeplex.com/workitem/440)
* [获取包的更新无法正常工作，这是在对话框中，或在控制台中选择所有聚合的源](http://nuget.codeplex.com/workitem/439)
* [获取包验证错误](http://nuget.codeplex.com/workitem/426)
* [用户无法从包对话框中添加安装包时警告](http://nuget.codeplex.com/workitem/425)
* [获取包的更新包的数量大时，更新将引发](http://nuget.codeplex.com/workitem/424)
* [提高时 nuspec 文件编写错误的错误处理](http://nuget.codeplex.com/workitem/423)
* [Nuget 包将忽略指定的文件](http://nuget.codeplex.com/workitem/422)
* [删除第二个至最后一包源，然后单击"下移"崩溃 VS](http://nuget.codeplex.com/workitem/418)
* [安装包时移除程序集引用](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException 时打开设置对话框](http://nuget.codeplex.com/workitem/411)
* [在程序包管理器控制台中的程序包源的访问密钥不起作用](http://nuget.codeplex.com/workitem/410)
* [NuGet VS 设置对话框访问键将焦点移至错误字段](http://nuget.codeplex.com/workitem/409)
* [包 ID intellisense 应不会查询太多的项](http://nuget.codeplex.com/workitem/404)
* [将包添加到项目中的项目名称的圆点字符与失败](http://nuget.codeplex.com/workitem/403)
* [Nuspec 中指定文件的问题](http://nuget.codeplex.com/workitem/400)
* [使用较新的生成时，应获取注册正确官方源](http://nuget.codeplex.com/workitem/399)
* [标记应使用空格而不是 #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata 缺少的一些有用信息](http://nuget.codeplex.com/workitem/388)
* [将报告滥用行为链接添加到对话框](http://nuget.codeplex.com/workitem/386)
* [使用 App_Data 来解压缩包 Visual Studio 中的分隔线](http://nuget.codeplex.com/workitem/380)
* [实现标记](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder 允许没有依赖项，要创建空包](http://nuget.codeplex.com/workitem/373)
* [添加包的所有者字段](http://nuget.codeplex.com/workitem/365)
* [更新 VSIX 清单可以显示为 NuGet 包管理器，而不是 VSIX 工具](http://nuget.codeplex.com/workitem/364)
* [获取包命令将引发错误时将选择所有源](http://nuget.codeplex.com/workitem/359)
* [允许包源选项对话框中的数据排序](http://nuget.codeplex.com/workitem/356)
* [更新包不会删除较旧版本](http://nuget.codeplex.com/workitem/352)
* [依赖关系的的实现版本范围规范](http://nuget.codeplex.com/workitem/347)
* [单击"添加新的包"时，visual Studio 崩溃](http://nuget.codeplex.com/workitem/346)
* [在添加包对话框中显示下载和评级](http://nuget.codeplex.com/workitem/345)
* [在对话框中的包源之间更改不会获得更新活动的源](http://nuget.codeplex.com/workitem/344)
* [删除程序包管理器控制台窗口的键绑定](http://nuget.codeplex.com/workitem/339)
* [安装包未被识别为 cmdlet 的名称...](http://nuget.codeplex.com/workitem/338)
* [从本地上正则馈送源依赖项安装程序包未解决](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies 应跳过仍在使用的依赖关系](http://nuget.codeplex.com/workitem/331)
* [如果正在取消页面导航，用户不能导航到其他页面时原始页请求返回](http://nuget.codeplex.com/workitem/325)
* [调查 NuPack.Server 性能来处理具有大量包的源。](http://nuget.codeplex.com/workitem/324)
* [包的第二个时间筛选它使用"新建"包源，而不是以前选择的源。](http://nuget.codeplex.com/workitem/321)
* [选择对话框上的"联机"选项卡时，应选择默认的程序包源。](http://nuget.codeplex.com/workitem/320)
* [默认情况下，列表包应显示已安装的软件包](http://nuget.codeplex.com/workitem/309)
* [程序集引用 HintPaths](http://nuget.codeplex.com/workitem/294)
* [打开程序包管理器控制台时异常](http://nuget.codeplex.com/workitem/268)
* [控制台 intellisense 下载整个源](http://nuget.codeplex.com/workitem/259)
* [Default 包源应重命名为 'Active'](http://nuget.codeplex.com/workitem/258)
* [包源 UI： 按确定应添加新的源，如果名称/源字段都为非空](http://nuget.codeplex.com/workitem/257)
* [已安装的包的数量很大时，对话框变得非常缓慢](http://nuget.codeplex.com/workitem/243)
* [支持强名称程序集绑定重定向](http://nuget.codeplex.com/workitem/238)
* [添加程序包引用...UI，以包括包源向下拖放](http://nuget.codeplex.com/workitem/226)
* [NuPack 需要支持 agnostically 的配置文件名称的配置转换](http://nuget.codeplex.com/workitem/224)
* [允许 BasePath 要在 NuPack.exe 中的重写](http://nuget.codeplex.com/workitem/222)
* [包源回退行为](http://nuget.codeplex.com/workitem/204)
* [有关 GUI 崩溃](http://nuget.codeplex.com/workitem/201)
* [添加排序选项添加包对话框](http://nuget.codeplex.com/workitem/179)
* [要清除 Package Manager Console 快捷键](http://nuget.codeplex.com/workitem/174)
* [PowerConsole 导致 NuPack 控制台失败](http://nuget.codeplex.com/workitem/166)
* [控制台和添加包对话框应在请求中设置用户代理](http://nuget.codeplex.com/workitem/141)
* [在生成中设置的 VSIX 和 NuPack.exe 的版本号。](http://nuget.codeplex.com/workitem/134)
* [隐藏从-常见的 PowerShell 参数？](http://nuget.codeplex.com/workitem/118)
* [Add-有关控制台命令的详细的帮助](http://nuget.codeplex.com/workitem/110)
* [添加包对话框应允许选择的当前程序包源](http://nuget.codeplex.com/workitem/88)
* [将 NuPack.Core 类移到不同的命名空间](http://nuget.codeplex.com/workitem/50)
* [添加到 cmdlet 的帮助](http://nuget.codeplex.com/workitem/23)
* [包下载后验证从馈送的哈希](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

以下是在 CTP 2 中所做的最重大更改：

* 切换到 OData 服务终结点从 ATOM 馈送的包： 如果你升级到 CTP2 版本的 NuGet，请务必为程序包源中添加下面的 URL: `https://feed.nuget.org/ctp2/odata/v1/`。
* 重命名为添加程序包命令*安装包*。
* 更新`.nuspec`格式。 `.nuspec`格式现在包括*iconUrl*字段用于指定将仅显示在包对话框中添加一个 32 x 32 png 图标。 因此请务必设置，若要将你的包区分开来。 `.nuspec`格式还包括新*projectUrl*字段可以用于指向提供有关你的包的详细信息的网页。

此版本不会使用旧`.nupkg`文件。 获取空引用异常时，如果你使用的旧`.nupkg`文件，并需要重建与已更新[NuGet 命令行工具](http://nuget.codeplex.com/releases/52017/download/165468)。

以下是功能和的 NuGet CTP 2 （不包括 bug 的细微的代码清理等）。 已修复的 bug 的列表。

* [错误解包的包程序集时指定的程序集 TargetFramework。](http://nuget.codeplex.com/workitem/10)
* [NuPack 控制台窗口进行更容易地发现](http://nuget.codeplex.com/workitem/14)
* [ILMerge nupack.exe 版本](http://nuget.codeplex.com/workitem/19)
* [更好的错误/异常处理](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager 应妥善处理源相关的错误](http://nuget.codeplex.com/workitem/28)
* [为控制台需要新建图标](http://nuget.codeplex.com/workitem/29)
* [在对话框中的字符串本地化](http://nuget.codeplex.com/workitem/38)
* [NuPack 缓存下载.nupack 在内存中的文件](http://nuget.codeplex.com/workitem/40)
* [NuPack 控制台： 更改用于显示控制台的默认快捷方式](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem 应支持的公共属性的默认值](http://nuget.codeplex.com/workitem/49)
* [使用一个 nuspec 文件的文件夹中运行 nupack.exe 应使用该 nuspec](http://nuget.codeplex.com/workitem/52)
* [即使在加载没有项目/解决方案时将显示项目菜单](http://nuget.codeplex.com/workitem/54)
* [对基本代码的干净克隆 build.cmd 失败](http://nuget.codeplex.com/workitem/56)
* [更新可用功能](http://nuget.codeplex.com/workitem/57)
* [对话框： 添加包通过对话框中会删除提示在控制台中](http://nuget.codeplex.com/workitem/73)
* [通过单击安装来添加包通常速度慢，没有可视反馈](http://nuget.codeplex.com/workitem/80)
* [没有方法来发现哪些我已安装的程序包具有更新。](http://nuget.codeplex.com/workitem/82)
* [没有方法以更新对话框中的已安装的程序包。](http://nuget.codeplex.com/workitem/83)
* [无法卸载对话框中的安装的包](http://nuget.codeplex.com/workitem/84)
* [&ldquo;添加程序包引用&hellip;&rdquo;出现在上下文菜单中的已安装的引用](http://nuget.codeplex.com/workitem/85)
* [更新后从控制台的包，它显示了旧版本和最新版本为已安装](http://nuget.codeplex.com/workitem/86)
* [活动在控制台中，在使用对话框中，在使用后就会消失](http://nuget.codeplex.com/workitem/87)
* [清除命令行分析中 nupack.exe](http://nuget.codeplex.com/workitem/89)
* [将一个友好名称添加到包源](http://nuget.codeplex.com/workitem/98)
* [更新.nuspec 以支持包括包图标](http://nuget.codeplex.com/workitem/103)
* [源的 UI 不允许复制 URL](http://nuget.codeplex.com/workitem/105)
* [更好删除包的错误处理。](http://nuget.codeplex.com/workitem/107)
* [在控制台窗口中键入取决于游标焦点](http://nuget.codeplex.com/workitem/112)
* [错误消息查找很多次](http://nuget.codeplex.com/workitem/116)
* [删除包的包的未安装的性能已损坏](http://nuget.codeplex.com/workitem/117)
* [删除程序包失败时没有包源](http://nuget.codeplex.com/workitem/119)
* [失败的包源不存在时删除包](http://nuget.codeplex.com/workitem/120)
* [添加到包元数据和源的标题。](http://nuget.codeplex.com/workitem/125)
* [添加回添加包-源参数](http://nuget.codeplex.com/workitem/127)
* [列出程序包应有-源参数](http://nuget.codeplex.com/workitem/128)
* [更新 NuPack.Server 需要 NuPack 用户代理到下载更新包](http://nuget.codeplex.com/workitem/142)
* [许可证接受对话框必须对所有依赖项，要求用户接受列出许可证](http://nuget.codeplex.com/workitem/145)
* [在包源中引发时记录错误](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe 不应允许一个空&lt;licenseurl&gt;元素](http://nuget.codeplex.com/workitem/152)
* [将列出程序包重命名为 Get 包，添加的包安装包和删除包到卸载包](http://nuget.codeplex.com/workitem/155)
* [使用从解决方案导航器的添加程序包引用菜单项使 Visual Studio 崩溃](http://nuget.codeplex.com/workitem/158)
* ["可用包源"标签缺少冒号](http://nuget.codeplex.com/workitem/160)
* [请.nuspec xml 元素的大小写一致地 camel 大小写形式](http://nuget.codeplex.com/workitem/161)
* [NuPack VSIX 清单需要开启 admin 位](http://nuget.codeplex.com/workitem/162)
* [如果你运行了任何源的列表包，则出现 null ref 错误](http://nuget.codeplex.com/workitem/164)
* [nuget.exe： 指定目标路径](http://nuget.codeplex.com/workitem/171)
* [Powershell 错误打开 WinXP 上的包管理控制台](http://nuget.codeplex.com/workitem/175)
* [尝试加载包列表时的 VS 崩溃](http://nuget.codeplex.com/workitem/176)
* [允许元程序包 （没有文件，只有依赖关系）](http://nuget.codeplex.com/workitem/180)
* [将 Powershell 脚本转换为 Powershell 2.0 模块](http://nuget.codeplex.com/workitem/181)
* [指定目标时，PathResolver 应丢弃路径部分前面通配符字符](http://nuget.codeplex.com/workitem/183)
* [没有依赖关系](http://nuget.codeplex.com/workitem/186)
* [安装 Elmah 时出错](http://nuget.codeplex.com/workitem/192)
* [配置转换不正常使用&lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [变量 $全局： projectCache 无法检索，因为尚未设置](http://nuget.codeplex.com/workitem/203)
* [添加用于创建 NuPack 程序包的 MSBuild 任务](http://nuget.codeplex.com/workitem/205)
* [需要支持搜索/筛选列表程序包](http://nuget.codeplex.com/workitem/206)
* [始终为许可证显示一个链接，如果程序包作者提供了一个许可证 URL](http://nuget.codeplex.com/workitem/208)
* [使用删除包偶尔发生"拒绝访问"异常](http://nuget.codeplex.com/workitem/213)
* [未通过的单元测试： InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [如果找不到特定 framework 版本，允许回退/默认组的文件](http://nuget.codeplex.com/workitem/223)
* [添加程序包引用...UI 中不能删除包](http://nuget.codeplex.com/workitem/225)
* [添加程序包引用崩溃 studio 时一个或多个项目已卸载](http://nuget.codeplex.com/workitem/228)
* [配置转换似乎未处理 web.debug.config 文件](http://nuget.codeplex.com/workitem/229)
* [init.ps1 未触发上自定义包](http://nuget.codeplex.com/workitem/237)
* [将路径添加到 feedlist，默认按钮时将设置为确定，因此如果按下 enter 键会自动关闭](http://nuget.codeplex.com/workitem/240)
* [尝试卸载依赖关系将崩溃 VS，如果在行中尝试 2 次](http://nuget.codeplex.com/workitem/241)
* [在添加包对话框中显示项目 URL](http://nuget.codeplex.com/workitem/253)
* [默认安装的程序包添加包对话框](http://nuget.codeplex.com/workitem/254)
* [更改添加包对话框菜单项。](http://nuget.codeplex.com/workitem/261)
* [重命名命名空间和程序集](http://nuget.codeplex.com/workitem/274)
* [将 NuPack 项目重命名为 NuGet](http://nuget.codeplex.com/workitem/282)
* [添加以下文本下的依赖关系列表](http://nuget.codeplex.com/workitem/288)
* [更改许可证接受对话框中的许可证接受文本](http://nuget.codeplex.com/workitem/291)
* [更改包的列表上面许可证接受对话框中的文本](http://nuget.codeplex.com/workitem/292)
* [OData 不适用于 fwlink URL](http://nuget.codeplex.com/workitem/304)
* [通过用于分页的包计数的主动缓存的程序包管理器 UI:](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet-&gt;程序包管理器控制台错误](http://nuget.codeplex.com/workitem/335)
* [添加包对话框显示许可证接受为已安装打包](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

以下是功能和 NuGet CTP 1 已修复的 bug 的列表。

* [包扩展应重命名为.nupack](http://nuget.codeplex.com/workitem/1)
* [将包文件移到文件夹](http://nuget.codeplex.com/workitem/2)
* [合并安装&amp;添加 PS 命令](http://nuget.codeplex.com/workitem/3)
* [为动词-名词的 cmdlet 创建别名](http://nuget.codeplex.com/workitem/4)
* [在 VS 中切换解决方案时，获取混淆 NuPack](http://nuget.codeplex.com/workitem/6)
* [我们将默认情况下隐藏的包解决方案文件夹](http://nuget.codeplex.com/workitem/11)
* [在内容项添加标记替换的支持。](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI 应使用 PackageSource API](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager 会将包标记为安装它们之前，安装](http://nuget.codeplex.com/workitem/27)
* [删除默认项目从解决方案仍为默认值会显示已删除的项目](http://nuget.codeplex.com/workitem/30)
* [新包将会失败并"不能将部件添加为指定的 URI 因为它已在包中。"](http://nuget.codeplex.com/workitem/32)
* [从 Visual Studio GUI 中删除"NuPack"字符串](http://nuget.codeplex.com/workitem/35)
* [添加 COPYRIGHT.txt 到 Apache 标头文件](http://nuget.codeplex.com/workitem/36)
* [删除更新 PackageSource 命令](http://nuget.codeplex.com/workitem/37)
* [程序包管理器不可用，加载配置文件时将引发异常](http://nuget.codeplex.com/workitem/39)
* [init.ps1 install.ps1，uninstall.ps1 需要接收其他状态](http://nuget.codeplex.com/workitem/41)
* [将控制台和 GUI 包合并到一个包](http://nuget.codeplex.com/workitem/42)
* [Xml 转换逻辑不起作用，如果应用于文件夹不是根目录的 XML](http://nuget.codeplex.com/workitem/43)
* [管理包源设置对话框不更新 NuPack 控制台](http://nuget.codeplex.com/workitem/44)
* [NuPack 控制台用户界面： 重命名为包源的包源下拉列表](http://nuget.codeplex.com/workitem/45)
* [NuPack 控制台选项： 重命名存储库 UI，以与 NuPack 控制台保持一致](http://nuget.codeplex.com/workitem/46)
* [针对从 IIS 或 URL 已打开的网站添加包失败](http://nuget.codeplex.com/workitem/53)
* [程序包管理器源不能使用 FwLink](http://nuget.codeplex.com/workitem/55)
* [设置默认的程序包源](http://nuget.codeplex.com/workitem/59)
* [当提供只有一个源时，请在选项中，添加包源，则假定它是默认设置。](http://nuget.codeplex.com/workitem/60)
* [对话框用户界面显示了假"最近"的程序包](http://nuget.codeplex.com/workitem/62)
* [选项： 单击取消按钮不会取消更改](http://nuget.codeplex.com/workitem/63)
* [添加包引用对话框搜索应区分大小写](http://nuget.codeplex.com/workitem/65)
* [修复 AssemblyInfo.cs 文件中的公司元数据](http://nuget.codeplex.com/workitem/67)
* [Vsix 的版本号](http://nuget.codeplex.com/workitem/71)
* [删除包： 使用-？显示帮助两次](http://nuget.codeplex.com/workitem/72)
* [执行项目级别包安装/卸载包](http://nuget.codeplex.com/workitem/74)
* [服务器无法验证一个 nupack 失败时创建源](http://nuget.codeplex.com/workitem/90)
* [需要更换 NuPack 图标](http://nuget.codeplex.com/workitem/94)
* [NTLM http 代理的身份验证不到包源。](http://nuget.codeplex.com/workitem/96)
* [对话框不会始终为中心 VS 在窗口中启动](http://nuget.codeplex.com/workitem/100)
* [许多包详细信息中的字段不会被填充在对话框中](http://nuget.codeplex.com/workitem/102)
* [对话框 UI 不显示作者的名称](http://nuget.codeplex.com/workitem/108)
* [为什么-删除包的版本](http://nuget.codeplex.com/workitem/113)
* [删除对话框 UI 上的新选项卡](http://nuget.codeplex.com/workitem/115)
* [VS 崩溃时正确打开对话框 UI 至少一个后单击解决方案文件夹。](http://nuget.codeplex.com/workitem/126)
* [更改列表包-本地参数到-安装](http://nuget.codeplex.com/workitem/129)
* [将 packages.xml 重命名为 NuPack.config](http://nuget.codeplex.com/workitem/132)
* [控制台强制光标到行的末尾](http://nuget.codeplex.com/workitem/135)
* [删除包 intellisense 已中断](http://nuget.codeplex.com/workitem/136)
* [将 RequireLicenseAcceptance 标志添加到.nuspec 和源](http://nuget.codeplex.com/workitem/137)
* [添加 LicenseUrl.nuspec 格式和包源](http://nuget.codeplex.com/workitem/138)
* [单击需要接受的包的安装应显示接受对话框](http://nuget.codeplex.com/workitem/139)
* [将免责声明文本添加到添加包对话框](http://nuget.codeplex.com/workitem/140)
* [添加免责声明时包控制台运行第一次](http://nuget.codeplex.com/workitem/143)
* [在控制台中安装包后显示免责声明](http://nuget.codeplex.com/workitem/144)
* [将.nupack 扩展重命名为.nupkg](http://nuget.codeplex.com/workitem/146)