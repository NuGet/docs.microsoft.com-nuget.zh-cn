---
title: 如何发布 NuGet 包
description: 详细说明如何将 NuGet 包发布到 nuget.org 或专用源，以及如何在 nuget.org 上管理包所有权。
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: fe5625247dca51c10d82fffe82022c40a4716069
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237927"
---
# <a name="publishing-packages"></a>发布包

创建程序包并获得 `.nupkg` 文件后，即可轻松以公开或私密方式将其提供给其他开发人员：

- 根据本文中的介绍，可通过 [nuget.org](https://www.nuget.org/packages/manage/upload) 将公共包全局提供给所有开发人员（需要 NuGet 4.1.0+）。
- 通过以下方式可以仅向团队或组织提供专用包：在文件共享、专用 NuGet 服务器、[Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) 或第三方存储库（如 myget、ProGet、Nexus 存储库和 Artifactory）上承载专用包。 有关其他详细信息，请参阅[承载包概述](../hosting-packages/overview.md)。

本文介绍如何发布到 nuget.org；有关发布到 Azure Artifacts 的信息，请参阅[包管理](https://www.visualstudio.com/docs/package/nuget/publish)。

## <a name="publish-to-nugetorg"></a>发布到 nuget.org

对于 nuget.org，必须使用 Microsoft 帐户进行登录，将需要在 nuget.org 中注册此帐户。

![NuGet 登录位置](media/publish_NuGetSignIn.png)

接下来，可根据以下各节中的介绍，通过 nuget.org Web 门户上传包、从命令行（需要 `nuget.exe` 4.1.0+）将包推送到 nuget.org 或通过 Azure DevOps Services 在 CI/CD 过程中发布包。

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Web 门户：使用 nuget.org 上的“上传包”选项卡

1. 选择 nuget.org 顶部菜单中的“上传”  ，并浏览到包位置。

    ![在 nuget.org 上上传包](media/publish_UploadYourPackage.PNG)

1. nuget.org 告知包名称是否可用。 如果无法使用，则更改项目中的包标识符、重新生成，并重试上传。

1. 如果包名称可用，nuget.org 将打开“验证”  部分，可以在其中查看包清单中的元数据。 若要更改任何元数据，请编辑项目（项目文件或 `.nuspec` 文件）、重新生成、重新创建包，然后再次上传。

1. 在“导入文档”  下，可以粘贴 Markdown、将 URL 指向文档，或上传文档文件。

1. 当所有信息准备就绪后，选择“提交”  按钮

### <a name="command-line"></a>命令行

若要将包推送到 nuget.org，首先需要一个 API 密钥，该密钥是在 nuget.org 上创建的。必须使用 dotnet.exe (.NET Core) 或 nuget.exe v4.1.0 或更高版本，它可实现所需的 NuGet 协议。
有关详细信息，请参阅 [.NET Core](/dotnet/core/install/)、[nuget.exe](https://www.nuget.org/downloads) 和 [NuGet 协议](../api/nuget-protocols.md)。

#### <a name="create-api-keys"></a>创建 API 密钥

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>用 dotnet nuget push 发布

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>用 nuget push 发布

1. 在命令提示符处运行以下命令，将 `<your_API_key>` 替换为从 nuget.org 获取的密钥：

    ```cli
    nuget setApiKey <your_API_key>
    ```

    此命令将 API 密钥存储在 NuGet 配置中，以便无需在同一台计算机上再次重复此步骤。

    > [!NOTE]
    > API 密钥不用于向专用源进行身份验证。 请参考 [`nuget sources` 命令](../reference/cli-reference/cli-ref-sources.md)来管理用于向源进行身份验证的凭据。
    > API 密钥可以从单个 NuGet 服务器获取。 若要为 nuget.org 创建和管理 APIKey，请参阅[创建 API 密钥](#create-api-keys)。

1. 使用以下命令将包推送到 NuGet 库：

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>发布已签名的包

若要提交已签名的包，必须首先[注册用于签名包的证书](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg)。 

> [!Warning]
> nuget.org 会拒绝不满足[签名包要求](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg)的包。

### <a name="package-validation-and-indexing"></a>包验证和编制索引

推送到 nuget.org 的包会进行多项验证，如病毒检查。 （定期扫描 nuget.org 上的所有包。）

包通过所有验证检查后，对包编制索引并将其显示在搜索结果中可能需要一些时间。 编制索引完成后，你会收到一封确认已成功发布包的电子邮件。 如果包未通过验证检查，将更新包详细信息页面以显示相关错误，同时你也会收到包含相关通知的电子邮件。

包验证和编制索引所需的时间通常不超过 15 分钟。 如果发布包所用时间超出预期，请访问 [status.nuget.org](https://status.nuget.org/) 检查 nuget.org 是否遇到任何中断。 如果所有系统均正常运行，但一个小时之内还未成功发布包，请登录 nuget.org 并使用包页面上的“联系支持人员”链接与我们联系。

若要查看包状态，请选择 nuget.org 上帐户名称下的“管理包”  。完成验证时，会收到确认电子邮件。

请注意，对包编制索引并将其显示在搜索结果中供其他人查找可能需要一些时间。在此期间，包页面上会出现以下消息：

![指示尚未发布包的消息](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a>Azure DevOps Services (CI/CD)

如果在持续集成/部署过程中使用 Azure DevOps Services 将包推送到 nuget.org，必须在 NuGet 任务中使用 `nuget.exe` 4.1 或更高版本。 要了解详细信息，请参阅 [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/)（在生成中使用最新 NuGet）（Microsoft DevOps 博客）。

## <a name="managing-package-owners-on-nugetorg"></a>在 nuget.org 上管理包所有者

尽管每个 NuGet 包的 `.nuspec` 文件定义了该包的创建者，但 nuget.org 库不使用该元数据定义所有权。 相反，nuget.org 将初始所有权分配给发布包的人员。 他们通常是通过 nuget.org UI 上传包的已登录用户，或其 API 密钥与 `nuget SetApiKey` 或 `nuget push` 配合使用的用户。

所有包所有者均拥有包的完全权限，包括添加和删除其他所有者以及发布更新。

要更改包的所有权，请执行以下操作：

1. 使用包的当前所有者的帐户登录 nuget.org。
1. 选择帐户名称，选择“管理包”  ，然后展开“已发布的包”  。
1. 选择要管理的包，然后在右侧选择“管理所有者”  。

此时，你具有多个选择：

1. 删除“当前所有者”  下列出的任何所有者。
1. 在“添加所有者”  下添加所有者，方法是通过输入其用户名和一条消息，然后选择“添加”  。 此操作会向该新共有者发送包含确认链接的电子邮件。 确认后，此人拥有添加和删除所有者的完全权限。 （确认之前，“当前所有者”  部分指示此人的状态为“待审批”。）
1. 要转让所有权（如变更所有权或在错误的帐户下发布包时），请添加新所有者，他们确认所有权后，即可将你从列表中删除。

要将所有权分配给公司或组，请使用转发到适当团队成员的电子邮件别名创建 nuget.org 帐户。 例如，各种 Microsoft ASP.NET 包由 [microsoft](https://nuget.org/profiles/microsoft) 和 [aspnet](https://nuget.org/profiles/aspnet) 帐户共同拥有，这两个帐户就是此类别名。

### <a name="recovering-package-ownership"></a>恢复包的所有权

有时，包所有者可能不太活跃。 例如，原始所有者可能已离开生产该包的公司，nuget.org 凭据丢失，或库中的早期 bug 导致包不具有所有者。

如果你是包的合法所有者且需要重新获得所有权，请使用 nuget.org 上的[联系表单](https://www.nuget.org/policies/Contact)向 NuGet 团队解释相关情况。 然后，我们按照流程验证你对包的所有权，包括通过包的项目 URL、Twitter、电子邮件或其他方式尝试找出现有所有者。 但如果所有其他方式均失败，我们会向你发送成为所有者的邀请。
