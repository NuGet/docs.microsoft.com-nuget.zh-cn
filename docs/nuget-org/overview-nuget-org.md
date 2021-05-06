---
title: NuGet.org 概述
description: NuGet.org 概述
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 2dac6ebd6367f3ed1a5ef9e81d843867a4a22f62
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901871"
---
# <a name="overview-of-nugetorg"></a>NuGet.org 概述

NuGet.org 是 NuGet 包的公用主机，每天都有数百万 .NET 和 .NET Core 开发人员使用它。

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a>NuGet.org 在 NuGet 生态系统中的角色

作为公用主机，NuGet.org 本身在 [nuget.org](https://www.nuget.org) 上维护超过 100,000 个独特包的中央存储库。NuGet.org 不是包的唯一可能主机。 NuGet 技术还支持在云中（如在 Azure DevOps 上）、在私有网络中或者甚至直接在本地文件系统以私密方式托管包。 如果对其他主机或承载选项感兴趣，请参阅[承载自己的 NuGet 源](../hosting-packages/overview.md)。

与 NuGet 包的任何主机一样，NuGet.org 充当包创建者和包消费者之间的连接点。 创建者生成有用的 NuGet 包并将其发布。 然后，使用者可以在可访问的主机上搜索有用且兼容的包，下载包并将其包含在项目中。 在项目中安装包后，包的 API 将可用于其余项目代码。

![包创建者、包主机和包使用者之间的关系](media/nuget-roles.png)

## <a name="accounts"></a>帐户

要在 NuGet.org 上发布包，首先要创建一个[个人（用户）帐户](individual-accounts.md)。 这将成为你在 NuGet.org 上的标识。

通过 NuGet.org 还可创建[组织帐户](organizations-on-nuget-org.md)。 组织帐户具有一个或多个个人帐户作为其成员。 成员可以管理一组包，同时保持所有权的单一标识。 通过你的个人帐户，你可以成为任意数量组织的成员。

包可以属于组织帐户，也可以属于个人帐户。 包使用者看不到个人帐户或组织帐户之间的任何差异：两者都显示为包 `owners`。

## <a name="api-keys"></a>API 密钥

具有要发布的 NuGet 包（.nupkg 文件）后，可以使用 nuget.exe CLI 或 dotnet.exe CLI 以及从 NuGet.org 获得的 [API 密钥](scoped-api-keys.md)将其发布到 NuGet.org。

在[发布包](../create-packages/creating-a-package.md)时，请在 CLI 命令中包含 API 密钥值。

## <a name="id-prefixes"></a>ID 前缀

发布包时，可以通过[保留 ID 前缀](id-prefix-reservation.md)来保留和保护标识。 安装包时，包使用者会收到附加信息，其中指出他们使用的包在标识属性中并不具有欺骗性。

## <a name="api-endpoint-for-nugetorg"></a>适用于 NuGet.org 的 API 终结点

若要将 NuGet.org 用作 NuGet 客户端的包存储库，应使用以下 V3 API 终结点： 

`https://api.nuget.org/v3/index.json`

旧客户端仍然可以使用 V2 协议来访问 NuGet.org。不过，请注意，NuGet 客户端 3.0 或更高版本使用 V2 协议会使服务变慢且不太可靠：

`https://www.nuget.org/api/v2`（V2 协议已弃用！）
