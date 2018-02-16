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
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2018
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a><span data-ttu-id="84e78-104">对 Visual Studio 中的包还原错误进行故障排除</span><span class="sxs-lookup"><span data-stu-id="84e78-104">Troubleshooting package restore errors in Visual Studio</span></span>

> [!Note]
> <span data-ttu-id="84e78-105">本页着重介绍在 Visual Studio 中还原包时遇到的常见错误以及相应的解决步骤。</span><span class="sxs-lookup"><span data-stu-id="84e78-105">This page focuses on common errors when restoring packages in Visual Studio and steps to resolve them.</span></span> <span data-ttu-id="84e78-106">若要了解如何还原包，请参阅[包还原](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)。</span><span class="sxs-lookup"><span data-stu-id="84e78-106">For how-to restore packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="84e78-107">默认情况下，在 Visual Studio 中生成项目时，会自动还原项目中引用的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="84e78-107">By default, building a project in Visual Studio automatically restores NuGet packages referenced in the project.</span></span> <span data-ttu-id="84e78-108">但是，如果在“工具”>“选项”>“NuGet 包管理器”>“包还原”设置中禁用了包还原，且计算机上没有所需的包，则生成将失败。</span><span class="sxs-lookup"><span data-stu-id="84e78-108">However, builds will fail if package restore is disabled in the **Tools > Options > NuGet Package Manager > Package Restore** settings and the necessary packages are not available on your computer.</span></span> <span data-ttu-id="84e78-109">在这些情况下，可能出现下列错误：</span><span class="sxs-lookup"><span data-stu-id="84e78-109">In these cases you may see the following errors:</span></span>

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

<span data-ttu-id="84e78-110">若要启用包还原，请打开“工具”>“选项”>“NuGet 包管理器”，选中“允许 NuGet 下载缺少的包”和“在 Visual Studio 中生成期间自动检查缺少的包”选项：</span><span class="sxs-lookup"><span data-stu-id="84e78-110">To enable package restore, open **Tools > Options > NuGet Package Manager** and select the options for **Allow NuGet to download missing packages** and **Automatically check for missing packages during build in Visual Studio**:</span></span>

![在“工具”/“选项”中启用 NuGet 包还原](../consume-packages/media/restore-01-autorestoreoptions.png)
