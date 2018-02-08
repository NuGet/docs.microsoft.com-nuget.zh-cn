---
title: "NuGet project.json 存档内容 | Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/17/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "从 NuGet 文档的其他区域中删除了 project.json 内容的其他位。"
keywords: "NuGet project.json 文件"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 42a40c6c637839c13effc9e476ac5702a92cfd2a
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="projectjson-archive"></a>project.json 存档

NuGet 3.x 引入了 `project.json` 引用格式，并用于某些项目类型。 该格式已被弃用，引入 PackageReference 格式，其中项目文件中直接列出了依赖项。

另请参见：

- [project.json 架构](project-json.md)
- [project.json 对包作者的影响](project-json-impact.md)
- [project.json 和 UWP](project-json-and-uwp.md)

## <a name="projectjson-reference-format"></a>project.json 引用格式

*最初在[包还原](../what-is-nuget.md)中。*

在引用格式列表中：

- [`project.json`](project-json.md)：*（已弃用）*一种 JSON 文件，用于维护项目依赖项的列表，同时将包的整体信息图存储在关联文件 `project.lock.json` 中。 此格式已被弃用，被 PackageReference 取代。

## <a name="nuget-restore-on-mono"></a>Mono 上的 nuget 还原

*最初在[安装 NuGet 客户端工具](../install-nuget-client-tools.md)中。*

适用于 `project.json`。

## <a name="constraining-package-versions-with-restore"></a>使用还原约束包版本

*最初在[包还原](../consume-packages/package-restore.md#constraining-package-versions-with-restore)中。*

- `project.json` 使用依赖项的版本号直接指定版本范围。 例如:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a>NuGet CLI 命令

- `nuget install` 不适用于 `project.json`。
- `nuget restore`：对于使用 `project.json` 的项目，生成 `project.lock.json` 文件和 `<project>.nuget.props` 文件（如果需要）。 （这两个文件在源代码管理中都可以忽略。）`<projectPath>` 参数可以指向 `project.json` 文件，并具有与指向 `packages.config` 或项目文件相同的行为。 在包文件夹的优先顺序中，使用 `project.json` 时首先搜索 `%userprofile%\.nuget\packages`。
- `nuget update`：在 Mono 中，此命令不适用于使用 `project.json` 的项目。

## <a name="dependency-resolution-with-packagereference"></a>利用 PackageReference 解析依赖项

*最初在[依赖项解析](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)中。*

PackageReference 的行为也适用于 `project.json`。 NuGet 还原将依赖项关系图写入 `project.json` 旁边名为 `project.lock.json` 的文件。

## <a name="managing-dependency-assets"></a>管理依赖项资产

*最初在[依赖项解析](../consume-packages/dependency-resolution.md#managing-dependency-assets)中。*

使用 `project.json` 格式时，可以控制依赖项中的哪些资产可流入顶层项目。 有关详细信息，请参阅 [project.json](project-json.md)。

## <a name="excluding-references"></a>排除引用

*最初在[依赖项解析](../consume-packages/dependency-resolution.md#excluding-references)。*

- `project.json`：在 PackageC 的依赖项中添加 `"exclude" : "all"`：

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a>解决包不兼容错误

*最初在[依赖项解析](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors)。*

增加的错误解决方式：

- **不推荐做法**：作为与包创建者合作的临时解决方案，面向 `netcore`、`netstandard` 和 `netcoreapp` 的项目可以表示其他兼容框架，并因此允许使用面向其他框架的包。 请参阅 [project.json imports](project-json.md#imports) 和 [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback)。 这将导致意外行为，因此再次提醒，与包创建者协作是解决更新时遇到的包不兼容问题的最佳做法。

## <a name="target-frameworks"></a>目标框架

*最初在[目标框架](../reference/target-frameworks.md)中。*

- [project.json](project-json.md)：`frameworks` 节点指定可编译项目的框架版本。

## <a name="creating-a-package"></a>创建包

*最初在[创建包](../create-packages/creating-a-package.md)中*

### <a name="setting-a-package-type"></a>设置包类型

有了 .NET Core 1.x，安装 DotnetCliTool 包时，Visual Studio 将包置于 `project.json` `tools` 节点而不是 `dependencies` 节点中。

包类型在 `project.json` 文件中设置。

- `project.json`：指示 `packOptions.packageType` 属性 json 中的包类型：

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a>添加 MSBuild 的目标和属性

*最初在[使用 Visual Studio 2015 创建 .NET Standard NuGet 包](../guides/create-net-standard-packages-vs2015.md)中。*

使用 `project.json` 时，目标不添加到项目，而是通过 `project.lock.json` 提供。

### <a name="package-versioning"></a>包版本控制

*最初在[包版本控制](../reference/package-versioning.md)中。*

使用 `project.json` 格式时，NuGet 还支持使用通配符表示法 \* 来表示版本号的主要、次要、修补程序和预发布后缀部分。

### <a name="nugetconfig-reference"></a>NuGet.Config 引用

*最初在 [NuGet.Config 引用](../reference/nuget-config-file.md)中。*

`globalPackagesFolder` 仅适用于 `project.json`

### <a name="nuspec-file-reference"></a>nuspec 文件引用

*最初在 [nuspec 引用](../reference/nuspec.md)中。*

`project.json` 使用 `<contentFiles>` 元素替代 `<files>`。

### <a name="package-manager-options-control"></a>程序包管理器选项控件

*最初在[程序包管理器 UI 引用](../tools/package-manager-ui.md)中。*

使用 `project.json` 引用格式的项目仅显示“显示预览窗口”选项。

### <a name="visual-studio-templates"></a>Visual Studio 模板

*最初在 [Visual Studio 模板中的 NuGet 包](../visual-studio-extensibility/visual-studio-templates.md)中。*

最佳做法：模板不包括 `project.json` 文件，也不包括安装 NuGet 包时将添加的任何引用或内容。