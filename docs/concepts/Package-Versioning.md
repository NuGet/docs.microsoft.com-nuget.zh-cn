---
title: NuGet 包版本引用
description: 详细介绍如何为 NuGet 包所依赖的其他包指定版本号和范围以及如何安装依赖项的确切信息。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520347"
---
# <a name="package-versioning"></a>包版本控制

始终使用特定包的包标识符和确切的版本号来引用该包。 例如，nuget.org 上的[实体框架](https://www.nuget.org/packages/EntityFramework/)提供了数十个特定包，范围从版本 4.1.10311 到版本 6.1.3（最新稳定版）以及各种预发布版本（例如 6.2.0-beta1）    。

创建包时，可以分配带有可选预发布文本后缀的特定版本号。 另一方面，使用包时，可以指定确切的版本号或可接受的版本范围。

本主题内容：

- [版本基础知识](#version-basics)，包括预发布后缀。
- [版本范围和通配符](#version-ranges-and-wildcards)
- [规范化的版本号](#normalized-version-numbers)

## <a name="version-basics"></a>版本基础知识

特定版本号的格式为 Major.Minor.Patch[-Suffix]  ，其中的组件具有以下含义：

- *Major*：重大更改
- *Minor*：新增功能，但可向后兼容
- *Patch*：仅可向后兼容的 bug 修复
- *-Suffix*（可选）：连字符后跟字符串，表示预发布版本（遵循[语义化版本控制或 SemVer 1.0 约定](http://semver.org/spec/v1.0.0.html)）。

**示例：**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org 拒绝缺少确切版本号的任何包上传。 必须在用于创建包的 `.nuspec` 或项目文件中指定版本。

### <a name="pre-release-versions"></a>预发布版本

从技术上讲，包创建者可以将任何字符串用作后缀来表示预发布版本，因为 NuGet 会将任何此类版本视为预发布版本，而不进行任何其他解释。 也就是说，NuGet 在任何涉及的 UI 中显示完整版本字符串，并让使用者自行理解后缀的含义。

综上所述，包开发人员通常遵循识别的命名约定：

- `-alpha`：Alpha 版本，通常用于在制品和试验品。
- `-beta`：Beta 版本，通常指可用于下一计划版本的功能完整的版本，但可能包含已知 bug。
- `-rc`：候选发布，通常可能为最终（稳定）版本，除非出现重大 bug。

> [!Note]
> NuGet 4.3.0+ 支持 [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html)，后者支持采用点表示法的预发布号，如 1.0.1-build.23  中所示。 NuGet 4.3.0 之前的版本不支持点表示法。 可以使用类似于 1.0.1-build23 的形式  。

解析包引用时，如果多个包版本只有后缀不同，NuGet 会首先选择不带后缀的版本，然后按反向字母顺序来排列预发布版本的优先顺序。 例如，将按显示的确切顺序选择以下版本：

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>语义化版本控制 2.0.0

借助 NuGet 4.3.0+ 和 Visual Studio 2017 版本 15.3+，NuGet 支持[语义化版本控制 2.0.0](http://semver.org/spec/v2.0.0.html)。

旧客户端不支持 SemVer v2.0.0 的某些语义。 在以下任意一种情况下，NuGet 会将包版本视为特定于 SemVer v2.0.0：

- 预发布标签以点分隔，例如，1.0.0-alpha.1 
- 版本具有生成元数据，例如，1.0.0+githash 

对于 nuget.org，在以下任意一种情况下，会将包定义为 SemVer v2.0.0 包：

- 按照上述定义，包自己的版本与 SemVer v2.0.0 兼容，但与 SemVer v1.0.0 不兼容。
- 按照上述定义，包的任何依赖项版本范围都具有与 SemVer v2.0.0 兼容但与 SemVer v1.0.0 不兼容的最低版本或最高版本；例如，[1.0.0-alpha.1, )  。

如果将 SemVer v2.0.0 特定包上传到 nuget.org，则该包对较旧的客户端不可见，并且仅可用于以下 NuGet 客户端：

- NuGet 4.3.0+
- Visual Studio 2017 版本 15.3+
- 带有 [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix) 的 Visual Studio 2015
- dotnet
  - dotnetcore.exe (.NET SDK 2.0.0+)

第三方客户端：

- JetBrains Rider
- Paket 版本 5.0+

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>版本范围和通配符

引用包依赖项时，NuGet 支持使用间隔表示法来指定版本范围，汇总如下：

| Notation | 应用的规则 | 说明 |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | 最低版本（包含） |
| (1.0,) | x > 1.0 | 最低版本（独占） |
| [1.0] | x == 1.0 | 精确的版本匹配 |
| (,1.0] | x ≤ 1.0 | 最高版本（包含） |
| (,1.0) | x < 1.0 | 最高版本（独占） |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | 精确范围（包含） |
| (1.0,2.0) | 1.0 < x < 2.0 | 精确范围（独占） |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | 混合了最低版本（包含）和最高版本（独占） |
| (1.0)    | 无效 | 无效 |

使用 PackageReference 格式时，NuGet 还支持使用通配符表示法 \* 来表示版本号的主要、次要、修补程序和预发布后缀部分。 `packages.config` 格式不支持使用通配符。

> [!Note]
> PackageReference 中的版本范围包括预发布版本。 按照设计，可变版本不会解析预发布版本，除非选择加入。 有关相关功能请求的状态，请参阅[问题 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297)。

### <a name="examples"></a>示例

始终指定项目文件、`packages.config` 文件和 `.nuspec` 文件中的包依赖项的版本或版本范围。 如果没有版本或版本范围，NuGet 2.8. x 及更早版本会在解析依赖项时选择最新的可用包版本，而 NuGet 3.x 及更高版本会选择最低的包版本。 指定版本或版本范围可以避免这种不确定性。

#### <a name="references-in-project-files-packagereference"></a>项目文件中的引用 (PackageReference)

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**`packages.config` 中的引用：**

在 `packages.config` 中，通过还原包时使用的确切 `version` 属性列出每个依赖项。 `allowedVersions` 属性仅在更新操作过程中用于将版本约束到包可能更新到的版本。

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

**`.nuspec` 文件中的引用**

`<dependency>` 元素中的 `version` 属性描述了依赖项可接受的范围版本。

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a>规范化的版本号

> [!Note]
> 这是 NuGet 3.4 及更高版本的重大更改。

当在安装、重新安装或还原操作过程中从存储库获取包时，NuGet 3.4+ 会按如下所示处理版本号：

- 从版本号中删除前导零：

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- 将忽略版本号第四部分中的零

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

`pack` 和 `restore` 操作可尽可能规范化版本。 对于已生成的包，此规范化不会影响包本身的版本号；仅影响 NuGet 在解析依赖项时匹配版本的方式。

但是，NuGet 包存储库必须以与 NuGet 相同的方式处理这些值，以防止包版本重复。 因此，包含包版本 1.0 的存储库还不应将版本 1.0.0 作为单独的不同包进行托管   。
