---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860585"
---
使用 [restore](../../reference/cli-reference/cli-ref-restore.md) 命令，该命令可下载并安装“包”文件夹中缺少的所有包  。

对于迁移到 PackageReference 的项目，请使用 [msbuild -t:restore](../package-restore.md#restore-using-msbuild) 还原程序包。

`restore` 仅将包添加到磁盘，但不会更改项目的依赖项。 要还原项目依赖项，请修改 `packages.config`，然后使用 `restore` 命令。

与其他 `nuget.exe` CLI 命令一样，先打开命令行并切换到包含项目文件的目录。

使用 `restore` 还原包：

```cli
nuget restore MySolution.sln
```