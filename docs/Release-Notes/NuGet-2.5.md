---
title: NuGet 2.5 发行说明 |Microsoft 文档
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 2.5 发行说明。
keywords: NuGet 2.5 发行说明，bug 修复的已知问题，添加了一些功能，DCRs
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4495e1ea9cc4ec13ef330e56d12de1320cf10b24
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-25-release-notes"></a>NuGet 2.5 发行说明

[NuGet 2.2.1 发行说明](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 发行说明](../release-notes/nuget-2.6.md)

NuGet 2.5 已于 2013 年 4 月 25 日发布。 此版本已大以至于，我们觉得必须跳过版本 2.3 和 2.4 ！ 到目前为止，这是我们已在 nuget，最大版本通过[160 工作项](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all)发行版中的。

## <a name="acknowledgements"></a>致谢

我们真诚地感谢以下外部参与者所做出的重要贡献到 NuGet 2.5:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [# 2847年](https://nuget.codeplex.com/workitem/2847)-添加 MonoAndroid、 MonoTouch 和 MonoMac 到已知的目标框架标识符的列表。
1. [Andres G.Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [# 2865年](https://nuget.codeplex.com/workitem/2865)-修复拼写`NuGet.targets`区分大小写的操作系统
1. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - 请在 Mono 上生成的解决方案。
1. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - 修复 Mono 上失败的单元测试。
1. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [# 2920年](https://nuget.codeplex.com/workitem/2920)-nuget.exe 包命令不会传播到 MSBuild 属性
1. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [# 1511年](https://nuget.codeplex.com/workitem/1511)-修改 XML 处理代码以保留格式化。
1. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - 添加到自定义的字典，以允许 build.cmd 成功识别的字。
1. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - 在本地化 VS 中运行时，请修复单元测试。
1. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - 从 PackageService 提取的接口
1. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
    - [#936](https://nuget.codeplex.com/workitem/936) -时封装处理项目依赖项
1. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
    - [# 2991年](https://nuget.codeplex.com/workitem/2991)， [#3164](https://nuget.codeplex.com/workitem/3164) -支持清除文本密码时在 nuget.cofig 文件中存储包源凭据
1. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
    - [#3190](http://nuget.codeplex.com/workitem/3190)， [#3191](http://nuget.codeplex.com/workitem/3191) -修复 Get 包帮助说明

我们还非常感谢下列人员有关如何查找 bug 与 NuGet 2.5 Beta/RC 批准并在最终发布之前修复：

1. [Tony 墙](https://www.codeplex.com/site/users/view/CodeChief)([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) -与最新 NuGet 2.4 和 2.5 生成中断的 MSTest

## <a name="notable-features-in-the-release"></a>发行版中的值得注意的功能

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>允许用户覆盖已存在的内容文件

所有时间的最常请求的功能之一已被覆盖已存在时 NuGet 程序包中包含的磁盘的内容文件的能力。 从 NuGet 2.5 开始，识别这些冲突，并提示您覆盖文件，而以前始终跳过这些文件。

![覆盖内容文件](./media/NuGet-2.5/overwrite-file.png)

nuget.exe 更新和 Install-package 现在都具有一个新选项-FileConflictAction 设置一些默认值为命令行的方案。

从包文件已存在目标项目中时，请设置的默认操作。 设置为覆盖以始终覆盖文件。 设置为忽略可跳过的文件。 如果未指定，则它将提示输入每个冲突的文件。

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>MSBuild 目标与属性文件的自动导入

已为用户创建一个新的常规文件夹，在 NuGet 包的最高级别。  作为的对等方`\lib`， `\content`，和`\tools`，你现在可以包含`\build`包中的文件夹。  在此文件夹下，可以将带有固定名称的两个文件`{packageid}.targets`或`{packageid}.props`。 这两个文件可以是直接在`build`或在其他文件夹一样的特定于框架的文件夹下。 选取最佳匹配的 framework 文件夹的规则正是与那些相同。

当 NuGet \build 文件安装包时，它会将添加 MSBuild`<Import>`指向项目文件中的元素`.targets`和`.props`文件。 `.props`的顶部，添加文件，而`.targets`文件添加到底部。

### <a name="specify-different-references-per-platform-using-references-element"></a>指定每个平台使用的不同引用`<References/>`元素

2.5 中之前, 在`.nuspec`文件，用户可以仅指定要为所有 framework 添加的引用文件。 现在在 2.5 此新功能，用户可以编写`<reference/>`元素为每个受支持的平台，例如：

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

下面是如何 NuGet 添加对基于项目的引用的流`.nuspec`文件：

1. 查找`lib`适合于目标框架，并从该文件夹中获得的程序集列表的文件夹
1. 单独查找适合于目标框架的引用组，并从该组中获得的程序集列表。 没有指定的目标框架的引用组是回退的组。
1. 查找的交集的两个列表中，并使用它作为引用添加

此新功能将允许包作者引用功能用于将程序集的子集应用于不同的框架，否则将需要执行在多个重复的程序集时`lib`文件夹。

注意： 你必须目前用于 nuget.exe 包使用此功能;NuGet 包资源管理器尚不支持它。

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>更新所有按钮，以允许同时更新所有包

你们中的许多了解的有关"更新包"PowerShell cmdlet 以更新的所有包;现在是 UI 以及通过执行此操作的简单办法。

若要尝试此功能：

1. 创建新的 ASP.NET MVC 应用程序
1. 启动管理 NuGet 包对话框
1. 选择更新
1. 单击全部更新按钮

![更新对话框中的所有按钮](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>改进的项目引用支持 nuget.exe 包

现在 nuget.exe 包命令流程引用项目使用以下规则：

1. 如果引用的项目都有相应`.nuspec`文件，例如，存在名为的文件`proj1.nuspec`在所在的文件夹`proj1.csproj`，则此项目将添加为依赖项到包中，使用 id 并从读取版本`.nuspec`文件。
1. 否则，引用的项目的文件会捆绑到包中。 然后将使用 sames 规则以递归方式处理此项目引用的项目。
1. 所有 DLL， `.pdb`，和`.exe`添加文件。
1. 添加所有其他内容的文件。
1. 合并所有依赖项。

这样，被视为依赖项，如果没有一个引用的项目`.nuspec`文件，否则，它将成为包的一部分。

此处更多详细信息： [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>将最小 NuGet 版本属性添加到包

现在，新的元数据属性调用 minClientVersion 可以指示使用包所需的最小 NuGet 客户端版本。

此功能可帮助包作者指定，包将仅在特定版本的 NuGet 后正常工作。 作为新`.nuspec`添加功能，在 NuGet 2.5 之后包将能够声明的最小的 NuGet 版本。

```xml
<metadata minClientVersion="2.6">
```

如果用户已安装的 NuGet 2.5 并且为需要 2.6 确定包，视觉提示将赋予指示包将不可安装的用户。 然后将指导用户更新其版本的 NuGet。

这将改进了现有的包从其中开始安装，但无法，该值指示无法识别的架构版本已标识的经验。

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>依赖项是不再不必要地更新包安装

在 NuGet 2.5 之前安装包时，依赖于在项目中，已安装的包依赖项将会更新属于新安装，即使现有版本满足依赖项。

如果依赖项版本不满足为已从 NuGet 2.5，依赖项将不会更新在其他包安装过程。

**方案：**

1. 源存储库包含版本 1.0.0 和 1.0.2 包 B。 它还包含程序包 A B 具有依赖关系 (> = 1.0.0)。
1. 假定当前项目已具有包 B 版本 1.0.0 安装。 现在你想要安装包 a。

**在 NuGet 2.2 和更早：**

* 在安装时包 A，NuGet 将自动更新 B 到 1.0.2，即使现有版本 1.0.0 已满足的依赖项版本约束，这是 > = 1.0.0。

**在 NuGet 2.5 和更高版本：**

* NuGet 将不再更新 B，因为它检测到现有的版本 1.0.0 满足的依赖项版本约束。

有关此更改的更多背景，读取详细[工作项](http://nuget.codeplex.com/workitem/1681)以及相关[讨论线程](http://nuget.codeplex.com/discussions/436712)。

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe 包含详细的详细级别的输出结果 http 请求

如果进行故障排除 nuget.exe 或只想哪些 HTTP 请求都在操作期间，-详细的详细信息交换机现在将输出发出的所有 HTTP 请求。

![从 nuget.exe 的 HTTP 输出](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>nuget.exe 推送现在支持 UNC 和文件夹的源

之前 NuGet 2.5 中，如果尝试运行 'nuget.exe push' 到包源基于的 UNC 路径或本地文件夹，将失败的推送。 通过使用最近添加的层次结构配置功能中，它已成为常见的 nuget.exe 需要一个 UNC/文件夹源或基于 HTTP 的 NuGet 库为目标。

从开始 NuGet 2.5 中，如果 nuget.exe 标识 UNC/文件夹源，它将执行文件复制到源。

以下命令将失败：

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe 支持显式指定配置文件

现在访问配置 （除规范和包全部） 的 nuget.exe 命令支持的新-ConfigFile 选项，这会强制要用于取代了 %appdata%\nuget\nuget.config 的默认配置文件的特定配置文件。

示例:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>对本机项目的支持

NuGet 2.5 与 NuGet 工具现已可供 Visual Studio 中的本机项目。 我们的预期最本机包将使用更高版本，MSBuild 导入功能使用由工具[CoApp 项目](http://coapp.org)。 详细信息，请阅读[有关该工具的详细信息](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html)coapp.org 网站上。

"本机"的目标框架名称是用于时包安装到本机项目 \build、 \content 和 \tools 中包括的文件的包引入的。  \`Lib 文件夹不用于本机项目。
