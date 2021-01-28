---
title: 使用 COM 互操作程序集创建包
description: 介绍如何创建包含 COM 互操作程序集的包
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 0c663863673b50d0ba4969adf3a5d95151b2ca49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774497"
---
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a>创建包含 COM 互操作程序集的 NuGet 包

包含 COM 互操作程序集的包必须包含合适的[目标文件](creating-a-package.md#include-msbuild-props-and-targets-in-a-package)，使正确的 `EmbedInteropTypes` 元数据使用 PackageReference 格式添加到项目。 默认情况下，使用 PackageReference 时，`EmbedInteropTypes` 元数据对所有程序集一直为 false，所以目标文件显式添加此元数据。 为了避免冲突，目标名称必须是唯一的；理想情况下，使用包名称和嵌入程序集的组合，使用此值替换下例中的 `{InteropAssemblyName}`。 （有关示例，另请参阅 [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop)。）

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

请注意，在使用 `packages.config` 管理格式时，将引用从包添加到程序集会导致 NuGet 和 Visual Studio 检查 COM 互操作程序集并在项目文件中将 `EmbedInteropTypes` 设为 true。 在这种情况下，目标被替代。

此外，默认情况下，[生成资产不以可传递的方式流动](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。 当此处所述的创作的包作为可传递的依赖项从项目拉取到项目引用时，它们会以不同的方式工作。 包使用者通过将 PrivateAssets 默认值修改为不包含生成使其流动。

<a name="creating-the-package"></a>