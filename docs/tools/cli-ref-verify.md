---
title: NuGet CLI 验证命令
description: 参考 nuget.exe 验证命令
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c80334104f7d8b2ccbf16ea2c11dc37b39408eeb
ms.sourcegitcommit: c8485dc61469511485367d2067b97d6f74b49f6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
ms.locfileid: "34462847"
---
# <a name="verify-command-nuget-cli"></a>verify 命令 (NuGet CLI)

**适用于：** 打包消耗&bullet;**受支持的版本：** 4.6 +

验证包。

在.NET 核心，Mono、 下或在非 Windows 平台上尚不支持验证的已签名的软件包。

## <a name="usage"></a>用法

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

其中`<package(s)>`一个或多个`.nupkg`文件。

## <a name="nuget-verify--all"></a>nuget 验证-所有

指定所有验证可能，应都执行的程序包。

## <a name="nuget-verify--signatures"></a>nuget 验证的签名

指定应执行包签名验证。

## <a name="options-for-verify--signatures"></a>"验证的签名"的选项

| 选项 | 描述 |
| --- | --- |
| CertificateFingerprint | 指定一个或多个 sha-256 证书指纹的证书 (s) 必须使用签名的已签名的软件包。 Sha-256 证书指纹是该证书的 sha-256 哈希。 多个输入应为以分号分隔。 |

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。|
| ForceEnglishOutput | 强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。 |

## <a name="examples"></a>示例

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```