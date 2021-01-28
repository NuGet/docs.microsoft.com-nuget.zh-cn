---
title: 设置 NuGet 包类型
description: 介绍包类型以指示包的预计用途。
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 990ac580f4031615566d78e359a24eaedaaf3e07
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774367"
---
# <a name="set-a-nuget-package-type"></a>设置 NuGet 包类型

通过 NuGet 3.5+ 可以使用特定的包类型标记包以指示其预期用途  。 未标记类型的包（包含使用更早版本的 NuGet 创建的所有包）默认为 `Dependency` 类型。

- `Dependency` 类型包将生成或运行时资产添加到库和应用程序，并且可以在任何项目类型中安装（假设它们相互兼容）。

- `DotnetTool` 类型包是 [dotnet CLI](/dotnet/articles/core/tools/index) 的扩展，并且从命令行中调用。 该包仅在 .NET Core 项目中安装并且不影响还原操作。 [.NET Core 扩展性](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility)文档中提供更多有关这些项目扩展的详细信息。

- `Template` 类型包提供[自定义模板](/dotnet/core/tools/custom-templates)，这些模板可以用来创建文件或项目，例如应用、服务、工具或类库。

- 自定义类型包使用与包 ID 遵守相同格式规则的任意类型标识符。 但是，任何不是 `Dependency` 和 `DotnetTool` 的类型不会被 Visual Studio 中的 NuGet 包管理器识别。

包类型在 `.nuspec` 文件中设置。 后向兼容最好不显式设置 `Dependency` 类型，而是依赖 NuGet 在没有指定类型时假设此类型。

- `.nuspec`：指示 `<metadata>` 元素的 `packageTypes\packageType` 节点中的包类型：

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
