---
title: NuGet CLI 镜像命令
description: Nuget.exe 镜像命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 81866172bfbf55c42ee96c213c0117f1f986235c
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959712"
---
# <a name="mirror-command-nuget-cli"></a>mirror 命令 (NuGet CLI)

**适用于:** 包发布&bullet; **支持的版本:** 3.2 + 中弃用

将包及其依赖项从指定的源存储库镜像到目标存储库。

> [!NOTE]
> ServerExtensions 和 NuGet-Signed 以前在 NuGet 2.x 中支持此命令 (通过将 NuGet-Signed 重命名为 nuget.exe) 已不再可供下载。 若要使用与此类似的命令, 请尝试[NuGetMirror](https://www.nuget.org/packages/NuGetMirror/)。

## <a name="usage"></a>用法

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

其中`<packageID>` , 是要镜像的包, `<configFilePath>`或标识`packages.config`列出要镜像的包的文件。

指定源存储库, 并`<publishUrlTarget>`指定目标存储库。 `<listUrlTarget>`

如果目标存储库在运行`https://machine/repo` [NuGet. 服务器](../../hosting-packages/nuget-server.md)的上, 则列表和推送 url 将分别为`https://machine/repo/nuget`和`https://machine/repo/api/v2/package`。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ApiKey | 目标存储库的 API 密钥。 如果不存在, 则使用配置文件中指定的一个 (`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config` (Mac/Linux))。 |
| Help | 显示命令的帮助信息。 |
| NoCache | 阻止 NuGet 使用缓存的包。 请参阅[管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。 |
| Noop | 记录将执行的操作, 但不执行操作;假定推送操作成功。 |
| 早期 | 在镜像操作中包括预发行程序包。 |
| Source | 要镜像的包源的列表。 如果未指定任何源, 将使用配置文件中定义的源 (请参阅上面的 ApiKey), 如果未指定, 则默认为 nuget.org。 |
| 超时 | 指定推送到服务器的超时值 (以秒为单位)。 默认值为300秒 (5 分钟)。 |
| Version | 要安装的包的版本。 如果未指定, 则将镜像最新版本。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
