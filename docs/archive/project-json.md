---
title: 适用于 NuGet 的 project.json 文件引用
description: 在某些项目类型中，project.json 维护项目中使用的 NuGet 包列表。
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: e4d8b5b9ab4605516827ead8939f278d110c7a48
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547779"
---
# <a name="projectjson-reference"></a>project.json 引用

NuGet 3.x+

`project.json` 文件维护项目中使用的包列表，称为包管理格式。 它会取代 `packages.config`，但在 NuGet 4.0+ 中又被 [PackageReference](../consume-packages/package-references-in-project-files.md) 取代。

[`project.lock.json`](#projectlockjson) 文件（如下所述）也用于采用 `project.json` 的项目。

`project.json` 具有以下基本结构，其中四个顶层对象均可拥有任意数量的子对象：

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a>依赖项

以下面的形式列出项目的 NuGet 包依赖项：

```json
"PackageID" : "version_constraint"
```

例如:

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

`dependencies` 部分是“NuGet 包管理器”对话框向项目中添加包依赖项的位置。

包 ID 对应于 nuget.org 上包的 ID，与包管理器控制台中使用的 ID 相同：`Install-Package Microsoft.NETCore`。

还原包时，`"5.0.0"` 版本约束意味着 `>= 5.0.0`。 也就是说，如果 5.0.0 在服务器上不可用，但 5.0.1 可用，则 NuGet 安装 5.0.1，并发出有关升级的警告。 否则，NuGet 尽可能在服务器上选取最低的版本，以与约束匹配。

请参阅[依赖项解析](../consume-packages/dependency-resolution.md)深入了解解析规则。

### <a name="managing-dependency-assets"></a>管理依赖项资产

依赖项的哪些资产流入顶级项目是通过在依赖项引用的 `include` 和 `exclude` 属性中指定一组以逗号分隔的标记来控制的。 下表中列出了这些标记：

| 包括/排除标记 | 受影响的目标文件夹 |
| --- | --- |
| contentFiles | 内容  |
| Runtime — 运行时 | 运行时、资源和 FrameworkAssemblies  |
| 编译 | lib |
| 生成 | 生成（MSBuild 属性和目标） |
| 本机 | 本机 |
| 无 | 无文件夹 |
| 全部 | 全部文件夹 |

用 `exclude` 指定的标记优先于用 `include` 指定的标记。 例如，`include="runtime, compile" exclude="compile"` 和 `include="runtime"` 相同。

例如，若要包括依赖项的 `build` 和 `native` 文件夹，请使用以下内容：

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

若要排除依赖项的 `content` 和 `build` 文件夹，请使用以下内容：

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a>框架

列出项目运行的框架，如 `net45`、`netcoreapp`、`netstandard`。

```json
"frameworks": {
    "netcore50": {}
    }
 ```

`frameworks` 部分仅允许一个条目。 （例外情况是用于 ASP.NET 项目的 `project.json` 文件，它们通过弃用的 DNX 工具链生成，可允许多个目标。）

## <a name="runtimes"></a>运行时

列出应用运行的操作系统和体系结构，如 `win10-arm`、`win8-x64`、`win8-x86`。

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

可在任何运行时上运行的包含 PCL 的包不需要指定运行时。 这还必须对任何依赖项适用，否则必须指定运行时。


## <a name="supports"></a>支持

为包依赖项定义一组检查。 可以定义期望 PCL 或应用运行的位置。 定义限制并不严格，因为代码可在其他位置运行。 但指定这些检查会让 NuGet 检查所有依赖项在所列 TxM 上是否满足。 此支持的值的示例有：`net46.app`、`uwp.10.0.app` 等。

在“可移植类库目标”对话框中选择条目时，此部分应自动填充。

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>导入

导入旨在允许使用 `dotnet` TxM 的包处理未声明 dotnet TxM 的包。 如果项目使用的是 `dotnet` TxM，那么依赖的所有包也必须有 `dotnet` TxM，除非将以下内容添加到 `project.json` 中，以允许非 `dotnet` 平台与 `dotnet` 兼容：

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

如果使用的是 `dotnet` TxM，那么 PCL 项目系统会基于支持的目标添加相应的 `imports` 语句。

## <a name="differences-from-portable-apps-and-web-projects"></a>可移植应用和 Web 项目的区别

NuGet 使用的 `project.json` 文件是 ASP.NET Core 项目中该文件的子集。 在 ASP.NET Core 中，`project.json` 用于项目元数据、编译信息和依赖项。 在其他项目系统中使用时，这三项内容则拆分为单独的文件，并且 `project.json` 包含的信息更少。 明显的区别包括：

- `frameworks` 部分仅可有一个框架。

- 该文件不能包含 DNX `project.json` 文件中可看到的依赖项、编译选项等。 鉴于只能有一个框架，输入框架特定的依赖项毫无意义。

- 编译由 MSBuild 处理，因此编译选项、预处理器定义等都属于 MSBuild 项目文件而不是 `project.json`。

在 NuGet 3+ 中，不需要开发人员手动编辑 `project.json`，因为 Visual Studio 中的包管理器 UI 会操作内容。 即便如此，当然还是可以编辑文件，但必须生成项目以启动包还原或以其他方式调用还原。 请参阅[包还原](../consume-packages/package-restore.md)。


## <a name="projectlockjson"></a>project.lock.json

在还原使用 `project.json` 的项目中的 NuGet 包的过程中，会生成 `project.lock.json` 文件。 它拥有 NuGet 在走包的关系图时生成的所有信息的快照，并包括项目中所有包的版本、内容和依赖项。 生成项目时，生成系统根据此快照从相关的全局位置选择包，而不是依靠项目本身中的本地包文件夹。 这使得生成性能更快，因为仅需读取 `project.lock.json` 而不是许多单独的 `.nuspec` 文件。

`project.lock.json` 在包还原时自动生成，因此可通过将其添加到 `.gitignore` 和 `.tfignore` 文件，将其从源代码管理去掉（请参阅[包和源代码管理](../consume-packages/packages-and-source-control.md)）。 但是，如果将其包括在源代码管理中，更改历史记录会显示随着时间推移解析的依赖项的更改。
