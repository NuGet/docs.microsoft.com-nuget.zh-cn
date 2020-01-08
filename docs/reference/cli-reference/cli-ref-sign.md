---
title: NuGet CLI 签名命令
description: 针对 nuget.exe sign 命令的参考
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 746f7a421bd855b77716388b4af2fecbd5cf5a68
ms.sourcegitcommit: 96aab8a1ad35eca0c029679d0158d9cc93d66009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/06/2020
ms.locfileid: "75676401"
---
# <a name="sign-command-nuget-cli"></a>sign 命令 (NuGet CLI)

**适用于：** 包创建 &bullet;**支持的版本：** 4.6 +

使用证书对匹配第一个参数的所有包进行签名。 可以通过提供使用者名称或指纹，从文件或证书存储中安装的证书获取带有私钥的证书。

> [!Note]
> .NET Core、Mono 或非 Windows 平台上尚不支持包签名。

## <a name="usage"></a>用量

```cli
nuget sign <package(s)> [options]
```

其中 `<package(s)>` 是一个或多个 `.nupkg` 文件。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| CertificateFingerprint | 指定用于搜索证书的本地证书存储区的证书的 SHA-1 指纹。 |
| CertificatePassword | 如果需要，指定证书密码。 如果证书受密码保护，但未提供密码，则该命令将在运行时提示输入密码，除非传递了-非交互式选项。 |
| CertificatePath | 指定用于对包进行签名的证书的文件路径。 |
| CertificateStoreLocation | 指定用于搜索证书的 x.509 证书存储区的名称。 默认为 "CurrentUser"，当前用户使用的 x.509 证书存储。 当通过-CertificateSubjectName 或-CertificateFingerprint 选项指定证书时，应使用此选项。 |
| CertificateStoreName | 指定用于搜索证书的 x.509 证书存储区的名称。 默认值为 "My"，适用于个人证书的 x.509 证书存储。 当通过-CertificateSubjectName 或-CertificateFingerprint 选项指定证书时，应使用此选项。 |
| CertificateSubjectName | 指定用于在本地证书存储区中搜索证书的证书的使用者名称。  搜索是使用提供的值进行区分大小写的字符串比较，它将查找使用者名称包含该字符串的所有证书，而与其他使用者值无关。  可以通过-CertificateStoreName 和-CertificateStoreLocation 选项指定证书存储区。 |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定，则使用 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。|
| ForceEnglishOutput | 使用固定的、基于英语的区域性强制执行 nuget.exe。 |
| HashAlgorithm | 用于对包进行签名的哈希算法。 默认值为 SHA256。 |
| 帮助 | 显示命令的帮助信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| OutputDirectory | 指定应将已签名的包保存到的目录。 默认情况下，已签名的包将覆盖原始包。 |
| 覆盖 | 切换以指示是否应覆盖当前签名。 默认情况下，如果包已有签名，则该命令将失败。 |
| Timestamper | RFC 3161 时间戳服务器的 URL。 |
| TimestampHashAlgorithm | RFC 3161 时间戳服务器使用的哈希算法。 默认值为 SHA256。 |
| 详细级别 | 指定在输出中显示的详细信息量： "*正常*"、"*静默*"、"*详细*"。 |

## <a name="examples"></a>示例

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
