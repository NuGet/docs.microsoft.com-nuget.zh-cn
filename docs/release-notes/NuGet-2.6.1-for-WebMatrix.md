---
title: NuGet 2.6.1 for WebMatrix 发行说明
description: 发行说明适用于 NuGet 2.6.1 的 WebMatrix 包括已知的问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550312"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 for WebMatrix 发行说明

[NuGet 2.6 发行说明](../release-notes/nuget-2.6.md) | [NuGet 2.7 发行说明](../release-notes/nuget-2.7.md)

NuGet 团队于 2014 年 3 月 26 日发布的 WebMatrix 的更新的 NuGet 包管理器扩展。  可以从安装此更新[WebMatrix 扩展库](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery)使用以下步骤：

1. 打开 WebMatrix 3
1. 单击主页功能区中的扩展图标
1. 选择更新选项卡
1. 单击此项可更新到 2.6.1 的 NuGet 包管理器
1. 关闭并重新启动 WebMatrix 3

## <a name="notable-changes"></a>值得注意的更改

最大的问题用户此扩展更新解决两个已经遇到过 WebMatrix 中的使用 NuGet 包。  第一种是 NuGet 架构版本错误和第二个是指向零字节 Dll 错误`bin`文件夹。

### <a name="nuget-schema-version-error"></a>NuGet 架构版本错误

WebMatrix 3 已自发布以来，到适用于 NuGet 包需要新的架构版本的 NuGet 已引入新功能。  在尝试管理 NuGet 程序包在您的网站，这些新的包可能会导致你在 WebMatrix 中看到的错误。

![出现了错误。 架构版本不兼容。 请升级到最新版本的 NuGet。](./media/NuGet-2.8/webmatrix-schema-version.png)

此最新版本提供了与最新的 NuGet 包，防止发生此错误的兼容性。 现在可以在 WebMatrix 中安装新版本的包包括 Microsoft.AspNet.WebPages。  这些包的一些已使用的 NuGet 功能，如[XDT 配置转换](../release-notes/nuget-2.6.md#xdt)，这不受支持的在 WebMatrix 中到目前为止。

### <a name="zero-byte-dlls-in-bin-folder"></a>Bin 文件夹中的零字节 Dll

某些用户报告的后安装 NuGet 中的包中包含 Dll 复制到 bin 的 WebMatrix Dll 显示`bin`0 字节的文件的文件夹。  这将在运行时中断该应用程序。

[此问题](https://nuget.codeplex.com/workitem/4060)现已修复。

## <a name="other-recent-improvements"></a>其他最新的改进

NuGet 包管理器 2.8 for Visual Studio 发布时，我们还为 WebMatrix 发布 NuGet 包管理器 2.5.0。  虽然这中所述[NuGet 2.8 发行说明](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)，我们没有提到特定的新功能引入了该更新。

### <a name="update-all"></a>全部更新

现在，您可以更新所有在一个步骤中的 web 站点的包 ！  在 WebMatrix 中打开 NuGet 扩展时，所有程序包的列表上看到库、 安装，和具有可用的更新。  以前，必须单独更新每个包，但现在没有显示在更新选项卡的有用"全部更新"按钮。

![单击全部更新，以使用可用的更新来更新所有包](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>覆盖现有文件

安装时包含您的网站中已存在的文件的包，NuGet 已始终只以无提示方式忽略这些文件 （保留不动现有文件）。  这可能导致包已安装，或当事实上没有正确更新的印象。  NuGet 现在将提示输入覆盖文件。

![文件冲突解决方法](./media/NuGet-2.8/webmatrix-overwrite-file.png)
