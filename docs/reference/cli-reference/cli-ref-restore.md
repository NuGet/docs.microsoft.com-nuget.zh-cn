---
title: NuGet CLI restore 命令
description: nuget.exe restore 命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 49fabbd0ef0c1c0c16f13bdf741296575fa72359
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780025"
---
# <a name="restore-command-nuget-cli"></a> (NuGet CLI 还原命令) 

**适用于：** 包使用 &bullet; **受支持的版本：** 2.7 +

下载并安装文件夹中缺少的任何程序包 `packages` 。 与 NuGet 4.0 + 和 PackageReference 格式一起使用时，会 `<project>.nuget.props` 在需要时在文件夹中生成文件 `obj` 。  (可以从源代码管理中省略该文件。 ) 

在 Mono 上带有 CLI 的 Mac OSX 和 Linux 上，PackageReference 不支持还原包。

## <a name="usage"></a>使用情况

```cli
nuget restore <projectPath> [options]
```

其中 `<projectPath>` 指定解决方案或文件的位置 `packages.config` 。 有关行为的详细信息，请参阅下面的 [备注](#remarks) 。

## <a name="options"></a>选项

- **`-ConfigFile`**

  要应用的 NuGet 配置文件。 如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-DirectDownload`**

  *(4.0 +)* 直接下载包，而不填充包含任何二进制文件或元数据的缓存。

- **`-DisableParallelProcessing`**

   禁用并行还原多个包。

- **`-FallbackSource`**

  *(3.2 +)* 在主或默认源中找不到包时要用作回退的包的列表。 使用分号分隔列表项。

- **`-Force`**

  在基于 PackageReference 的项目中，将强制解析所有依赖项，即使上次还原已成功。 指定此标志与删除 `project.assets.json` 文件类似。 这不会绕过 http 缓存。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 使用固定的、基于英语的区域性强制运行 nuget.exe。

- **`-ForceEvaluate`**

  即使锁定文件已存在，也会强制还原以重新评估所有依赖项。

- **`-?|-help`**

  显示命令的帮助信息。

- **`-LockFilePath`**

  写入项目锁定文件的输出位置。 默认情况下，该属性为 `PROJECT_ROOT\packages.lock.json`。

- **`-LockedMode`**

  不允许更新项目锁定文件。

- **`-MSBuildPath`**

   *(4.0 +)* 指定要与命令一起使用的 MSBuild 的路径，优先于 `-MSBuildVersion` 。

- **`-MSBuildVersion`**

  *(3.2 +)* 指定要与此命令一起使用的 MSBuild 版本。 支持的值为4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。 默认情况下，将选取路径中的 MSBuild，否则默认为已安装的最高版本的 MSBuild。

- **`-NoCache`**

  阻止 NuGet 使用缓存的包。 请参阅 [管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。

- **`-NonInteractive`**

  禁止提示用户输入或确认。

- **`-OutputDirectory`**

  指定在其中安装包的文件夹。 如果未指定文件夹，则使用当前文件夹。 使用文件进行还原时必需， `packages.config` 除非 `PackagesDirectory` `SolutionDirectory` 使用或。

- **`-PackageSaveMode`**

  指定包安装后要保存的文件类型： `nuspec` 、 `nupkg` 或 `nuspec;nupkg` 。

- **`-PackagesDirectory`**

  与 `OutputDirectory` 相同。 使用文件进行还原时必需， `packages.config` 除非 `OutputDirectory` `SolutionDirectory` 使用或。

- **`-Project2ProjectTimeOut`**

  解析项目到项目引用的超时时间（秒）。

- **`-Recursive`**

  *(4.0 +)* 还原 UWP 和 .NET Core 项目的所有引用项目。 不适用于使用 `packages.config` 的项目。

- **`-RequireConsent`**

  验证在下载和安装包之前是否启用了还原包。 有关详细信息，请参阅 [包还原](../../consume-packages/package-restore.md)。

- **`-SolutionDirectory`**

  指定解决方案文件夹。 还原解决方案的包时无效。 使用文件进行还原时必需， `packages.config` 除非 `PackagesDirectory` `OutputDirectory` 使用或。

- **`-Source`**

  将包源的列表指定为要用于还原的 Url)  (。 如果省略，则该命令将使用配置文件中提供的源，请参阅 [配置 NuGet 行为](../../consume-packages/configuring-nuget-behavior.md)。 使用分号分隔列表项。

- **`-UseLockFile`**

  允许生成项目锁定文件并与还原一起使用。

- **`-Verbosity [normal|quiet|detailed]`**

  指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。

另请参阅 [环境变量](cli-ref-environment-variables.md)

## <a name="remarks"></a>备注

Restore 命令执行以下步骤：

1. 确定 restore 命令的操作模式。

   | projectPath 文件类型 | 行为 |
   | --- | --- |
   | 解决方案 (文件夹)  | NuGet 查找 `.sln` 文件并使用该文件（如果找到的话）; 否则将会出现错误。 `(SolutionDir)\.nuget` 用作起始文件夹。 |
   | `.sln` 文件 | 还原解决方案标识的包;如果 `-SolutionDirectory` 使用了，则会出现错误。 `$(SolutionDir)\.nuget` 用作起始文件夹。 |
   | `packages.config` 或项目文件 | 还原文件中列出的包，解析和安装依赖项。 |
   | 其他文件类型 | 文件被假定为如上所述的 `.sln` 文件; 如果该文件不是解决方案，NuGet 将提供错误。 |
   | 未指定 (projectPath)  | <ul><li>NuGet 在当前文件夹中查找解决方案文件。 如果找到一个文件，则使用该文件还原包;如果找到多个解决方案，NuGet 将提供错误。</li><li>如果没有解决方案文件，NuGet 将查找 `packages.config` 并使用它来还原包。</li><li>如果未找到任何解决方案或 `packages.config` 文件，NuGet 将提供错误。</ul> |

2. 使用以下优先级顺序确定包文件夹 (NuGet 会在找不到任何这些文件夹时出现错误) ：

    - 用指定的文件夹 `-PackagesDirectory` 。
    - `repositoryPath`中的值`Nuget.Config`
    - 指定的文件夹 `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. 还原解决方案的包时，NuGet 会执行以下操作：
    - 加载解决方案文件。
    - 将中列出的解决方案级别包还原 `$(SolutionDir)\.nuget\packages.config` 到 `packages` 文件夹中。
    - 将中列出的包还原 `$(ProjectDir)\packages.config` 到 `packages` 文件夹中。 对于指定的每个包，请并行还原包，除非 `-DisableParallelProcessing` 指定了。

## <a name="examples"></a>示例

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
