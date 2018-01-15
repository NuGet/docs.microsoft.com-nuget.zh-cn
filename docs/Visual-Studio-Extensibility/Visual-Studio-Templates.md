---
title: "Visual Studio 模板中的 NuGet 包 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/3/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "在 Visual Studio 项目和项模板中添加 NuGet 包的说明。"
keywords: "Visual Studio 中的 NuGet, Visual Studio 项目模板, Visual Studio 项模板, 项目模板中的包, 项模板中的包"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 45a2ca2c08660be650f9cf38301f628923e1f8be
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="packages-in-visual-studio-templates"></a>Visual Studio 模板中的包

创建项目或项时，Visual Studio 项目和项模板通常需要确保某些包已安装。 例如，ASP.NET MVC 3 模板安装 jQuery、Modernizr 和其他包。

若要支持此功能，模板作者可指示 NuGet 安装必需的包，而不是单独的库。 此后，开发人员可随时轻松更新这些包。

要了解有关创作模板本身的详细信息，请参阅[如何：创建项目模板](/visualstudio/ide/how-to-create-project-templates)或[创建自定义项目和项模板](/visualstudio/extensibility/creating-custom-project-and-item-templates)。

本节其余部分介绍创作模板以正确添加 NuGet 包时应采取的具体步骤。

- [将包添加到模板](#adding-packages-to-a-template)
- [最佳做法](#best-practices)

有关示例，请参阅 [NuGetInVsTemplates 示例](https://bitbucket.org/marcind/nugetinvstemplates)。

## <a name="adding-packages-to-a-template"></a>将包添加到模板

实例化模板后，会调用[模板向导](/visualstudio/extensibility/how-to-use-wizards-with-project-templates)加载要安装的包列表以及有关在何处查找这些包的信息。 包可嵌入 VSIX，嵌入模板，或者位于本地硬盘上（在这种情况下，请使用注册表项引用文件路径）。 本节稍后将提供这些位置的详细信息。

预安装的包使用[模板向导](/visualstudio/extensibility/how-to-use-wizards-with-project-templates)工作。 模板实例化后会调用特殊向导。 该向导会加载需要安装的包列表，并将该信息传递到相应的 NuGet API。

将包添加到模板的步骤：

1. 在 `vstemplate` 文件中，通过添加 [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) 元素向 NuGet 模板向导添加引用：

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll` 为仅包含 `TemplateWizard` 类的程序集，该类是调用 `NuGet.VisualStudio.dll` 中实际实现的简单包装器。 程序集版本永远不会更改，因此项目/项模板可继续用于新版本的 NuGet。

1. 在项目中添加要安装的包列表：

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    (NuGet 2.2.1+) 该向导支持多个 `<package>` 元素，从而支持多个包源。 `id` 和 `version` 属性都是必需的，这意味着即使可使用较新版本，仍将安装包的特定版本。 这可以防止包更新中断模板，并将是否更新包的选择权留给使用模板的开发人员。

1. 指定 NuGet 可找到包的存储库，如以下各节中所述。

### <a name="vsix-package-repository"></a>VSIX 包存储库

建议用于 Visual Studio 项目/项模板的部署方法是 [VSIX 扩展](/visualstudio/extensibility/shipping-visual-studio-extensions)，因为借助它，可将多个项目/项模板打包在一起，而且开发人员可使用 VS 扩展管理器或 Visual Studio 库轻松发现模板。 也可使用 [Visual Studio 扩展管理器自动更新机制](/visualstudio/extensibility/how-to-update-a-visual-studio-extension)轻松部署扩展更新。

VSIX 本身可用作模板所需包的源：

1. 修改 `.vstemplate` 文件中的 `<packages>` 元素，如下所示：

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    `repository` 属性将存储库类型指定为 `extension`，而 `repositoryId` 是 VSIX 本身的唯一标识符（它是扩展的 `vsixmanifest` 文件中 `ID` 属性的值，请参阅 [VSIX 扩展架构 2.0 参考](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)）。

1. 将 `nupkg` 文件放置于 VSIX 中名为 `Packages` 的文件夹中。

1. 添加必要的包文件作为 `vsixmanifest`文件中的 `<Asset>`（请参阅 [VSIX 扩展架构 2.0 参考](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)：

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. 请注意，可在项目模板所在的同一 VSIX 中提供包，或者可将其放置在单独的 VSIX 中（如果这样对于你的方案更合理）。 但是，请不要引用任何你无法控制的 VSIX，因为对该扩展进行更改可能会中断模板。

### <a name="template-package-repository"></a>模板包存储库

如果仅分发一个项目/项模板且无需将多个模板打包在一起，则可使用更为简单但受限更多的方法，该方法直接在项目/项模板 ZIP 文件中添加包：

1. 修改 `.vstemplate` 文件中的 `<packages>` 元素，如下所示：

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    `repository` 属性具有值 `template`，不需要 `repositoryId` 属性。

1. 将包放置在项目/项模板 ZIP 文件的根文件夹中。

请注意，如果一个或多个包对模板通用，则在包含多个模板的 VSIX 中使用此方法会导致不必要的膨胀。 在这种情况下，请将 [VSIX 用作存储库](#vsix-package-repository)，如上一节中所述。

### <a name="registry-specified-folder-path"></a>注册表指定的文件夹路径

使用 MSI 安装的 SDK 可直接在开发人员计算机上安装 NuGet 包。 这使其在使用项目或项模板时立即可用，而不必在此期间进行提取。 ASP.NET 模板使用此方法。

1. 利用 MSI 将包安装到计算机。 可仅安装 `.nupkg` 文件，也可将其与扩展内容一起安装，这可在使用模板时减少额外的步骤。 在这种情况下，请遵循 NuGet 的标准文件夹结构，其中 `.nupkg` 文件位于根文件夹中，然后每个包都有子文件夹，子文件夹使用 id/版本对作为名称。

1. 写入注册表项以标识包位置：

    - 项位置：如果是计算机范围内的 `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository`，或为每个用户安装的模板和包，则使用 `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`
    - 项名称：使用唯一的名称。 例如，适用于 VS 2012 的 ASP.NET MVC 4 模板使用 `AspNetMvc4VS11`。
    - 值：包文件夹的完整路径。

1. 在 `.vstemplate` 文件的 `<packages>` 元素中，添加属性 `repository="registry"` 并在 `keyName` 属性中指定注册表项名称。

    - 如果已预先解压缩包，请使用 `isPreunzipped="true"` 属性。
    - (NuGet 3.2 +) 如果希望在包安装结束时强制执行设计时生成，请添加 `forceDesignTimeBuild="true"` 属性。
    - 作为优化，添加 `skipAssemblyReferences="true"`，因为模板本身已包括必要的引用。

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>最佳做法

1. 通过在 VSIX 清单中添加对其的引用，声明 NuGet VSIX 上的依赖项：

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. 通过在 `.vstemplate` 文件中包括 [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates)，要求在创建时保存项目/项模板。

1. 模板不包括 `packages.config` 或 `project.json` 文件，也不包括安装 NuGet 包时将添加的任何引用或内容。
