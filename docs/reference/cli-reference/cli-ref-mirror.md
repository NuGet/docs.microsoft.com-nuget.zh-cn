---
title: NuGet CLI 镜像命令
description: nuget.exe 镜像命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6ecd5c11383f78fdaeb01090366a8ffe294b4f8b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779167"
---
# <a name="mirror-command-nuget-cli"></a> (NuGet CLI 的镜像命令) 

**适用于：** 包发布 &bullet; **支持的版本：** 3.2 + 中弃用

将包及其依赖项从指定的源存储库镜像到目标存储库。

> [!NOTE]
> NuGet.ServerExtensions.dll 和 NuGet-Signed.exe 以前在 NuGet 2.x (中支持此命令，方法是将 NuGet-Signed.exe 重命名为 nuget.exe) 不再可供下载。 若要使用与此类似的命令，请尝试 [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/)。

## <a name="usage"></a>使用情况

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

其中 `<packageID>` ，是要镜像的包，或 `<configFilePath>` 标识 `packages.config` 列出要镜像的包的文件。

`<listUrlTarget>`指定源存储库，并 `<publishUrlTarget>` 指定目标存储库。

如果目标存储库在 `https://machine/repo` 运行 [NuGet. 服务器](../../hosting-packages/nuget-server.md)的上，则列表和推送 url 将分别为 `https://machine/repo/nuget` 和 `https://machine/repo/api/v2/package` 。

## <a name="options"></a>选项

- **`-ApiKey`**

  目标存储库的 API 密钥。 如果不存在，则使用配置文件中指定的 (`%AppData%\NuGet\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) # A5。

- **`-Help`**

  显示命令的帮助信息。

- **`-NoCache`**

  阻止 NuGet 使用缓存的包。 请参阅 [管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。

- **`-Noop`**

  记录将执行的操作，但不执行操作;假定推送操作成功。

- **`-PreRelease`**

  在镜像操作中包括预发行程序包。

- **`-Source`**

  要镜像的包源的列表。 如果未指定源，则配置文件中定义的 (参阅) 使用上述 ApiKey，如果未指定，则默认为 nuget.org。

- **`-Timeout`**

  指定推送到服务器的超时值（以秒为单位）。 默认值为 300 秒（5 分钟）。

- **`-Version`**

  要安装的包的版本。 如果未指定，则将镜像最新版本。

另请参阅 [环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
