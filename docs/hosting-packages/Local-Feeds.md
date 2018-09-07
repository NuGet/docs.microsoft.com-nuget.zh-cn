---
title: 设置本地 NuGet 源
description: 如何在本地网络上使用文件夹创建 NuGet 包的本地源
author: karann-msft
ms.author: karann
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 91c072c8895ab4267c64fd04deae010ae5af4d37
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545447"
---
# <a name="local-feeds"></a>本地源

本地 NuGet 包源只是本地网络（甚至自己的计算机）上放置包的分层文件夹结构。 然后，这些源可在使用 CLI、包管理器 UI 和包管理器控制台的所有其他 NuGet 操作中用作包源。

若要启用源，请使用[包管理器 UI](../tools/package-manager-ui.md#package-sources) 或 [`nuget sources`](../tools/cli-ref-sources.md) 命令将其路径名（如 `\\myserver\packages`）添加到源列表中。

> [!Note]
> NuGet 3.3+ 中支持分层文件夹结构。 较旧版本的 NuGet 仅使用包含包的一个文件夹，其性能远低于层次结构。

## <a name="initializing-and-maintaining-hierarchical-folders"></a>初始化和维护分层文件夹

分层版本控制的文件夹树具有以下常规结构：

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

当使用 [`nuget add`](../tools/cli-ref-add.md) 命令将包复制到源时，NuGet 自动创建此结构：

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

`nuget add` 命令一次仅用于一个包，这在设置具有多个包的源时会造成不便。

在此情况下，请使用 [`nuget init`](../tools/cli-ref-init.md) 命令将文件夹中的所有包复制到源，就像在每个源上单独运行 `nuget add`。 例如，以下命令将所有包从 `c:\packages` 复制到 `\\myserver\packages` 上的分层树中：

```cli
nuget init c:\packages \\myserver\packages
```

与 `add` 命令一样，`init` 为每个包标识符创建文件夹，每个文件夹中包含具有相应包的版本号文件夹。
