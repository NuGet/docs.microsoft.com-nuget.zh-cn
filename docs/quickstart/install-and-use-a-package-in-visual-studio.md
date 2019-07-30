---
title: 在 Visual Studio 中安装和使用 NuGet 包
description: 有关如何在 Visual Studio 项目中安装并使用 NuGet 包的演练教程。
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: a2be42aeb322cfd0ab43c9cec6ad1b063cbc3089
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68462479"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a>快速入门：在 Visual Studio 中安装和使用包（仅适用于 Windows）

NuGet 包包含其他开发人员提供的在项目中使用的可重用代码。 请参阅[什么是 NuGet？](../What-is-NuGet.md)，了解背景信息。 使用 NuGet 包管理器或包管理器控制台在 Visual Studio 项目中安装包。 本文介绍使用热门的 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 包和 Windows Presentation Foundation (WPF) 项目的过程。 相同的过程适用于任何其他 .NET 或 .NET Core 项目。

安装完成后，请引用具有 `using <namespace>` 的代码中的包，其中 \<namespace\> 特定于正在使用的包。 建立引用后，可通过相应的 API 调用包。

> [!Tip]
> **nuget.org 入门**：为查找可在自己的应用程序中重用的组件，.NET 开发人员通常都会浏览 nuget.org  。 可以直接搜索 nuget.org 或根据本文中的介绍，在 Visual Studio 中查找和安装包  。 有关一般信息，请参阅[查找和评估 NuGet 包](../consume-packages/finding-and-choosing-packages.md)。

## <a name="prerequisites"></a>系统必备

- Visual Studio 2019 .NET 桌面开发工作流。

可以从 [visualstudio.com](https://www.visualstudio.com/) 免费安装 2019 Community 版，或者使用 Professional 或 Enterprise 版。

如果使用的是 Visual Studio for Mac，请参阅[在项目中包括 NuGet 包](/visualstudio/mac/nuget-walkthrough)。

## <a name="create-a-project"></a>创建项目

可将 NuGet 包安装到任何 .NET 项目，前提是包支持与项目相同的目标框架。

本演练使用简单的 WPF 应用。 使用以下方法在 Visual Studio 中创建项目：单击“文件”>“新建项目...”  ，在搜索框中键入“.NET”  ，然后选择“WPF 应用(.NET Framework)”  。 单击 **“下一步”** 。 出现提示时，接受 Framework  的默认值。

Visual Studio 创建项目，该项目将在解决方案资源管理器中打开。

## <a name="add-the-newtonsoftjson-nuget-package"></a>添加 Newtonsoft.Json Nuget 包

若要安装此包，可以使用 NuGet 包管理器或包管理器控制台。 安装包时，NuGet 会将依赖项记录在项目文件或 `packages.config` 文件中（具体位置取决于项目格式）。 有关详细信息，请参阅[包使用概述和工作流](../consume-packages/Overview-and-Workflow.md)。

### <a name="nuget-package-manager"></a>NuGet 程序包管理器

1. 在解决方案资源管理器中，右键单击“引用”，选择“管理 NuGet 包”   。

    ![管理项目引用的 NuGet 包命令](media/QS_Use-02-ManageNuGetPackages.png)

1. 将“nuget.org”选择为“包源”，选择“浏览”选项卡并搜索“Newtonsoft.Json”，在列表中选择该包，然后选择“安装”     ：

    ![定位 Newtonsoft.Json 包](media/QS_Use-03-NewtonsoftJson.png)

    若要了解有关 NuGet 包管理器的详细信息，请参阅[使用 Visual Studio 安装和管理包](../consume-packages/install-use-packages-visual-studio.md)。

1. 接受任何许可证提示。

1. （仅适用于 Visual Studio 2017）如果系统提示选择包管理格式，请选择  “项目文件中的 PackageReference”：

    ![选择包管理格式](media/QS_Use-03b-SelectFormat.png)

1. 如果系统提示查看更改，请选择“确定”  。

### <a name="package-manager-console"></a>程序包管理器控制台

1. 选择“工具”>“NuGet 包管理器”>“程序包管理器控制台”菜单命令。 

1. 控制台打开后，检查  “默认项目”下拉列表中是否显示在程序包中要安装的项目。 如果在解决方案中有一个项目，则它已被选中。

    ![定位 Newtonsoft.Json 包](media/QS_Use-08-Console1.png)

1. 输入命令 `Install-Package Newtonsoft.Json`（请参阅 [Install-Package](../reference/ps-reference/ps-ref-install-package.md)）。 控制台窗口会显示该命令的输出。 错误通常指示程序包与项目的目标框架不兼容。

   若要了解有关包管理器控制台的详细信息，请参阅[使用包管理器控制台安装和管理包](../consume-packages/install-use-packages-powershell.md)。

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>在应用中使用 Newtonsoft.Json API

使用项目中的 Newtonsoft.Json 包，可调用 `JsonConvert.SerializeObject` 方法将对象转换为可人工读取的字符串。

1. 打开 `MainWindow.xaml` 并将现有 `Grid` 元素替换为以下内容：

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. 打开 `MainWindow.xaml.cs` 文件（位于 `MainWindow.xaml` 节点下的解决方案资源管理器中），然后在 `MainWindow` 类中插入以下代码：

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. 尽管已将 Newtonsoft.Json 包添加到项目中，因为你需要使用代码文件最上方的 `using` 语句，所以 `JsonConvert` 下仍会出现红色波形曲线：

    ```cs
    using Newtonsoft.Json;
    ```

1. 若要生成并运行应用，请按 F5 或选择“调试”>“启动调试”  ：

    ![WPF 应用的初始输出](media/QS_Use-06-AppStart.png)

1. 选择按钮，查看替换为某些 JSON 文本的 TextBlock 的内容：

    ![选择按钮后 WPF 应用的输出](media/QS_Use-07-AppEnd.png)

## <a name="next-steps"></a>后续步骤

祝贺你安装并使用第一个 NuGet 包！

> [!div class="nextstepaction"]
> [使用 Visual Studio 安装和管理包](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [使用包管理器控制台安装和管理包](../consume-packages/install-use-packages-powershell.md)

若要了解更多 NuGet 产品，请选择以下链接。

- [包使用的概述和工作流](../consume-packages/overview-and-workflow.md)
- [查找和选择包](../consume-packages/finding-and-choosing-packages.md)
- [项目文件中的包引用](../consume-packages/package-references-in-project-files.md)
