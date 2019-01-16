---
title: 适用于 NuGet 的.NET 编译器平台分析器格式
description: .NET 分析器的约定，与实现 API 或库的 NuGet 包一起打包并分发。
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0a8db9f6c55b7e79f9b338119e0b3ac6cb7a1e35
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324794"
---
# <a name="analyzer-nuget-formats"></a>分析器 NuGet 格式

.NET 编译器平台 (也称为"Roslyn") 允许开发人员创建[分析器](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix)，检查语法树和语义的代码是在编写。 如这些有助于指导如何使用特定的 API 或库，这为开发人员提供了一种方式创建特定于域的分析工具。 可以在 [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki 上找到详细信息。 另请参阅下文：MSDN 杂志中的[使用 Roslyn 编写 API 的实时代码分析器](https://msdn.microsoft.com/magazine/dn879356.aspx)

分析器本身通常作为实现 API 或相关库的 NuGet 包的一部分进行打包和分发。

有关典型的示例，请参阅 [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) 包，其中包含以下内容：

- analyzers\dotnet\System.Runtime.Analyzers.dll
- analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.Common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- build\System.Runtime.VisualBasic.Analyzers.props
- tools\install.ps1
- tools\uninstall.ps1

正如所见，分析器 DLL 放置于包中的 `analyzers` 文件夹中。

属性文件放置于 `build` 文件夹中，包括这些文件是为了禁用旧的 FxCop 规则以支持分析器实现。

支持使用 `packages.config` 的项目的安装和卸载脚本放置于 `tools` 中。

另请注意，因为此包没有平台特定的需求，因此 `platform` 文件夹已省略。


## <a name="analyzers-path-format"></a>分析器路径格式

`analyzers` 文件夹的使用类似于用于 [框架目标](../create-packages/supporting-multiple-target-frameworks.md)，只是路径中的说明符描述开发主机依赖项而不是生成时。 常规格式如下所示：

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- **framework_name**：所包含 DLL 需要运行的 .NET framework 的可选 API 外围应用。 `dotnet` 是目前唯一有效的值，因为 Roslyn 是唯一可运行分析器的主机。 如果未指定目标，则假定 DLL 适用于所有目标。
- **supported_language**：DLL 适用的语言，`cs` (C#)、`vb` (Visual Basic) 和 `fs` 中的一种。 语言表示应仅为使用该语言的项目加载分析器。 如果未指定任何语言，则假定 DLL 要应用于*所有*支持分析器的语言。
- **analyzer_name**：指定分析器的 DLL。 如果需要 DLL 以外的其他文件，必须通过目标或属性文件包括它们。


## <a name="install-and-uninstall-scripts"></a>安装和卸载脚本

如果使用用户的项目`packages.config`，选取分析器的 MSBuild 脚本不会不起作用，因此应放置`install.ps1`和`uninstall.ps1`中`tools`如下所述的内容的文件夹。

**install.ps1 文件内容**

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Install the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Install language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}
```


**uninstall.ps1 文件内容**

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                try
                {
                    $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
                }
                catch
                {

                }
            }
        }
    }
}
```
