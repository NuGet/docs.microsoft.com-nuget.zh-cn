---
title: NuGet CLI 验证命令
description: nuget.exe verify 命令的参考
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7ce08f11195437e94bfe69883ff525e9ad3a73f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238135"
---
# <a name="verify-command-nuget-cli"></a> (NuGet CLI 验证命令) 

**适用于：** 包使用 &bullet; **受支持的版本：** 4.6 +

验证包。

Mono 不支持验证已签名的包。

## <a name="usage"></a>使用情况

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

其中 `<package(s)>` ，是一个或多个 `.nupkg` 文件。

## <a name="nuget-verify--all"></a>nuget 验证-全部

指定应对包执行的所有可能的验证。

## <a name="nuget-verify--signatures"></a>nuget 验证-签名

指定应执行的包签名验证。

## <a name="options-for-verify--signatures"></a>用于 "验证-签名" 的选项

- **`-CertificateFingerprint`**

  指定一个或多256个证书证书指纹 (s，) 必须用来签署哪些签名包。 证书 256 SHA-1 指纹是证书的 SHA-256 哈希。 多个输入应以分号分隔。

## <a name="options"></a>选项

- **`-ConfigFile`**

  要应用的 NuGet 配置文件。 如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-ForceEnglishOutput`**

  使用固定的、基于英语的区域性强制运行 nuget.exe。

- **`-?|-help`**

  显示命令的帮助信息。

- **`-NonInteractive`**

  禁止提示用户输入或确认。

- **`-Verbosity [normal|quiet|detailed]`**

  指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。

## <a name="examples"></a>示例

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```