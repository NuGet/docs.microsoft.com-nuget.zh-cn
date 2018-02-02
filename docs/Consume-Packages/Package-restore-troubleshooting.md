---
title: "对 Visual Studio 中的 NuGet 包还原进行故障排除 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "介绍 Visual Studio 中常见的 NuGet 还原错误以及相应的故障排除方法。"
keywords: "NuGet 包还原, 还原包, 故障排除, 故障排除"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c0993e2585452e3c64da28d14bb1bbe1bea27768
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a>对 Visual Studio 中的包还原错误进行故障排除

> [!Note]
> 本页着重介绍在 Visual Studio 中还原包时遇到的常见错误以及相应的解决步骤。 若要了解如何还原包，请参阅[包还原](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)。

默认情况下，在 Visual Studio 中生成项目时，会自动还原项目中引用的 NuGet 包。 但是，如果在“工具”>“选项”>“NuGet 包管理器”>“包还原”设置中禁用了包还原，且计算机上没有所需的包，则生成将失败。 在这些情况下，可能出现下列错误：

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name} 
```

若要启用包还原，请打开“工具”>“选项”>“NuGet 包管理器”，选中“允许 NuGet 下载缺少的包”和“在 Visual Studio 中生成期间自动检查缺少的包”选项：

![在“工具”/“选项”中启用 NuGet 包还原](../consume-packages/media/restore-01-autorestoreoptions.png)
