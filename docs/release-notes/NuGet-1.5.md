---
title: NuGet 1.5 的发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 1.5 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c2b549f65e675e5fde9ae1dfea3f44f7d691a86b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548720"
---
# <a name="nuget-15-release-notes"></a>NuGet 1.5 的发行说明

[NuGet 1.4 发行说明](../release-notes/nuget-1.4.md) | [NuGet 1.6 发行说明](../release-notes/nuget-1.6.md)

NuGet 1.5 已于 2011 年 8 月 30 日发布。

## <a name="features"></a>功能

### <a name="project-templates-with-preinstalled-nuget-packages"></a>使用预安装的 NuGet 包的项目模板
创建新的 ASP.NET MVC 3 项目模板时，项目中包含的 jQuery 脚本库实际上放在那里通过安装 NuGet 包。

ASP.NET MVC 3 项目模板包含一系列调用项目模板时已安装的 NuGet 包。 此功能包含 NuGet 包的项目模板现在是一项功能的 NuGet，_任何_项目模板现在可以充分利用。

有关此功能的详细信息，请参阅这[的功能的开发人员的博客文章](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)。

### <a name="explicit-assembly-references"></a>显式程序集引用

添加了新`<references />`用于显式指定的程序集内的元素应引用包。

例如，如果添加以下：

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

然后仅`xunit.dll`并`xunit.extensions.dll`将引用从相应[framework/配置文件的子文件夹](../reference/nuspec.md#explicit-assembly-references)的`lib`即使文件夹中没有其他程序集的文件夹。

如果省略此元素，则适用的常见行为，即引用中的每个程序集`lib`文件夹。

__此功能的用途是什么？__

此功能支持设计时只有程序集。 例如，在使用代码约定，则需要进行补充，以便 Visual Studio 可以找到它们，但协定程序集不应实际引用由项目并不会复制到运行时程序集旁协定程序集`bin`文件夹。

同样，该功能可以用于到如 XUnit 需要旁边运行时程序集，但从项目引用中排除其工具程序集的单元测试框架。

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>添加了排除.nuspec 中的文件的功能
`<file>`元素内的`.nuspec`文件可用于包含特定文件或一组使用通配符的文件。 在使用通配符，没有方法来排除包含的文件的特定子集。 例如，假设您希望在除特定文件夹内的所有文本文件。

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

使用分号来指定多个文件。

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

或使用通配符来排除一组文件，如所有备份文件

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>删除包使用的对话框会提示删除依赖项
卸载包具有依赖项，NuGet 提示时，请允许包的依赖项包以及删除。

![删除的依赖项包](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` 命令的改进
`Get-Package`命令现在支持`-ProjectName`参数。 因此该命令

    Get-Package –ProjectName A

将列出项目 A.中安装的所有包

### <a name="support-for-proxies-that-require-authentication"></a>代理需要身份验证的支持
在要求身份验证的代理后面使用 NuGet，NuGet 将现在会提示输入代理凭据。 输入凭据允许 NuGet 连接到远程存储库。

### <a name="support-for-repositories-that-require-authentication"></a>支持的要求进行身份验证的存储库
NuGet 现在支持连接到[专用存储库](../hosting-packages/local-feeds.md)需要基本或 NTLM 身份验证。

将在未来的版本中添加对摘要式身份验证支持。

### <a name="performance-improvements-to-the-nugetorg-repository"></a>对 nuget.org 存储库的性能改进
我们进行了到 nuget.org 库，若要使包列表和搜索速度更快的一些性能改进。

### <a name="solution-dialog-project-filtering"></a>解决方案对话框项目筛选
在解决方案级对话框中，若要安装哪些项目提示时，我们只显示所选包与兼容的项目。

### <a name="package-release-notes"></a>包发行说明
NuGet 包现在包括发行说明的支持。 发行说明邮件时查看仅显示_更新_对于包，因此它没有意义将它们添加到你的第一个发布。

![在更新选项卡中的发行说明](./media/manage-nuget-packages-release-notes.png)

若要添加到包的发行说明，请使用新`<releaseNotes />`NuSpec 文件中的元数据元素。

### <a name="nuspec-ltfiles-gt-improvement"></a>.nuspec & ltfiles /&gt;改进
`.nuspec`文件现在允许空`<files />`元素，它告知 nuget.exe 不以在包中包含的任何文件。

## <a name="bug-fixes"></a>Bug 修复
NuGet 1.5 有工作项修复 107 总共。 103 的那些已标记为 bug。

有关工作的完整列表项中已修复 NuGet 1.5，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)。

## <a name="bug-fixes-worth-noting"></a>值得注意的 bug 修复：

* [问题 1273年](http://nuget.codeplex.com/workitem/1273)： 进行`packages.config`友好通过按字母顺序排序的包和删除额外的空格的更多版本控制。
* [问题 844](http://nuget.codeplex.com/workitem/844)： 现在规范化后的版本号，以便`Install-Package 1.0`适用于具有版本包`1.0.0`。
* [问题 1060年](http://nuget.codeplex.com/workitem/1060)： 创建使用 nuget.exe，包时`-Version`标志替代`<version />`元素。
