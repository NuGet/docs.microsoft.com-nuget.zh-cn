---
title: NuGet 1.5 的发行说明
description: 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 1.5 的发行说明。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1f2f7ebe718ce943faa31b7e19395eead8726648
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821338"
---
# <a name="nuget-15-release-notes"></a>NuGet 1.5 的发行说明

[NuGet 1.4 的发行说明](../release-notes/nuget-1.4.md) | [NuGet 1.6 发行说明](../release-notes/nuget-1.6.md)

NuGet 1.5 已于 2011 年 8 月 30 日发布。

## <a name="features"></a>功能

### <a name="project-templates-with-preinstalled-nuget-packages"></a>使用预安装的 NuGet 包的项目模板
创建新的 ASP.NET MVC 3 项目模板时，jQuery 脚本库项目中包含实际放在此处通过安装 NuGet 包。

ASP.NET MVC 3 项目模板包含一组调用项目模板时，获取安装的 NuGet 包。 将 NuGet 程序包的项目模板包括此功能现在是一项功能的 NuGet 的_任何_项目模板现在可以充分利用。

有关此功能的详细信息，请参阅此[功能的开发人员的博客文章](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)。

### <a name="explicit-assembly-references"></a>显式程序集引用

添加一个新`<references />`用于显式指定的程序集内的元素应引用包。

例如，如果你将以下代码添加：

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

然后仅`xunit.dll`和`xunit.extensions.dll`将引用从相应[framework/配置文件子文件夹](../reference/nuspec.md#explicit-assembly-references)的`lib`即使文件夹中没有其他程序集的文件夹。

如果省略此元素，则适用常用的行为，即引用中的每个程序集`lib`文件夹。

__此功能的用途是什么？__

此功能支持设计时只有程序集。 例如，当使用代码协定，则需要进行补充，以便 Visual Studio 可以找到它们，但协定程序集不应实际引用由项目并不会复制到运行时程序集旁是协定程序集`bin`文件夹。

同样，该功能可用来为单元测试框架，例如 XUnit 需要旁边运行时程序集，但从项目引用中排除其工具程序集。

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>添加以排除.nuspec 中的文件的能力
`<file>`中的元素`.nuspec`文件可以用于包括特定文件或一组使用通配符的文件。 在使用通配符时，没有方法来排除包含的文件的特定子集。 例如，假设你想在除特定文件夹内的所有文本文件。

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

使用分号指定多个文件。

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

或使用通配符来排除一套例如所有备份文件的文件

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>删除包使用对话框提示以删除依赖关系
卸载程序包依赖项而 NuGet 提示时，允许包的依赖关系和程序包一起删除。

![删除依赖的包](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` 命令改善
`Get-Package`命令现在支持`-ProjectName`参数。 因此该命令

    Get-Package –ProjectName A

将列出项目 A.中安装的所有包

### <a name="support-for-proxies-that-require-authentication"></a>代理需要身份验证的支持
在要求身份验证的代理后面使用 NuGet，NuGet 将现在将提示输入代理服务器凭据。 输入凭据允许连接到远程存储库的 NuGet。

### <a name="support-for-repositories-that-require-authentication"></a>对要求进行身份验证的存储库的支持
NuGet 现在支持连接到[专用的存储库](../hosting-packages/local-feeds.md)需要基本或 NTLM 身份验证。

未来版本中，将添加为摘要式身份验证的支持。

### <a name="performance-improvements-to-the-nugetorg-repository"></a>到 nuget.org 存储库的性能改进
我们已进行了 nuget.org 库，以使包列出和更快地搜索到的一些性能改进。

### <a name="solution-dialog-project-filtering"></a>解决方案对话框项目筛选
在解决方案级别对话框中，当提示输入要安装哪些项目时，我们只会显示所选包与兼容的项目。

### <a name="package-release-notes"></a>包发行说明
NuGet 包现在包括对发行说明支持。 发行说明邮件查看时仅显示_更新_对于包，因此它没有意义将它们添加到你的第一个发布。

![在更新选项卡内的发行说明](./media/manage-nuget-packages-release-notes.png)

若要添加到包的发行说明，使用新`<releaseNotes />`NuSpec 文件中的元数据元素。

### <a name="nuspec-ltfiles-gt-improvement"></a>.nuspec 和 ltfiles /&gt;改善
`.nuspec`文件现在允许空`<files />`元素，它告知 nuget.exe 不要包含在包中的任何文件。

## <a name="bug-fixes"></a>Bug 修复
NuGet 1.5 具有总共 107 工作固定的项。 103 的那些已标记为 bug。

有关工作的完整列表项固定 NuGet 1.5 中请视图[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)。

## <a name="bug-fixes-worth-noting"></a>值得注意的 bug 修复：

* [问题 1273年](http://nuget.codeplex.com/workitem/1273)： 进行`packages.config`友好按字母顺序排序包并删除多余的空格的多个版本控制。
* [问题 844](http://nuget.codeplex.com/workitem/844)： 现在规范化版本号，以便`Install-Package 1.0`适用于版本的包`1.0.0`。
* [问题 1060年](http://nuget.codeplex.com/workitem/1060)： 创建使用 nuget.exe，包时`-Version`标志替代`<version />`元素。
