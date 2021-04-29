---
title: NuGet 包与源代码管理
description: 介绍有关以下内容的注意事项：如何在版本控制和源代码管理系统中处理 NuGet 包，以及如何使用 Git 和 TFVC 省略包。
author: JonDouglas
ms.author: jodou
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: fa3ec6992002224c9fb56a53aee9096e6d2c6fbb
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901663"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>在源代码管理系统中省略 NuGet 包

开发人员通常省略源代码管理存储库中的 NuGet 包，且改为依赖[包还原](package-restore.md)在生成前重新安装项目的依赖项。

以下是依赖包还原的原因：

1. 分布式版本控制系统（如 Git）包括存储库中每个文件每个版本的完整副本。 频繁更新的二进制文件会造成大量膨胀并延长克隆存储库所需的时间。
1. 当存储库中包含包时，开发人员负责将引用直接添加到磁盘上的包内容中，而不是通过 NuGet 引用包（可导致项目中的硬编码路径名）。
1. 清理任何未使用包文件夹的解决方案会变得更困难，因为需要确保不删除仍在使用的任何包文件夹。
1. 通过省略包，可以在代码和所依赖的其他包之间维护清晰的所有权边界。 许多 NuGet 包已在其自己的源代码管理存储库中进行了维护。

尽管包还原是 NuGet 的默认行为，但省略源代码管理中的包&mdash;即项目中的 `packages` 文件夹&mdash;仍需进行一些手动操作，详情请见本文。

## <a name="omitting-packages-with-git"></a>使用 Git 省略包

使用 [.gitignore 文件](https://git-scm.com/docs/gitignore)忽略 NuGet 包 (`.nupkg`)、`packages` 文件夹、`project.assets.json` 及其他内容。 有关参考，请参阅 [Visual Studio 项目的示例 `.gitignore`](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)：

以下是 `.gitignore` 文件的重要部分：

```gitignore
# Ignore NuGet Packages
*.nupkg

# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*

# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/

# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config

# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json (NuGet v3); project.assets.json is used in conjunction with the PackageReference
# format (NuGet v4 and .NET Core).
project.lock.json
project.assets.json
```

## <a name="omitting-packages-with-team-foundation-version-control"></a>使用 Team Foundation 版本控制省略包

> [!Note]
> 向源代码管理添加项目之前，请尽量按照这些说明进行操作。 否则，请手动删除存储库中的 `packages` 文件夹并签入该更改，然后才能继续。

要使用 TFVC 为选定的文件禁用源代码管理集成，请执行以下操作：

1. 在解决方案文件夹（`.sln` 文件所在的位置）中创建名为 `.nuget` 的文件夹。
    - 提示：对于 Windows，若要在 Windows 资源管理器中创建此文件夹，请使用具有尾随点的名称 `.nuget.` 。

1. 在该文件夹中，创建名为 `NuGet.Config` 的文件，将其打开进行编辑。

1. 至少添加以下文本，其中 [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) 设置指示 Visual Studio 跳过 `packages` 文件夹中的所有内容：

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. 如果使用的是 TFS 2010 或更早版本，请掩蔽工作区映射中的 `packages` 文件夹。

1. 对于 TFS 2012 或更高版本/Visual Studio Team Services，按照[将文件添加到服务器](/vsts/tfvc/add-files-server?view=vsts#tfignore&preserve-view=true)中所述操作来创建 `.tfignore` 文件。 在该文件中，包括以下内容以显式忽略对存储库级别上的 `\packages` 文件夹和其他几个中间文件的修改。 （可以使用具有尾随点的 `.tfignore.` 名称在 Windows 资源管理器中创建文件，但可能需要首先禁用“隐藏已知文件扩展名”选项。）：

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. 向源代码管理添加 `NuGet.Config` 和 `.tfignore`，并签入更改。
