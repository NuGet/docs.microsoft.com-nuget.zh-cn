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
# <a name="set-a-nuget-package-type"></a>设置 NuGet 包类型

包可以用多于一个包类型进行标记，以指示其预期用途。

## <a name="known-package-types"></a>已知包类型

- `Dependency` 类型包将生成或运行时资产添加到库和应用程序，并且可以在任何项目类型中安装（假设它们相互兼容）。

- `DotnetTool` 类型包是可以通过 [dotnet CLI](/dotnet/articles/core/tools/index) 安装的 .NET 工具。

- `Template` 类型包提供[自定义模板](/dotnet/core/tools/custom-templates)，这些模板可以用来创建文件或项目，例如应用、服务、工具或类库。

未标记类型的包（包含使用更早版本的 NuGet 创建的所有包）默认为 `Dependency` 类型。

> [!NOTE]
> 已在 NuGet 3.5 中添加对包类型的支持。
> 如果不需要自定义包类型，最好不要显式设置包类型。
> 如果未指定类型，则 NuGet 默认为 `Dependency` 类型。

## <a name="custom-package-types"></a>自定义包类型

如果其用途不适合[已知包类型](#known-package-types)，则可以使用一个或多个自定义包类型来标记包。

例如，假设 `Contoso` 应用程序的客户可以安装扩展。 应用程序可能需要扩展作者以使用自定义包类型 `ContosoExtension` 将其包标识为遵循所需约定的适当扩展。

> [!WARNING]
> 无法通过 Visual Studio 或 nuget.exe 安装具有自定义包类型的包。 有关详细信息，请参阅 [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468)。

# <a name="using-dotnet-cli"></a>[使用 dotnet CLI](#tab/dotnet)

包类型可以在项目文件 (`.csproj`) 中设置：

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

具有多个预期用途的包可以使用 `;` 分隔符标记多个包类型：

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

可以使用包类型和 [`Version`](/dotnet/api/system.version) 字符串之间的 `,` 分隔符对包类型进行版本控制：

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[使用 nuget.exe](#tab/nugetexe)

包类型可以在 `.nuspec` 元素中的 `packageTypes\packageType` 节点下的 `<metadata>` 文件中设置：

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

具有多个预期用途的包可能使用多个包类型进行标记：

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

可以使用 [`Version`](/dotnet/api/system.version) 字符串对包类型进行版本控制：

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

包类型字符串的格式与包 ID 完全相同。 这表示包类型是与正则表达式 `^\w+([_.-]\w+)*$`（具有最少 1 个字符，最多 100 个字符）相符的不区分大小写字符串。

如果提供，则包类型版本是一个 [`Version`](/dotnet/api/system.version) 字符串。 包类型版本是可选的，默认为 `0.0`。
