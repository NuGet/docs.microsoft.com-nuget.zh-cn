---
title: NuGet 的 nuspec 文件引用
description: .nuspec 文件包含生成包时使用的，并向包使用者提供信息的包元数据。
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6bd730db16d8e8783f0d949bb04cf3b52c642cd0
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380557"
---
# <a name="nuspec-reference"></a>.nuspec 引用

`.nuspec` 文件是包含包元数据的 XML 清单。 此清单同时用于生成包以及为使用者提供信息。 清单始终包含在包中。

在本主题中：

- [常规形式和架构](#general-form-and-schema)
- [替换令牌](#replacement-tokens)（用于 Visual Studio 项目时）
- [依赖关系](#dependencies)
- [显式程序集引用](#explicit-assembly-references)
- [Framework 程序集引用](#framework-assembly-references)
- [包括程序集文件](#including-assembly-files)
- [包括内容文件](#including-content-files)
- [示例 nuspec 文件](#example-nuspec-files)

## <a name="project-type-compatibility"></a>项目类型兼容性

- 将 `.nuspec` 与使用 `packages.config` 的非 SDK 样式项目 `nuget.exe pack` 使用。

- 创建[sdk 样式项目](../resources/check-project-format.md)包（通常是 .net Core 和使用[sdk 特性](/dotnet/core/tools/csproj#additions).NET Standard 项目）不需要 `.nuspec` 文件。 （请注意，当你创建包时，将生成一个 `.nuspec`。）

   如果要使用 `dotnet.exe pack` 或 `msbuild pack target` 创建包，我们建议您改为在项目文件中的 `.nuspec` 文件中[包含所有属性](../reference/msbuild-targets.md#pack-target)。 不过，您可以改为选择[使用 `.nuspec` 文件，以使用 `dotnet.exe` 或 `msbuild pack target` 进行打包](../reference/msbuild-targets.md#packing-using-a-nuspec)。

- 对于从 `packages.config` 迁移到[PackageReference](../consume-packages/package-references-in-project-files.md)的项目，创建包不需要 `.nuspec` 文件。 相反，请使用[t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)。

## <a name="general-form-and-schema"></a>常规形式和架构

当前 `nuspec.xsd` 架构文件可在 [NuGet GitHub 存储库](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)中找到。

在此构架中，`.nuspec` 文件具有以下常规形式：

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

有关架构的清晰可视表示形式，请在 Visual Studio 中以“设计”模式打开架构文件，然后单击“XML 架构资源管理器”链接。 或者，将该文件作为代码打开，在编辑器中右键单击，然后选择“显示 XML 架构资源管理器”。 无论哪种方式，都会获得如下所示的视图（大多数部件都处于扩展状态）：

![nuspec.xsd 打开时的 Visual Studio 架构资源管理器](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a>所需的元数据元素

尽管以下元素是包的最低要求，但应该考虑添加[可选元数据元素](#optional-metadata-elements)以改善开发人员对包的整体体验。 

这些元素必须出现在 `<metadata>` 元素中。

#### <a name="id"></a>id 
不区分大小写的包标识符，在 nuget.org 或包驻留的任意库中必须是唯一的。 ID 不得包含空格或对 URL 无效的字符，通常遵循 .NET 命名空间规则。 有关指南，请参阅[选择唯一的包标识符](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)。
#### <a name="version"></a>版本
遵循 major.minor.patch 模式的包版本。 版本号可能包括预发布后缀，如[包版本控制](../concepts/package-versioning.md#pre-release-versions)中所述。 
#### <a name="description"></a>说明
用于 UI 显示的包的说明。
#### <a name="authors"></a>作者
以逗号分隔的包作者列表，与 nuget.org 上的配置文件名称匹配。它们显示在 nuget.org 上的 NuGet 库中，并用于通过相同作者交叉引用包。 

### <a name="optional-metadata-elements"></a>可选元数据元素

#### <a name="owners"></a>所有者
使用 nuget.org 上的配置文件名称的包创建者的逗号分隔列表。这通常与 `authors` 中的列表相同，并且在将包上传到 nuget.org 时将被忽略。请参阅[在 nuget.org 上管理包所有者](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg)。 

#### <a name="projecturl"></a>projectUrl
包的主页 URL，通常显示在 UI 中以及 nuget.org 中。 

#### <a name="licenseurl"></a>licenseUrl
> [!Important]
> licenseUrl 已被弃用。 请改用许可证。

包的许可证的 URL，通常显示在 Ui （如 nuget.org）中。

#### <a name="license"></a>照
包中的许可证文件的 SPDX 许可证表达式或路径，通常显示在 Ui 中，如 nuget.org。如果要使用常见许可证（如 MIT 或 BSD-2 子句）来授权包，请使用关联的[SPDX 许可证标识符](https://spdx.org/licenses/)。 例如:

`<license type="expression">MIT</license>`

> [!Note]
> NuGet.org 仅接受开源计划或免费 Software Foundation 批准的许可表达式。

如果你的包在多个常用许可证下获得许可，则可以使用[SPDX 表达式语法版本 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)指定复合许可证。 例如:

`<license type="expression">BSD-2-Clause OR MIT</license>`

如果使用许可证表达式不支持的自定义许可证，则可以使用许可证文本打包 `.txt` 或 `.md` 文件。 例如:

```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

对于 MSBuild 等效项，请查看[打包许可证表达式或许可证文件](msbuild-targets.md#packing-a-license-expression-or-a-license-file)。

下面的[ABNF](https://tools.ietf.org/html/rfc5234)中介绍了 NuGet 的许可证表达式的确切语法。
```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a>iconUrl

> [!Important]
> iconUrl 已被弃用。 改为使用图标。

64x64 透明背景图像的 URL，用作 UI 显示中包的图标。 请确保此元素包含直接图像 URL，而不是包含图像的网页的 URL。 例如，若要使用 GitHub 中的映像，请使用<em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>等原始文件 URL。 
   
#### <a name="icon"></a>按钮

它是指向包内的映像文件的路径，通常显示在 Ui 中，如 nuget.org 作为包图标。 图像文件大小限制为 1 MB。 支持的文件格式包括 JPEG 和 PNG。 建议将 resoulution 为64x64 的映像。

例如，使用 nuget.exe 创建包时，会将以下内容添加到 nuspec：

```xml
<package>
  <metadata>
    ...
    <icon>images\icon.png</icon>
    ...
  </metadata>
  <files>
    ...
    <file src="..\icon.png" target="images\" />
    ...
  </files>
</package>
```

[包图标 nuspec 示例。](https://github.com/NuGet/Samples/tree/master/PackageIconNuspecExample)

对于 MSBuild 等效项，请查看对[图标图像文件进行打包](msbuild-targets.md#packing-an-icon-image-file)。

#### <a name="requirelicenseacceptance"></a>requireLicenseAcceptance
一个布尔值，用于指定客户端是否必须提示使用者接受包许可证后才可安装包。

#### <a name="developmentdependency"></a>developmentDependency
(2.8+) 一个布尔值，用于指定包是否被标记为仅开发依赖项，从而防止包作为依赖项包含到其他包中。 对于 PackageReference （NuGet 4.8 +），此标志还意味着它将从编译中排除编译时资产。 请参阅[DevelopmentDependency support For PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)

#### <a name="summary"></a>摘要
> [!Important]
> 即将弃用 `summary`。 请改用 `description` 。

用于 UI 显示的包的简要说明。 如果省略，则使用 `description` 的截断版本。

#### <a name="releasenotes"></a>releaseNotes
(1.5+) 此版本包中所作更改的说明，通常代替包说明用在 UI 中，如 Visual Studio 包管理器的“更新”选项卡。

#### <a name="copyright"></a>copyright
(1.5+) 包的版权详细信息。

#### <a name="language"></a>语言
包的区域设置 ID。 请参阅[创建本地化包](../create-packages/creating-localized-packages.md)。

#### <a name="tags"></a>标记
以空格分隔的标记和关键字列表，描述包并通过搜索和筛选辅助包的可发现性。 

#### <a name="serviceable"></a>可用 
(3.3+) 仅限内部使用。

#### <a name="repository"></a>储存库
存储库元数据，由四个可选属性组成： `type` 和 `url` *（4.0 +）* 以及 `branch` 和 `commit` *（4.6 +）* 。 通过这些属性，可以将 `.nupkg` 映射到生成它的存储库，并将其作为单独的分支名称和/或提交生成包的 SHA-1 哈希。 这应该是公开提供的 url，可由版本控制软件直接调用。 它不应是 html 页面，因为这是用于计算机的。 对于 "链接到项目" 页，请改用 `projectUrl` 字段。

例如:
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2016/06/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

#### <a name="title"></a>标题
可在某些 UI 显示中使用的包的友好标题。 （Visual Studio 中的 nuget.org 和包管理器不显示标题）

#### <a name="collection-elements"></a>集合元素

#### <a name="packagetypes"></a>packageTypes
*(3.5+)* 如果不是传统的依赖项包，则为指定包类型的包括零个或多个 `<packageType>` 元素的集合。 每个 packageType 都具有 name 和 version 特性。 请参阅[设置包类型](../create-packages/set-package-type.md)。
#### <a name="dependencies"></a>依赖项
零个或多个 `<dependency>` 元素的集合，用来指定包的依赖项。 每个 dependency 都具有 id、version、include (3.x+) 和 exclude (3.x+) 特性。 请参阅下面的[依赖项](#dependencies-element)。
#### <a name="frameworkassemblies"></a>frameworkAssemblies
(1.2+) 零个或多个 `<frameworkAssembly>` 元素的集合，用来标识此包要求的 .NET Framework 程序集引用，从而确保引用添加到使用该包的项目。 每个 frameworkAssembly 都具有 assemblyName 和 targetFramework 特性。 请参阅下面的[指定 Framework 程序集引用 GAC](#specifying-framework-assembly-references-gac)。
#### <a name="references"></a>引用
(1.5+) 零个或多个 `<reference>` 元素的集合，用来指定包的 `lib` 文件夹中添加为项目引用的程序集。 每个 reference 都具有 file 特性。 `<references>` 也可包含具有 targetFramework 特性的 `<group>` 元素，然后包含 `<reference>` 元素。 如果省略，则包含 `lib` 中的全部引用。 请参阅下面的[指定显式程序集引用](#specifying-explicit-assembly-references)。
#### <a name="contentfiles"></a>contentFiles
(3.3+) `<files>` 元素的集合，用来标识包含在使用项目中的内容文件。 这些文件用一组特性指定，用于描述如何在项目系统中使用这些文件。 请参阅下面的[指定包含在包中的文件](#specifying-files-to-include-in-the-package)。
#### <a name="files"></a>文件 
@No__t_0 节点可能包含一个 `<files>` 节点作为 `<metadata>` 的同级，并且在 `<metadata>` 下的 `<contentFiles>` 子节点指定要包含在包中的程序集和内容文件。 有关详细信息，请参阅本主题后面的[包含程序集文件](#including-assembly-files)和[包含内容文件](#including-content-files)。

### <a name="metadata-attributes"></a>metadata 特性

#### <a name="minclientversion"></a>minClientVersion
指定可安装此包的最低 NuGet 客户端版本，并由 nuget.exe 和 Visual Studio 程序包管理器强制实施。 只要包依赖于特定 NuGet 客户端版本中添加的 `.nuspec` 文件的特定功能，就会使用此功能。 例如，使用 `developmentDependency` 特性的包应为 `minClientVersion` 指定“2.8”。 同样，使用 `contentFiles` 元素（请参阅下一部分）的包应将 `minClientVersion` 设置为“3.3”。 另请注意，早于 2.5 的 NuGet 客户端无法识别此标记，所以无论 `minClientVersion` 包含什么内容，它们总是拒绝安装该包。

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/01/nuspec.xsd">
    <metadata minClientVersion="100.0.0.1">
        <id>dasdas</id>
        <version>2.0.0</version>
        <title />
        <authors>dsadas</authors>
        <owners />
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>My package description.</description>
    </metadata>
    <files>
        <file src="content\one.txt" target="content\one.txt" />
    </files>
</package>
```

## <a name="replacement-tokens"></a>替换令牌

创建包时，[`nuget pack` 命令](../reference/cli-reference/cli-ref-pack.md)使用来自项目文件的值或 `pack` 命令的 `-properties` 开关来替换 `.nuspec` 文件的 `<metadata>` 节点中带 $ 分隔符的令牌。

在命令行中，可使用 `nuget pack -properties <name>=<value>;<name>=<value>` 指定令牌值。 例如，可使用 `.nuspec` 中的 `$owners$` 和 `$desc$` 令牌，并在封装时提供值，如下所示：

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

如要使用项目中的值，请指定下表中描述的令牌（AssemblyInfo 指的是 `Properties` 中的文件，如 `AssemblyInfo.cs` 或 `AssemblyInfo.vb`）。

若要使用这些令牌，请通过项目文件而不仅仅是 `.nuspec` 来运行 `nuget pack`。 例如，使用以下命令时，`.nuspec` 文件中的 `$id$` 和 `$version$` 令牌会被替换为项目的 `AssemblyName` 和 `AssemblyVersion` 值：

```ps
nuget pack MyProject.csproj
```

通常情况下，如果已有项目，最初会使用自动包含一些标准令牌的 `nuget spec MyProject.csproj` 创建 `.nuspec`。 然而，如果项目缺少要求的 `.nuspec` 元素的值，那么 `nuget pack` 失败。 此外，如果更改项目值，请确定在创建包之前重新生成，可通过 pack 命令的 `build` 开关方便地完成此操作。

除 `$configuration$` 外，项目中的值优先于在命令行上分配给相同令牌的任何值。

| 标记 | 值来源 | “值”
| --- | --- | ---
| **$id$** | 项目文件 | 项目文件中的 AssemblyName （title） |
| **$version$** | AssemblyInfo | AssemblyInformationalVersion（如果存在），否则为 AssemblyVersion |
| **$author$** | AssemblyInfo | AssemblyCompany |
| **$title $** | AssemblyInfo | AssemblyTitle |
| **$description$** | AssemblyInfo | AssemblyDescription |
| **$copyright$** | AssemblyInfo | AssemblyCopyright |
| **$configuration$** | 程序集 DLL | 用于生成程序集的配置，默认为 Debug。 请注意，若要使用 Release 配置创建包，应始终在命令行上使用 `-properties Configuration=Release`。 |

包含[程序集文件](#including-assembly-files)和[内容文件](#including-content-files)时，令牌也可用于解析路径。 这些令牌与 MSBuild 属性具有相同的名称，因此可根据当前生成配置来选择要包含的文件。 例如，如果在 `.nuspec` 文件中使用以下令牌：

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

在 MSBuild 中生成具有 `Release` 配置且 `AssemblyName` 为 `LoggingLibrary` 的程序集，包中 `.nuspec` 文件中的结果行如下所示：

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a>依赖项元素

`<metadata>` 中的 `<dependencies>` 元素包含任意数量的 `<dependency>` 元素，用来标识顶级包所依赖的其他包。 每个 `<dependency>` 的特性如下所示：

| 特性 | 描述 |
| --- | --- |
| `id` | （必须）依赖项的包 ID，如“EntityFramework”和“NUnit”，同时也是 nuget.org 在包页面上显示的包名称。 |
| `version` | （必需）可接受作为依赖项的版本范围。 有关准确语法，请参阅[包版本控制](../concepts/package-versioning.md#version-ranges-and-wildcards)。 不支持通配符（浮动）版本。 |
| include | 包括/排除标记的逗号分隔列表（见下文），指示要包含在最终包中的依赖项。 默认值为 `all`。 |
| exclude | 包括/排除标记的逗号分隔列表（见下文），指示要排除在最终包外的依赖项。 默认值为 `build,analyzers`，可以覆盖此值。 但仍会在最终包中隐式排除 `content/ ContentFiles`，这是无法覆盖的。 用 `exclude` 指定的标记优先于用 `include` 指定的标记。 例如，`include="runtime, compile" exclude="compile"` 和 `include="runtime"` 相同。 |

| 包括/排除标记 | 受影响的目标文件夹 |
| --- | --- |
| contentFiles | 内容 |
| Runtime — 运行时 | 运行时、资源和 FrameworkAssemblies |
| 编译 | lib |
| 生成 | 生成（MSBuild 属性和目标） |
| 本机 | 本机 |
| 无 | 无文件夹 |
| 全部 | 全部文件夹 |

例如，以下行指示 `PackageA` 版本 1.1.0 或更高版本，以及 `PackageB` 版本 1.x 的依赖项。

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

以下行指示相同包上的依赖项，但指定包括 `PackageA` 的 `contentFiles` 和 `build` 文件夹，以及除 `PackageB` 的 `native` 和 `compile` 文件夹以外的所有文件夹。

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> 使用 `nuget spec` 从项目创建 `.nuspec` 时，该项目中存在的依赖项不会自动包括在生成的 `.nuspec` 文件中。 请改用 `nuget pack myproject.csproj`，并从*nupkg*文件中获取*nuspec*文件。 *Nuspec*包含依赖项。

### <a name="dependency-groups"></a>依赖项组

版本 2.0+

作为单个简单列表的替代方法，可使用 `<dependencies>` 中的 `<group>` 元素根据目标项目的框架配置文件指定依赖项。

每个组都有一个名为 `targetFramework` 的特性，并包含零个或多个 `<dependency>` 元素。 当目标框架与项目的框架配置文件兼容时，将会一起安装这些依赖项。

无 `targetFramework` 特性的 `<group>` 元素被用作依赖项的默认列表或回退列表。 有关确切的框架标识符，请参阅[目标框架](../reference/target-frameworks.md)。

> [!Important]
> 组格式不能与简单列表混合使用。

以下示例显示了 `<group>` 元素的不同变体：

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>显式程序集引用

使用 `packages.config` 的项目使用 `<references>` 元素显式指定目标项目在使用包时应引用的程序集。 显式引用通常用于仅设计时程序集。 有关详细信息，请参阅有关详细信息，请参阅[选择项目引用的程序集](../create-packages/select-assemblies-referenced-by-projects.md)。

例如，以下 `<references>` 元素指示 NuGet 仅对 `xunit.dll` 和 `xunit.extensions.dll` 添加引用，即使包中还有其他程序集：

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a>引用组

作为单个简单列表的替代方法，可使用 `<references>` 中的 `<group>` 元素根据目标项目的框架配置文件指定引用。

每个组都有一个名为 `targetFramework` 的特性，并包含零个或多个 `<reference>` 元素。 当目标框架与项目的框架配置文件兼容时，会将引用添加到项目中。

无 `targetFramework` 特性的 `<group>` 元素被用作引用的默认列表或回退列表。 有关确切的框架标识符，请参阅[目标框架](../reference/target-frameworks.md)。

> [!Important]
> 组格式不能与简单列表混合使用。

以下示例显示了 `<group>` 元素的不同变体：

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a>Framework 程序集引用

Framework 程序集是 .NET Framework 的一部分，并已存在于任何给定计算机的全局程序集缓存 (GAC) 中。 通过在 `<frameworkAssemblies>` 元素中标识这些程序集，包可确保在项目尚未具有此类引用的情况下，将必需的引用添加到项目中。 当然，此类程序集不直接包含在包中。

`<frameworkAssemblies>` 元素包含零个或多个 `<frameworkAssembly>` 元素，这些元素指定以下特性：

| 特性 | 描述 |
| --- | --- |
| **assemblyName** | （必需）完全限定程序集名称。 |
| **targetFramework** | （可选）指定此引用适用的目标框架。 如果省略，则表示该引用适用于全部框架。 有关确切的框架标识符，请参阅[目标框架](../reference/target-frameworks.md)。 |

以下示例显示了对全部目标框架的 `System.Net` 的引用，以及对仅用于 .NET Framework 4.0 的 `System.ServiceModel` 的引用：

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>包含程序集文件

如果遵循[创建包](../create-packages/creating-a-package.md)中介绍的约定，则不必在 `.nuspec` 文件中显式指定文件列表。 `nuget pack` 命令自动选取所需的文件。

> [!Important]
> 当包安装到项目中时，NuGet 自动将程序集引用添加到包的 DLL，不包括命名为 `.resources.dll` 的内容，因为它们被假定为本地化的附属程序集。 为此，请避免对包含基本包代码的文件使用 `.resources.dll`。

若要绕过此自动行为，并显式控制包中包含的文件，请将 `<files>` 元素作为 `<package>` 的子元素（和 `<metadata>` 的同级元素），并使用单独的 `<file>` 元素标识每个文件。 例如:

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

在 NuGet 2.x 及更早版本中，如果项目使用 `packages.config`，在安装包时，`<files>` 元素也用于包含不可变的内容文件。 通过 NuGet 3.3+ 和项目 PackageReference，将改为使用 `<contentFiles>` 元素。 有关详细信息，请参阅下面的[包含内容文件](#including-content-files)。

### <a name="file-element-attributes"></a>文件元素特性

每个 `<file>` 元素指定以下特性：

| 特性 | 描述 |
| --- | --- |
| **src** | 文件或要包含的文件位置，受 `exclude` 特性指定排除规则约束。 路径是相对于 `.nuspec` 文件的路径，除非指定了绝对路径。 允许使用通配符 `*`，双通配符 `**` 意味着递归文件夹搜索。 |
| **target** | 放置源文件的包中文件夹的相对路径，必须以 `lib`、`content`、`build` 或 `tools` 开头。 请参阅[从基于约定的工作目录创建 .nuspec](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)。 |
| **exclude** | 要从 `src` 位置排除的文件或文件模式的分号分隔列表。 允许使用通配符 `*`，双通配符 `**` 意味着递归文件夹搜索。 |

### <a name="examples"></a>示例

**单个程序集**

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

**特定于目标框架的单个程序集**

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

**使用通配符的 DLL 集**

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

**适用于不同框架的 DLL**

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

**排除文件**

    Source files:
        \tools\fileA.bak
        \tools\fileB.bak
        \tools\fileA.log
        \tools\build\fileB.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a>包含内容文件

内容文件是包需要包含在项目中的不可变文件。 不可变文件指的是使用项目不会修改的文件。 内容文件示例包括：

- 作为资源嵌入的图像
- 已编译的源文件
- 需要包含在项目的生成输出中的脚本
- 需要包含在项目中，但不需要进行任何项目特定的更改的包的配置文件

内容文件使用 `<files>` 元素包含在包中，并在 `target` 特性中指定 `content` 文件夹。 但是，使用 PackageReference（而不是使用 `<contentFiles>` 元素）将包安装到项目中时，将忽略这些文件。

为了最大限度地兼容使用项目，一个包最好在两个元素中指定内容文件。

### <a name="using-the-files-element-for-content-files"></a>对内容文件使用文件元素

对于内容文件，只需使用与程序集文件相同的格式，但应在 `target` 属性中将 `content` 指定为基本文件夹，如以下示例所示。

**基本内容文件**

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

**具有目录结构的内容文件**

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

**特定于目标框架的内容文件**

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

**复制到名称中带点的文件夹的内容文件**

在此情况下，NuGet 发现 `target` 中的扩展名与 `src` 中的扩展名不匹配，因此将 `target` 中名称的该部分作为文件夹：

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

**不具有扩展名的内容文件**

若要包含不具有扩展名的文件，请使用 `*` 或 `**` 通配符：

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

**具有深层路径和深层目标的内容文件**

在此情况下，由于源文件和目标文件的扩展名匹配，NuGet 假定目标是文件名而不是文件夹：

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

**重命名包中的内容文件**

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

**排除文件**

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a>对内容文件使用 contentFiles 元素

*NuGet 4.0+ 与 PackageReference*

默认情况下，包将内容放置在 `contentFiles` 文件夹中（见下文），`nuget pack` 使用默认特性将全部文件包含在该文件夹中。 在此情况下，根本没有必要在 `.nuspec` 中包含 `contentFiles` 节点。

若要控制包含哪些文件，`<contentFiles>` 元素指定是 `<files>` 元素的集合，可标识包含的确切文件。

这些文件用一组特性指定，用于描述如何在项目系统中使用这些文件：

| 特性 | 描述 |
| --- | --- |
| **include** | （必需）文件或要包含的文件位置，受 `exclude` 特性指定的排除规则约束。 除非指定了绝对路径，否则路径相对于 `contentFiles` 文件夹。 允许使用通配符 `*`，双通配符 `**` 意味着递归文件夹搜索。 |
| **exclude** | 要从 `src` 位置排除的文件或文件模式的分号分隔列表。 允许使用通配符 `*`，双通配符 `**` 意味着递归文件夹搜索。 |
| **buildAction** | 要分配给 MSBuild 内容项的生成操作，例如 `Content`、`None`、`Embedded Resource`、`Compile` 等。默认值为 `Compile`。 |
| **copyToOutput** | 指示是否将内容项复制到生成（或发布）输出文件夹的布尔值。 默认值为 false。 |
| **flatten** | 一个布尔值，用于指示是将内容项复制到生成输出中的单个文件夹 (true)，还是保留包中的文件夹结构 (false)。 此标志仅在 copyToOutput 标志设置为 true 时才有效。 默认值为 false。 |

安装包时，NuGet 从上到下应用 `<contentFiles>` 的子元素。 如果多个条目与相同的文件匹配，那么应用全部条目。 如果相同特性发生冲突，则最上面的条目将替代靠下的条目。

#### <a name="package-folder-structure"></a>包文件夹结构

包项目应使用以下模式构建内容结构：

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- `codeLanguages` 可以是 `cs`、`vb`、`fs`、`any` 或给定 `$(ProjectLanguage)` 的小写等效形式
- `TxM` 是 NuGet 支持的任何合法目标框架名字对象（请参阅[目标框架](../reference/target-frameworks.md)）。
- 任何文件夹结构都可以附加到此语法的末尾。

例如:

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

空文件夹可以使用 `.` 来选择不提供特定语言和 TxM 组合的内容，例如：

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a>contentFiles 部分示例

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <contentFiles>
            <!-- Embed image resources -->
            <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
            <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

            <!-- Embed all image resources under contentFiles/cs/ -->
            <files include="cs/**/*.png" buildAction="EmbeddedResource" />

            <!-- Copy config.xml to the root of the output folder -->
            <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

            <!-- Copy run.cmd to the output folder and keep the directory structure -->
            <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

            <!-- Include everything in the scripts folder except exe files -->
            <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
        </contentFiles>
        </metadata>
</package>
```

## <a name="example-nuspec-files"></a>示例 nuspec 文件

**未指定依赖项或文件的简单 `.nuspec`**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

**具有依赖项的 `.nuspec`**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

**具有文件的 `.nuspec`**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

**具有 Framework 程序集的 `.nuspec`**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

在此示例中，为特定的项目目标安装了以下内容：

- .NET4 -> `System.Web``System.Net`
- .NET4 Client Profile -> `System.Net`
- Silverlight 3 -> `System.Json`
- WindowsPhone -> `Microsoft.Devices.Sensors`
