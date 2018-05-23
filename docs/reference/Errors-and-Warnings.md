---
title: NuGet 错误和警告参考
description: 针对警告和错误各种 NuGet 操作过程中从 NuGet 发出的完整参考。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: 748c2746a61886617e2eefe3e6c4a2e2a5b9d4d3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2018
---
# <a name="errors-and-warnings"></a>错误和警告

在 NuGet 4.3.0+ 错误和警告本主题中所述进行编号，并提供帮助您解决所涉及的问题详细的信息。

错误和警告在此处列出是仅适用于[PackageReference 基于](../consume-packages/package-references-in-project-files.md)项目和 NuGet 4.3.0+。 NuGet 也服从 MSBuild 属性，以禁止显示警告或将它们提升到错误。 有关详细信息，请参阅[如何： 禁止显示编译器警告](/visualstudio/ide/how-to-suppress-compiler-warnings)Visual Studio 文档中。

**错误**

| Group | 错误号 |
| --- | --- |
| [无效的输入的错误](#invalid-input-errors) | [NU1001](#nu1001)， [NU1002](#nu1002)， [NU1003](#nu1003) |
| [缺少的包和项目错误](#missing-package-and-project-errors) | [NU1100](#nu1100)， [NU1101](#nu1101)， [NU1102](#nu1102)， [NU1103](#nu1103)， [NU1104](#nu1104)， [NU1105](#nu1105)， [NU1106](#nu1106)， [NU1107](#nu1107) (以前 NU1607) [NU1108](#nu1108) (以前 NU1606) |
| [兼容性错误](#compatibility-errors) | [NU1201](#nu1201)， [NU1202](#nu1202)， [NU1203](#nu1203)， [NU1401](#nu1401) |

**警告**

| Group | 警告编号 |
| --- | --- |
| [无效的输入的警告](#invalid-input-warnings) | [NU1501](#nu1501)， [NU1502](#nu1502)， [NU1503](#nu1503) |
| [意外的包版本警告](#unexpected-package-version-warnings) | [NU1601](#nu1601)， [NU1602](#nu1602)， [NU1603](#nu1603)， [NU1604](#nu1604)， [NU1605](#nu1605) |
| [冲突解决程序冲突警告](#resolver-conflict-warnings) | [NU1608](#nu1608) |
| [包回退警告](#package-fallback-warnings) | [NU1701](#nu1701) |
| [源警告](#feed-warnings) | [NU1801](#nu1801) |
| [NuGet 内部错误和警告](#nuget-internal-errors-and-warnings) | [NU1000](#nu1000)， [NU1500](#nu1500) |
| [已签名的软件包 （创建和验证）](#signed-packages-creation-and-verification)| [NU3000](#nu3000)， [NU3001](#nu3001)， [NU3002](#nu3002)， [NU3004](#nu3004)， [NU3008](#nu3008)， [NU3018](#nu3018)， [NU3028](#nu3028) |

## <a name="invalid-input-errors"></a>无效的输入的错误

[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)

### <a name="nu1001"></a>NU1001

| | |
| --- | --- |
| **问题** | 项目不包含一个或多个框架。 |
| **示例消息** | *项目 projA c:\tmp\projA.csproj 中未指定任何目标框架* |
| **解决方案** | 添加`TargetFramework`或`TargetFrameworks`属性设置为指定的项目文件。 |

### <a name="nu1002"></a>NU1002

| | |
| --- | --- |
| **问题** | 无效的输入以及清除关键字的组合。 |
| **示例消息** | *清除不能在与其他值一起使用* |
| **解决方案** | 清除自行使用，而忽略所有其他输入。 |

### <a name="nu1003"></a>NU1003

| | |
| --- | --- |
| **问题** | `PackageTargetFallback` 和`AssetTargetFallback`用于选择资产提供不同的行为和不能一起使用。 |
| **示例消息** | *PackageTargetFallback 和 AssetTargetFallback 不能一起使用。从项目环境删除 PackageTargetFallback(deprecated) 的引用。* |
| **解决方案** | 删除不推荐使用`PackageTargetFallback`从项目的元素。 |

## <a name="missing-package-and-project-errors"></a>缺少的包和项目错误

[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)

### <a name="nu1100"></a>NU1100

| | |
| --- | --- |
| **问题** | 依赖关系组不被解析。 这是一个泛型类型不是包或项目的问题。 |
| **示例消息** | *无法解析 net45 System.Missing* |
| **解决方案** | 打开项目文件并检查其依赖项列表。 检查在你使用的包源上存在每个依赖关系和包支持项目的目标框架。 |

### <a name="nu1101"></a>NU1101

| | |
| --- | --- |
| **问题** | 在任何源上找不到包。 |
| **示例消息** | *找不到程序包 System.Missing。具有此 id 在源中存在的任何包： dotnet 核心、 dotnet roslyn、 nuget.org* |
| **解决方案** | 检查以确保使用正确的包标识符和版本号数目的 Visual Studio 中的项目的依赖关系。 此外检查[NuGet 配置](../consume-packages/Configuring-NuGet-Behavior.md)标识的包源你希望使用。 如果你使用具有的包[语义版本控制 2.0.0](../reference/package-versioning.md#semantic-versioning-200)，请确保你使用的源，V3`https://api.nuget.org/v3/index.json`中[NuGet 配置](../consume-packages/Configuring-NuGet-Behavior.md)。 |

### <a name="nu1102"></a>NU1102

| | |
| --- | --- |
| **问题** | 找到的包标识符，但在任何源上找不到指定的依赖范围内的版本。 可能由包和不是用户指定的范围。 |
| **示例消息** | *找不到版本包 NuGet.Versioning (> = 9.0.1)<br/> -于 nuget.org 中的找到 30 版本 [最接近的版本： 4.0.0]<br/> -dotnet buildtools 中找到的 10 版本 [最接近的版本： 4.0.0-rc-2129]<br/> -找到 9在 NuGetVolatile 版本 [最接近的版本： 3.0.0-beta-00032]<br/> -0 版本位于 dotnet 核心<br/>-0 版本位于 dotnet roslyn* |
| **解决方案** | 编辑项目文件以更正包版本。 此外检查[NuGet 配置](../consume-packages/Configuring-NuGet-Behavior.md)标识的包源你希望使用。 你可能需要更改 requeted 版本，如果此包被直接引用该项目。 |

### <a name="nu1103"></a>NU1103

| | |
| --- | --- |
| **问题** | 项目指定了依赖项的范围，稳定版本，但不稳定版本找该范围内。 预发行版本未找到，但不是允许。 |
| **示例消息** | *找不到稳定的包 NuGet.Versioning 随版本 (> = 3.0.0)<br/> -dotnet buildtools 中找到的 10 版本 [最接近的版本： 4.0.0-rc-2129]<br/> -NuGetVolatile 中的找到 9 版本 [最接近的版本： 3.0.0-beta-00032]<br/> -0 版本位于 dotnet 核心<br/>-0 版本位于 dotnet roslyn* |
| **解决方案** |  编辑项目文件以包括预发行版本中的版本范围。 请参阅[包版本控制](../reference/Package-Versioning.md)。 |

### <a name="nu1104"></a>NU1104

| | |
| --- | --- |
| **问题** | ProjectReference 指向不存在的文件。 |
| **示例消息** | *项目引用不存在 c:\a.csproj。检查项目引用有效以及项目文件是否存在。* |
| **解决方案** | 编辑项目文件以更正引用的项目的路径，或若要删除的引用一起删除，如果不再需要。 |

### <a name="nu1105"></a>NU1105

| | |
| --- | --- |
| **问题** | 项目文件存在，但不还原信息已为其提供。 |
| **示例消息** | *无法读取 c:\a.csproj 的项目信息。项目文件可能无效或缺少所需的还原的目标。* |
| **解决方案** | 在 Visual Studio 中，该错误可能意味着该项目已卸载，在这种情况下重新加载项目。 从命令行这可能表示该文件已损坏或，它不包含"之后导入"自定义所需的还原，以便读取项目的目标。 检查项目文件有效以及包含"之后导入"目标。 |

### <a name="nu1106"></a>NU1106

| | |
| --- | --- |
| **问题** | 无法解析依赖项约束。 |
| **示例消息** | *无法满足 {id} 互相冲突的请求: {冲突路径} Framework: {目标关系图}* |
| **解决方案** | 编辑项目文件以指定的依赖项而不是准确的版本更自由范围。 |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a>NU1107 (以前 NU1607)

| | |
| --- | --- |
| **问题** | 无法解析包之间的依赖关系约束。 |
| **示例消息** | *NuGet.Versioning 检测到的版本冲突。若要解决此问题的项目中直接引用包。<br/>NuGet.Packaging 3.5.0-> （= 3.5.0） NuGet.Versioning<br/> NuGet.Configuration 4.0.0-> 的 NuGet.Versioning （= 4.0.0）* |
| **解决方案** | 依赖项与上的约束的确切版本的包不允许其他包以根据需要增大版本号。 添加具有所需的确切版本对直接 （在项目文件中） 项目的引用。 |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a>NU1108 (以前 NU1606)

| | |
| --- | --- |
| **问题** | 检测到循环依赖关系。 |
| **示例消息** | *检测到循环： A-> B-> A* |
| **解决方案** | 不正确; 创作包请与联系软件包所有者以更正 bug。 |

## <a name="compatibility-errors"></a>兼容性错误

[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)

### <a name="nu1201"></a>NU1201

| | |
| --- | --- |
| **问题** | 依赖项项目不包含与当前项目兼容的框架。 通常情况下，项目的目标框架是比使用项目的更高版本。 |
| **示例消息** | *项目 ServerWeb 与不兼容 netstandard1.3 (。NETStandard，Version = v1.3)。项目 ServerWeb 支持：<br/> -netstandard1.6 (。NETStandard，Version = v1.6)<br/> -netcoreapp1.0 (。NETCoreApp，Version = v1.0)* |
| **解决方案** | 将项目的目标框架更改为使用项目的相等或更低版本。 |

### <a name="nu1202"></a>NU1202

| | |
| --- | --- |
| **问题** | 依赖项包不包含任何与项目兼容的资产。 |
| **示例消息** | *包 System.ComponentModel.EventBasedAsync 4.0.11 与不兼容 netstandard1.3 (。NETStandard，Version = v1.3)。打包 System.ComponentModel.EventBasedAsync 4.0.11 支持：<br/> -monoandroid10 (MonoAndroid，Version = v1.0)<br/> -monotouch10 (MonoTouch，Version = v1.0)<br/> -net45 (。NETFramework，Version = v4.5)<br/> -netcore50 (。NETCore，Version = 5.0 版)<br/> -netstandard1.0 (。NETStandard，Version = v1.0)<br/> -可移植 net45 + win8 + wp8 + wpa81 (。NETPortable，Version = v0.0，配置文件 = Profile259)<br/> -win8 (Windows、 版本 = v8.0)<br/> -wp8 (WindowsPhone，Version = v8.0)<br/> -wpa81 (WindowsPhoneApp，Version = v8.1)<br/> -xamarinios10 (Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*|
| **解决方案** | 将项目的目标框架更改为另一个包支持。 |

### <a name="nu1203"></a>NU1203

| | |
| --- | --- |
| **问题** | 包不支持项目的`RuntimeIdentifier`。 |
| **示例消息** | *System.Example 1.0.0 提供 a.dll 的编译时引用程序集上 net461，但没有兼容的运行时程序集。* |
| **解决方案** | 更改`RuntimeIdentifier`根据需要在项目中使用的值。 |

### <a name="nu1401"></a>NU1401

| | |
| --- | --- |
| **问题** | 包需要功能或框架当前不支持安装的 NuGet 版本。 |
| **示例消息** | *NuGet.Versioning 程序包需要 NuGet 客户端版本"5.0.0"或更高版本，但是当前 NuGet 版本为"4.3.0"。* |
| **解决方案** | 安装较新版本的 NuGet。 请参阅[安装 NuGet 客户端工具](../install-nuget-client-tools.md)。 |

## <a name="invalid-input-warnings"></a>无效的输入的警告

[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)

### <a name="nu1501"></a>NU1501

| | |
| --- | --- |
| **问题** | 项目还原尝试运行在未找到。 |
| **示例消息** | *文件夹 c:\projects\a 不包含要还原的项目。* |
| **解决方案** | 在包含项目的文件夹中运行 nuget 还原。 |

### <a name="nu1502"></a>NU1502

| | |
| --- | --- |
| **问题** | `RuntimeSupports` 包含无效的配置文件。 通常情况下，支持配置文件中找不`runtime.json`从当前的依赖项包文件。|
| **示例消息** | *未知的兼容性配置文件： aaa* |
| **解决方案** | 检查`RuntimeSupports`项目中的值。 |

### <a name="nu1503"></a>NU1503

| | |
| --- | --- |
| **问题** | 依赖项项目不能导入 NuGet 的恢复目标。 这是类似于 NU1105 但此处项目，将跳过并忽略而不是导致所有还原失败。 在复杂的解决方案通常有其他类型的可能不支持还原的项目中。 |
| **示例消息** | *正在跳过还原项目 c:\a.csproj。项目文件可能无效或缺少所需的还原的目标。* |
| **解决方案** | 这可能会导致不导入公共属性/目标的自动导入还原的项目。 如果项目不需要还原这可予以忽视。 否则，编辑受影响的项目添加为还原的目标。 |

## <a name="unexpected-package-version-warnings"></a>意外的包版本警告

[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)

### <a name="nu1601"></a>NU1601

| | |
| --- | --- |
| **问题** | 直接项目依赖项已解除了一个为更高版本比指定的项目。 |
| **示例消息** | *指定的依赖项已 NuGet.Versioning (> = 3.5.0) 但最终的 NuGet.Versioning 4.0.0。* |
| **解决方案** | 更新到适当版本的项目中的依赖关系。 |

### <a name="nu1602"></a>NU1602

| | |
| --- | --- |
| **问题** | 包依赖项缺少零下限。 这不允许还原，以便查找*最佳匹配*。 每个还原将浮动向下尝试查找可以使用较低版本。 这意味着此恢复将进入联机状态，以检查每个时间而不是在用户程序包文件夹中使用已存在的包的所有源。 |
| **示例消息** | *NuGet.Packaging 4.0.0 不依赖项 NuGet.Versioning (> 3.5.0) 提供包含下限。3.6.0 的近似最佳匹配已解决。* |
| **解决方案** | 这通常是创作错误的包。 请联系程序包作者以解决此问题。 |

### <a name="nu1603"></a>NU1603

| | |
| --- | --- |
| **问题** | 包依赖项指定未找到的版本。 通常情况下，包源中不包含预期的下限版本。 与它不同的包编写针对相反，使用更高版本。<br/><br/>这意味着找不到该还原*最佳匹配*。 每个还原将浮动向下尝试查找可以使用较低版本。 这意味着此恢复将进入联机状态，以检查每个时间而不是在用户程序包文件夹中使用已存在的包的所有源。 |
| **示例消息** | NuGet.Packaging 4.0.0 取决于 NuGet.Versioning (> = 4.0.0) 但找不到 4.0.0。 5.0.0 的近似最佳匹配已解决。 |
| **解决方案** | 如果尚未释放预期包，这可能是包创作错误。 请联系程序包作者以解决此问题。 如果已发布包，然后检查它是否可用上正在使用的包源。 如果使用私有源时，你可能需要更新上的源的包。 |

### <a name="nu1604"></a>NU1604

| | |
| --- | --- |
| **问题** | 项目依赖项未定义零下限。<br/><br/>这意味着找不到该还原*最佳匹配*。 每个还原将浮动向下尝试查找可以使用较低版本。 这意味着此恢复将进入联机状态，以检查每个时间而不是在用户程序包文件夹中使用已存在的包的所有源。 |
| **示例消息** | *项目依赖项 NuGet.Versioning (< = 9.0.0) doe 不包含包含下限。依赖项版本以确保一致还原结果中包括零下限。* |
| **解决方案** | 更新项目的`PackageReference``Version`属性以包括零下限。 |

### <a name="nu1605"></a>NU1605

| | |
| --- | --- |
| **问题** | 依赖项包指定比还原最终解决更高版本的包的版本约束。 也就是说，"最接近的 wins"规则在解析包时，由于在图中的最近包可能已重写相距包。 |
| **示例消息** | *检测到包降级： NuGet.Versioning 从 4.0.0 到 3.5.0。要选择的不同版本的项目中直接引用包。<br/>NuGet.Packaging 3.5.0-> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0-> NuGet.Configuration 4.0.0-> NuGet.Versioning 4.0.0* |
| **解决方案** | 添加到你想要使用的包的更高版本的项目的直接引用。 |

## <a name="resolver-conflict-warnings"></a>冲突解决程序冲突警告

### <a name="nu1608"></a>NU1608

| | |
| --- | --- |
| **问题** | 解决的包是不是依赖项约束允许，更高版本。 这意味着项目直接引用的包将从其他包的依赖项约束重写。|
| **示例消息** | *外部依赖关系约束的检测到的包版本： x 1.0.0 要求的 y （= 1.0.0），但版本 y 2.0.0 为已解决。* |
| **解决方案** | 在某些情况下，这是有意，可以禁止显示警告。 否则，更改以扩大其版本约束的包项目的引用。 |

## <a name="package-fallback-warnings"></a>包回退警告

### <a name="nu1701"></a>NU1701

| | |
| --- | --- |
| **问题** | `PackageTargetFallback` / `AssetTargetFallback` 用来从包选择资产。 警告让用户知道资产可能不兼容的 100%。 |
| **示例消息** | *包 NuGet.Versioning 已还原可移植 net45 + win8 改为使用项目目标框架 netstandard1.5。此程序包并不一定与你的项目完全兼容。* |
| **解决方案** | 将项目的目标框架更改为另一个包支持。 |

## <a name="feed-warnings"></a>源警告

### <a name="nu1801"></a>NU1801

| | |
| --- | --- |
| **问题** | 读取源时出错时`IgnoreFailedSources`设置为 true，将其转换为非致命性警告。 这可能包含的任何消息，并为泛型。 |
| **示例消息** | n/a |
| **解决方案** | 编辑你的配置来指定有效的源。 |

## <a name="nuget-internal-errors-and-warnings"></a>NuGet 内部错误和警告

[NU1000](#nu1000) | [NU1500](#nu1500)

### <a name="nu1000"></a>NU1000

| | |
| --- | --- |
| **问题** | 从 NuGet 非特定的内部错误。 |
| **解决方案** | 检查日志以了解更多信息 |

### <a name="nu1500"></a>NU1500

| | |
| --- | --- |
| **问题** | 从 NuGet 内部非特定警告。 |
| **解决方案** | 检查日志以了解更多信息 |

## <a name="signed-packages-creation-and-verification"></a>已签名的软件包 （创建和验证）

*NuGet 4.6.0+*

[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)

### <a name="nu3000"></a>NU3000

| | |
| --- | --- |
| **问题** | 非特定错误相关的包签名和签名包验证。 |
| **解决方案** | 请检查日志以了解更多信息。 |

### <a name="nu3001"></a>NU3001

| | |
| --- | --- |
| **问题** | 无效的自变量为[登录命令](../tools/cli-ref-sign.md)或[验证命令](../tools/cli-ref-verify.md)。 |
| **解决方案** | 检查并更正提供的自变量。 |

### <a name="nu3002"></a>NU3002

| | |
| --- | --- |
| **问题** | `-Timestamper`选项未指定与[nuget 登录命令](../tools/cli-ref-sign.md)。 |
| **示例消息** | *-Timestamper 未提供选项。签名的包不会加盖时间戳。* |
| **解决方案** | 指定`-Timestamper`选项与`nuget sign`。 |

### <a name="nu3004"></a>NU3004

| | |
| --- | --- |
| **问题** | 未签名的软件包提供给[nuget 验证命令](../tools/cli-ref-verify.md)。 |
| **解决方案** | 运行`nuget verify`与已签名的包。 请参阅[对包签名](../create-packages/Sign-a-Package.md)。 |

### <a name="nu3008"></a>NU3008

| | |
| --- | --- |
| **问题** | 包完整性检查失败，这意味着已签名的包已被篡改因为正进行签名。 |
| **解决方案** | 扫描计算机中的与防病毒软件。 然后从计算机中删除包、 重新安装它，和重试该操作。 如果问题仍然存在，请联系的包源的所有者和包所有者。 |

### <a name="nu3018"></a>NU3018

| | |
| --- | --- |
| **问题** | 证书链生成失败主签名。 主签名证书不受信任，被吊销，或者该证书的吊销信息不可用。 |
| **示例消息** | *警告： NU3018： 吊销功能无法检查吊销证书。* |
| **解决方案** | 使用一个受信任且有效的证书。 检查 internet 连接。 |

### <a name="nu3028"></a>NU3028

| | |
| --- | --- |
| **问题** | 证书链生成失败的时间戳签名。 时间戳签名证书不受信任，被吊销，或者该证书的吊销信息不可用。 |
| **示例消息** | *警告： NU3028： 吊销功能无法检查吊销证书。* |
| **解决方案** | 使用一个受信任且有效的证书。 检查 internet 连接。 |
