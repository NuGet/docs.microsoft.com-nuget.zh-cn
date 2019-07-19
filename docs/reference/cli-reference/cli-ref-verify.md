---
title: NuGet CLI 验证命令
description: Nuget.exe 验证命令的参考
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327494"
---
# <a name="verify-command-nuget-cli"></a>verify 命令 (NuGet CLI)

**适用于:** 包&bullet;使用**受支持的版本:** 4.6 +

验证包。

在 .NET Core、Mono 或非 Windows 平台上, 尚不支持验证已签名的包。

## <a name="usage"></a>用法

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

其中`<package(s)>` , 是一个或`.nupkg`多个文件。

## <a name="nuget-verify--all"></a>nuget 验证-全部

指定应在包上执行所有验证。

## <a name="nuget-verify--signatures"></a>nuget 验证-签名

指定应执行的包签名验证。

## <a name="options-for-verify--signatures"></a>用于 "验证-签名" 的选项

| 选项 | 描述 |
| --- | --- |
| CertificateFingerprint | 指定一个或多个证书的一个或多256个证书指纹, 证书必须用来签名包。 证书 256 SHA-1 指纹是证书的 SHA-256 哈希。 多个输入应以分号分隔。 |

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。|
| ForceEnglishOutput | 使用固定的、基于英语的区域性强制执行 nuget.exe。 |
| Help | 显示命令的帮助信息。 |
| Verbosity | 指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。 |

## <a name="examples"></a>示例

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```