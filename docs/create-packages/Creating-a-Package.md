---
title: 如何创建 NuGet 包
description: 设计和创建 NuGet 包流程的详细指南，包含文件和版本控制等关键决策点。
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: db02089bec3d2b8c001518fa0542375dc5418eb8
ms.sourcegitcommit: c825eb7e222d4a551431643f5b5617ae868ebe0a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/19/2018
ms.locfileid: "51944062"
---
# <a name="creating-nuget-packages"></a>创建 NuGet 包

无论包是什么用途或者它包含什么代码，均使用 `nuget.exe` 将该功能打包进可以与任意数量的其他开发人员共享且可以由其使用的组件中。 若要安装 `nuget.exe`，请参阅[安装 NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli)。 请注意，Visual Studio 不会自动包含 `nuget.exe`。

从技术角度来讲，NuGet 包仅仅是一个使用 `.nupkg` 扩展重命名且其中的内容与特定约定相匹配的 ZIP 文件。 本主题介绍创建满足这些约定的包的详细流程。 有关重点演练，请参阅[快速入门：创建和发布包](../quickstart/create-and-publish-a-package.md)。

包以编译的代码（程序集）、符号和/或需要作为包传送的其他文件开头（请参阅[概述和工作流](overview-and-workflow.md)）。 尽管可以使用项目文件中信息的描述来保持编译程序集和包的同步，但此流程独立于编译或生成进入包的文件。

> [!Note]
> 本主题适用于除使用 Visual Studio 2017 和 NuGet 4.0+ 的 .NET Core 项目以外的项目类型。 在这些 .NET Core 项目中，NuGet 直接使用项目文件中的信息。 有关详细信息，请参阅[使用 Visual Studio 2017 创建 .NET Standard 包](../guides/create-net-standard-packages-vs2017.md)和[ NuGet 包和作为 MSBuild 目标还原](../reference/msbuild-targets.md)。

## <a name="deciding-which-assemblies-to-package"></a>确定要打包的程序集

大多数通用包包含一个或多个其他开发人员可在其自己项目中使用的程序集。

- 通常情况下，最好每个 NuGet 包有一个程序集，前提是每个程序集可独立正常运行。 例如，如果有一个 `Utilities.dll` 依赖于 `Parser.dll` 且 `Parser.dll` 可独立正常运行，则为每一个创建一个包。 这样做使得开发人员能够独立于 `Utilities.dll` 使用 `Parser.dll`。

- 如果库由多个不能独立正常运行的程序集构成，那么可以将它们合并到一个包中。 使用上面的示例，如果 `Parser.dll` 包含仅由 `Utilities.dll` 使用的代码，那么可以将 `Parser.dll` 保留在同一包中。

- 同样，如果 `Utilities.dll` 依赖于 `Utilities.resources.dll` 并且后者不能独立正常运行，则将两者放入同一包中。

事实上，资源是一种特殊情况。 当包安装到项目中时，NuGet 自动将程序集引用添加到包的 DLL，不包含命名为 `.resources.dll` 的内容，因为它们被假定为本地化的附属程序集（请参阅[创建本地化包](creating-localized-packages.md)）。 为此，请避免对包含基本包代码的文件使用 `.resources.dll`。

如果库包含 COM 互操作程序集，请遵循[使用 COM 互操作程序集创作包](#authoring-packages-with-com-interop-assemblies)中的其他准则。

## <a name="the-role-and-structure-of-the-nuspec-file"></a>.nuspec 文件的角色和结构

一旦知道需要打包的文件后，下一步是在 `.nuspec` XML 文件中创建包清单。

清单：

1. 介绍包的内容和自己是否包含在包中。
1. 驱动包的创建并且指示 NuGet 如何将包安装到项目。 例如，清单识别其他包依赖项，这样，NuGet 还可以在安装主包时安装这些依赖项。
1. 如下所示，包含所需属性和可选属性。 有关确切的详细信息（包括此处未提及的其他属性），请参阅 [.nuspec 引用](../reference/nuspec.md)。

所需属性：

- 包标识符在承载包的库中必须是唯一的。
- 窗体 Major.Minor.Patch[-Suffix] 中特定的版本号，其中 -Suffix 标识[预发布版本](prerelease-packages.md)
- 包标题应出现在主机上（例如 nuget.org）
- 创建者和所有者信息。
- 对包的详细说明。

常见可选属性：

- 发行说明
- 版权信息
- 对 [Visual Studio 中的包管理器 UI](../tools/package-manager-ui.md) 的简短说明
- 区域设置 ID
- 项目 URL
- 作为表达式或文件的许可证（`licenseUrl` 将被弃用，请使用 [`license` nuspec 元数据元素](../reference/nuspec.md#license)）
- 图标 URL
- 依赖项和引用的列表
- 协助库搜索的标记

以下是典型（但虚构）的 `.nuspec` 文件，其中注释介绍属性：

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
        <!-- The identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- The package version number that is used when resolving dependencies -->
        <version>1.8.3-beta</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>
        
         <!-- Project URL provides a link for the gallery -->
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

         <!-- License information is displayed on the gallery -->
        <license type="expression">Apache-2.0</license>
        

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

有关声明依赖项并指定版本号的详细信息，请参阅[包版本控制](../reference/package-versioning.md)。 还可以使用 `dependency` 元素上的 `include` 和 `exclude` 特性直接在包中结合依赖项的资产。 请参阅 [.nuspec 引用 - 依赖项](../reference/nuspec.md#dependencies)。

因为清单包含在从清单创建的包中，所以可以通过检查现有包查找任意数目的其他示例。 计算机上的 global-packages 文件夹是一个不错的源，其位置由以下命令返回：

```cli
nuget locals -list global-packages
```

转到任意 package\version 文件夹，将 `.nupkg` 文件复制到 `.zip` 文件，然后打开该 `.zip` 文件并检查其中的 `.nuspec`。

> [!Note]
> 从 Visual Studio 项目创建 `.nuspec` 时，清单包含生成包时被项目信息替换的令牌。 请参阅[从 Visual Studio 项目创建 .nuspec](#from-a-visual-studio-project)。

## <a name="creating-the-nuspec-file"></a>创建 .nuspec 文件

创建完整的清单通常以通过以下其中一种方法生成的基础 `.nuspec` 文件开始：

- [基于约定的工作目录](#from-a-convention-based-working-directory)
- [程序集 DLL](#from-an-assembly-dll)
- [Visual Studio 项目](#from-a-visual-studio-project)    
- [包含默认值的新文件](#new-file-with-default-values)

然后手动编辑文件，使它可以在最终包中描述所需的确切内容。

> [!Important]
> 生成 `.nuspec` 文件包含的占位符必须在使用 `nuget pack` 命令创建包前修改。 如果 `.nuspec` 包含任意占位符，则命令失败。

### <a name="from-a-convention-based-working-directory"></a>来自基于约定的工作目录

因为 NuGet 包仅仅是使用 `.nupkg` 扩展名重命名的 ZIP 文件，所以在本地文件系统上创建所需文件夹结构，然后从该结构直接创建 `.nuspec` 文件通常最简单。 然后，`nuget pack` 命令自动将所有文件添加到该文件夹结构（不包含以 `.` 开头的文件夹，从而在同一结构中保留专用文件）。

此方法的优势是无需在清单中指定需要包含在包中的文件（如本主题后面所述）。 可以轻松使得生成进程生成进入包中的确切文件夹结构，并且可以轻松包含不是项目一部分的其他文件：

- 应注入目标项目的内容和源代码。
- PowerShell 脚本（NuGet 2.x 中使用的包也可以包含安装脚本，这在 NuGet 3.x 以及更高版本中不受支持）。
- 转换到现有配置和项目中的源代码文件。

文件夹约定如下所示：

| 文件夹 | 描述 | 包安装时的操作 |
| --- | --- | --- |
| （根） | readme.txt 的位置 | 包安装时，Visual Studio 在包根目录中显示 readme.txt 文件。 |
| lib/{tfm} | 特定目标框架名字对象 (TFM) 的程序集 (`.dll`)、文档 (`.xml`) 和符号 (`.pdb`) 文件 | 程序集添加为引用，以用于编译和运行时；`.xml` 和 `.pdb` 复制到项目文件夹中。 有关创建框架特定目标子文件夹的详细信息，请参阅[支持多个目标框架](supporting-multiple-target-frameworks.md)。 |
| ref/{tfm} | 给定目标框架名字对象 (TFM) 的程序集 (`.dll`) 和符号 (`.pdb`) 文件 | 程序集添加为引用，仅用于编译时；因此，不会向项目 Bin 文件夹复制任何内容。 |
| runtimes | 特定于体系结构的程序集 (`.dll`)、符号 (`.pdb`) 和本机源 (`.pri`) 文件 | 程序集添加为引用，仅用于运行时；其他文件复制到项目文件夹中。 在 `AnyCPU` 文件夹下应始终具有特定于相应的 (TFM) `/ref/{tfm}` 的程序集，以提供相应的编译时程序集。 请参阅[支持多个目标框架](supporting-multiple-target-frameworks.md)。 |
| 内容 | 任意文件 | 内容复制到项目根目录。 将“内容”文件夹视为最终使用包的目标应用程序的根目录。 若要使包在应用程序的 /images 文件夹中添加图片，请将其置于包的 content/images 文件夹中。 |
| 生成 | MSBuild `.targets` 和 `.props` 文件 | 自动插入到项目文件或 `project.lock.json` (NuGet 3.x+)。 |
| 工具 | 可从包管理器控制台访问 Powershell 脚本和程序 | `tools` 文件夹添加到仅适用于包管理器控制台的 `PATH` 环境变量（尤其是不作为 MSBuild 集在生成项目时添加到 `PATH`）。 |

因为文件夹结构可能包含任意数量的目标框架的任意数量的程序集，所以此方法在创建支持多个框架的包时是必要的。

在任何情况下，一旦准备好所需文件夹结构，则在该文件夹中运行以下命令以创建 `.nuspec` 文件：

```cli
nuget spec
```

同样，生成的 `.nuspec` 不包含文件夹结构中的文件的显式引用。 包创建时，NuGet 自动包含所有文件。 但是，还需在清单的其他部分中编辑占位符值。

### <a name="from-an-assembly-dll"></a>来自程序集 DLL

在从程序集创建包的简单情况下，可以使用以下命令从程序集中的元数据生成 `.nuspec` 文件：

```cli
nuget spec <assembly-name>.dll
```

使用此窗体将清单中的一些占位符替换为程序集的特定值。 例如，`<id>` 属性设为程序集名称，`<version>` 设为程序集版本。 但是，清单中的其他属性在程序集中没有匹配值，因此仍包含占位符。

### <a name="from-a-visual-studio-project"></a>来自 Visual Studio 项目

从 `.csproj` 或 `.vbproj` 文件创建 `.nuspec` 较为方便，因为其他已安装到这些项目的包会自动引用为依赖项。 只需使用与项目文件相同的文件夹中的命令：

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

生成的 `<project-name>.nuspec` 文件包含在打包时替换为项目值的令牌，包含对所有其他已安装的包的引用。

令牌在项目属性的两侧由 `$` 符号分隔。 例如，通过此方法生成的清单中的 `<id>` 值通常如下所示：

```xml
<id>$id$</id>
```

此令牌在打包时替换为项目文件的 `AssemblyName` 值。 有关项目值到 `.nuspec` 令牌的确切映射，请参阅[替换令牌引用](../reference/nuspec.md#replacement-tokens)。

借助令牌，更新项目时可以不再需要更新关键值，例如 `.nuspec` 中的版本号。 （如果需要，随时可以使用文本值替换令牌）。 

注意在 Visual Studio 项目中工作时，有多个可用的其他打包选项，如稍后的[运行 NuGet 包生成 .nupkg 文件](#running-nuget-pack-to-generate-the-nupkg-file)所述。

#### <a name="solution-level-packages"></a>解决方案级别包

*仅适用于 NuGet 2.x。在 NuGet 3.0+ 中不可用。*

NuGet 2.x 支持为包管理器控制台（`tools` 文件夹的内容）安装工具或其他命令的解决方案级别包的概念，但是不会将引用、内容或生成自定义添加到解决方案中的任何项目中。 该包在其直接 `lib`、`content` 或 `build` 文件夹中未包含文件，并且它的依赖项各自的 `lib`、`content` 或 `build` 文件夹中也没有文件。

NuGet 在 `.nuget` 文件夹的 `packages.config` 文件（而不是项目的 `packages.config` 文件）中，跟踪安装的解决方案级别包。

### <a name="new-file-with-default-values"></a>包含默认值的新文件

以下命令使用占位符创建默认清单，这可确保一开始就使用正确的文件结构：

```cli
nuget spec [<package-name>]
```

如果忽略 \<package-name\>，生成的文件是 `Package.nuspec`。 如果提供 `Contoso.Utility.UsefulStuff` 等名称，则文件是 `Contoso.Utility.UsefulStuff.nuspec`。

生成的 `.nuspec` 包含值的占位符（例如 `projectUrl`）。 请确保在使用文件创建最终 `.nupkg` 文件前编辑该文件。

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a>选择唯一包标识符并设置版本号

包标识符（`<id>` 元素）和版本号（`<version>` 元素）是清单中最重要的两个值，因为它们唯一标识包中包含的确切代码。

**针对包标识符的最佳做法：**

- **唯一性**：标识符在 nuget.org 或承载包的任意库中必须是唯一的。 确定标识符之前，请搜索适用库以检查该名称是否已使用。 为了避免冲突，最好使用公司名作为标识符的第一部分（例如 `Contoso.`）。
- **类似命名空间的名称**：遵循类似于 .NET 中命名空间的模式，使用点表示法而不是连字符。 例如，使用 `Contoso.Utility.UsefulStuff` 而不是 `Contoso-Utility-UsefulStuff` 或 `Contoso_Utility_UsefulStuff`。 当包标识符与代码中使用的命名空间相匹配时，这个方法也很有用。
- **示例包**：如果生成演示如何使用另一个包的示例代码的包，则附加 `.Sample` 作为标识符的后缀，与 `Contoso.Utility.UsefulStuff.Sample` 中相似。 （当然，示例包会在其他包上有依赖项。）创建示例包时，使用前面介绍的基于约定的工作目录方法。 在 `content` 文件夹中，在名为 `\Samples\<identifier>` 的文件夹中排列示例代码，与 `\Samples\Contoso.Utility.UsefulStuff.Sample` 中相似。

**针对包版本的最佳做法：**

- 一般情况下，将包的版本设置为与库相匹配，但这不是必须的。 如之前在[确定要打包的程序集](#deciding-which-assemblies-to-package)中所述，将包限制到单个程序集是一个简单的问题。 总的来说，请记住解析依赖项时，NuGet 自己处理包版本而不是程序集版本。
- 使用非标准版本方案时，请确保考虑使用 NuGet 版本控制规则，如[包版本控制](../reference/package-versioning.md)中所述。

> 以下一系列简短博客文章也有助于理解版本控制：
>
> - [第 1 部分：解决 DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [第 2 部分：核心算法](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [第 3 部分：通过绑定重定向统一](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a>设置包类型

通过 NuGet 3.5+ 可以使用特定的包类型标记包以指示其预期用途。 未标记类型的包（包含使用更早版本的 NuGet 创建的所有包）默认为 `Dependency` 类型。

- `Dependency` 类型包将生成或运行时资产添加到库和应用程序，并且可以在任何项目类型中安装（假设它们相互兼容）。

- `DotnetCliTool` 类型包是 [.NET CLI](/dotnet/articles/core/tools/index) 的扩展，并且从命令行中调用。 该包仅在 .NET Core 项目中安装并且不影响还原操作。 [.NET Core 扩展性](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility)文档中提供更多有关这些项目扩展的详细信息。

- 自定义类型包使用与包 ID 遵守相同格式规则的任意类型标识符。 但是，任何不是 `Dependency` 和 `DotnetCliTool` 的类型不会被 Visual Studio 中的 NuGet 包管理器识别。

包类型在 `.nuspec` 文件中设置。 后向兼容最好不显式设置 `Dependency` 类型，而是依赖 NuGet 在没有指定类型时假设此类型。

- `.nuspec`：指示 `<metadata>` 元素的 `packageTypes\packageType` 节点中的包类型：

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

## <a name="adding-a-readme-and-other-files"></a>添加自述文件和其他文件

若要直接指定要包含在包中的文件，请使用 `.nuspec` 中的 `<files>` 节点，其遵循 `<metadata>` 标记：

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> 使用基于约定的工作目录方法时，可以将 readme.txt 置于包根目录中并将其他内容置于 `content` 文件夹中。 清单中不需要 `<file>` 元素。

如果包根目录中包含名为 `readme.txt` 的文件，Visual Studio 在直接安装包之后立即将该文件的内容显示为纯文本。 （对于安装为依赖项的包，不会显示自述文件）。 例如，下面是 HtmlAgilityPack 包的自述文件的显示方式：

![安装时 NuGet 包的自述文件的显示](media/Create_01-ShowReadme.png)

> [!Note]
> 如果 `.nuspec` 文件中包含空 `<files>` 节点，则 NuGet 不会在包中包含除 `lib` 文件夹中的内容以外的任何其他内容。

## <a name="including-msbuild-props-and-targets-in-a-package"></a>包含包中的 MSBuild 属性和目标

在某些情况下，可能需要在使用包的项目中添加自定义生成目标或属性，例如生成期间运行自定义工具或进程。 通过将文件置于项目的 `\build` 文件夹中的窗体 `<package_id>.targets` 或 `<package_id>.props`（例如 `Contoso.Utility.UsefulStuff.targets`）中执行此操作。

根 `\build` 文件夹中的文件被视为适用于所有目标框架。 若要提供特定于框架的文件，首先将其放置到合适的子文件夹中，如下所示：

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

然后在 `.nuspec` 文件中，确保参阅 `<files>` 节点中的这些文件：

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

在包中包含 MSBuild 属性和目标是 [NuGet 2.5 中引入的功能](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files)，因此建议将 `minClientVersion="2.5"` 属性添加到 `metadata` 元素，以指示使用该包所需的最低 NuGet 客户端版本。

当 NuGet 使用 `\build` 文件安装包时，它在指向 `.targets` 和 `.props` 文件的项目文件中添加 MSBuild `<Import>` 元素。 （`.props` 添加到项目文件顶部；`.targets` 添加到底部。）为每个目标框架添加了单独的条件 MSBuild `<Import>` 元素。

可将跨框架目标的 MSBuild `.props` 和 `.targets` 文件置于 `\buildCrossTargeting` 文件夹中。 在包安装期间，NuGet 将相应的 `<Import>` 元素添加到项目文件中，前提是目标框架未设置（MSBuild 属性 `$(TargetFramework)` 必须为空）。

对于 NuGet 3.x，目标不添加到项目，而是通过 `project.lock.json` 提供。

## <a name="authoring-packages-with-com-interop-assemblies"></a>使用 COM 互操作程序集创作包

包含 COM 互操作程序集的包必须包含合适的[目标文件](#including-msbuild-props-and-targets-in-a-package)，使正确的 `EmbedInteropTypes` 元数据使用 PackageReference 格式添加到项目。 默认情况下，使用 PackageReference 时，`EmbedInteropTypes` 元数据对所有程序集一直为 false，所以目标文件显式添加此元数据。 为了避免冲突，目标名称必须是唯一的；理想情况下，使用包名称和嵌入程序集的组合，使用此值替换下例中的 `{InteropAssemblyName}`。 （有关示例，另请参阅 [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop)。）

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

请注意，在使用 `packages.config` 管理格式时，将引用从包添加到程序集会导致 NuGet 和 Visual Studio 检查 COM 互操作程序集并在项目文件中将 `EmbedInteropTypes` 设为 true。 在这种情况下，目标被替代。

此外，默认情况下，[生成资产不以可传递的方式流动](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。 当此处所述的创作的包作为可传递的依赖项从项目拉取到项目引用时，它们会以不同的方式工作。 包使用者通过将 PrivateAssets 默认值修改为不包含生成使其流动。

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a>运行 NuGet 包生成 .nupkg 文件

使用程序集或基于约定的工作目录时，通过使用 `.nuspec` 文件运行 `nuget pack` 创建包，使用特定的文件名替换 `<project-name>`：

```cli
nuget pack <project-name>.nuspec
```

使用 Visual Studio 项目时，使用项目文件运行 `nuget pack`，该项目文件自动加载项目的 `.nuspec` 文件并使用项目文件中的值替换其中的任意令牌：

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> 令牌替换需要直接使用项目文件，因为项目是令牌值的源。 如果将 `nuget pack` 用于 `.nuspec` 文件，不会发生令牌替换。

在所有情况下，`nuget pack` 不包含句点开头的文件夹，例如 `.git` 或 `.hg`。

NuGet 指示需要更正的 `.nuspec` 文件中是否有错误，例如忘记更改清单中的占位符值。

一旦 `nuget pack` 成功，就有一个可以发布到合适库的 `.nupkg` 文件，如[发布包](../create-packages/publish-a-package.md)中所述。

> [!Tip]
> 一个检查创建后的包的有用方法是在[包资源管理器](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)工具中打开它。 这会为你提供包内容及其清单的图形视图。 还可以将生成的 `.nupkg` 文件重命名为 `.zip` 文件并直接浏览其内容。

### <a name="additional-options"></a>附加选项

可通过 `nuget pack` 使用多种命令行开关，以排除文件、替代清单中的版本号和更改输出文件夹等。 有关完整列表，请参考[包命令引用](../tools/cli-ref-pack.md)。

以下是 Visual Studio 项目中的一些常见选项：

- **引用项目**：如果项目引用其他项目，通过使用 `-IncludeReferencedProjects` 选项，可以将引用项目添加为包的一部分或依赖项：

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    此包含过程是递归的，所以如果 `MyProject.csproj` 引用项目 B 和 C，且这些项目引用 D、E 和 F，那么 B、C、D、E 和 F 中的文件包含在包中。

    如果引用的项目包含其自身的 `.nuspec` 文件，那么 NuGet 将该引用的项目添加为依赖项。  需要单独打包和发布该项目。

- **生成配置**：默认情况下，NuGet 使用项目文件中设置的默认生成配置，通常是“调试”。 若要从不同的生成配置（例如“发布”）中打包文件，使用包含以下配置的 `-properties` 选项：

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **符号**：若要包含允许使用者在调试器中单步执行包代码的符号，请使用 `-Symbols` 选项：

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a>测试包安装

发布包前，通常需要测试将包安装到项目的过程。 测试确保所有文件一定在项目中正确的位置结束。

可以在 Visual Studio 中手动测试安装，或是使用常规[包安装步骤](../consume-packages/ways-to-install-a-package.md)在命令行上测试。

对于自动测试，基本流程如下所示：

1. 将 `.nupkg` 文件复制到本地文件夹。
1. 使用 `nuget sources add -name <name> -source <path>` 命令将文件夹添加到包源（请参阅 [nuget 源](../tools/cli-ref-sources.md)）。 请注意，只需在任意给定计算机上设置一次此本地源。
1. 使用 `nuget install <packageID> -source <name>`（其中 `<name>` 与提供给 `nuget sources` 的源名称相匹配）从该源安装包。 指定源可确保包从该源中单独安装。
1. 检查文件系统以检查文件是否正确安装。

## <a name="next-steps"></a>后续步骤

创建包（`.nupkg` 文件）后，可以将其发布到选择的库，如[发布包](../create-packages/publish-a-package.md)中所述。

你可能还希望扩展包的功能，或者支持其他方案，如以下主题所述：

- [包版本控制](../reference/package-versioning.md)
- [支持多个目标框架](../create-packages/supporting-multiple-target-frameworks.md)
- [源和配置文件的转换](../create-packages/source-and-config-file-transformations.md)
- [本地化](../create-packages/creating-localized-packages.md)
- [预发布版本](../create-packages/prerelease-packages.md)

最后，有需要注意的其他包类型：

- [本机包](../create-packages/native-packages.md)
- [符号包](../create-packages/symbol-packages.md)
