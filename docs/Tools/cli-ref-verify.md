---
title: "NuGet CLI 验证命令 |Microsoft 文档"
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "参考 nuget.exe 验证命令"
keywords: "nuget 验证引用，验证命令"
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 096c79670267d9b602dd6ad30640e832441c31c5
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="verify-command-nuget-cli"></a>验证命令 (NuGet CLI)

**适用于：**打包消耗&bullet;**受支持的版本：** 4.6 +

验证包。

## <a name="usage"></a>用法

```cli
nuget verify <package(s)> [options]
```

其中`<package(s)>`一个或多个`.nupkg`文件。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| 全部 | 指定所有验证可能，应都执行的程序包。 |
| CertificateFingerprint | 指定一个或多个 sha-256 证书指纹的证书 (s) 必须使用签名的已签名的软件包。 Sha-256 证书指纹是该证书的 sha-256 哈希。 多个输入应为以分号分隔。 |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。|
| ForceEnglishOutput | 强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 签名 | 指定应执行包签名验证。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。 |

## <a name="examples"></a>示例

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```