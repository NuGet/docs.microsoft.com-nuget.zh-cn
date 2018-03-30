---
title: NuGet 包中的预发行版本 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 用于生成预发行包的指南
keywords: 版本控制, NuGet 包版本控制, NuGet 预发行版本, NuGet 预发行包, 预览包版本, RC 包版本, Beta 包版本, NuGet 语义化版本控制
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 57f59e3906e2d49b6b6e078f530885a601553b06
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="building-pre-release-packages"></a>生成预发行包

每当发布具有新版本号的更新包时，NuGet 将其视为所示的“最新稳定版本”，以 Visual Studio 中的包管理器 UI 为例：

![显示最新稳定版本的包管理器 UI](media/Prerelease_01-LatestStable.png)

稳定版本是指被视为足够可靠，可在生产中使用的版本。 最新稳定版本也指作为包更新安装或在包还原期间安装的版本（受制于[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md)中所述的约束）。

为了支持软件的版本生命周期，NuGet 1.6 及更高版本允许分配预发行包，其中的版本号包括语义化版本控制后缀，如 `-alpha`、`-beta` 或 `-rc`。 有关详细信息，请参阅[包版本控制](../reference/package-versioning.md#pre-release-versions)。

可通过以下两种方式指定此类版本：

- `.nuspec` 文件：在 `version` 元素中包括语义化版本后缀：

    ```xml
    <version>1.0.1-alpha</version>
    ```

- 程序集属性：生成 Visual Studio 项目的包（`.csproj` 或 `.vbproj`）时，使用 `AssemblyInformationalVersionAttribute` 指定版本：

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    NuGet 选取此值，而不是在 `AssemblyVersion` 属性中指定的不支持语义化版本控制的值。

做好发布稳定版本的准备后，只需删除后缀，该包便优先于任何预发行版本。 同样，请参阅[包版本控制](../reference/package-versioning.md#pre-release-versions)。

## <a name="installing-and-updating-pre-release-packages"></a>安装和更新预发行包

默认情况下，NuGet 在处理包时不会包括预发行版本，但按照下文所述方法可更改此行为：

- Visual Studio 中的包管理器 UI：在“管理 NuGet 包”UI 中，选中“包括预发行版”框：

    ![Visual Studio 中的“包括预发行版”复选框](media/Prerelease_02-CheckPrerelease.png)

    设置或清除此框将刷新包管理器 UI 和可安装的可用版本的列表。

- **包管理器控制台**：将 `-IncludePrerelease` 开关与 `Find-Package`、`Get-Package`、`Install-Package`、`Sync-Package` 和 `Update-Package` 命令配合使用。 请参阅 [PowerShell 参考](../tools/powershell-reference.md)。

- **NuGet CLI**：将 `-prerelease` 开关与 `install`、`update`、`delete` 和 `mirror` 命令配合使用。 请参阅 [NuGet CLI 参考](../tools/nuget-exe-cli-reference.md)

## <a name="semantic-versioning"></a>语义化版本控制

[语义化版本控制或 SemVer 约定](http://semver.org/spec/v1.0.0.html)介绍如何利用版本号中的字符串传达基础代码的含义。

在此约定中，每个版本由三部分组成，即 `Major.Minor.Patch`，其含义分别是：

- `Major`：重大更改
- `Minor`：新增功能，但可向后兼容
- `Patch`：仅可向后兼容的 bug 修复

然后，通过在修补程序编号后追加连字符和字符串表示预发行版本。 从技术上说，可在连字符后使用任意字符串，NuGet 都会将包视为预发行版。 然后，NuGet 在适用的 UI 中显示完整的版本号，供使用者自己解读其含义。

出于这种考虑，通常最好遵照如下所示的公认命名约定：

- `-alpha`：Alpha 版本，通常用于在制品和试验品
- `-beta`：Beta 版本，通常指可用于下一计划版本的功能完整的版本，但可能包含已知 bug。
- `-rc`：候选发布，通常可能为最终（稳定）版本，除非出现重大 bug。

> [!Note]
> NuGet 4.3.0+ 支持[语义化版本控制 v2.0.0](http://semver.org/spec/v2.0.0.html)，后者支持采用点表示法的预发布号，如 `1.0.1-build.23` 中所示。 NuGet 4.3.0 之前的版本不支持点表示法。 在 NuGet 的早期版本中，可以使用 `1.0.1-build23` 之类的格式，但这始终被视为预发布版本。

但是，无论使用何种后缀，NuGet 都会按照反向字母顺序向它们赋予优先级：

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

如上所示，没有任何后缀的版本始终优先于预发行版本。 另请注意，如果在可能使用两位数（或更多数字）的预发行版本标记中使用数字后缀，请使用前导零，如 beta01 和 beta05，以便确保数字增大时，可以正确地进行排序。
