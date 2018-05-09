---
title: 从 Visual Studio 中使用 NuGet 包的介绍性指南
description: 有关如何在 Visual Studio 项目中安装并使用 NuGet 包的演练教程。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: c61f8929d34bc9ff1a84ee186636543da5bcee63
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a>快速入门：在 Visual Studio 中安装和使用包

NuGet 包包含其他开发人员提供的在项目中使用的可重用代码。 请参阅[什么是 NuGet？](../What-is-NuGet.md)，了解背景信息。 使用包管理器 UI 或包管理器控制台的 Visual Studio 项目中安装包。 本文介绍使用热门的 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 包和通用 Windows 平台 (UWP) 项目的过程。 相同的过程适用于任何其他 .NET 或 .NET Core 项目。

安装完成后，请引用具有 `using <namespace>` 的代码中的包，其中 \<namespace\> 特定于正在使用的包。 建立引用后，可通过相应的 API 调用包。

> [!Tip]
> **nuget.org 入门**：浏览 nuget.org 是 .NET 开发人员通常在自己的应用程序中查找可重用组件的方式。 你可以直接搜索 nuget.org 或根据本文中的介绍，在 Visual Studio 中查找和安装包。

## <a name="prerequisites"></a>系统必备

- 具有通用 Windows 平台开发工作负载的 Visual Studio 2017，或
- 适用于通用 Windows 应用的 Visual Studio 2015 Update 3

可以从 [visualstudio.com](https://www.visualstudio.com/) 免费安装 2017 Community 版，或者使用 Professional 或 Enterprise 版。

## <a name="create-a-project"></a>创建项目

可将 NuGet 包安装到任何 .NET 项目，前提是包支持与项目相同的目标框架。

对于本演练，将使用简单的通用 Windows (UWP) 应用。 要在 Visual Studio 中创建项目，请使用“文件 > 新建项目...”，然后选择“Windows 通用 > 空白应用(通用 Windows)”。 出现提示时，接受“目标版本”和“最低版本”的默认值。

## <a name="add-the-newtonsoftjson-nuget-package"></a>添加 Newtonsoft.Json Nuget 包

若要安装此程序包，可以使用程序包管理器 UI 或程序包管理器控制台。 安装包时，NuGet 会将依赖项记录在项目文件或 `packages.config` 文件中。 有关详细信息，请参阅[包使用概述和工作流](../consume-packages/Overview-and-Workflow.md)。

### <a name="package-manager-ui"></a>包管理器 UI

1. 在解决方案资源管理器中，右键单击“引用”，选择“管理 NuGet 包”。

    ![管理项目引用的 NuGet 包命令](media/QS_Use-02-ManageNuGetPackages.png)

1. 将“nuget.org”选择为“包源”，选择“浏览”选项卡并搜索“Newtonsoft.Json”，在列表中选择该包，然后选择“安装”：

    ![定位 Newtonsoft.Json 包](media/QS_Use-03-NewtonsoftJson.png)

1. 接受任何许可证提示。

1. (Visual Studio 2017) 如果系统提示选择程序包管理格式，请选择“项目文件中的 PackageReference”：

    ![选择包管理格式](media/QS_Use-03b-SelectFormat.png)

1. 如果系统提示查看更改，请选择“确定”。

### <a name="package-manager-console"></a>程序包管理器控制台

1. 选择“工具”>“NuGet 包管理器”>“程序包管理器控制台”菜单命令。

1. 控制台打开后，检查“默认项目”下拉列表中是否显示在程序包中要安装的项目。 如果在解决方案中有一个项目，则它已被选中。

    ![定位 Newtonsoft.Json 包](media/QS_Use-08-Console1.png)

1. 输入命令 `Install-Package Newtonsoft.json`（请参阅 [Install-Package](../tools/ps-ref-install-package.md)）。 控制台窗口会显示该命令的输出。 错误通常指示程序包与项目的目标框架不兼容。

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>在应用中使用 Newtonsoft.Json API

使用项目中的 Newtonsoft.Json 包，可调用 `JsonConvert.SerializeObject` 方法将对象转换为可人工读取的字符串。

1. 打开 `MainPage.xaml` 并将现有 `Grid` 元素替换为以下内容：

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. 打开 `MainPage.xaml.cs` 文件（位于 `MainPage.xaml` 节点下的解决方案资源管理器中），然后在 `MainPage` 构造函数中插入以下代码：

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
    using Newtonsoft.json;
    ```

1. 若要生成并运行应用，请按 F5 或选择“调试”>“启动调试”：

    ![UWP 应用的初始输出](media/QS_Use-06-AppStart.png)

1. 选择按钮，查看替换为某些 JSON 文本的 TextBlock 的内容：

    ![选择按钮后 UWP 应用的输出](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a>相关文章

- [包使用的概述和工作流](../consume-packages/overview-and-workflow.md)
- [查找和选择包](../consume-packages/finding-and-choosing-packages.md)
- [安装包的方式](../consume-packages/ways-to-install-a-package.md)
- [配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)
