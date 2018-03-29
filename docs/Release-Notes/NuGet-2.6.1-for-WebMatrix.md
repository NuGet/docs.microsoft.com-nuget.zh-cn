---
title: NuGet 2.6.1 for WebMatrix 发行说明 |Microsoft 文档
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet 2.6.1 为 WebMatrix 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs 的发行说明。
keywords: NuGet 2.6.1 WebMatrix 发行说明、 bug 修复、 已知的问题，添加了一些功能，DCRs
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 505054e42234f313bade496315e94ad485050dbb
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 for WebMatrix 发行说明

[NuGet 2.6 发行说明](../release-notes/nuget-2.6.md) | [NuGet 2.7 发行说明](../release-notes/nuget-2.7.md)

NuGet 团队在 2014 年 3 月 26 日为 WebMatrix 中发布更新的 NuGet 包管理器扩展。  此更新可以从安装[WebMatrix 扩展库](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery)使用以下步骤：

1. 打开 WebMatrix 3
1. 单击主页功能区中的扩展图标
1. 选择更新选项卡
1. 单击以更新到 2.6.1 的 NuGet 包管理器
1. 关闭并重新启动 WebMatrix 3

## <a name="notable-changes"></a>重大更改

此扩展更新两个用户的地址的最大问题做出两难 WebMatrix 内的使用 NuGet 包。  第一个 NuGet 架构版本错误，并且第二种是通向零字节 Dll bug`bin`文件夹。

### <a name="nuget-schema-version-error"></a>NuGet 架构版本错误

自发布 WebMatrix 3 后, 到 NuGet 需要新的架构版本为 NuGet 包已引入新功能。  在尝试管理 NuGet 程序包在您的网站，这些新的包可能导致你在 WebMatrix 中看到的错误。

![出现了错误。 架构版本不兼容。 请升级到最新版本的 NuGet。](./media/NuGet-2.8/webmatrix-schema-version.png)

此最新版本提供了与最新的 NuGet 包，阻止发生此错误的兼容性。 现在可以在 WebMatrix 中安装新版本的包包括 Microsoft.AspNet.WebPages。  这些包的某些已使用 NuGet 功能，如[XDT 配置转换](../release-notes/nuget-2.6.md#xdt)，它不支持在 WebMatrix 中到目前为止。

### <a name="zero-byte-dlls-in-bin-folder"></a>Bin 文件夹中的零字节 Dll

某些用户报告，之后安装 NuGet 包中包含要装箱，将被复制的 Dll 的 WebMatrix Dll 显示`bin`0 字节的文件的文件夹。  这在运行时将中断应用程序。

[此问题](https://nuget.codeplex.com/workitem/4060)现已修复。

## <a name="other-recent-improvements"></a>其他最新改进

当 NuGet 包管理器 2.8 已发布 for Visual Studio 中时，我们还为 WebMatrix 发布 NuGet 包管理器 2.5.0。  虽然这中所述[NuGet 2.8 发行说明](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)，我们没有提到特定于新功能引入该更新。

### <a name="update-all"></a>更新所有

现在，您可以更新的所有 web 站点的包在一个步骤 ！  当你在 WebMatrix 中打开 NuGet 扩展时，你将看到上的库、 安装，然后使用提供的更新的所有程序包的列表。  以前，每个包需要单独更新，但现在没有显示在更新选项卡的有用"全部更新"按钮。

![单击所有更新，以使用可用的更新来更新所有包](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>覆盖现有文件

安装程序包包含已在您的网站中存在的文件时，NuGet 具有始终只以无提示方式忽略 （保留现有的文件不动） 这些文件。  这可能导致这样的印象包已安装，或当实际上它未正确更新。  现在，NuGet 将提示输入覆盖文件。

![文件冲突解决](./media/NuGet-2.8/webmatrix-overwrite-file.png)
