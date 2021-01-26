---
title: NuGet 2.6.1 for WebMatrix 发行说明
description: NuGet 2.6.1 for WebMatrix 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780415"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 for WebMatrix 发行说明

[NuGet 2.6 发行说明](../release-notes/nuget-2.6.md)  | [NuGet 2.7 发行说明](../release-notes/nuget-2.7.md)

NuGet 团队在2014年3月26日发布了更新的适用于 WebMatrix 的 NuGet 包管理器扩展。  可以使用以下步骤从 [WebMatrix 扩展库](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) 安装此更新：

1. 打开 WebMatrix 3
1. 单击 "主页" 功能区中的扩展图标
1. 选择 "更新" 选项卡
1. 单击以将 NuGet 包管理器更新到2.6。1
1. 关闭并重新启动 WebMatrix 3

## <a name="notable-changes"></a>显著更改

此扩展更新解决了用户在 WebMatrix 中使用 NuGet 包的两个最大问题。  第一种是 NuGet 架构版本错误，第二种是导致文件夹中的零字节 Dll 出现错误 `bin` 。

### <a name="nuget-schema-version-error"></a>NuGet 架构版本错误

由于 WebMatrix 3 已发布，因此 NuGet 中引入了新功能，需要 NuGet 包的新架构版本。  尝试在网站中管理 NuGet 包时，这些新包可能会导致在 WebMatrix 中看到的错误。

![出现了错误。 架构版本不兼容。 请将 NuGet 升级到最新版本。](./media/NuGet-2.8/webmatrix-schema-version.png)

此最新版本提供了与最新 NuGet 包的兼容性，从而防止发生此错误。 新版本的包（包括 Microsoft）现在可以安装在 WebMatrix 中。  其中一些包使用的是 NuGet 功能，如 [XDT config 转换](../release-notes/nuget-2.6.md#xdt)，这在 WebMatrix 中目前不受支持。

### <a name="zero-byte-dlls-in-bin-folder"></a>Zero-Byte bin 文件夹中的 Dll

某些用户报告在 WebMatrix 中安装了包含复制到 bin 的 Dll 的 NuGet 包后，Dll 会在文件夹中显示 `bin` 为0字节文件。  这会在运行时中断应用程序。

[此问题](https://nuget.codeplex.com/workitem/4060) 现已解决。

## <a name="other-recent-improvements"></a>其他最新改进

发布适用于 Visual Studio 的 NuGet 包管理器2.8 时，我们还发布了适用于 WebMatrix 的 NuGet 包管理器2.5.0。  虽然 [NuGet 2.8 发行说明](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)中提到了这一点，但我们并未提到更新引入的特定新功能。

### <a name="update-all"></a>全部更新

现在，你可以在一个步骤中更新网站的所有包！  当你在 WebMatrix 中打开 NuGet 扩展时，会看到库中所有包的列表、已安装的包以及具有可用更新的包的列表。  以前，每个包都必须单独更新，但现在 "更新" 选项卡上显示了一个有用的 "全部更新" 按钮。

![单击 "全部更新" 以使用可用更新更新所有包](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>覆盖现有文件

当安装的包包含您的网站中已存在的文件时，NuGet 始终只是以无提示方式忽略这些文件 (仅) 保留现有文件。  这可能会导致程序包安装或更新正确，但事实上它并不是这样。  NuGet 现在将提示文件被覆盖。

![文件冲突解决](./media/NuGet-2.8/webmatrix-overwrite-file.png)
