---
title: "NuGet CLI 登录命令 |Microsoft 文档"
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 登录命令参考"
keywords: "nuget 符号引用，登录命令"
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 109b0f6aca0ebaae2ea56fbb45226bc1b14f2ea1
ms.sourcegitcommit: df7158169e84900d135416cd5e52f937df0beb52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="sign-command-nuget-cli"></a>登录命令 (NuGet CLI)

**适用于：** ，创建包&bullet;**受支持的版本：** 4.6 +

对匹配的第一个参数使用证书的所有包进行都签名。 从文件或从安装在证书存储区中，通过提供使用者名称或指纹的证书，则可以获取具有私钥的证书。

包签名尚不支持在 Mono 下或在非 Windows 平台上。

## <a name="usage"></a>用法

```cli
nuget sign <package(s)> [options]
```

其中`<package(s)>`一个或多个`.nupkg`文件。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| CertificateFingerprint | 指定用于搜索的证书的本地证书存储区的证书的 sha-1 指纹。 |
| CertificatePassword | 如果需要请指定证书密码。 如果证书受密码保护，但提供没有密码，该命令将提示输入密码在运行时，除非-非交互式选项传递。 |
| CertificatePath | 指定要用于对包进行签名的证书的文件路径。 |
| CertificateStoreLocation | 指定与 X.509 证书存储用于搜索该证书的名称。 默认值为"CurrentUser"，使用当前用户的 X.509 证书存储区。 指定通过-CertificateSubjectName 或-CertificateFingerprint 选项证书时，应使用此选项。 |
| CertificateStoreName | 指定要用于搜索该证书的 X.509 证书存储区的名称。 默认值为"My"，个人证书的 X.509 证书存储。 指定通过-CertificateSubjectName 或-CertificateFingerprint 选项证书时，应使用此选项。 |
| CertificateSubjectName | 指定用于搜索的证书的本地证书存储区的证书的使用者名称。  搜索不使用所提供的值，将查找所有证书使用者名称为包含该字符串，而不考虑其他使用者值不区分大小写的字符串比较。  可以通过-CertificateStoreName 和-CertificateStoreLocation 选项指定的证书存储区。 |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定， *%AppData%\NuGet\NuGet.Config*使用。 |
| ForceEnglishOutput | 强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| HashAlgorithm | 要用于对包进行签名的哈希算法。 默认值为 SHA256。 |
| 帮助 | 显示的帮助命令的信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| OutputDirectory | 指定保存签名的包的目录。 默认情况下已签名的软件包的情况下会覆盖原始包。 |
| Overwrite | 开关，这表示是否应覆盖当前的签名。 默认情况下如果包已签名，则该命令将失败。 |
| Timestamper | 到 RFC 3161 时间戳服务器的 URL。 |
| TimestampHashAlgorithm | 要由 RFC 3161 时间戳服务器的哈希算法。 默认值为 SHA256。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。 |

## <a name="examples"></a>示例

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```