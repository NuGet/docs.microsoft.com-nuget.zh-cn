---
title: 标识项目格式
description: 介绍如何标识项目格式
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488484"
---
# <a name="identify-the-project-format"></a>标识项目格式

NuGet 适用于所有 .NET 项目。 但是，项目格式（SDK 样式或非 SDK 样式）决定了使用和创建 NuGet 包所需的一些工具和方法。 SDK 样式的项目使用 [SDK 属性](/dotnet/core/tools/csproj#additions)。 确定项目类型非常重要，因为用于使用和创建 NuGet 包的方法和工具都依赖于项目格式。 对于非 SDK 样式的项目，方法和工具还取决于项目是否迁移到 `PackageReference` 格式。

项目是否为 SDK 样式取决于用于创建项目的方法。 下表显示了使用 Visual Studio 2017 及更高版本创建项目时的默认项目格式和相关的 CLI 工具。

| 项目&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 默认项目格式 | CLI 工具&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 说明 |
|:------------- |:-------------|:-----|:-----|
| .NET Standard | SDK 样式 | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | 在 Visual Studio 2017 之前创建的项目为非 SDK 样式。 使用 `nuget.exe` CLI。 |
| .NET Core | SDK 样式 | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | 在 Visual Studio 2017 之前创建的项目为非 SDK 样式。 使用 `nuget.exe` CLI。 |
| .NET Framework | 非 SDK 样式 | [nuget.exe CLI](../install-nuget-client-tools.md#nugetexe-cli) | 使用其他方法创建的 .NET Framework 项目可能是 SDK 样式项目。 对于这种情况，请改为使用 [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli)。 |
| [迁移的](../consume-packages/migrate-packages-config-to-package-reference.md) .NET 项目 | 非 SDK 样式| 要创建包，请使用 [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) 创建包。 | 要创建包，建议使用 `msbuild -t:pack`。 否则，使用 [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli)。 迁移的项目是非 SDK 样式的项目。 |

## <a name="check-the-project-format"></a>检查项目格式

如果不确定该项目是否是 SDK 样式的格式，请在项目文件中的 `<Project>` 元素中查找 SDK 属性（对于 C#，这是 *.csproj 文件）。 如果存在，则该项目是一个 SDK 样式的项目。

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a>在 Visual Studio 中检查项目格式

如果在 Visual Studio 中进行操作，可以使用以下方法之一快速检查项目格式：

- 在解决方案资源管理器中右键单击该项目，然后选择“编辑 myprojectname.csproj”  。

   此选项从 Visual Studio 2017 开始仅对使用 SDK 样式属性的项目可用。 否则，请使用其他方法。

   ![编辑项目文件](media/edit-project-file.png)

   一个 SDK 样式的项目会在项目文件中显示 [SDK 属性](/dotnet/core/tools/csproj#additions)。
   
- 在“项目”  菜单中选择“卸载项目”  （或右键单击项目并选择“卸载项目”  ）。

   该项目将不在项目文件中包含 SDK 属性。 它不是 SDK 样式的项目。

   ![卸载项目](media/unload-project.png)

   然后，右键单击卸载的项目并选择“编辑 myprojectname.csproj”  。

## <a name="see-also"></a>另请参阅

- [使用 dotnet CLI 创建 .NET Standard 包](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [使用 Visual Studio 创建 .NET Standard 包](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [创建并发布 .NET Framework 包 (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [作为 MSBuild 目标的 NuGet 包和还原](../reference/msbuild-targets.md)
