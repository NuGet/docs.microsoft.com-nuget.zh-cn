---
title: "对 Visual Studio 中的 NuGet 包还原进行故障排除 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: b70326a0-5bfc-4b7c-881d-7a7d5ebeeed5
description: "介绍 Visual Studio 中常见的 NuGet 还原错误以及相应的故障排除方法。"
keywords: "NuGet 包还原, 还原包, 故障排除, 故障排除"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c23a9ed2b7cffbf904018a089ccde000adaa517f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a>对 Visual Studio 中的包还原错误进行故障排除

> [!Note]
> 本页着重介绍在 Visual Studio 中还原包时遇到的常见错误以及相应的解决步骤。 若要了解如何还原包，请参阅[包还原](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore)。

默认情况下，在 Visual Studio 中生成项目时，会自动还原项目中引用的 NuGet 包。 但是，如果在“工具”>“选项”>“NuGet 包管理器”>“包还原”设置中禁用了包还原，且计算机上没有所需的包，则生成将失败。 在这些情况下，可能出现下列错误：

```
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

```
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name} 
```

若要启用包还原，请打开“工具”>“选项”>“NuGet 包管理器”，选中“允许 NuGet 下载缺少的包”和“在 Visual Studio 中生成期间自动检查缺少的包”选项：

![在“工具”/“选项”中启用 NuGet 包还原](../Consume-Packages/media/restore-01-autorestoreoptions.png)

