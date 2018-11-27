---
title: 受信任的签名者的 NuGet CLI 命令
description: Nuget.exe 受信任的签名者命令参考
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ffd0cf5d50a2deed16e1722b32e43047bc81df2f
ms.sourcegitcommit: a1846edf70ddb2505d58e536e08e952d870931b0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2018
ms.locfileid: "52303683"
---
# <a name="trusted-signers-command-nuget-cli"></a>受信任的签名者命令 (NuGet CLI)

**适用于：** 打包消耗&bullet;**支持的版本：** 4.9 +

获取或设置 NuGet 配置受信任的签名者。 有关其他用法，请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)。 有关详细信息如何 nuget.config 架构看起来，请参阅[NuGet 配置文件引用](../reference/nuget-config-file.md)。

## <a name="usage"></a>用法

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

如果没有`list|add|remove|sync`指定，则该命令将默认为`list`。

## <a name="nuget-trusted-signers-list"></a>nuget 受信任的签名者列表

列出了在配置中所有受信任的签名者。 此选项将包括所有证书 （具有指纹和指纹算法） 具有每个签名者。 如果证书具有前面`[U]`，则意味着证书条目已`allowUntrustedRoot`设置为`true`。

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

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>nuget 受信任的签名添加 [选项]

将具有给定名称信任的签名添加到配置。此选项具有不同的手势，若要添加受信任的作者或存储库。

## <a name="options-for-add-based-on-a-package"></a>添加基于包的选项

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

其中`<package(s)>`是一个或多个`.nupkg`文件。

| 选项 | 描述 |
| --- | --- |
| 作者 | 指定应受信任的程序包作者签名。 |
| 存储库 | 指定的存储库签名或副署的包应为受信任。 |
| AllowUntrustedRoot | 指定是否应链接到不受信任的根允许受信任的签名者的证书。 |
| Owners | 受信任的所有者来进一步限制的信任存储库的以分号分隔列表。 仅在使用时有效`-Repository`选项。 |

同时提供`-Author`和`-Repository`不支持在同一时间。

## <a name="options-for-add-based-on-a-service-index"></a>添加基于服务索引的选项

```cli
nuget trusted-signers add -Name <name> [options]
```

_请注意_： 此选项将仅添加受信任的存储库。 

| 选项 | 描述 |
| --- | --- |
| ServiceIndex | 指定要为受信任的存储库的 V3 服务索引。 此存储库必须支持存储库签名资源。 如果未提供，该命令将查找具有相同的包源`-Name`并从中获取服务索引。 |
| AllowUntrustedRoot | 指定是否应链接到不受信任的根允许受信任的签名者的证书。 |
| Owners | 受信任的所有者来进一步限制的信任存储库的以分号分隔列表。 |

## <a name="options-for-add-based-on-the-certificate-information"></a>添加根据证书信息的选项

```cli
nuget trusted-signers add -Name <name> [options]
```

_请注意_： 如果已存在具有给定名称信任的签名，会将证书项添加到该签名者。 否则将使用证书项目中创建受信任的作者从给定的证书信息。

| 选项 | 描述 |
| --- | --- |
| CertificateFingerprint | 指定必须使用签名的已签名的包的证书指纹的证书。 证书指纹是证书的哈希。 在指定的哈希算法用于计算此哈希值应为`FingerprintAlgorithm`选项。 |
| FingerprintAlgorithm | 指定用于计算证书指纹的哈希算法。 默认为 `SHA256`。 支持的值为`SHA256`，`SHA384`和 `SHA512` |
| AllowUntrustedRoot | 指定是否应链接到不受信任的根允许受信任的签名者的证书。 |

## <a name="nuget-trusted-signers-remove--name-name"></a>nuget 受信任的签名 remove-名称 <name>

删除任何受信任的签名者与给定名称匹配。

## <a name="nuget-trusted-signers-sync--name-name"></a>nuget 受信任的签名同步-名称 <name>

请求的证书在当前受信任的存储库中用于更新的最新列表中受信任的签名者的现有证书列表。

_请注意_： 此手势将删除当前证书列表和其替换为存储库中的最新列表。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。|
| ForceEnglishOutput | 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| 详细级别 | 指定的输出中显示的详细信息：*正常*，*静默*，*详细*。 |

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