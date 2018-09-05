---
title: NuGet CLI 验证命令
description: 引用用于 nuget.exe 验证命令
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545208"
---
# <a name="verify-command-nuget-cli"></a>verify 命令 (NuGet CLI)

**适用于：** 打包消耗&bullet;**支持的版本：** 4.6 +

验证包。

在 Mono 下或在非 Windows 平台上的.NET Core 中尚不支持签名的包的验证。

## <a name="usage"></a>用法

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

其中`<package(s)>`是一个或多个`.nupkg`文件。

## <a name="nuget-verify--all"></a>nuget-全部验证

指定可能的所有验证后，应执行包。

## <a name="nuget-verify--signatures"></a>nuget 验证的签名

指定应执行包签名验证。

## <a name="options-for-verify--signatures"></a>"验证-签名"选项

| 选项 | 描述 |
| --- | --- |
| CertificateFingerprint | 指定一个或多个 SHA-256 证书指纹的证书 (s) 必须使用签名的签名的包。 SHA-256 证书指纹是证书的 SHA-256 哈希。 多个输入应为以分号分隔。 |

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。|
| ForceEnglishOutput | 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| 详细级别 | 指定的输出中显示的详细信息：*正常*，*静默*，*详细*。 |

## <a name="examples"></a>示例

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```