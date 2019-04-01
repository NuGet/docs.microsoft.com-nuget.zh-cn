---
title: NuGet CLI pack 命令
description: Nuget.exe pack 命令参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 9db24b2dd6ced0869ac84b25f9796ded5df10f86
ms.sourcegitcommit: d5a35a097e6b461ae791d9f66b3a85d5219d7305
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56145639"
---
# <a name="pack-command-nuget-cli"></a>pack 命令 (NuGet CLI)

**适用于：** 创建包&bullet;**受支持的版本：** 2.7+

创建基于指定的 NuGet 包`.nuspec`或项目文件。 `dotnet pack`命令 (请参阅[dotnet 命令](dotnet-Commands.md)) 和`msbuild -t:pack`(请参阅[MSBuild 目标](../reference/msbuild-targets.md)) 可以用作备用项。

> [!Important]
> 在 Mono 下从项目文件创建包不支持。 您还需要调整中的非本地路径`.nuspec`nuget.exe 不会将自身的 Windows 路径名转换为 Unix 样式的路径，到文件。

## <a name="usage"></a>用法

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

其中`<nuspecPath>`并`<projectPath>`指定`.nuspec`或项目文件，分别。

## <a name="options"></a>选项

| Option | 描述 |
| --- | --- |
| BasePath | 设置中定义的文件的基路径`.nuspec`文件。 |
| Build | 指定应在生成包之前生成项目。 |
| Exclude | 指定创建包时要排除的一个或多个通配符模式。 若要指定多个模式，请重复-排除标志。 请参阅下面的示例。 |
| ExcludeEmptyDirectories | 生成包时，会阻止包含空的目录。 |
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。 |
| ConfigFile | 指定 pack 命令的配置文件。 |
| Help | 显示的帮助命令的信息。 |
| IncludeReferencedProjects | 指示生成的包应包括引用的项目作为依赖项或作为包的一部分。 如果引用的项目有一个相应`.nuspec`具有相同名称，为项目，则该引用的项目添加为依赖项的文件。 否则，引用的项目添加为包的一部分。 |
| MinClientVersion | 设置*minClientVersion*创建的包的属性。 此值将覆盖现有值*minClientVersion*中的属性 （如果有）`.nuspec`文件。 |
| MSBuildPath | *（4.0 +)* 指定的路径优先于命令中使用 MSBuild `-MSBuildVersion`。 |
| MSBuildVersion | *（3.2 +)* 指定要用于此命令的 MSBuild 版本。 支持的值为 4，12、 14、 15.1、 15.3、 15.4、 15.5、 15.6、 15.7、 15.8，15.9。 默认情况下，选择你的路径中的 MSBuild，否则它默认为最高的已安装版本的 MSBuild。 |
| NoDefaultExcludes | 可防止默认排除的 NuGet 包文件和文件和文件夹启动带有圆点，如`.svn`和`.gitignore`。 |
| NoPackageAnalysis | 指定 pack 不应在生成包后运行包分析。 |
| OutputDirectory | 指定在其中存储创建的包的文件夹。 如果未不指定任何文件夹，则使用当前文件夹。 |
| Properties | 其他选项后应显示最后一个命令行上。 指定重写项目文件中; 中的值的属性的列表请参阅[常用的 MSBuild 项目属性](/visualstudio/msbuild/common-msbuild-project-properties)属性名称。 此处的属性参数是一系列令牌 = 值对，用分号分隔，其中的每个匹配项`$token$`中`.nuspec`文件将替换为给定的值。 值可以为在引号内的字符串。 请注意，对于"配置"属性中，默认值"Debug"。 若要将更改为发布配置，请使用`-Properties Configuration=Release`。 |
| Suffix | *(3.4.4+)* 将后缀追加到在内部生成的版本号，通常用于追加生成或其他预发布版本标识符。 例如，使用`-suffix nightly`将使用版本编号类似于创建包`1.2.3-nightly`。 后缀必须以字母以避免警告、 错误和使用不同版本的 NuGet 和 NuGet 包管理器可能不兼容问题开头。 |
| Symbols | 指定包包含源和符号。 与一起使用时`.nuspec`文件，这将创建常规 NuGet 包文件和对应的符号包。 默认情况下它会创建[旧符号包](../create-packages/Symbol-Packages.md)。 符号包的新推荐格式为 .snupkg。 请参阅[创建符号包 (.snupkg)](../create-packages/Symbol-Packages-snupkg.md)。 |
| Tool | 指定应将该项目的输出文件放在`tool`文件夹。 |
| Verbosity | 指定的输出中显示的详细信息：*正常*，*静默*，*详细*。 |
| Version | 重写从版本号`.nuspec`文件。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>不包括开发依赖项

一些 NuGet 包可为开发依赖项，帮助你创作你自己的库，但不一定需要为实际的包依赖项。

`pack`命令将忽略`package`中的条目`packages.config`具有`developmentDependency`属性设置为`true`。 将作为依赖项中创建的包中包括这些项。

例如，请考虑以下`packages.config`源项目文件中：

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

对于此项目，包创建的`nuget pack`将具有依赖关系`jQuery`并`microsoft-web-helpers`但不是`netfx-Guard`。

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
