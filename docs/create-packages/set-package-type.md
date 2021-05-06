---
title: 设置 NuGet 包类型
description: 介绍包类型以指示包的预计用途。
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: fa369e8327330e13f5adda39a75008e42ac99896
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067267"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="324f2-103">设置 NuGet 包类型</span><span class="sxs-lookup"><span data-stu-id="324f2-103">Set a NuGet package type</span></span>

<span data-ttu-id="324f2-104">包可以用多于一个包类型进行标记，以指示其预期用途。</span><span class="sxs-lookup"><span data-stu-id="324f2-104">Packages can be marked with one more more *package types* to indicate its intended use.</span></span>

## <a name="known-package-types"></a><span data-ttu-id="324f2-105">已知包类型</span><span class="sxs-lookup"><span data-stu-id="324f2-105">Known package types</span></span>

- <span data-ttu-id="324f2-106">`Dependency` 类型包将生成或运行时资产添加到库和应用程序，并且可以在任何项目类型中安装（假设它们相互兼容）。</span><span class="sxs-lookup"><span data-stu-id="324f2-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="324f2-107">`DotnetTool` 类型包是可以通过 [dotnet CLI](/dotnet/articles/core/tools/index) 安装的 .NET 工具。</span><span class="sxs-lookup"><span data-stu-id="324f2-107">`DotnetTool` type packages are .NET tools that can be installed by the [dotnet CLI](/dotnet/articles/core/tools/index).</span></span>

- <span data-ttu-id="324f2-108">`Template` 类型包提供[自定义模板](/dotnet/core/tools/custom-templates)，这些模板可以用来创建文件或项目，例如应用、服务、工具或类库。</span><span class="sxs-lookup"><span data-stu-id="324f2-108">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

<span data-ttu-id="324f2-109">未标记类型的包（包含使用更早版本的 NuGet 创建的所有包）默认为 `Dependency` 类型。</span><span class="sxs-lookup"><span data-stu-id="324f2-109">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

> [!NOTE]
> <span data-ttu-id="324f2-110">已在 NuGet 3.5 中添加对包类型的支持。</span><span class="sxs-lookup"><span data-stu-id="324f2-110">Support for package types was added in NuGet 3.5.</span></span>
> <span data-ttu-id="324f2-111">如果不需要自定义包类型，最好不要显式设置包类型。</span><span class="sxs-lookup"><span data-stu-id="324f2-111">If you don't need a custom package type, it's best to *not* explicitly set the package type.</span></span>
> <span data-ttu-id="324f2-112">如果未指定类型，则 NuGet 默认为 `Dependency` 类型。</span><span class="sxs-lookup"><span data-stu-id="324f2-112">NuGet defaults to the `Dependency` type when no type is specified.</span></span>

## <a name="custom-package-types"></a><span data-ttu-id="324f2-113">自定义包类型</span><span class="sxs-lookup"><span data-stu-id="324f2-113">Custom package types</span></span>

<span data-ttu-id="324f2-114">如果其用途不适合[已知包类型](#known-package-types)，则可以使用一个或多个自定义包类型来标记包。</span><span class="sxs-lookup"><span data-stu-id="324f2-114">You can mark your package with one or more custom package types if its use does not fit the [known package types](#known-package-types).</span></span>

<span data-ttu-id="324f2-115">例如，假设 `Contoso` 应用程序的客户可以安装扩展。</span><span class="sxs-lookup"><span data-stu-id="324f2-115">For example, imagine that customers of the `Contoso` app can install extensions.</span></span> <span data-ttu-id="324f2-116">应用程序可能需要扩展作者以使用自定义包类型 `ContosoExtension` 将其包标识为遵循所需约定的适当扩展。</span><span class="sxs-lookup"><span data-stu-id="324f2-116">The app could require extension authors to use the custom package type `ContosoExtension` to identify their packages as proper extensions that follow the required conventions.</span></span>

> [!WARNING]
> <span data-ttu-id="324f2-117">无法通过 Visual Studio 或 nuget.exe 安装具有自定义包类型的包。</span><span class="sxs-lookup"><span data-stu-id="324f2-117">A package with a custom package type cannot be installed by Visual Studio or nuget.exe.</span></span> <span data-ttu-id="324f2-118">有关详细信息，请参阅 [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468)。</span><span class="sxs-lookup"><span data-stu-id="324f2-118">See [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468) for more information.</span></span>

# <a name="using-dotnet-cli"></a>[<span data-ttu-id="324f2-119">使用 dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="324f2-119">Using dotnet CLI</span></span>](#tab/dotnet)

<span data-ttu-id="324f2-120">包类型可以在项目文件 (`.csproj`) 中设置：</span><span class="sxs-lookup"><span data-stu-id="324f2-120">Package types can be set in the project file (`.csproj`):</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="324f2-121">具有多个预期用途的包可以使用 `;` 分隔符标记多个包类型：</span><span class="sxs-lookup"><span data-stu-id="324f2-121">Packages with multiple intended uses can be marked with multiple package types using the `;` delimiter:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="324f2-122">可以使用包类型和 [`Version`](/dotnet/api/system.version) 字符串之间的 `,` 分隔符对包类型进行版本控制：</span><span class="sxs-lookup"><span data-stu-id="324f2-122">Package types can be versioned using a `,` delimiter between the package type and its [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[<span data-ttu-id="324f2-123">使用 nuget.exe</span><span class="sxs-lookup"><span data-stu-id="324f2-123">Using nuget.exe</span></span>](#tab/nugetexe)

<span data-ttu-id="324f2-124">包类型可以在 `.nuspec` 元素中的 `packageTypes\packageType` 节点下的 `<metadata>` 文件中设置：</span><span class="sxs-lookup"><span data-stu-id="324f2-124">Package types are set in the `.nuspec` file within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="ContosoExtension" />
        </packageTypes>
    </metadata>
</package>
```

<span data-ttu-id="324f2-125">具有多个预期用途的包可能使用多个包类型进行标记：</span><span class="sxs-lookup"><span data-stu-id="324f2-125">Packages with multiple intended uses may be marked with multiple package types:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

<span data-ttu-id="324f2-126">可以使用 [`Version`](/dotnet/api/system.version) 字符串对包类型进行版本控制：</span><span class="sxs-lookup"><span data-stu-id="324f2-126">Package types can be versioned using a [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" version="1.0.0.0" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

---

<span data-ttu-id="324f2-127">包类型字符串的格式与包 ID 完全相同。</span><span class="sxs-lookup"><span data-stu-id="324f2-127">The format of a package type string is exactly like a package ID.</span></span> <span data-ttu-id="324f2-128">这表示包类型是与正则表达式 `^\w+([_.-]\w+)*$`（具有最少 1 个字符，最多 100 个字符）相符的不区分大小写字符串。</span><span class="sxs-lookup"><span data-stu-id="324f2-128">That is, a package type is a case-insensitive string matching the regular expression `^\w+([_.-]\w+)*$` having at least one character and at most 100 characters.</span></span>

<span data-ttu-id="324f2-129">如果提供，则包类型版本是一个 [`Version`](/dotnet/api/system.version) 字符串。</span><span class="sxs-lookup"><span data-stu-id="324f2-129">If provided, the package type version is a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="324f2-130">包类型版本是可选的，默认为 `0.0`。</span><span class="sxs-lookup"><span data-stu-id="324f2-130">The package type version is optional and defaults to `0.0`.</span></span>
