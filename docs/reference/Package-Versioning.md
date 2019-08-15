---
title: NuGet 包版本引用
description: 有关为 NuGet 包所依赖的其他包指定版本号和范围的详细信息, 以及如何安装依赖项。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69019995"
---
# <a name="package-versioning"></a>包版本控制

特定包始终称为使用其包标识符和准确版本号。 例如, nuget.org 上的[实体框架](https://www.nuget.org/packages/EntityFramework/)有多个特定的包可用, 范围从版本*4.1.10311*到版本*ef6.1.3* (最新稳定版本) 以及各种预发布版本, 如*6.2.0-beta1*.

创建包时, 可使用可选的预发布文本后缀分配特定版本号。 另一方面, 使用包时, 可以指定确切的版本号或可接受的版本范围。

本主题内容：

- [版本基础知识](#version-basics), 包括预发布后缀。
- [版本范围和通配符](#version-ranges-and-wildcards)
- [规范化的版本号](#normalized-version-numbers)

## <a name="version-basics"></a>版本基础知识

特定版本号的格式为*主要. 次要修补程序 [-后缀]* , 其中的组件具有以下含义:

- *主要*:重大更改
- *次要*:新增功能，但可向后兼容
- *修补程序*:仅可向后兼容的 bug 修复
- *-后缀*(可选): 连字符后跟一个表示预发行版本的字符串 (遵循[语义版本控制或 SemVer 1.0 约定](http://semver.org/spec/v1.0.0.html))。

**示例**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org 拒绝缺少完全版本号的任何包上传。 必须在用于创建包的`.nuspec`或项目文件中指定版本。

### <a name="pre-release-versions"></a>预发行版本

从技术上讲, 包创建者可以使用任何字符串作为后缀来表示预发布版本, 因为 NuGet 会将任何此类版本视为预发布版本, 不进行任何其他解释。 也就是说, NuGet 将在涉及的任何 UI 中显示完整的版本字符串, 并将后缀含义的任何解释留给使用者。

也就是说, 包开发人员通常遵循识别的命名约定:

- `-alpha`：Alpha 版本, 通常用于进行工作和试验。
- `-beta`：Beta 版本，通常指可用于下一计划版本的功能完整的版本，但可能包含已知 bug。
- `-rc`：候选发布，通常可能为最终（稳定）版本，除非出现重大 bug。

> [!Note]
> NuGet 4.3.0 + 支持[SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), 它支持带点表示法的预发行版数字, 如*1.0.1-版本 23*中所示。 NuGet 4.3.0 之前的版本不支持点表示法。 您可以使用类似于*build23*的形式。

解析包引用时, 如果多个包版本只有后缀不同, NuGet 将选择不带后缀的版本, 然后将优先顺序按反向字母顺序应用到预发布版本。 例如, 以下版本将按显示的准确顺序选择:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>语义版本控制2.0。0

Nuget 4.3.0 + 和 Visual Studio 2017 版本 15.3 + 支持[语义版本控制 2.0.0](http://semver.org/spec/v2.0.0.html)。

旧客户端不支持 SemVer v 2.0.0 的某些语义。 如果以下任一陈述成立, NuGet 会将包版本视为特定于 SemVer v 2.0.0:

- 预发行版标签以点分隔, 例如, *1.0.0-alpha。 1*
- 版本具有生成元数据, 例如*1.0.0 + githash*

对于 nuget.org, 如果下列任一语句为 true, 则将包定义为 SemVer v 2.0.0 包:

- 根据上面定义的, 包的版本 SemVer v 2.0.0 兼容, 但不符合 SemVer 1.0.0。
- 包的所有依赖项版本范围具有的最小或最大版本是 SemVer v 2.0.0 兼容的, 但不符合前面定义的 SemVer 1.0.0;例如, *[1.0.0-alpha. 1,)* 。

如果将 SemVer v 2.0.0 特定包上传到 nuget.org, 则包对于旧版客户端不可见, 且仅可用于以下 NuGet 客户端:

- NuGet 4.3.0 +
- Visual Studio 2017 版本 15.3 +
- Visual Studio 2015 with [NUGET VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore (.NET SDK 2.0.0 +)

第三方客户端:

- JetBrains 附件
- Paket 5.0 版 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>版本范围和通配符

引用包依赖项时, NuGet 支持使用间隔表示法来指定版本范围, 总结如下:

| Notation | 应用的规则 | 描述 |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | 最低版本 (含) |
| (1.0,) | x > 1.0 | 最低版本, 独占 |
| [1.0] | x == 1.0 | 精确的版本匹配 |
| (,1.0] | x ≤ 1.0 | 最高版本 (含) |
| (,1.0) | x < 1.0 | 最高版本, 独占 |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | 精确范围 (包含) |
| (1.0,2.0) | 1.0 < x < 2.0 | 精确范围, 排他 |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | 混合包含的最小和独占最高版本 |
| (1.0)    | 无效 | 无效 |

使用 PackageReference 格式时, NuGet 还支持使用通配符表示法, \*用于表示数字的主要、次要、修补和预发行后缀部分。 `packages.config`格式不支持通配符。

> [!Note]
> PackageReference 中的版本范围包括预发行版本。 按照设计, 浮动版本不会解析预发布版本, 除非选择加入。 有关相关功能请求的状态, 请参阅[问题 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297)。

### <a name="examples"></a>示例

始终指定项目文件、 `packages.config`文件和`.nuspec`文件中的包依赖项的版本或版本范围。 如果没有版本或版本范围, NuGet 2.8. x 和更早版本会在解析依赖项时选择最新的可用包版本, 而 NuGet 2.x 和更高版本将选择最低的包版本。 指定版本或版本范围可以避免这种不确定性。

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

**`packages.config`引用内容:**

在`packages.config`中, 每个依赖项都列出`version`了还原包时使用的确切属性。 `allowedVersions`特性仅在更新操作过程中使用, 以限制包可能更新到的版本。

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

**文件中`.nuspec`的引用**

元素中的`version`属性描述了依赖项可接受的范围版本。 `<dependency>`

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
> 这是 NuGet 3.4 和更高版本的重大更改。

当在安装、重新安装或还原操作过程中从存储库获取包时, NuGet 3.4 + 会按如下所示处理版本号:

- 从版本号中删除前导零:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- 将忽略版本号的第四部分中的零

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

`pack`和`restore`操作尽可能规范化版本。 对于已生成的包, 此规范化不会影响包本身中的版本号;它仅影响 NuGet 在解析依赖项时如何匹配版本。

但是, NuGet 包存储库必须以与 NuGet 相同的方式处理这些值, 以防止包版本重复。 因此, 包含包*1.0*版的存储库还不应将版本*1.0.0*作为单独的不同包进行托管。
