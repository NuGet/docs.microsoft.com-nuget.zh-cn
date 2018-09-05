---
title: NuGet CLI 镜像命令
description: Nuget.exe 镜像命令参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550201"
---
# <a name="mirror-command-nuget-cli"></a>mirror 命令 (NuGet CLI)

**适用于：** 包发布&bullet;**支持的版本：** 3.2 + 中不推荐使用

镜像包并从指定的源存储库到目标存储库及其依赖项。

> [!NOTE]
> 若要启用此命令的 NuGet 版本 3.2 之前，请转到[ https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)中，选择最新稳定版本，下载`NuGet.ServerExtensions.dll`并`Nuget-Signed.exe`到你的本地磁盘和重命名`Nuget-Signed.exe`到`nuget.exe`。

## <a name="usage"></a>用法

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

其中`<packageID>`是包以镜像，或`<configFilePath>`标识`packages.config`文件，其中列出要镜像的包。

`<listUrlTarget>`指定的源存储库和`<publishUrlTarget>`指定目标存储库。

如果目标存储库位于`https://machine/repo`运行[NuGet.Server](../hosting-packages/nuget-server.md)，将列表和推送 url`https://machine/repo/nuget`和`https://machine/repo/api/v2/package`分别。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ApiKey | 目标存储库 API 密钥。 如果不存在，请在配置文件中指定使用 (`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux))。 |
| 帮助 | 显示的帮助命令的信息。 |
| NoCache | 阻止 NuGet 使用缓存的包。 请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 |
| Noop | 记录的内容就执行此操作，但不会执行操作;假定对于推送操作成功。 |
| 预发行版 | 在镜像操作中包括预发行包。 |
| 源 | 包源进行镜像的列表。 如果指定了不到源，在中定义的配置文件 （请参阅上面的 ApiKey） 使用，如果未指定任何默认设置为 nuget.org。 |
| 超时 | 指定的超时，以秒为单位，以便将推送到服务器。 默认值为 300 秒 （5 分钟）。 |
| 版本 | 要安装的包的版本。 如果未指定，镜像最新版本。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
