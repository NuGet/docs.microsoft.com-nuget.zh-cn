---
title: NuGet CLI 受信任-签署者命令
description: nuget.exe 受信任的签名者命令的参考
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9e25f439617a76d30880bea3c10a5d063e681a41
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238148"
---
# <a name="trusted-signers-command-nuget-cli"></a> (NuGet CLI 的受信任的签名者命令) 

**适用于：** 包使用 &bullet; **受支持的版本：** 4.9.1 +

获取或设置 NuGet 配置的受信任签署者。 有关其他用法，请参阅 [常见 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)。 有关 nuget.config 架构的外观的详细信息，请参阅 [NuGet 配置文件参考](../nuget-config-file.md)。

## <a name="usage"></a>使用情况

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

如果 `list|add|remove|sync` 未指定任何，则该命令将默认为 `list` 。

## <a name="nuget-trusted-signers-list"></a>nuget 可信-签署者列表

列出配置中的所有受信任签署者。 此选项将包括每个签名者)  (具有指纹和指纹算法的所有证书。 如果证书前面有一个 `[U]` ，则表示证书项已 `allowUntrustedRoot` 设置为 `true` 。

下面是此命令的示例输出：

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>nuget 可信-签署者添加 [选项]

向配置添加具有给定名称的受信任的签名者。此选项具有不同的手势来添加受信任的作者或存储库。

## <a name="options-for-add-based-on-a-package"></a>基于包的 "添加" 选项

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

其中 `<package(s)>` ，是一个或多个 `.nupkg` 文件。

- **`-Author`**

  指定应信任包 () 的作者签名。

- **`-AllowUntrustedRoot`**

  指定是否允许受信任的签名者的证书链接到不受信任的根。

- **`-Owners`**

  以分号分隔的受信任所有者列表，进一步限制了存储库的信任。 仅在使用选项时有效 `-Repository` 。

- **`-Repository`**

  指定应信任包 (s) 的存储库签名或副署。

`-Author`不支持同时提供和 `-Repository` 。

## <a name="options-for-add-based-on-a-service-index"></a>基于服务索引添加的选项

```cli
nuget trusted-signers add -Name <name> [options]
```

_注意_ ：此选项将只添加受信任的存储库。 

- **`-AllowUntrustedRoot`**

  指定是否允许受信任的签名者的证书链接到不受信任的根。

- **`-Owners`**

  以分号分隔的受信任所有者列表，进一步限制了存储库的信任。

- **`-ServiceIndex`**

  指定要信任的存储库的 V3 服务索引。 此存储库必须支持存储库签名资源。 如果未提供，则该命令将查找具有相同的包源 `-Name` ，并从中获取服务索引。

## <a name="options-for-add-based-on-the-certificate-information"></a>基于证书信息添加的选项

```cli
nuget trusted-signers add -Name <name> [options]
```

_注意_ ：如果已存在具有给定名称的受信任的签名者，则会将证书项目添加到该签名者。 否则，将创建一个受信任的作者，其中包含来自给定证书信息的证书项目。


- **`-AllowUntrustedRoot`**

  指定是否允许受信任的签名者的证书链接到不受信任的根。

- **`-CertificateFingerprint`**

  指定证书的证书指纹，必须使用该证书对签名的包进行签名。 证书指纹是证书的哈希。 用于计算此哈希的哈希算法应在选项中指定 `FingerprintAlgorithm` 。

- **`-FingerprintAlgorithm`**

  指定用于计算证书指纹的哈希算法。 默认为 `SHA256`。 支持的值为 `SHA256` 、 `SHA384` 和 `SHA512` 。

## <a name="nuget-trusted-signers-remove--name-name"></a>nuget 可信-签名者删除名称 \<name\>

删除任何与给定名称匹配的受信任签署者。

## <a name="nuget-trusted-signers-sync--name-name"></a>nuget 可信-签署者同步名称 \<name\>

请求当前受信任的存储库中使用的最新证书列表，以更新受信任的签名者中的现有证书列表。

_注意_ ：此笔势将删除当前的证书列表，并将其替换为存储库中的最新列表。

## <a name="options"></a>选项

- **`-ConfigFile`**

  要应用的 NuGet 配置文件。 如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-ForceEnglishOutput`**

  使用固定的、基于英语的区域性强制运行 nuget.exe。

- **`-?|-help`**

  显示命令的帮助信息。

- **`-Name`**

  受信任的签名者的名称。

- **`-NonInteractive`**

  禁止提示用户输入或确认。

- **`-Verbosity [normal|quiet|detailed]`**

  指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。


## <a name="examples"></a>示例

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
