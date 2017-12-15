---
title: "NuGet CLI 镜像命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 190d7010-172e-44b8-8a32-94a2a63be4f3
description: "Nuget.exe 镜像命令参考"
keywords: "nuget 镜像引用，镜像命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67daa1aa278b42b7974c562ba4097a525e7bb105
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="mirror-command-nuget-cli"></a>镜像命令 (NuGet CLI)

**适用于：**包发布&bullet;**受支持的版本：** 3.2 + 中不推荐使用

镜像包和到目标存储库及其依赖项从指定的源存储库。

> [!NOTE]
> 若要在 3.2 之前启用 NuGet 版本为此命令，请转到[https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)，选择最新稳定版本，下载`NuGet.ServerExtensions.dll`和`Nuget-Signed.exe`到你的本地磁盘和重命名`Nuget-Signed.exe`到`nuget.exe`.

## <a name="usage"></a>用法

```
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

其中`<packageID>`是包镜像，或`<configFilePath>`标识`packages.config`列出要镜像的包文件。

`<listUrlTarget>`指定源存储库，和`<publishUrlTarget>`指定目标存储库。

如果你的目标存储库位于`https://machine/repo`运行[NuGet.Server](../hosting-packages/NuGet-Server.md)，将列表和推送 url`https://machine/repo/nuget`和`https://machine/repo/api/v2/package`分别。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ApiKey | 目标存储库的 API 密钥。 如果不存在，请在指定某一*%AppData%\NuGet\NuGet.Config*使用。 |
| 帮助 | 显示的帮助命令的信息。 |
| NoCache | 防止 NuGet 使用从本地计算机缓存的包。 |
| Noop | 记录操作即告完成的内容，但不会执行操作;假定推送操作的成功。 |
| 预发行版 | 在镜像的操作中包含预发行程序包。 |
| 源 | 要镜像的包源的列表。 如果不指定任何源，则在定义*%AppData%\NuGet\NuGet.Config*使用，如果未指定任何默认为 nuget.org。 |
| 超时 | 指定超时，以秒为单位，以便将推送到服务器。 默认值为 300 秒 （5 分钟）。 |
| 版本 | 要安装的包的版本。 如果未指定，正在镜像的最新版本。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
