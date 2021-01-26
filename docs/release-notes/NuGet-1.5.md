---
title: NuGet 1.5 发行说明
description: NuGet 1.5 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c9946f3d8cf545ec14f842c40105743c231b4b72
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777087"
---
# <a name="nuget-15-release-notes"></a>NuGet 1.5 发行说明

[NuGet 1.4 发行说明](../release-notes/nuget-1.4.md)  | [NuGet 1.6 发行说明](../release-notes/nuget-1.6.md)

NuGet 1.5 于2011年8月30日发布。

## <a name="features"></a>功能

### <a name="project-templates-with-preinstalled-nuget-packages"></a>预安装了 NuGet 包的项目模板
创建新的 ASP.NET MVC 3 项目模板时，项目中包含的 jQuery 脚本库实际上是通过安装 NuGet 包放置在那里。

ASP.NET MVC 3 项目模板包含一组在调用项目模板时安装的 NuGet 包。 此功能能够将 NuGet 包包含到项目模板中，它现在是 NuGet 的一项功能，现在 _任何_ 项目模板都可以利用。

有关此功能的更多详细信息，请阅读此博客文章，了解该 [功能的开发人员](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)。

### <a name="explicit-assembly-references"></a>显式程序集引用

添加了一个新 `<references />` 元素，用于显式指定应引用包中的程序集。

例如，如果添加以下内容：

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

然后 `xunit.dll` ，将仅 `xunit.extensions.dll` 从文件夹的相应 [框架/配置文件子](../reference/nuspec.md#explicit-assembly-references) 文件夹中引用和， `lib` 即使该文件夹中存在其他程序集。

如果省略此元素，则会应用常用行为，即引用文件夹中的每个程序集 `lib` 。

__此功能的用途是什么？__

此功能支持仅设计时程序集。 例如，使用代码协定时，协定程序集需要位于它们增加的运行时程序集旁边，以便 Visual Studio 可以找到它们，但是协定程序集实际上不应被项目引用，因此不应复制到 `bin` 文件夹中。

同样，此功能可用于单元测试框架（如 XUnit），这需要将其工具程序集放在运行时程序集旁边，但从项目引用中排除。

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>添加了排除 nuspec 中的文件的功能
`<file>`文件中的元素 `.nuspec` 可用于包含特定文件或使用通配符的一组文件。 使用通配符时，无法排除包含的文件的特定子集。 例如，假设您希望文件夹中的所有文本文件除外。

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

或使用通配符排除一组文件，如所有备份文件

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>使用对话框删除包会提示删除依赖项
卸载具有依赖项的包时，NuGet 会提示，允许删除包的依赖项和包。

![删除依赖包](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` 命令改进
`Get-Package`命令现在支持 `-ProjectName` 参数。 因此命令

```
Get-Package –ProjectName A
```

将列出在项目 A 中安装的所有包。

### <a name="support-for-proxies-that-require-authentication"></a>支持需要身份验证的代理
使用需要身份验证的代理后面的 NuGet 时，NuGet 现在会提示输入代理凭据。 输入凭据后，NuGet 即可连接到远程存储库。

### <a name="support-for-repositories-that-require-authentication"></a>支持需要身份验证的存储库
NuGet 现在支持连接到需要基本或 NTLM 身份验证的 [专用存储库](../hosting-packages/local-feeds.md) 。

未来版本中将添加对摘要式身份验证的支持。

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Nuget.org 存储库的性能改进
我们对 nuget.org 库进行了几项性能改进，使包列表和搜索速度更快。

### <a name="solution-dialog-project-filtering"></a>解决方案对话框项目筛选
在解决方案级对话框中，当提示您要安装的项目时，我们只显示与所选包兼容的项目。

### <a name="package-release-notes"></a>包发行说明
NuGet 包现在包括对发行说明的支持。 仅当查看包的 _更新_ 时才会显示发行说明，因此，将其添加到第一个版本中并没有什么意义。

!["更新" 选项卡中的发行说明](./media/manage-nuget-packages-release-notes.png)

若要向包添加发行说明，请 `<releaseNotes />` 在 NuSpec 文件中使用新的元数据元素。

### <a name="nuspec-ltfiles-gt-improvement"></a>. nuspec &ltfiles/ &gt; 改进
`.nuspec`文件现在允许空 `<files />` 元素，这会告诉 nuget.exe 不包含包中的任何文件。

## <a name="bug-fixes"></a>Bug 修复
NuGet 1.5 总共修复了107个工作项。 103标记为 bug。

有关 NuGet 1.5 中已修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)。

## <a name="bug-fixes-worth-noting"></a>需要注意的 Bug 修复：

* [问题 1273](http://nuget.codeplex.com/workitem/1273)： `packages.config` 通过按字母顺序对包排序并删除额外的空白，使版本控制更友好。
* [问题 844](http://nuget.codeplex.com/workitem/844)：版本号现已规范化，因此适用于版本为的 `Install-Package 1.0` 包 `1.0.0` 。
* [问题 1060](http://nuget.codeplex.com/workitem/1060)：使用 nuget.exe 创建包时，标志将 `-Version` 重写 `<version />` 元素。
