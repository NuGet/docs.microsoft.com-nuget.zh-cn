---
title: 设置 NuGet 包类型
description: 介绍包类型以指示包的预计用途。
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 8a3ba6af19125b75af17cab8c093e89485e20324
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843489"
---
# <a name="set-a-nuget-package-type"></a>设置 NuGet 包类型

通过 NuGet 3.5+ 可以使用特定的包类型标记包以指示其预期用途  。 未标记类型的包（包含使用更早版本的 NuGet 创建的所有包）默认为 `Dependency` 类型。

- `Dependency` 类型包将生成或运行时资产添加到库和应用程序，并且可以在任何项目类型中安装（假设它们相互兼容）。

- `DotnetCliTool` 类型包是 [dotnet CLI](/dotnet/articles/core/tools/index) 的扩展，并且从命令行中调用。 该包仅在 .NET Core 项目中安装并且不影响还原操作。 [.NET Core 扩展性](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility)文档中提供更多有关这些项目扩展的详细信息。

- 自定义类型包使用与包 ID 遵守相同格式规则的任意类型标识符。 但是，任何不是 `Dependency` 和 `DotnetCliTool` 的类型不会被 Visual Studio 中的 NuGet 包管理器识别。

包类型在 `.nuspec` 文件中设置。 后向兼容最好不显式设置 `Dependency` 类型，而是依赖 NuGet 在没有指定类型时假设此类型  。

- `.nuspec`：指明 `packageTypes\packageType` 节点中 `<metadata>` 元素下的包类型：

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
