---
title: "创建和发布 NuGet 包的介绍性指南 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/03/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "使用 nuget.exe 命令行接口和 Visual Studio 创建和发布 NuGet 包的演练教程。"
keywords: "NuGet 包创建, NuGet 包发布, NuGet 教程"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 53d29283c9e786fc27e9a608d7d251d8d0b5b0b2
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2018
---
# <a name="create-and-publish-a-package"></a>创建和发布包

从 .NET 类库创建 NuGet 包并将其发布到 nuget.org 是很简单的过程。本文将逐步介绍使用 NuGet 命令行接口 (CLI) 和 Visual Studio 的过程：

## <a name="pre-requisites"></a>先决条件

1. 从 [visualstudio.com](https://www.visualstudio.com/) 安装任意版本的 Visual Studio 2017。

1. 安装 NuGet CLI 工具，`nuget.exe`，方法是从 [nuget.org/downloads](https://nuget.org/downloads) 下载最新版本的 `nuget.exe` 并将 `.exe` 保存到你的路径中的位置。 请注意，下载是工具本身，而不是安装程序。

1. 为要打包的代码创建合适的 .NET 类库项目。 如果还没有项目，可按如下所示创建一个简单的项目：
    1. 在 Visual Studio 中，选择“文件”>“新建”>“项目”，展开“Visual C# > Windows”节点，选择“类库”模板，将项目命名为“AppLogger”，然后单击“确定”。
    1. 右键单击生成的项目文件并选择“生成”，确保已正确创建项目。 DLL 位于调试文件夹中（或发布中，如果生成的是该配置）。

    当然，在实际的 NuGet 包中，可实现许多有用的功能，其他人可基于这些功能生成应用程序。 但是对于本演练，无需编写其他任何代码，因为模板的类库足以创建包。

## <a name="create-the-nuspec-package-manifest-file"></a>创建 .nuspec 程序包清单文件

每个 NuGet 包都需要清单 &mdash; 一种 `.nuspec` 文件 &mdash; 以描述其内容和依赖项。 `nuget spec` 命令会创建此文件，然后你可对其进行自定义。 在此示例中，将从项目文件创建 `.nuspec`；还可以通过[创建包](../create-packages/creating-a-package.md)中所述的其他方式创建清单。

1. 打开命令提示符并导航到包含项目文件的文件夹 (`.csproj`)。

1. 运行 NuGet CLI `spec` 命令生成清单，清单以项目命名，如 `AppLogger.nuspec`：

    ```cli
    nuget spec
    ```

1. 在文本编辑器中打开文件。 清单看起来类似于下面的代码，其中 `<token>` 形式的令牌（例如，`$id$`）在打包过程中被替换为项目的 Properties/AssemblyInfo.cs 文件中的值。 有关令牌的更多详细信息，请参阅[创建 .nuspec 文件](../create-packages/creating-a-package.md#creating-the-nuspec-file)。

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. 选择在 nuget.org 上唯一的包 ID。我们建议使用[创建包](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)中所述的命名约定。 务必更新作者和说明标记，否则下一步会出现错误。 以下是已更新 `.nuspec` 文件的示例：

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> 对于供公共使用而生成的包，请特别注意 `<tags>` 元素，因为这些标记可帮助其他人查找包并了解其用途。

## <a name="run-the-pack-command"></a>运行 pack 命令

若要从项目中生成 NuGet 包（一个 `.nupkg` 文件），请运行 `pack` 命令：

```cli
nuget pack AppLogger.csproj
```

此命令使用 `.nuspec` 文件的包名称和版本号创建 `AppLogger.1.0.0.0.nupkg`。 如果尚未更新 `.nuspec` 文件的各个字段的默认值，该命令会发出警告。

## <a name="publish-the-package"></a>发布包

拥有 `.nupkg` 文件后，使用 `push` 命令将其发布到 nuget.org。 （或者，可以使用 [nuget.org 发布工作流](../create-packages/publish-a-package.md#publish-to-nugetorg)。

> [!Warning]
> 发布到 nuget.org 的包对其他开发人员公开可见。 若要专门托管包，请参阅[托管包](../hosting-packages/overview.md)。

1. 在 [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) 上创建免费帐户，如果已有帐户，请登录。 创建新帐户会发送确认电子邮件。 必须先确认该帐户，才能上传包。

1. 登录后，选择用户名（在右上角），然后选择“API 密钥”。

1. 选择“创建”，提供密钥的名称，在“API 密钥”下选择“选择作用域”>“推送”，为“Glob 模式”输入 *，然后选择“创建”。

1. 创建密钥后，选择“复制”，检索需要在 CLI 中使用的访问密钥：

    ![将 API 密钥复制到剪贴板](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > 将密钥保存在安全位置并保密。 如果密钥意外泄露，可随时重新生成密钥。 如果不再希望通过 CLI 推送包，还可以删除 API 密钥。

1. 在命令提示符处，运行以下命令，指定包名称并使用步骤 4 中复制的值替换密钥：

    ```cli
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe 会显示发布过程的结果：

    ```output
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. 从 nuget.org 上的配置文件中，选择“管理包”，查看刚刚发布的包。 同样也会收到确认电子邮件。 请注意，包可能需要一些时间才能编入索引并显示在可供他人查看的搜索结果中。 在该时间段，包页面会显示以下消息：

    ![此包未编制索引。 它将显示在搜索结果中，并可在索引编制完成后用于安装/还原。](media/QS_Create-03-NotIndexed.png)

> [!Note]
> **病毒扫描**：所有上传到 nuget.org 的包都会进行病毒扫描，如果发现任何病毒，将拒绝包。 此外，还会定期扫描 nuget.org 上列出的所有包。

就是这么简单！ 刚刚已将第一个 NuGet 包发布到 [nuget.org](https://www.nuget.org/)，其他开发人员可在自己的项目中使用它。

## <a name="related-topics"></a>相关主题

- [创建包](../create-packages/creating-a-package.md)
- [发布包](../create-packages/publish-a-package.md)
- [支持多个目标框架](../create-packages/supporting-multiple-target-frameworks.md)
- [包版本控制](../reference/package-versioning.md)
- [创建本地化包](../create-packages/creating-localized-packages.md)
