---
title: NuGet CLI 添加命令
description: nuget.exe add 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 89d268946243e8eae07e482db48e809a15260c38
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622897"
---
# <a name="add-command-nuget-cli"></a> (NuGet CLI 添加命令) 

**适用**于：包发布 &bullet; **支持的版本**： 3.3 +

将指定的包添加到 (文件夹或 UNC 路径的非 HTTP 包源中) 在层次结构布局中，其中为包 ID 和版本号创建了文件夹。 例如：

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

针对包源还原或更新时，分层布局提供明显更好的性能。

若要将包中的所有文件展开到目标包源，请使用 `-Expand` 开关。 这通常会导致在目标中出现其他子文件夹，例如 `tools` 和 `lib` 。

## <a name="usage"></a>使用情况

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

其中， `<packagePath>` 是要添加的包的路径名，并指定要将 `<sourcePath>` 包添加到的基于文件夹的包源。 HTTP 源不受支持。

## <a name="options"></a>选项

- **`-ConfigFile`**

  要应用的 NuGet 配置文件。 如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-Expand`**

  将包中的所有文件添加到包源。

- **`-ForceEnglishOutput`**

  * (3.5 +) * 使用固定的、基于英语的区域性强制运行 nuget.exe。
使用固定的、基于英语的区域性强制运行 nuget.exe。

- **`-?|-help`**

  显示命令的帮助信息。

- **`-NonInteractive`**

  禁止提示用户输入或确认。

- **`-src|-Source`**

   指定将向其添加 nupkg 的包源（文件夹或 UNC 共享）。 Http 源不受支持。

- **`-Verbosity [normal|quiet|detailed]`**

  指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。

另请参阅 [环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
