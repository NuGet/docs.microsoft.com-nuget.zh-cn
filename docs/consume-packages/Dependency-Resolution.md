---
title: NuGet 包依赖项解析
description: 详细说明解析 NuGet 包的依赖项以及在 NuGet 2.x 和 NuGet 3.x+ 上安装依赖项的流程。
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: cdbe13df04bb27091b684a4ae27b0e751da1098f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549029"
---
# <a name="how-nuget-resolves-package-dependencies"></a>NuGet 如何解析包依赖项

每当安装或重新安装包（包括在[还原](../consume-packages/package-restore.md)过程中安装）时，NuGet 还会安装第一个包所依赖的任何其他包。

这些直接依赖项可能本身也具有依赖项，并可能继续延伸到任意深度。 这便形成了所谓的“依赖项关系图”，用于说明各级包之间的关系。

当多个包具有相同的依赖项时，同一个包 ID 会在关系图中多次出现且可能具有不同的版本约束。 但是，一个项目中只能使用给定包的一个版本，因此 NuGet 必须选择要使用的版本。 确切流程取决于要使用的包管理格式。

## <a name="dependency-resolution-with-packagereference"></a>利用 PackageReference 解析依赖项

当将包安装到使用 PackageReference 格式的项目中时，NuGet 将添加对相应文件中的平面包关系图的引用并提前解决冲突。 此过程称为“传递还原”。 重新安装或还原包指的是下载关系图中列出的包的过程，此过程可加快生成的速度和提高其可预测性。 还可以利用通配符（可变）版本（如 2.8.\*），避免对客户端计算机和生成服务器上的 `nuget update` 进行成本高昂且容易出错的调用。

当 NuGet 还原进程在生成之前运行时，它将首先解析内存中的依赖项，然后将生成的关系图写入名为 `project.assets.json` 的文件（位于使用 PackageReference 的项目的 `obj` 文件夹中）。 MSBuild 随后将读取此文件并将其转换成一组文件夹（可在其中找到潜在引用），然后将它们添加到内存中的项目树。

该锁定文件是临时的，不应添加到源代码管理中。 默认情况下，此文件将在 `.gitignore` 和 `.tfignore` 中列出。 请参阅[包与源代码管理](packages-and-source-control.md)。

### <a name="dependency-resolution-rules"></a>依赖项解析规则

传递还原应用 4 条主要规则来解析依赖项：最低适用版本、可变版本、选择最近项和等距依赖项。

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>最低适用版本

最低适用版本规则根据包依赖项的定义还原包的最低可能版本。 此规则还适用于应用程序上或类库上未声明为[可变](#floating-versions)的依赖项。

例如在下图中，1.0 beta 版本低于 1.0，因此 NuGet 选择 1.0 版本：

![选择最低适用版本](media/projectJson-dependency-1.png)

在下图中，版本约束为 >= 2.1，但源上未提供版本 2.1 ，因此 NuGet 选取能找到的下一个最低版本，在此示例中即为 2.2：

![选择源上提供的下一个最低版本](media/projectJson-dependency-2.png)

当源上未提供应用程序指定的确切版本号（如 1.2）时，NuGet 将在尝试安装或还原包时出错并导致失败：

![NuGet 在未提供确切包版本时生成错误](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a>可变（通配符）版本

可变或通配符依赖项版本通过 \* 通配符（如 6.0.\*）进行指定。 此版本规格表示“使用最新的 6.0.x 版本”；4.\* 则表示“使用最新的 4.x 版本”。 使用通配符可允许依赖项包继续延伸，但无需更改所使用的应用程序（或包）。

使用通配符时，NuGet 将解析与版本模式匹配的最高包版本，例如，请求 6.0\* 将获得以 6.0 开头的最高包版本：

![请求可变版本 6.0.* 时，选取版本 6.0.1](media/projectJson-dependency-4.png)

> [!Note]
> 有关通配符和预发行版本的行为的信息，请参阅[包版本控制](../reference/package-versioning.md#version-ranges-and-wildcards)。


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>选择最近项

当应用程序的包关系图包含相同包的不同版本时，NuGet 将选择关系图中最接近应用程序的包并忽略所有其他包。 通过此行为，应用程序能够替代依赖项关系图中的任何特定包版本。

在下面的示例中，应用程序直接依赖于版本约束为 >=2.0 的包 B。 应用程序还依赖于版本约束为 >=1.0 的包 A，此包依赖于包 B。 在关系图中，由于包 B 2.0 上的依赖项更接近应用程序，因此将使用该版本：

![使用“选择最近项”规则的应用程序](media/projectJson-dependency-5.png)

>[!Warning]
> “选择最近项”规则可导致包版本降级，可能破坏关系图中的其他依赖项。 因此用户应用此规则时会收到警告提醒。

此规则还可提高大型依赖项关系图（如具有 BCL 包的关系图）的效率，因为忽略某个给定依赖项后，NuGet 还将忽略关系图中该分支上的所有其余依赖项。 例如在下图中，由于使用了包 C 2.0，因此 NuGet 忽略了关系图中引用旧版包 C 的所有分支：

![当 NuGet 忽略关系图中的某个包时，它将忽略其所在的整个分支](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>等距依赖项

当关系图中引用的不同包版本与应用程序具有相同距离时，NuGet 将使用满足所有版本要求的最低版本（与[最低适用版本](#lowest-applicable-version)和[可变版本](#floating-versions)规则相似）。 例如在下图中，2.0 版本的包 B 满足另一个 >=1.0 约束，因此使用此包：

![使用满足所有约束的较低版本解析等距依赖项](media/projectJson-dependency-7.png)

某些情况下无法满足所有版本要求。 如下所示，如果包 A 明确要求包 B 1.0，而包 C 要求包 B >=2.0，NuGet 则无法解析依赖项并显示错误。

![确切版本要求导致无法解析依赖项](media/projectJson-dependency-8.png)

在此情况下，顶层使用者（应用程序或包）应在包 B 上添加其自己的直接依赖项，以便应用[选择最近项](#nearest-wins)规则。

## <a name="dependency-resolution-with-packagesconfig"></a>利用 packages.config 解析依赖项

利用 `packages.config`，项目依赖项 将作为简单列表写入 `packages.config`。 这些包的所有依赖项也将写入同一列表。 安装包时，NuGet 可能还会修改 `.csproj` 文件、`app.config`、`web.config` 和其他单独文件。

利用 `packages.config`，NuGet 可尝试解决在安装每个单独包期间出现的依赖项冲突。 也就是说，如果正在安装包 A 并且其依赖于包 B，同时包 B 已作为其他项的依赖项在 `packages.config` 中列出，则 NuGet 将比较所请求的包 B 版本，并尝试找到满足所有版本约束的版本。 具体而言，NuGet 将选择可满足依赖项的较低 major.minor 版本。

默认情况下，NuGet 2.8 会查找最低的修补程序版本（请参阅 [NuGet 2.8 发行说明](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)）。 可以通过 `Nuget.Config` 中的 `DependencyVersion` 属性和命令行上的 `-DependencyVersion` 开关控制此设置。  

用于解析依赖项的 `packages.config` 进程会随着依赖项关系图的规模增大而愈加复杂。 每次安装新包都需要遍历整个关系图，并且可能引发版本冲突。 发生冲突时，安装将停止，此时项目处于不确定状态，很可能导致项目文件本身发生更改。 使用其他包管理格式时则不会出现此问题。

## <a name="managing-dependency-assets"></a>管理依赖项资产

使用 PackageReference 格式时，可以控制依赖项中的哪些资产可流入顶层项目。 有关详细信息，请参阅 [PackageReference](package-references-in-project-files.md#controlling-dependency-assets)。

当顶层项目本身是一个包时，还需要使用其依赖项在 `.nuspec` 文件中列出的 `include` 和 `exclude` 属性来控制此流。 请参阅 [.nuspec 引用 - 依赖项](../reference/nuspec.md#dependencies)。

## <a name="excluding-references"></a>排除引用

对于有些方案，同一项目中可能多次引用具有相同名称的程序集，并因此生成设计时和生成时错误。 例如，某个项目既包含自定义版本的 `C.dll`，又引用同样包含 `C.dll` 的包 C。 同时，该项目还依赖于同样依赖于包 C 和 `C.dll` 的包 B。 在此情况下，NuGet 无法确定要使用哪一个 `C.dll`，但你也不能直接删除包 C 上的项目依赖项，因为包 B 也依赖于此依赖项。

要解决此问题，必须直接引用所需的 `C.dll`（或使用其他引用正确对象的包），然后在包 C 上添加不包括其所有资产的依赖项。 此方法如下所示，具体取决于当前使用的包管理格式：

- [PackageReference](../consume-packages/package-references-in-project-files.md)：在依赖项中添加 `Exclude="All"`：

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" Exclude="All" />
    ```

- `packages.config`：从 `.csproj` 文件中删除对 PackageC 的引用，以便它仅引用所需版本的 `C.dll`。
    
## <a name="dependency-updates-during-package-install"></a>在安装包期间更新依赖项 

如果依赖项版本已满足，则在其他程序包安装期间不会更新依赖项。 例如，假设包 A 依赖于包 B 并且指定版本号 1.0。 源存储库包含程序包 B 的版本 1.0、1.1 和 1.2。如果将 A 安装在已包含 B 版本 1.0 的项目中，则 B 1.0 将保持使用状态，因为它满足版本限制。 但是，如果包 A 请求 1.1 或更高版本的 B，则会安装 B 1.2。 

## <a name="resolving-incompatible-package-errors"></a>解决包不兼容错误

在包还原操作期间，可能会看到错误“一个或多个包不兼容...”或包与项目的目标框架“不兼容”。

如果项目中引用的一个或多个包未指示其支持包的目标框架，则会出现此错误；即，包的 `lib` 文件夹中不包含与此项目兼容的目标框架的适用 DLL。 （请参阅[目标框架](../reference/target-frameworks.md)获取列表。） 

例如，如果项目面向 `netstandard1.6`，并且你尝试安装仅在 `lib\net20` 和 `\lib\net45` 文件夹中包含 DLL 的包，则将看到类似如下针对包或其依赖项的消息：

```output
Restoring packages for myproject.csproj...
Package ContosoUtilities 2.1.2.3 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoUtilities 2.1.2.3 supports:
  - net20 (.NETFramework,Version=v2.0)
  - net45 (.NETFramework,Version=v4.5)
Package ContosoCore 0.86.0 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoCore 0.86.0 supports:
  - 11 (11,Version=v0.0)
  - net20 (.NETFramework,Version=v2.0)
  - sl3 (Silverlight,Version=v3.0)
  - sl4 (Silverlight,Version=v4.0)
One or more packages are incompatible with .NETStandard,Version=v1.6.
Package restore failed. Rolling back package changes for 'MyProject'.
```

要解决不兼容问题，请执行下列操作之一：

- 将项目重定向到要使用的包所支持的框架。
- 联系包创建者并与其协作添加对所选框架的支持。 [nuget.org](https://www.nuget.org/) 中每个列出包的页面均针对此目的提供了“联系所有者”链接。

