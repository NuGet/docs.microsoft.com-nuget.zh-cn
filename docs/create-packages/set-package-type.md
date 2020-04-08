---
title: 设置 NuGet 包类型
description: 介绍包类型以指示包的预计用途。
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 1d869f616ce0291cf1c0a17b7ff20fc61e6a3bd5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230819"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="a8fab-103">设置 NuGet 包类型</span><span class="sxs-lookup"><span data-stu-id="a8fab-103">Set a NuGet package type</span></span>

<span data-ttu-id="a8fab-104">通过 NuGet 3.5+ 可以使用特定的包类型标记包以指示其预期用途  。</span><span class="sxs-lookup"><span data-stu-id="a8fab-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="a8fab-105">未标记类型的包（包含使用更早版本的 NuGet 创建的所有包）默认为 `Dependency` 类型。</span><span class="sxs-lookup"><span data-stu-id="a8fab-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="a8fab-106">`Dependency` 类型包将生成或运行时资产添加到库和应用程序，并且可以在任何项目类型中安装（假设它们相互兼容）。</span><span class="sxs-lookup"><span data-stu-id="a8fab-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="a8fab-107">`DotnetTool` 类型包是 [dotnet CLI](/dotnet/articles/core/tools/index) 的扩展，并且从命令行中调用。</span><span class="sxs-lookup"><span data-stu-id="a8fab-107">`DotnetTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="a8fab-108">该包仅在 .NET Core 项目中安装并且不影响还原操作。</span><span class="sxs-lookup"><span data-stu-id="a8fab-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="a8fab-109">[.NET Core 扩展性](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility)文档中提供更多有关这些项目扩展的详细信息。</span><span class="sxs-lookup"><span data-stu-id="a8fab-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="a8fab-110">`Template` 类型包提供[自定义模板](/dotnet/core/tools/custom-templates)，这些模板可以用来创建文件或项目，例如应用、服务、工具或类库。</span><span class="sxs-lookup"><span data-stu-id="a8fab-110">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

- <span data-ttu-id="a8fab-111">自定义类型包使用与包 ID 遵守相同格式规则的任意类型标识符。</span><span class="sxs-lookup"><span data-stu-id="a8fab-111">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="a8fab-112">但是，任何不是 `Dependency` 和 `DotnetTool` 的类型不会被 Visual Studio 中的 NuGet 包管理器识别。</span><span class="sxs-lookup"><span data-stu-id="a8fab-112">Any type other than `Dependency` and `DotnetTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="a8fab-113">包类型在 `.nuspec` 文件中设置。</span><span class="sxs-lookup"><span data-stu-id="a8fab-113">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="a8fab-114">后向兼容最好不显式设置  *类型，而是依赖 NuGet 在没有指定类型时假设此类型*`Dependency`。</span><span class="sxs-lookup"><span data-stu-id="a8fab-114">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="a8fab-115">`.nuspec`：指示 `packageTypes\packageType` 元素的 `<metadata>` 节点中的包类型：</span><span class="sxs-lookup"><span data-stu-id="a8fab-115">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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
