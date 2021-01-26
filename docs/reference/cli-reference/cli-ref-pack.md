---
title: NuGet CLI 包命令
description: nuget.exe pack 命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e2906d53119cb8c922df7d177cd686836ac50a5a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780046"
---
# <a name="pack-command-nuget-cli"></a> (NuGet CLI) 打包命令

**适用于：** 创建包的 &bullet; **支持版本：** 2.7 +

基于指定的 [nuspec](../nuspec.md) 或项目文件创建 NuGet 包。 `dotnet pack`命令 (参阅[dotnet 命令](../dotnet-Commands.md)) 和 `msbuild -t:pack` (查看[MSBuild 目标](../msbuild-targets.md)) 可用作备用项。

> [!Important]
> [`dotnet pack`](../dotnet-Commands.md) [`msbuild -t:pack`](../msbuild-targets.md) 为基于[PackageReference](../../consume-packages/package-references-in-project-files.md)的项目使用或。
> 在 Mono 下，不支持从项目文件创建包。 还需要将文件中的非本地路径调整 `.nuspec` 为 Unix 样式路径，因为 nuget.exe 不会转换 Windows 路径名本身。

## <a name="usage"></a>使用情况

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

， `<nuspecPath>` 并 `<projectPath>` 分别指定 `.nuspec` 或项目文件。

## <a name="options"></a>选项
- **`-BasePath`**

   设置在 [nuspec](../nuspec.md) 文件中定义的文件的基路径。

- **`-Build`**

  指定应在生成包之前生成项目。

- **`-ConfigFile`**

  要应用的 NuGet 配置文件。 如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-Exclude`**

  指定创建包时要排除的一个或多个通配符模式。 若要指定多个模式，请重复-Exclude 标志。 请参阅以下示例。

- **`-ExcludeEmptyDirectories`**

  在生成包时阻止包含空目录。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 使用固定的、基于英语的区域性强制运行 nuget.exe。

- **`-?|-help`**

  显示命令的帮助信息。

- **`-IncludeReferencedProjects`**

  指示生成的包应包含作为依赖项或包的一部分的引用项目。 如果引用的项目具有与 `.nuspec` 项目具有相同名称的相应文件，则会将引用的项目添加为依赖项。 否则，被引用项目作为包的一部分添加。

- **`-InstallPackageToOutputPath`**

  指定该命令是否应准备包输出目录以支持共享作为源。

- **`-MinClientVersion`**

  设置所创建的包的 *minClientVersion* 属性。 如果文件中有任何)  (，此值将覆盖现有的 *minClientVersion* 属性的值 `.nuspec` 。

- **`-MSBuildPath`**

  *(4.0 +)* 指定要与命令一起使用的 MSBuild 的路径，优先于 `-MSBuildVersion` 。

- **`-MSBuildVersion`**

  *(3.2 +)* 指定要与此命令一起使用的 MSBuild 版本。 支持的值为4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。 默认情况下，将选取路径中的 MSBuild，否则默认为已安装的最高版本的 MSBuild。

- **`-NoDefaultExcludes`**

  禁止默认排除 NuGet 包文件和以点（例如和）开头的文件和文件夹 `.svn` `.gitignore` 。

- **`-NonInteractive`**

  禁止提示用户输入或确认。

- **`-NoPackageAnalysis`**

  指定 pack 不应在生成包后运行包分析。

- **`-OutputDirectory`**

  指定在其中存储创建的包的文件夹。 如果未指定文件夹，则使用当前文件夹。

- **`-OutputFileNamesWithoutVersion`**

  指定该命令是否应在不包含版本的情况下准备包输出名称。

- **`-PackagesDirectory`**

  指定包文件夹。

- **`-p|-Properties`**

  应在其他选项后出现在命令行的最后。 指定重写项目文件中的值的属性的列表;请参阅属性名称的 [常用 MSBuild 项目属性](/visualstudio/msbuild/common-msbuild-project-properties) 。 此处的 Properties 参数是标记 = 值对列表，用分号分隔，其中每个 `$token$` 在文件中出现的 `.nuspec` 都将替换为给定的值。 值可以是用引号引起来的字符串。 请注意，对于 "配置" 属性，默认值为 "调试"。 若要更改为发布配置，请使用 `-Properties Configuration=Release` 。 **一般情况** 下，属性应该与在相应的项目生成过程中使用的属性相同，以避免潜在的异常行为。

- **`-SolutionDirectory`**

  指定解决方案目录。

- **`-Suffix`**

  *(3.4.4 +)* 将后缀追加到内部生成的版本号，通常用于追加生成或其他预发行标识符。 例如，使用 `-suffix nightly` 将创建一个版本号与相同的包 `1.2.3-nightly` 。 后缀必须以字母开头，以避免与不同版本的 NuGet 和 NuGet 包管理器的警告、错误和可能的不兼容性。

- **`-SymbolPackageFormat`**

  创建符号包时，允许在和格式之间进行 `snupkg` 选择 `symbols.nupkg` 。

- **`-Symbols`**

  指定包包含源和符号。 与文件一起使用时 `.nuspec` ，将创建一个常规 NuGet 包文件和相应的符号包。 默认情况下，它会创建 [旧的符号包](../../create-packages/Symbol-Packages.md)。 符号包的新推荐格式为 .snupkg。 请参阅[创建符号包 (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md)。

- **`-Tool`**

   指定应将项目的输出文件放在 `tool` 文件夹中。

- **`-Verbosity [normal|quiet|detailed]`**

  指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。

- **`-Version`**

  覆盖文件中的版本号 `.nuspec` 。

另请参阅 [环境变量](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>排除开发依赖项

某些 NuGet 包可用作开发依赖项，它们可帮助你创作自己的库，但不一定是实际的包依赖项。

`pack`命令将忽略 `package` 中 `packages.config` `developmentDependency` 属性设置为的项 `true` 。 这些项不会作为依赖项包含在所创建的包中。

例如，请考虑 `packages.config` 源项目中的以下文件：

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

对于此项目，创建的包 `nuget pack` 将依赖于 `jQuery` 和， `microsoft-web-helpers` 而不是 `netfx-Guard` 。

## <a name="suppressing-pack-warnings"></a>抑制包警告

尽管建议你在包操作期间解决所有 NuGet 警告，但在某些情况下禁止它们是保证的。

可以通过以下方式实现此目的： 

> nuget.exe pack nuspec-Properties NoWarn = NU5104

## <a name="examples"></a>示例

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
