---
title: NuGet 程序包版本引用 |Microsoft 文档
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/23/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 指定版本号和其他包 NuGet 包依赖，和如何安装依赖关系后的范围的准确详细信息。
keywords: 版本控制、 NuGet 包依赖项、 NuGet 依赖项版本、 NuGet 版本数字、 NuGet 程序包版本、 版本范围、 版本规范、 规范化的版本号
ms.reviewer:
- anandr
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 678ad79d9106a9f592ae4f47bc93cc117496e2c9
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="package-versioning"></a>包版本控制

特定包始终指使用其包标识符和确切的版本号。 例如，[实体框架](https://www.nuget.org/packages/EntityFramework/)nuget.org 上具有多个装入数十： 特定包可用，范围从版本*4.1.10311*到版本*6.1.3* （最新稳定释放） 等各种预发行版本，以及将*6.2.0-beta1*。

创建包时，则指定可选的预发行版文本后缀的特定版本号。 另一方面，在使用包，可以指定确切的版本号或一系列可接受的版本。

本主题内容：

- [版本基础知识](#version-basics)包括预发行后缀。
- [版本范围和通配符](#version-ranges-and-wildcards)
- [规范化的版本号](#normalized-version-numbers)

## <a name="version-basics"></a>版本基础知识

在窗体中的特定版本号是*Major.Minor.Patch [-后缀]*，其中的组件具有以下含义：

- *主要*： 重大更改
- *次要*： 新功能，但向后兼容
- *修补程序*： 向后兼容 bug 修复
- *-后缀*（可选）： 连字符后跟表示的预发行版本字符串 (以下[语义版本控制或 SemVer 1.0 约定](http://semver.org/spec/v1.0.0.html))。

**示例：**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org 拒绝任何缺少的确切的版本号的程序包上载。 必须在指定的版本`.nuspec`或用于创建包的项目文件。

### <a name="pre-release-versions"></a>预发布版本

从技术角度讲，包创建者可以使用任何字符串作为后缀来表示的预发行版本，NuGet 将视为预发行版的任何此类版本，会不使任何其他解释。 也就是说，涉及 NuGet 显示任何 UI 中的完整版本字符串，请保留的后缀含义任何解释为使用者。

话虽如此，但包开发人员通常遵循识别的命名约定：

- `-alpha`: Alpha 版本中，通常用于工作进度和实验。
- `-beta`：Beta 版本，通常指可用于下一计划版本的功能完整的版本，但可能包含已知 bug。
- `-rc`：候选发布，通常可能为最终（稳定）版本，除非出现重大 bug。

> [!Note]
> NuGet 4.3.0+ 支持[SemVer 2.0.0](http://semver.org/spec/v2.0.0.html)，它支持使用点表示法的预发行版号作为 in *1.0.1-build.23*。 NuGet 4.3.0 之前的版本不支持点表示法。 你可以使用窗体为*1.0.1-build23*。

当解决包引用和多个包版本的差异仅在于后缀，NuGet 首先，选择不带后缀的版本，然后应用优先预发行版本按反向字母顺序。 例如，将显示的确切顺序选择以下版本：

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>语义版本控制 2.0.0

使用 NuGet 4.3.0+ 和 Visual Studio 2017 15.3 以上版本，支持 NuGet[语义版本控制 2.0.0](http://semver.org/spec/v2.0.0.html)。

在较旧的客户端中不支持某些语义 SemVer 2.0.0 版。 NuGet 要考虑为特定的 SemVer 2.0.0 版，如果以下语句之一为 true 的包版本：

- 预发行版标签是点分隔的例如， *1.0.0-alpha.1*
- 例如，扩展的版本具有生成的元数据， *1.0.0+githash*

对于 nuget.org，包被定义为 SemVer 2.0.0 版包中，如果以下语句之一为 true:

- 包的版本是符合 SemVer 2.0.0 版，但不是 SemVer v1.0.0 符合，如上文所定义。
- 任何包的依赖项版本范围必须是符合 SemVer 2.0.0 版，但不是符合，SemVer v1.0.0; 上面定义的最小值或最大版本例如， *[1.0.0-alpha.1,)*。

如果将 SemVer 2.0.0 版特定包上载到 nuget.org 中时，包已向旧客户端不可见并且可用于仅以下 NuGet 客户端：

- NuGet 4.3.0+
- Visual Studio 2017 version 15.3+
- Visual Studio 2015 [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet.exe (.NET SDK 2.0.0+)

第三方客户端：

- JetBrains 附件
- Paket 版本 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>版本范围和通配符

当引用包的依赖项，NuGet 将支持使用间隔表示法指定版本范围，汇总为如下：

| Notation | 已应用的规则 | 描述 |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | 非独占的最低版本 |
| (1.0,) | x > 1.0 | 独占的最低版本 |
| [1.0] | x == 1.0 | 精确版本匹配 |
| (,1.0] | x ≤ 1.0 | 非独占的最高版本 |
| (,1.0) | x < 1.0 | 独占的最高版本 |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | 非独占的确切范围 |
| (1.0,2.0) | 1.0 < x < 2.0 | 确切的范围独占 |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | 混合的非独占最小值和独占最高版本 |
| (1.0)    | 无效 | 无效 |

使用 PackageReference 格式时，NuGet 还支持使用通配符表示法， \*、 主要、 次要、 修补程序，和的数的预发行后缀部分。 不支持通配符`packages.config`格式。

> [!Note]
> 在解析版本范围时，将不包括预发行版本。 预发布版本*是*时使用通配符，包括 (\*)。 版本范围*[1.0,2.0]*，例如，不包括 2.0 beta，但通配符表示法_2.0-*_未。 请参阅[发出 912](https://github.com/NuGet/Home/issues/912)有关预发行通配符的进一步讨论。

### <a name="examples"></a>示例

始终在项目文件中指定某个版本或包的依赖项的版本范围`packages.config`文件，和`.nuspec`文件。 不带版本或版本范围，NuGet 2.8.x 和前面选择的最新的可用程序包版本时解决一个依赖项，而 NuGet 3.x 和更高版本选择的最低的包版本。 指定的版本或范围可避免这种不确定性的版本。

#### <a name="references-in-project-files-packagereference"></a>在项目文件 (PackageReference) 中的引用

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

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**在引用`packages.config`:**

在`packages.config`，每个依赖项列出与确切`version`在还原包时使用的属性。 `allowedVersions`属性仅在更新操作期间使用来约束可能会向其更新的包的版本。

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

当包从存储库获取期间安装，请重新安装，或还原操作，NuGet 3.4 +，如下所示处理版本号：

- 前导零会从版本号：

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- 将省略的版本号的第四个部分中零

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

此正则化不会影响包本身; 中的版本号它会影响仅如何 NuGet 版本时匹配解析的依赖关系。

但是，NuGet 包存储库必须作为 NuGet 相同方式来防止包版本重复处理这些值。 因此的存储库包含版本*1.0*的包不还会托管版本*1.0.0*以分别进行不同的包的形式。
