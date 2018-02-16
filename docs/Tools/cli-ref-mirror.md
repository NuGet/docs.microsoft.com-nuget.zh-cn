---
title: "NuGet CLI 镜像命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 镜像命令参考"
keywords: "nuget 镜像引用，镜像命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 80b8f9a3b74030ffd3f1c7b784204d98be67d684
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2018
---
# <a name="mirror-command-nuget-cli"></a>镜像命令 (NuGet CLI)

**适用于：**包发布&bullet;**受支持的版本：** 3.2 + 中不推荐使用

镜像包和到目标存储库及其依赖项从指定的源存储库。

> [!NOTE]
> 若要在 3.2 之前启用 NuGet 版本为此命令，请转到[https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)，选择最新稳定版本，下载`NuGet.ServerExtensions.dll`和`Nuget-Signed.exe`到你的本地磁盘和重命名`Nuget-Signed.exe`到`nuget.exe`.

## <a name="usage"></a>用法

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

其中`<packageID>`是包镜像，或`<configFilePath>`标识`packages.config`列出要镜像的包文件。

`<listUrlTarget>`指定源存储库，和`<publishUrlTarget>`指定目标存储库。

如果你的目标存储库位于`https://machine/repo`运行[NuGet.Server](../hosting-packages/nuget-server.md)，将列表和推送 url`https://machine/repo/nuget`和`https://machine/repo/api/v2/package`分别。

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

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
