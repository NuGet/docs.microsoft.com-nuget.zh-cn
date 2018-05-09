---
title: 重新安装并更新 NuGet 包
description: 有关何时需要重新安装和更新包的详细信息，与 Visual Studio 中损坏的包引用一样。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: conceptual
ms.openlocfilehash: fc2c1a58f787da61041c644085058355de4f12ea
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="how-to-reinstall-and-update-packages"></a>如何重新安装和更新包

[何时重新安装包](#when-to-reinstall-a-package)中描述了大量有关对包的引用可能在 Visual Studio 项目中损坏的情况。 在这些情况下，卸载并重新安装同一版本的包会将这些应用还原为正常工作状态。 更新包仅意味着安装更新版本，这常常将包还原为正常工作状态。

更新和重新安装包按以下方式实现：

| 方法 | 更新 | 重新安装 |
| --- | --- | --- |
| 包管理器控制台（[使用 Update-Package](#using-update-package) 中所述） | `Update-Package` 命令 | `Update-Package -reinstall` 命令 |
| 包管理器 UI | 在“更新”选项卡上，选择一个或多个包并选择“更新” | 在“已安装”选项卡上，选择一个包，记录其名称，然后选择“卸载”。 切换到“浏览”选项卡，搜索包名称并选中，然后选择“安装”。 |
| nuget.exe CLI | `nuget update` 命令 | 对于所有包，删除包文件夹，然后运行 `nuget install`。 对于单个包，删除包文件夹并使用 `nuget install <id>` 再安装一个。 |

本文内容：

- [何时重新安装包](#when-to-reinstall-a-package)
- [约束升级版本](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>何时重新安装包

1. **包还原后的损坏引用**：如果已打开项目并还原了 NuGet 包，但仍看见了损坏的引用，请尝试重新安装每个包。
1. **项目因删除文件损坏**：NuGet 不会阻止删除从包添加的项，因此很容易在无意中修改从包安装的内容并损坏项目。 要还原项目，请重新安装受影响的包。
1. **包更新损坏了项目**：如果包的更新损坏了项目，则故障通常由可能也已更新的依赖项包引起。 要还原依赖项的状态，请重新安装该特定包。
1. **项目重定向或升级**：这在项目已重定向或升级时并且如果包因为更改目标框架需要重新安装时有用。 NuGet 在项目重定向后立即显示该情况下的生成错误，后续生成警告会提醒你包可能需要重新安装。 对于项目升级，NuGet 显示项目升级日志中的错误。
1. **开发期间重新安装包**：包创作者常常需要重新安装与他们开发来测试行为的包版本相同的包。 `Install-Package` 命令不提供强制重新安装选项，所以换成使用 `Update-Package -reinstall`。

## <a name="constraining-upgrade-versions"></a>约束升级版本

默认情况下，重新安装或更新包常常会安装包源中提供的最新版本。

但是，在使用 `packages.config` 管理格式的项目中，可以专门约束版本范围。 例如，如果知道可能因为包 API 中存在重要更改，应用程序只能使用 1.x 版本的包，而不是 2.0 以及更高版本的包，则需要将升级约束为 1.x 版本。 这会阻止可能损坏应用程序的意外更新。

要设置约束，在文本编辑器中打开 `packages.config`，找到有问题的依赖项，然后添加带版本范围的 `allowedVersions` 属性。 例如，要将更新约束为版本 1.x，请将 `allowedVersions` 设为 `[1,2)`：

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

在所有情况下，都使用[包版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)中介绍的表示法。

## <a name="using-update-package"></a>使用 Update-Package

注意下述的[注意事项](#considerations)，可以使用 Visual Studio 包管理器控制台中的 [Update-Package 命令](../Tools/ps-ref-update-package.md)（“工具” > “NuGet 包管理器” > “包管理器控制台”）轻松重新安装任意包：

```ps
Update-Package -Id <package_name> –reinstall
```

使用此命令比删除包然后尝试在 NuGet 库中找到同一版本的同一包更加简单。 请注意，`-Id` 开关是可选的。

没有 `-reinstall` 更新的相同命令会将包更新为更新的版本（如果适用）。 如果有问题的包未安装在项目中，则命令会生成一个错误；即 `Update-Package` 未直接安装包。

```ps
Update-Package <package_name>
```

默认情况下，`Update-Package` 会影响解决方案中的所有项目。 要将操作限制于特定项目，请使用 `-ProjectName` 开关，使用出现在解决方案资源管理器中的项目的名称：

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

要更新一个项目中的所有包（或者使用 `-reinstall` 重新安装），请使用 `-ProjectName` 而无需指定任意特定的包：

```ps
Update-Package -ProjectName MyProject
```

要更新一个解决方案中的所有包，只需使用 `Update-Package`，无需其他参数或开关。 请谨慎使用此窗格，因为它可能需要大量时间来执行所有的更新：

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

使用 [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) 更新项目或解决方案中的包始终会更新为最新版本的包（不包括预发布包）。 如果需要，使用 `packages.config` 的项目可以限制更新版本，如下方[约束更新版本](#constraining-upgrade-versions)中所述。

有关命令的完整详细信息，请参阅 [Update-Package](../Tools/ps-ref-update-package.md) 引用。

### <a name="considerations"></a>注意事项

重新安装包可能影响以下内容：

1. **根据项目目标框架重定向重新安装包**
    - 在简单的情况下，可以仅使用 `Update-Package –reinstall <package_name>` 重新安装包。 会卸载根据旧的目标框架安装的包，同时会根据项目的当前目标框架安装相同的包。
    - 在某些情况下，可能会有不支持新目标框架的包。
        - 如果包支持可移植类库 (PCL) 并且项目重定向到包不再支持的平台组合，则将在重新安装后会失去对包的引用。
        - 这可能会呈现直接使用的包或者作为依赖项安装的包。 直接使用的包可能支持新的目标框架，而其依赖项不支持。
        - 如果重定向应用程序后重新安装包导致生成或运行时错误，则可能需要还原目标框架，或者搜索正确支持新目标框架的替换包。

1. **项目重定向或升级后添加到 packages.config 中的 requireReinstallation 属性**
    - 如果 NuGet 检测到包受到重定向或升级项目的影响，它会将 `packages.config` 中的 `requireReinstallation="true"` 属性添加到所有受影响的包引用。 因此，Visual Studio 中的每个后续生成会引发这些包的生成警告，提醒你重新安装它们。

1. **使用依赖项重新安装包**
    - `Update-Package –reinstall` 重新安装与初始包相同的版本，但是，如果没有提供特定的版本约束，则安装依赖项的最新版本。 这样可以按需仅更新依赖项以解决问题。 但是，如果这将依赖项滚动回早期版本，则可以使用 `Update-Package <dependency_name>` 重新安装该依赖项，而不会影响依赖的包。
    - `Update-Package –reinstall <packageName> -ignoreDependencies` 重新安装同一版本的初始包，但不重新安装依赖项。 在更新包依赖项时使用可能会导致损坏状态

1. **涉及依赖版本时重新安装包**
    - 如上所述，重新安装包不更改依赖它的其他任何已安装包的版本。 然后，重新安装依赖项可能会损坏依赖包。
