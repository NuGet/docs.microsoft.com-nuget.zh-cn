---
title: NuGet CLI 登录命令
description: Nuget.exe 登录命令的引用
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546358"
---
# <a name="sign-command-nuget-cli"></a>sign 命令 (NuGet CLI)

**适用于：** 创建包&bullet;**支持的版本：** 4.6 +

对匹配的证书的第一个参数的所有包进行都签名。 从文件或安装在证书存储区中，通过提供使用者名称或指纹的证书，可以获取具有私钥的证书。

包签名尚不支持在 Mono 下或在非 Windows 平台上的.NET Core 中。

## <a name="usage"></a>用法

```cli
nuget sign <package(s)> [options]
```

其中`<package(s)>`是一个或多个`.nupkg`文件。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| CertificateFingerprint | 指定用于搜索该证书的本地证书存储的证书的 sha-1 指纹。 |
| CertificatePassword | 如果需要请指定证书密码。 如果证书受密码保护，但不提供密码，该命令将提示输入密码在运行时，除非-传递非交互选项。 |
| CertificatePath | 指定要用于对包进行签名的证书的文件路径。 |
| CertificateStoreLocation | 指定要搜索该证书的 X.509 证书存储区使用的名称。 默认值为"CurrentUser"，当前用户使用的 X.509 证书存储。 指定的证书通过-CertificateSubjectName 或-CertificateFingerprint 选项时，应使用此选项。 |
| CertificateStoreName | 指定要用于搜索该证书的 X.509 证书存储的名称。 默认值为"My"，个人证书的 X.509 证书存储区。 指定的证书通过-CertificateSubjectName 或-CertificateFingerprint 选项时，应使用此选项。 |
| CertificateSubjectName | 指定用于搜索该证书的本地证书存储的证书的使用者名称。  搜索是使用提供的值，将查找所有证书主题名称中包含该字符串，而不考虑其他使用者值不区分大小写的字符串比较。  可以通过-CertificateStoreName 和-CertificateStoreLocation 选项指定的证书存储区。 |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。|
| ForceEnglishOutput | 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。 |
| HashAlgorithm | 要用来对包进行签名的哈希算法。 默认值为 SHA256。 |
| 帮助 | 显示的帮助命令的信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| OutputDirectory | 指定应在其中保存已签名的包的目录。 默认情况下已签名的包会覆盖原始包。 |
| Overwrite | 开关，这表示是否应覆盖的当前签名。 默认情况下如果包已签名，则该命令将失败。 |
| Timestamper | RFC 3161 时间戳服务器 URL。 |
| TimestampHashAlgorithm | 要由 RFC 3161 时间戳服务器使用的哈希算法。 默认值为 SHA256。 |
| 详细级别 | 指定的输出中显示的详细信息：*正常*，*静默*，*详细*。 |

## <a name="examples"></a>示例

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```