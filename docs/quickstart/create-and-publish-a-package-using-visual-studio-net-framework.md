---
title: 在 Windows 上使用 Visual Studio 创建和发布 .NET Framework 包
description: 在 Windows 上使用 Visual Studio 2017 创建和发布 .NET Framework NuGet 包的演练教程。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: c537ee97b79648428df2c1b52894f536f5626a9e
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508252"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a>快速入门：使用 Visual Studio 创建和发布包（.NET Framework、Windows）

若要从 .NET Framework 类库创建 NuGet 包，需要在 Windows 上的 Visual Studio 中创建 DLL，然后使用 nuget.exe 命令行工具创建并发布包。

> [!Note]
> 本快速入门教程仅适用于 Visual Studio 2017 for Windows。 Visual Studio for Mac 不包括此处所述的功能。 改为使用 [dotnet CLI 工具](create-and-publish-a-package-using-the-dotnet-cli.md)。

## <a name="prerequisites"></a>系统必备

1. 通过任何与 .NET 相关的工作负载从 [visualstudio.com](https://www.visualstudio.com/) 安装任意版本的 Visual Studio 2017。 安装 .NET 工作负载时，Visual Studio 2017 会自动包含 NuGet 功能。

1. 要安装 `nuget.exe` CLI，从 [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) 下载它，将 `.exe` 文件保存到合适的文件夹，然后将该文件夹添加到 PATH 环境变量中。

1. 如果你还没有帐户，请[在 nuget.org 上注册一个免费帐户](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)。 创建新帐户会发送确认电子邮件。 必须先确认该帐户，才能上传包。

## <a name="create-a-class-library-project"></a>创建类库项目

可以使用现有的 .NET Framework 类库项目用于要打包的代码，或者创建一个简单的项目，如下所示：

1. 在 Visual Studio 中，选择“文件”>“新建”>“项目”，再依次选择“Visual C#”节点、“类库(.NET Framework)”模板，将项目命名为“AppLogger”，然后单击“确定”。

1. 右键单击生成的项目文件并选择“生成”，确保已正确创建项目。 DLL 位于调试文件夹中（或发布中，如果生成的是该配置）。

当然，在实际的 NuGet 包中，可实现许多有用的功能，让其他人可通过这些功能生成应用程序。 也可以按个人喜欢的方式设置目标框架。 有关示例，请参阅 [UWP](../guides/create-uwp-packages.md) 和 [Xamarin](../guides/create-packages-for-xamarin.md) 指南。

但是对于本演练，无需编写其他任何代码，因为模板的类库足以创建包。 但是，如果你需要此程序包的某个功能代码，请使用以下命令：

```cs
using System;

namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> 除非你有其他选择理由，否则 .NET Standard 是 NuGet 包的首选目标，因为它提供了与最广泛的使用项目的兼容性。 请参阅[使用 Visual Studio 创建和发布包 (.NET Standard)](create-and-publish-a-package-using-visual-studio.md)。

## <a name="configure-project-properties-for-the-package"></a>配置包的项目属性

NuGet 包中包含清单（`.nuspec` 文件），其中包含相关的元数据，例如包标识符、版本号和描述等。 其中一些元数据可直接从项目属性中获取，避免在项目和清单中对其进行单独更新。 本节介绍在何处设置适用的属性。

1. 选择“项目”>“属性”菜单命令，然后选择“应用程序”选项卡。

1. 在“程序集名称”字段中，为包提供唯一标识符。

    > [!Important]
    > 你必须为包提供一个在 nuget.org 中唯一或你使用的任何主机的标识符。 对于本次演练，我们建议在名称中包含“Sample”或“Test”，因为稍后的发布步骤确实会使该包公开显示（尽管实际上不太可能有人会使用它）。
    >
    > 如果你尝试发布名称已存在的包，则会看到一个错误。

1. 选择“程序集信息...”按钮，此时会出现一个对话框，可在其中输入清单中的其他属性（请参阅 [.nuspec 文件引用 - 替换令牌](../reference/nuspec.md#replacement-tokens)）。 最常用的字段是“标题”、“描述”、“公司”、“版权所有”和“程序集版本”。 这些属性最终会随包出现在主机上（例如 nuget.org ），因此请确保对其进行完整描述。

    ![Visual Studio 内 .NET Framework 项目中的程序集信息](media/qs_create-vs-01b-project-properties.png)

1. 可选：若要直接查看和编辑属性，请打开项目中的 `Properties/AssemblyInfo.cs` 文件。

1. 设置属性时，请将项目配置设置为“发布”并重新生成项目以生成更新的 DLL。

## <a name="generate-the-initial-manifest"></a>生成初始清单

既然已准备好 DLL 并已设置项目属性，现在即可使用 `nuget spec` 命令从项目生成初始 `.nuspec` 文件。 此步骤包括相关替换令牌，便于从项目文件中提取信息。

仅运行一次 `nuget spec` 即可生成初始清单。 更新包时，可以更改项目中的值或直接编辑清单。

1. 打开命令提示符并导航到包含 `AppLogger.csproj` 文件的项目文件夹。

1. 运行以下命令：`nuget spec AppLogger.csproj`。 通过指定项目，NuGet 会创建匹配项目名称的清单，在此示例中为 `AppLogger.nuspec`。 它还会包括清单中的替换令牌。

1. 在文本编辑器中打开 `AppLogger.nuspec` 以检查其内容，其内容应如下所示：

    ```xml
    <?xml version="1.0"?>
    <package >
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
        <copyright>Copyright 2018</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a>编辑清单

1. 如果尝试在 `.nuspec` 文件中创建包含默认值的包，NuGet 会产生错误，因此在继续操作之前必须编辑以下字段。 请参阅 [.nuspec 文件引用 - 可选元数据元素](../reference/nuspec.md#optional-metadata-elements)，了解如何使用它们。

    - licenseUrl
    - projectUrl
    - iconUrl
    - releaseNotes
    - 标记

1. 对于面向公共使用而生成的包，请特别注意 Tags 属性，因为这些标记可帮助其他人在源中（例如 nuget.org）查找包并了解其用途。

1. 也可以在此时向清单中添加任何其他元素，如 [.nuspec 文件引用](../reference/nuspec.md)中所述。

1. 在继续之前保存文件。

## <a name="run-the-pack-command"></a>运行 pack 命令

1. 从包含 `.nuspec` 文件的文件夹中的命令提示符，运行命令 `nuget pack`。

1. NuGet 以 identifier-version.nupkg 形式生成 `.nupkg` 文件，你可在当前文件夹中找到该文件。

## <a name="publish-the-package"></a>发布包

有了 `.nupkg` 文件后，可以使用 `nuget.exe` 以及从 nuget.org 获取的 API 密钥将其发布到 nuget.org。对于 nuget.org，必须使用 `nuget.exe` 4.1.0 或更高版本。

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>获取 API 密钥

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>用 nuget push 发布

1. 更改到包含 `.nupkg` 文件的文件夹。

1. 运行以下命令，指定包名称并使用你的 API 密钥替换密钥值：

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe 会显示发布过程的结果：

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

请参阅 [nuget push](../tools/cli-ref-push.md)。

### <a name="publish-errors"></a>发布错误

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>管理已发布的包

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>相关主题

- [创建包](../create-packages/creating-a-package.md)
- [发布包](../create-packages/publish-a-package.md)
- [预发行包](../create-packages/Prerelease-Packages.md)
- [支持多个目标框架](../create-packages/supporting-multiple-target-frameworks.md)
- [包版本控制](../reference/package-versioning.md)
- [创建本地化包](../create-packages/creating-localized-packages.md)
