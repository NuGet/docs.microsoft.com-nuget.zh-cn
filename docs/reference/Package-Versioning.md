---
title: NuGet 包版本参考
description: 在指定的版本号和其他包所依赖的 NuGet 包，和如何安装依赖项的范围的准确详细信息。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: b980c1084fe8e31573053a4dcf38bbfa6146e6de
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549768"
---
# <a name="package-versioning"></a>包版本控制

使用其包标识符和确切的版本号是始终引用特定的包。 例如，[实体框架](https://www.nuget.org/packages/EntityFramework/)nuget.org 上具有多个几十个： 特定包可用，从版本范围*4.1.10311*到版本*6.1.3* （最新稳定版发布） 和不同的预发行版本喜欢*6.2.0-beta1*。

创建包时，则指定带有可选的预发布的文本后缀的特定版本号。 但是，当使用包，可以指定确切的版本号或一系列可接受的版本。

本主题内容：

- [版本基础知识](#version-basics)包括预发行后缀。
- [版本范围和通配符](#version-ranges-and-wildcards)
- [规范化的版本号](#normalized-version-numbers)

## <a name="version-basics"></a>版本基础知识

在窗体中的特定版本号是*Major.Minor.Patch [-后缀]*，其中的组件具有以下含义：

- *主要*： 重大更改
- *次要*： 新功能，但可向后兼容
- *修补程序*： 向后兼容 bug 修复
- *-后缀*（可选）： 连字符后跟一个表示的预发行版本的字符串 (下面[语义化版本控制或 SemVer 1.0 约定](http://semver.org/spec/v1.0.0.html))。

**示例：**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org 会拒绝任何缺少的确切版本号的包上传。 必须在指定版本`.nuspec`或用于创建包的项目文件。

### <a name="pre-release-versions"></a>预发布版本

从技术上讲，包创建者可以使用任何字符串作为后缀来表示的预发行版本，NuGet 将任何此类版本视为预发行版并使其他的解释。 也就是说，涉及 NuGet 显示的完整版本字符串中的任何 UI，向使用者离开后缀的含义的任何解释。

话虽如此，但包开发人员通常遵循公认命名约定：

- `-alpha`: Alpha 版本，通常用于开发过程和试验。
- `-beta`：Beta 版本，通常指可用于下一计划版本的功能完整的版本，但可能包含已知 bug。
- `-rc`：候选发布，通常可能为最终（稳定）版本，除非出现重大 bug。

> [!Note]
> NuGet 4.3.0 支持[SemVer 2.0.0](http://semver.org/spec/v2.0.0.html)，如支持采用点表示法的预发布号*1.0.1-build.23*。 NuGet 4.3.0 之前的版本不支持点表示法。 可以使用之类的格式*1.0.1-build23*。

解决包引用和多个包版本的差异仅在于后缀，NuGet 首先，选择不带后缀的版本，然后应用预发布版本按反向字母顺序的优先级。 例如，将按照所示的确切顺序选择以下版本：

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>语义化版本控制 2.0.0

NuGet 4.3.0 和 Visual Studio 2017 版本 15.3 +，NuGet 支持[语义化版本控制 2.0.0](http://semver.org/spec/v2.0.0.html)。

在较旧的客户端中不支持的 SemVer 2.0.0 版的特定语义。 NuGet 会考虑以下语句为真要 SemVer 2.0.0 版特定包版本：

- 预发行版标签是以点号分隔，例如， *1.0.0-alpha.1*
- 版本具有生成的元数据，例如， *1.0.0+githash*

对于 nuget.org，包被定义为 SemVer 2.0.0 版包中，如果以下语句之一为 true:

- 包的版本是 SemVer 2.0.0 版兼容，但不是符合 SemVer v1.0.0 如上文所定义。
- 任何包的依赖项版本范围具有是 SemVer 2.0.0 版兼容，但不是符合 SemVer v1.0.0; 上面定义的最小值或最大版本例如， *[1.0.0-alpha.1,)*。

将 SemVer 2.0.0 版特定包上传到 nuget.org，该程序包对较旧的客户端不可见，并可用于仅以下 NuGet 客户端：

- NuGet 4.3.0
- Visual Studio 2017 版本 15.3 +
- 使用 visual Studio 2015 [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (.NET SDK 2.0.0+)

第三方客户端：

- JetBrains 的 Rider
- Paket 依存版本 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>版本范围和通配符

如果引用到包的依赖项，NuGet 支持使用间隔表示法用于指定版本范围，总结如下：

| Notation | 已应用的规则 | 描述 |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | 非独占的最低版本 |
| (1.0,) | x > 1.0 | 独占的最低版本 |
| [1.0] | x == 1.0 | 精确的版本匹配 |
| (,1.0] | x ≤ 1.0 | 非独占的最高版本 |
| (,1.0) | x < 1.0 | 排他的最高版本 |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | 确切的范围包括 |
| (1.0,2.0) | 1.0 < x < 2.0 | 确切的范围，排他 |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | 混合的非独占最小值和独占最高版本 |
| (1.0)    | 无效 | 无效 |

使用 PackageReference 格式时，NuGet 还支持使用通配符表示法， \*、 主要、 次要、 修补程序，和数字的预发布后缀部分。 不支持通配符`packages.config`格式。

> [!Note]
> 解析版本范围时，将不包括预发布版本。 预发布版本*都*时使用通配符，包括 (\*)。 版本范围 *[1.0,2.0]*，例如，不包括 2.0 beta 版，但通配符表示法_2.0-*_ does。 请参阅[发出 912](https://github.com/NuGet/Home/issues/912)有关预发行版通配符的进一步讨论。

### <a name="examples"></a>示例

始终在项目文件中指定的版本或版本范围为包依赖项`packages.config`文件，和`.nuspec`文件。 不带版本或版本范围，NuGet 2.8.x 和前面选择的最新可用的包版本时解析依赖项，而 NuGet 3.x 和更高版本选择最低的包版本。 指定的版本或版本范围可以避免这种不确定性。

#### <a name="references-in-project-files-packagereference"></a>项目文件 (PackageReference) 中的引用

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

**在引用`packages.config`:**

在中`packages.config`，每个依赖项列出与精确`version`还原包时使用的属性。 `allowedVersions`属性仅在更新操作期间使用来约束可能会向其更新的包的版本。

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

**在引用`.nuspec`文件**

`version`属性中`<dependency>`元素描述的某个依赖项可接受的范围版本。

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

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
> 这是一项重大更改 NuGet 3.4 及更高版本。

当在安装期间，从存储库获取程序包重新安装，或还原操作，NuGet 3.4 + 将按如下所示处理版本号：

- 前导零，已从版本号：

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- 将省略版本号的第四个部分的值为零

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

这种规范化不会影响包本身; 中的版本号它会影响仅如何 NuGet 匹配版本解析依赖项时。

但是，NuGet 包存储库必须作为 NuGet 的相同方式，以防止包版本重复处理这些值。 因此包含版本的存储库*1.0*的包不应还托管版本*1.0.0*以独立且不同包的形式。
