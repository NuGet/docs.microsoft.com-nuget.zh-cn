---
title: NuGet CLI 包命令
description: Nuget.exe 包命令参考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3140d56ac827d932c2323182ad040b8a4d14da5c
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818027"
---
# <a name="pack-command-nuget-cli"></a>包 (NuGet CLI) 命令

**适用于：** ，创建包&bullet;**受支持的版本：** 2.7 +

创建根据指定的 NuGet 包`.nuspec`或项目文件。 `dotnet pack`命令 (请参阅[dotnet 命令](dotnet-Commands.md)) 和`msbuild /t:pack`(请参阅[MSBuild 目标](../reference/msbuild-targets.md)) 可用作备用项。

> [!Important]
> 下单声道，从项目文件创建包不支持。 你还需要调整中的非本地路径`.nuspec`文件于 Unix 样式的路径，如 nuget.exe 未转换 Windows 路径名本身。

## <a name="usage"></a>用法

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

其中`<nuspecPath>`和`<projectPath>`指定`.nuspec`或项目文件中，分别。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| BasePath | 设置中定义的文件的基路径`.nuspec`文件。 |
| 生成 | 指定应在生成包之前生成项目。 |
| 排除 | 指定一个或多个要在创建包时排除的通配符模式。 若要指定多个模式，请重复-排除标志。 请参阅下面的示例。 |
| ExcludeEmptyDirectories | 生成包时，可以防止包含空的目录。 |
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| IncludeReferencedProjects | 该值表示依赖关系或作为包的一部分，生成的包应包含引用的项目。 如果所引用的项目都有一个相应`.nuspec`具有与项目中，相同的名称，则该引用的项目添加为依赖项的文件。 否则，引用的项目将添加作为包的一部分。 |
| MinClientVersion | 设置*minClientVersion*创建的包的属性。 此值将重写现有值*minClientVersion*属性 （如果有） 中`.nuspec`文件。 |
| MSBuildPath | *（4.0 +)* 指定 MSBuild 使用执行命令，优先于的路径`-MSBuildVersion`。 |
| MSBuildVersion | *（3.2 +)* 指定要用于此命令的 MSBuild 的版本。 支持的值为 4、 12、 14、 15。 默认情况下，选择你的路径中的 MSBuild，否则，它默认为最高的已安装版本的 MSBuild。 |
| NoDefaultExcludes | 阻止的 NuGet 的默认排除包文件和文件和文件夹从一个点，如`.svn`和`.gitignore`。 |
| NoPackageAnalysis | 指定 pack 不应在生成包后运行包分析。 |
| OutputDirectory | 指定在其中存储创建的包的文件夹。 如果未不指定任何文件夹，则使用当前文件夹。 |
| 属性 | 应在其他选项后显示最后一个命令行上。 指定的重写项目文件; 中的值的属性的列表请参阅[常用 MSBuild 项目属性](/visualstudio/msbuild/common-msbuild-project-properties)属性名称。 此处的属性自变量是令牌的列表 = 值对，由分号分隔，其中的每个匹配项`$token$`中`.nuspec`文件将替换为给定的值。 值可以是用引号引起来的字符串。 请注意，对于"配置"属性中，默认值是"Debug"。 若要将更改为发布配置，使用`-Properties Configuration=Release`。 |
| 后缀 | *(3.4.4+)* 将后缀追加到内部生成的版本号，通常用于追加生成或其他预发行标识符。 例如，使用`-suffix nightly`将创建具有版本数字类似的包`1.2.3-nightly`。 后缀必须以字母以避免警告、 错误和使用不同版本的 NuGet 和 NuGet 包管理器不兼容的潜在问题开头。 |
| 符号 | 指定包中包含源和符号。 如果用于`.nuspec`文件，这将创建常规的 NuGet 包文件和相应符号包。 |
| 工具 | 指定应将项目的输出文件放在`tool`文件夹。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。 |
| 版本 | 重写从版本号`.nuspec`文件。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>排除开发依赖项

一些 NuGet 程序包都可用作开发依赖关系，可帮助你创作你自己的库，但不一定需要实际包依赖关系。

`pack`命令将忽略`package`中的条目`packages.config`具有`developmentDependency`属性设置为`true`。 这些项将不包括作为中创建的包的依赖关系中。

例如，考虑以下`packages.config`源项目文件中：

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

对于此项目，包创建的`nuget pack`将具有依赖关系`jQuery`和`microsoft-web-helpers`但不是`netfx-Guard`。

## <a name="examples"></a>示例

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
