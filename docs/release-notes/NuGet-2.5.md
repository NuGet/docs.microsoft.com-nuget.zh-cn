---
title: NuGet 2.5 发行说明
description: NuGet 2.5 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: efcfb9767772c9e27372b4616f817656d51efed8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776857"
---
# <a name="nuget-25-release-notes"></a>NuGet 2.5 发行说明

[NuGet 2.2.1 发行说明](../release-notes/nuget-2.2.1.md)  | [NuGet 2.6 发行说明](../release-notes/nuget-2.6.md)

NuGet 2.5 于2013年4月25日发布。 此版本非常大，我们认为我们会跳过版本2.3 和2.4！ 迄今为止，这是我们为 NuGet 提供的最大版本，其中包含160多个 [工作项](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) 。

## <a name="acknowledgements"></a>致谢

我们想感谢以下外部参与者对 NuGet 2.5 的重大贡献：

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted)) 
    - [#2847](https://nuget.codeplex.com/workitem/2847) -将 MonoAndroid、Monotouch.dialog 和 MonoMac 添加到已知目标框架标识符的列表。
2. [Andres Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte)) 
    - [#2865](https://nuget.codeplex.com/workitem/2865) -修复 `NuGet.targets` 区分大小写的操作系统的拼写
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl)) 
    - 使解决方案在 Mono 上构建。
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken)) 
    - 修复 Mono 上失败的单元测试。
5. [Marc-olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool)) 
    - [#2920](https://nuget.codeplex.com/workitem/2920) nuget.exe pack 命令未将属性传播到 MSBuild
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos)) 
    - 用于保留格式的[#1511](https://nuget.codeplex.com/workitem/1511)修改的 XML 处理代码。
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph)) 
    - 已将识别的字词添加到自定义字典，以允许成功生成 .cmd。
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - 在本地化和中运行时修复单元测试
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - 已从 PackageService 中提取接口
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou)) 
     - [#936](https://nuget.codeplex.com/workitem/936) -在打包时处理项目依赖项
11. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster)) 
     - [#2991](https://nuget.codeplex.com/workitem/2991)，在 cofig 文件中存储包源凭据时， [#3164](https://nuget.codeplex.com/workitem/3164) 支持明文密码
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj)) 
     - [#3190](http://nuget.codeplex.com/workitem/3190)， [#3191](http://nuget.codeplex.com/workitem/3191) 修复 Get-Package 帮助说明

此外，我们还会感谢以下人员查找在最终版本之前批准和修复的 NuGet 2.5 Beta/RC bug：

1. [Tony 墙](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief)) 
    - [#3200](https://nuget.codeplex.com/workitem/3200) -MSTest 中断了最新 NuGet 2.4 和2.5 版本

## <a name="notable-features-in-the-release"></a>版本中值得注意的功能

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>允许用户覆盖已存在的内容文件

所有时间最常请求的功能之一是能够覆盖包含在 NuGet 包中的已存在于磁盘上的内容文件。 从 NuGet 2.5 开始，会识别这些冲突，并提示您覆盖这些文件，而以前这些文件始终被跳过。

![覆盖内容文件](./media/NuGet-2.5/overwrite-file.png)

"nuget.exe 更新" 和 "安装包" 现在都有一个新选项 "-FileConflictAction" 用于为命令行方案设置某些默认值。

当目标项目中已存在来自包的文件时，设置默认操作。 设置为 "覆盖" 以始终覆盖文件。 设置为 "Ignore" 可跳过文件。 如果未指定，则会提示输入每个冲突的文件。

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>MSBuild 目标和属性文件的自动导入

已在 NuGet 包的顶层创建了一个新的传统文件夹。  作为对、和的对等， `\lib` `\content` `\tools` 你现在可以 `\build` 在包中包含一个文件夹。  在此文件夹下，您可以放置两个具有固定名称的文件， `{packageid}.targets` 或 `{packageid}.props` 。 这两个文件可以直接位于 `build` 框架特定的文件夹下，也可以在其下，就像其他文件夹一样。 选择最佳匹配框架文件夹的规则与这些文件夹的规则完全相同。

当 NuGet 使用 \build 文件安装包时，它将 `<Import>` 在指向和文件的项目文件中添加 MSBuild 元素 `.targets` `.props` 。 `.props`文件将添加到顶部，而 `.targets` 文件将添加到底部。

### <a name="specify-different-references-per-platform-using-references-element"></a>使用元素为每个平台指定不同的引用 `<References/>`

在2.5 之前， `.nuspec` 用户只能为所有框架指定要添加的引用文件。 现在，在2.5 中提供了这项新功能，用户可以 `<reference/>` 为每个受支持的平台创作元素，例如：

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

下面是 NuGet 如何根据文件添加对项目的引用的流程 `.nuspec` ：

1. 查找 `lib` 适用于目标框架的文件夹，并从该文件夹获取程序集列表
1. 分别查找适用于目标框架的引用组，并从该组获取程序集列表。 未指定目标框架的引用组是回退组。
1. 查找两个列表的交集，并将其用作要添加的引用

如果需要在多个文件夹中包含重复的程序集，则此新功能将允许包作者使用 "引用" 功能将程序集的子集应用于不同框架 `lib` 。

注意：你目前必须使用 nuget.exe pack 才能使用此功能;NuGet 包资源管理器尚不支持。

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>"全部更新" 按钮允许同时更新所有包

许多人都知道，"更新包" PowerShell cmdlet 可用于更新所有包;现在，还可以通过 UI 轻松完成此操作。

要尝试此功能，请执行以下操作：

1. 新建 ASP.NET MVC 应用程序
1. 启动 "管理 NuGet 包" 对话框
1. 选择 "更新"
1. 单击 "全部更新" 按钮

![对话框中的 "全部更新" 按钮](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>提高了对 nuget.exe Pack 的项目引用支持

现在 nuget.exe pack 命令处理具有以下规则的引用项目：

1. 如果引用的项目具有相应的 `.nuspec` 文件（例如，在与相同的文件夹中有一个名为的文件）， `proj1.nuspec` `proj1.csproj` 则此项目将作为依赖项添加到包，并使用从文件中读取的 id 和版本 `.nuspec` 。
1. 否则，被引用项目的文件捆绑到包中。 然后，将以递归方式使用 sames 规则处理此项目引用的项目。
1. 添加所有 DLL、 `.pdb` 和 `.exe` 文件。
1. 添加了其他所有内容文件。
1. 所有依赖项都将合并。

这允许将引用的项目视为依赖项（如果存在 `.nuspec` 文件），否则它会成为包的一部分。

有关详细信息，请参阅： [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>向包中添加 "最小 NuGet 版本" 属性

名为 "minClientVersion" 的新元数据属性现在可以指示使用包所需的最小 NuGet 客户端版本。

此功能有助于包作者指定仅在特定版本的 NuGet 后使用包。 由于在 `.nuspec` NuGet 2.5 后添加了新功能，包将能够声明最低版本的 nuget。

```xml
<metadata minClientVersion="2.6">
```

如果用户安装了 NuGet 2.5，并且包被标识为需要2.6，则将向用户提供视觉提示，指示将无法安装包。 然后，用户将指导更新其 NuGet 的版本。

这会改进现有的体验，其中包开始安装，但随后会失败，指示标识了无法识别的架构版本。

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>包安装过程中不再需要再更新依赖项

在 NuGet 2.5 之前，当安装了依赖于项目中已安装的包的包时，该依赖项将作为新安装的一部分进行更新，即使现有版本满足了依赖关系也是如此。

从 NuGet 2.5 开始，如果依赖项版本已满足，则不会在其他包安装期间更新依赖项。

**方案：**

1. 源存储库包含版本1.0.0 和1.0.2 的包 B。 它还包含包 A，它依赖于 B ( # B0 = 1.0.0) 。
1. 假定当前项目已安装了包 B 1.0.0 版。 现在，你想要安装包 A。

**在 NuGet 2.2 和更早版本中：**

* 安装包 A 时，NuGet 将自动更新 B 到1.0.2，即使现有版本1.0.0 已经满足依赖项版本约束，该约束 >= 1.0.0。

**在 NuGet 2.5 和更高版本中：**

* NuGet 将不再更新 B，因为它检测到现有版本1.0.0 满足依赖项版本约束。

有关此更改的更多背景信息，请阅读详细的 [工作项](http://nuget.codeplex.com/workitem/1681) 和相关的 [讨论线索](http://nuget.codeplex.com/discussions/436712)。

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe 输出 http 请求以及详细详细信息

如果正在排查 nuget.exe 或只想知道在操作期间发出了哪些 HTTP 请求，"-详细信息" 开关现在会输出发出的所有 HTTP 请求。

![nuget.exe 的 HTTP 输出](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>nuget.exe 推送现在支持 UNC 和文件夹源

在 NuGet 2.5 之前，如果尝试根据 UNC 路径或本地文件夹运行 "nuget.exe 推送" 到包源，推送会失败。 使用最近添加的层次结构配置功能，nuget.exe 需要以 UNC/文件夹源或基于 HTTP 的 NuGet 库为目标。

从 NuGet 2.5 开始，如果 nuget.exe 标识 UNC/文件夹源，则将对源执行文件复制。

现在可以使用以下命令：

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe 支持显式指定的配置文件

访问配置 (除 "spec" 和 "pack ) " 之外的所有 nuget.exe 命令现在支持新的 "-Read-configfile" 选项，该选项强制使用特定的配置文件来代替% AppData% \nuget\Nuget.Config 的默认配置文件。

示例：

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>对本机项目的支持

使用 NuGet 2.5，NuGet 工具现在可用于 Visual Studio 中的本机项目。 我们预计大多数本机包都将使用 [CoApp 项目](http://coapp.org)创建的工具来利用上述 MSBuild 导入功能。 有关详细信息，请参阅 coapp.org 网站上 [有关该工具的详细](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) 信息。

当包安装到本机项目中时，将为包引入 "本机" 的目标框架名称，以包括 \build、\content 和 \tools 中的文件。  \`Lib 文件夹不用于本机项目。
