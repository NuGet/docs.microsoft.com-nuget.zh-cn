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
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="ffb6c-103">设置 NuGet 包类型</span><span class="sxs-lookup"><span data-stu-id="ffb6c-103">Set a NuGet package type</span></span>

<span data-ttu-id="ffb6c-104">通过 NuGet 3.5+ 可以使用特定的包类型标记包以指示其预期用途  。</span><span class="sxs-lookup"><span data-stu-id="ffb6c-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="ffb6c-105">未标记类型的包（包含使用更早版本的 NuGet 创建的所有包）默认为 `Dependency` 类型。</span><span class="sxs-lookup"><span data-stu-id="ffb6c-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="ffb6c-106">`Dependency` 类型包将生成或运行时资产添加到库和应用程序，并且可以在任何项目类型中安装（假设它们相互兼容）。</span><span class="sxs-lookup"><span data-stu-id="ffb6c-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="ffb6c-107">`DotnetCliTool` 类型包是 [dotnet CLI](/dotnet/articles/core/tools/index) 的扩展，并且从命令行中调用。</span><span class="sxs-lookup"><span data-stu-id="ffb6c-107">`DotnetCliTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="ffb6c-108">该包仅在 .NET Core 项目中安装并且不影响还原操作。</span><span class="sxs-lookup"><span data-stu-id="ffb6c-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="ffb6c-109">[.NET Core 扩展性](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility)文档中提供更多有关这些项目扩展的详细信息。</span><span class="sxs-lookup"><span data-stu-id="ffb6c-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="ffb6c-110">自定义类型包使用与包 ID 遵守相同格式规则的任意类型标识符。</span><span class="sxs-lookup"><span data-stu-id="ffb6c-110">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="ffb6c-111">但是，任何不是 `Dependency` 和 `DotnetCliTool` 的类型不会被 Visual Studio 中的 NuGet 包管理器识别。</span><span class="sxs-lookup"><span data-stu-id="ffb6c-111">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="ffb6c-112">包类型在 `.nuspec` 文件中设置。</span><span class="sxs-lookup"><span data-stu-id="ffb6c-112">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="ffb6c-113">后向兼容最好不显式设置 `Dependency` 类型，而是依赖 NuGet 在没有指定类型时假设此类型  。</span><span class="sxs-lookup"><span data-stu-id="ffb6c-113">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="ffb6c-114">`.nuspec`：指明 `packageTypes\packageType` 节点中 `<metadata>` 元素下的包类型：</span><span class="sxs-lookup"><span data-stu-id="ffb6c-114">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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
