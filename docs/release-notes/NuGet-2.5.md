---
title: NuGet 2.5 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 2.5 发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 29d0b33714a574281680e110b967269699afbaf1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550478"
---
# <a name="nuget-25-release-notes"></a>NuGet 2.5 发行说明

[NuGet 2.2.1 发行说明](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 发行说明](../release-notes/nuget-2.6.md)

NuGet 2.5 已于 2013 年 4 月 25 日发布。 此版本都是如此之大，我们觉得有必要，若要跳过版本 2.3 和 2.4 ！ 到目前为止，这是我们已将适用于 NuGet，使用的最大版本通过[160 工作项](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all)发行版中的。

## <a name="acknowledgements"></a>致谢

我们要特别感谢以下外部参与者的重要贡献到 NuGet 2.5:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [# 2847年](https://nuget.codeplex.com/workitem/2847)-添加 MonoAndroid、 MonoTouch 和 MonoMac 到已知的目标框架标识符的列表。
2. [Andres G.Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [# 2865年](https://nuget.codeplex.com/workitem/2865)-修复拼写`NuGet.targets`区分大小写的 os
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - 请在 Mono 上构建的解决方案。
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - 修复失败的 Mono 上的单元测试。
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [# 2920年](https://nuget.codeplex.com/workitem/2920)-nuget.exe pack 命令不会传播到 MSBuild 属性
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [# 1511年](https://nuget.codeplex.com/workitem/1511)-修改 XML 处理代码以保留格式设置。
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - 添加到自定义字典，以允许 build.cmd 成功识别的字词。
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - 在本地化 VS 中运行时，请修复单元测试。
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - 从 PackageService 提取的接口
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) -打包时处理项目依赖项
11. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [# 2991年](https://nuget.codeplex.com/workitem/2991)， [#3164](https://nuget.codeplex.com/workitem/3164) -支持清除文本密码时在 nuget.cofig 文件中存储包源凭据
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190)， [#3191](http://nuget.codeplex.com/workitem/3191) -修复 Get-package 帮助说明

我们还用于查找 bug 与 NuGet 2.5 Beta/RC 的已批准并最终发布之前得到修复非常感谢下列人员：

1. [Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) -MSTest 断开与最新 NuGet 2.4 和 2.5 生成

## <a name="notable-features-in-the-release"></a>在版本中值得注意的功能

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>允许用户覆盖已存在的内容文件

所有时间的最热门的功能之一已被覆盖时包含在 NuGet 包中的磁盘已存在的内容文件的功能。 从 NuGet 2.5 开始，标识这些冲突，系统会提示你覆盖文件，而以前这些文件被始终跳过。

![覆盖内容文件](./media/NuGet-2.5/overwrite-file.png)

nuget.exe 更新和安装包现在都有一个新选项-FileConflictAction 设置一些默认的命令行方案。

从包文件已存在目标项目中时，请设置了默认操作。 设置为覆盖始终覆盖文件。 设置为忽略以跳过的文件。 如果未指定，它将提示输入每个冲突文件。

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>自动导入的 MSBuild 目标和属性文件

NuGet 包的最高级别，已创建一个新的传统文件夹。  作为对等`\lib`， `\content`，并`\tools`，现在可以包括`\build`在包中的文件夹。  在此文件夹下可以放置两个文件的固定名称，`{packageid}.targets`或`{packageid}.props`。 这两个文件可以是直接在`build`或特定于框架的文件夹，就像其他文件夹下。 选取最佳匹配的 framework 文件夹的规则完全是与那些相同。

当 NuGet 使用 \build 文件安装包时，它会将添加 MSBuild`<Import>`指向的项目文件中的元素`.targets`和`.props`文件。 `.props`在顶部，添加文件，而`.targets`文件添加到底部。

### <a name="specify-different-references-per-platform-using-references-element"></a>指定每个平台使用不同的引用`<References/>`元素

前 2.5 中，在`.nuspec`文件中，用户仅可以指定要添加的所有框架的引用文件。 现在，使用在 2.5 此新功能，用户可以创作`<reference/>`元素为每个受支持的平台，例如：

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

下面是有关 NuGet 如何添加对基于项目的引用的流程`.nuspec`文件：

1. 查找`lib`适合于目标框架，从该文件夹中获取的程序集列表的文件夹
1. 单独查找适合于目标框架的引用组，并从该组中获取的程序集列表。 而无需指定目标框架的引用组是回退的组。
1. 查找两个列表的交集，并使用它作为引用添加

这一新功能将允许包创建者使用引用功能，适用于不同框架的程序集的子集，否则将需要在多个执行重复的程序集时`lib`文件夹。

注意： 必须目前使用 nuget.exe 包以使用此功能;NuGet 包资源管理器尚不支持它。

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>更新所有按钮，以便一次性更新所有包

很多人了解的有关"更新包"PowerShell cmdlet 来更新所有包;现在是通过用户界面以及执行此操作的简单办法。

若要试用此功能：

1. 创建新的 ASP.NET MVC 应用程序
1. 启动管理 NuGet 包对话框
1. 选择更新
1. 单击全部更新按钮

![更新对话框中的所有按钮](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>改进了的项目引用支持 nuget.exe 包

现在 nuget.exe pack 命令进程引用项目的以下规则：

1. 如果引用的项目都有相应`.nuspec`文件中，例如没有名为的文件`proj1.nuspec`所在的同一文件夹中`proj1.csproj`，然后向添加此项目作为依赖项包，使用 id 和版本从读取`.nuspec`文件。
1. 否则，所引用项目的文件打包为包。 然后将使用 sames 规则以递归方式处理此项目引用的项目。
1. 所有 DLL `.pdb`，和`.exe`添加文件。
1. 其他所有内容文件添加。
1. 将合并所有依赖项。

这样，引用的项目被视为依赖项是否存在`.nuspec`文件中，否则，将包的一部分。

有关详细信息： [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>将最小值 NuGet 版本属性添加到包

现在，新的元数据属性名为 minClientVersion 可以指示使用包所需的最低 NuGet 客户端版本。

此功能可帮助包作者指定，包将仅在特定版本的 NuGet 后正常工作。 作为新`.nuspec`功能后，添加 NuGet 2.5 中，包将能够声明最小的 NuGet 版本。

```xml
<metadata minClientVersion="2.6">
```

如果用户已安装的 NuGet 2.5 并且包被标识为需要 2.6，将向用户指示包将不可安装提供视觉提示。 然后将指导用户更新他们的 NuGet 版本。

这将提高时安装，但无法识别无法识别的架构版本，该值指示包开始位置的现有体验。

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>在包安装期间不能再不必要地更新依赖项

在 NuGet 2.5 之前已安装包依赖于在项目中，已安装的包依赖项将会更新作为新安装的一部分即使现有版本满足了依赖关系。

如果已满足依赖项版本，从具有 NuGet 2.5 开始，将依赖关系将不会更新在其他包安装期间。

**方案：**

1. 源存储库包含程序包 B 使用版本 1.0.0 和 1.0.2。 它还包含包 A B 具有依赖关系 (> = 1.0.0)。
1. 假设当前项目已具有包 B 版本 1.0.0 安装。 现在你想要安装包 a。

**在 NuGet 2.2 和更低版本：**

* 在安装包 A 时，NuGet 将自动更新 B 到 1.0.2，即使现有版本 1.0.0 已满足依赖项版本约束，这是 > = 1.0.0。

**在 NuGet 2.5 及更高版本：**

* NuGet 将不再更新 B，因为它检测到的现有版本 1.0.0 满足依赖项版本约束。

有关此更改的更多背景，阅读详细[工作项](http://nuget.codeplex.com/workitem/1681)以及相关[讨论线索](http://nuget.codeplex.com/discussions/436712)。

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe 详细输出的 http 请求

如果要解决 nuget.exe 或只是想什么 HTTP 请求都在操作期间，-详细详细级别交换机现在将输出发出的所有 HTTP 请求。

![Nuget.exe HTTP 输出](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>nuget.exe 推送现在支持 UNC 和文件夹的源

之前 NuGet 2.5 中，如果你尝试运行 nuget.exe 推送到包源基于的 UNC 路径或本地文件夹，推送会失败。 使用最近添加的层次结构配置功能，它已成为常见的 nuget.exe 以需要以 UNC/文件夹源或基于 HTTP 的 NuGet 库为目标。

从具有 NuGet 2.5 开始，如果 nuget.exe 标识 UNC/文件夹源，它将执行文件复制到源。

以下命令将失败：

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe 支持显式指定配置文件

立即访问配置 （全部规范和包除外） 的 nuget.exe 命令支持的新-ConfigFile 选项，这会强制一个特定的配置文件用于替代默认配置文件位于 %appdata%\nuget\nuget.config。

示例:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>对本机项目的支持

对于 NuGet 2.5 的 NuGet 工具现已可供 Visual Studio 中的本机项目。 我们希望最本机包将使用更高版本，MSBuild 导入功能使用工具创建的[CoApp 项目](http://coapp.org)。 有关详细信息，请阅读[有关该工具的详细信息](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html)coapp.org 网站上。

当包安装到本机项目 \build、 \content 和 \tools 中包含文件的程序包引入了"本机"的目标框架名称。  \`Lib 文件夹不用于本机项目。
