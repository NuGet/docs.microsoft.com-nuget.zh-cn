---
title: "如何发布 NuGet 包 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/5/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2342aabd-983e-4db1-9230-57c84fa36969
description: "详细说明如何将 NuGet 包发布到 nuget.org 或专用源，以及如何在 nuget.org 上管理包所有权。"
keywords: "NuGet 包发布, 发布 NuGet 包, NuGet 包所有权, 发布到 nuget.org, NuGet 专用源"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: fab25931165afb65aa3fd09c5bc37492ce814a49
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="publishing-packages"></a>发布包

使用 `nuget pack` [创建包](../create-packages/creating-a-package.md)后，可轻松地以公开或私密方式将其提供给其他开发人员：

- 根据本主题中的介绍，可通过 [nuget.org](https://www.nuget.org/packages/manage/upload) 将公共包全局提供给所有开发人员。
- 通过以下方式可以仅向团队或组织提供专用包：在文件共享、专用 NuGet 服务器、[Visual Studio Team Services 包管理](https://www.visualstudio.com/docs/package/nuget/publish)或第三方存储库（如 myget、ProGet、Nexus 存储库和 Artifactory）上承载专用包。 有关其他详细信息，请参阅[承载包概述](../hosting-packages/overview.md)。

本主题介绍如何发布到 nuget.org；有关发布到 Visual Studio Team Services 的信息，请参阅[包管理](https://www.visualstudio.com/docs/package/nuget/publish)。

## <a name="publish-to-nugetorg"></a>发布到 nuget.org

对于 nuget.org，必须首先[注册一个免费帐户](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)或登录（如果已注册）：

![NuGet 的注册和登录位置](media/publish_NuGetSignIn.png)

接下来，可根据以下各节中的介绍，通过 nuget.org Web 门户 上传包、从命令行将包推送到 nuget.org 或通过 Visual Studio Team Services 在 CI/CD 过程中发布包。

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Web 门户：使用 nuget.org 上的“上传包”选项卡：

![使用 NuGet 包管理器上传包](media/publish_UploadYourPackage.PNG)

### <a name="command-line"></a>命令行：
> [!Important]
> 若要将包推送到 nuget.org，必须使用实现所需 [NuGet 协议](../api/nuget-protocols.md)的 [nuget.exe v4.1.0 或更高版本](https://www.nuget.org/downloads)。

1. 单击用户名，导航到帐户设置。
2. 在“API 密钥”下，单击“复制到剪贴板”，检索需要在 CLI 中使用的访问密钥：

    ![从帐户设置中复制 API 密钥](media/publish_APIKey.png)

3. 在命令提示符下，运行下列命令：

    ```
    nuget setApiKey Your-API-Key
    ```

    此命令会将 API 密钥存储在计算机上，因此无需在同一计算机上再次执行此步骤。

4. 使用以下命令将包推送到 NuGet 库：

    ```
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

5. 在公布之前，上传到 nuget.org 的所有包都会扫描是否存在病毒，如果发现任何病毒，将拒绝包。 此外，还会定期扫描 nuget.org 上列出的所有包。

6. 在 nuget.org 上的帐户中，单击“管理我的包”可查看刚刚发布的包；还会收到确认电子邮件。 请注意，对包编制索引并将其显示在搜索结果中供其他人查找可能需要一些时间。在此期间，包页面上会出现以下消息：

    ![指示尚未对包编制索引的消息](media/publish_NotYetIndexed.png)

### <a name="package-validation-and-indexing"></a>包验证和编制索引

推送到 NuGet.org 的包会进行多项验证。 包通过所有验证检查后，对包编制索引并将其显示在搜索结果中可能需要一些时间。 编制索引完成后，你将收到一封确认已成功发布包的电子邮件。 如果包未通过验证检查，将更新包详细信息页面以显示相关错误，同时你也会收到包含相关通知的电子邮件。

包验证和编制索引所需的时间通常不超过 15 分钟。 如果发布包所用时间超出预期，请访问 [status.nuget.org](https://status.nuget.org/) 检查 NuGet.org 是否遇到任何中断。 如果所有系统均正常运行，但一个小时之内还未成功发布包，请登录 NuGet.org 并使用包页面上的“联系支持人员”链接与我们联系。

### <a name="visual-studio-team-services-cicd"></a>Visual Studio Team Services (CI/CD)

如果在持续集成/部署过程中使用 Visual Studio Team Services 将包推送到 nuget.org，必须在 NuGet 任务中使用 nuget.exe 4.1 或更高版本。 要了解详细信息，请参阅 [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/)（在生成中使用最新 NuGet）（Microsoft DevOps 博客）。

## <a name="managing-package-owners-on-nugetorg"></a>在 nuget.org 上管理包所有者

尽管每个 NuGet 包的 `.nuspec` 文件定义了该包的创建者，但 nuget.org 库不使用该元数据定义所有权。 相反，nuget.org 将初始所有权分配给发布包的人员。 他们通常是通过 nuget.org UI 上传包的已登录用户，或其 API 密钥与 `nuget SetApiKey` 或 `nuget push` 配合使用的用户。

所有包所有者均拥有包的完全权限，包括添加和删除其他所有者以及发布更新。

要更改包的所有权，请执行以下操作：

1. 使用包的当前所有者的帐户登录 nuget.org。
1. 依次单击用户名和“管理我的包”，然后单击要管理的包。
1. 单击左侧的“管理所有者”链接。

此时，你具有多个选择：

1. 要添加所有者，请输入其 NuGet 帐户名称，然后单击“添加”。 此操作会向该新共有者发送包含确认链接的电子邮件。 确认后，此人拥有添加和删除所有者的完全权限。 （确认之前，“管理所有者”页面指示此人的状态为“待审批”）。
1. 要删除所有者，请在“管理所有者”上选择其名称，然后单击“删除”。
1. 要转让所有权（如变更所有权或在错误的帐户下发布包时），只需添加新所有者，他们确认所有权后，即可将你从列表中删除。

要将所有权分配给公司或组，请使用转发到适当团队成员的电子邮件别名创建 nuget.org 帐户。 例如，各种 Microsoft ASP.NET 包由 [microsoft](http://nuget.org/profiles/microsoft) 和 [aspnet](http://nuget.org/profiles/aspnet) 帐户共同拥有，这两个帐户就是此类别名。

### <a name="recovering-package-ownership"></a>恢复包的所有权

有时，包所有者可能不太活跃。 例如，原始所有者可能已离开生产该包的公司，nuget.org 凭据丢失，或库中的早期 bug 导致包不具有所有者。

如果你是包的合法所有者且需要重新获得所有权，请使用 nuget.org 上的[联系表单](https://www.nuget.org/policies/Contact)向 NuGet 团队解释相关情况。 然后，我们按照流程验证你对包的所有权，包括通过包的项目 URL、Twitter、电子邮件或其他方式尝试找出现有所有者。 但如果所有其他方式均失败，我们会向你发送成为所有者的邀请。
