---
title: "使用 NuGet 包的介绍性指南 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: f31f8259-20a8-4617-880e-5819299372d2
description: "有关如何在项目中安装并使用 NuGet 包的演练教程。"
keywords: "安装 NuGet, NuGet包使用, 安装 NuGet 包, NuGet 包引用, 使用 NuGet 包"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 639f4883f5ce904a44d8aa23d76c93ed79ea4b9d
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2018
---
# <a name="install-and-use-a-package"></a>安装并使用包

NuGet 包是其他开发者提供的在项目中使用的可重用代码单元。 请参阅[什么是 NuGet？](../What-is-NuGet.md)，了解背景信息。

[!INCLUDE [install-methods](../includes/install-methods.md)]

安装完成后，请引用具有 `using <namespace>` 的代码中的包，其中 \<namespace\> 特定于正在使用的包。 建立引用后，可通过相应的 API 调用包。

本主题的其余部分介绍如何使用包管理器 UI 在通用 Windows 平台 (UWP) 项目中安装常用的 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 包。 然后会显示使用包的示例。 对项目中使用的几乎每个 NuGet 包使用类似的工作流。

- [安装必备组件](#install-pre-requisites)
- [创建项目](#create-a-project)
- [添加 Newtonsoft.Json Nuget 包](#add-the-newtonsoftjson-nuget-package)
- [在应用中使用 Newtonsoft.Json API](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> **nuget.org 入门**：从 nuget.org 安装包是常见的工作流，.NET 开发人员使用此工作流查找可在自己的应用程序中重复使用的组件。 始终可以直接搜索 nuget.org 或根据本主题中的介绍，在 Visual Studio 中查找和安装包。

## <a name="install-pre-requisites"></a>安装必备组件

本教程需要具有适用于通用 Windows 应用的工具的 Visual Studio 2015 Update 3 或具有通用 Windows 平台开发工作负荷的 Visual Studio 2017。 如果已安装 Visual Studio，可再次运行安装程序以添加 UWP 工具。

可以从 [visualstudio.com](https://www.visualstudio.com/) 免费安装 Community 版，或者使用 Professional 或 Enterprise 版。 

## <a name="create-a-project"></a>创建项目

若要安装 NuGet 包，需要使用 Visual Studio 中某些基于 .NET 的项目。 在本演练中，可使用简单的 Windows Presentation Foundation (WPF) 或通用 Windows (UWP) 应用：

- 在 WPF (Windows 7+) 中，选择“文件”>“新建”>“项目”，展开“Visual C#”，选择“Windows 经典桌面”>“WPF 应用(.NET Framework)”，然后选择“确定”。
- 在 UWP (Windows 10) 中，请改用“Windows 通用”>“空白应用(通用 Windows)”。 出现提示时，接受“目标版本”和“最低版本”的默认值。

## <a name="add-the-newtonsoftjson-nuget-package"></a>添加 Newtonsoft.Json Nuget 包

1. 在解决方案资源管理器中，右键单击“引用”，选择“管理 NuGet 包”。

    ![管理项目引用的 NuGet 包命令](media/QS_Use-02-ManageNuGetPackages.png)

1. 将“nuget.org”选择为“包源”，选择“浏览”选项卡并搜索“Newtonsoft.Json”，在列表中选择该包，然后选择“安装”：

    ![定位 Newtonsoft.Json 包](media/QS_Use-03-NewtonsoftJson.png)

1. 如果系统提示选择包管理格式，请选择 PackageReference（推荐）或 `packages.config`：

    ![选择包引用格式](media/QS_Use-03b-SelectFormat.png)

1. 如果系统提示查看更改，请选择“确定”。

1. 在解决方案资源管理器中右键单击解决方案，然后选择“生成解决方案”。 此操作还原“引用”下列出的任何 NuGet 包。 有关更多详细信息，请参阅[包还原](../consume-packages/package-restore.md)。

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>在应用中使用 Newtonsoft.Json API

使用项目中的 Newtonsoft.Json 包，可调用 `JsonConvert.SerializeObject` 方法将对象转换为可人工读取的字符串。

1. 打开 `MainWindow.xaml` (WPF) 或 `MainPage.xaml` (UWP)，将现有 `Grid` 元素替换为以下内容：

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. 在解决方案资源管理器中展开 `MainWindow.xaml` (WPF) 或 `MainPage.xaml` (UWP) 节点，打开 `.cs` 文件，然后在 `MainWindow` 或 `MainPage` 类中的构造函数后插入以下代码：

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

1. 尽管已将 Newtonsoft.Json 包添加到项目中，`JsonConvert` 下仍出现红色波形曲线，因为需要使用 `using` 语句。 将鼠标悬停在有下划线的 `JsonConvert` 上方，将出现灯泡图标和“显示可能的修补程序”选项：

    ![灯泡图标和“显示可能的修补程序”命令](media/QS_Use-04-ShowPotentialFixes.png)


1. 单击“显示可能的修补程序”（或 灯泡图标），然后选择第一个推荐修补程序 `using Newtonsoft.Json;`。 此操作将必要的行添加到文件顶部。

    ![提供添加 using 语句选项的灯泡图标](media/QS_Use-05-AddUsing.png)

1. 若要生成并运行应用，请按 F5 或选择“调试”>“启动调试”（此处显示的是 UWP 中的操作；WPF 中的操作与之相似）：

    ![UWP 应用的初始输出](media/QS_Use-06-AppStart.png)

1. 选择按钮，查看替换为某些 JSON 文本的 TextBlock 的内容：

    ![选择按钮后 UWP 应用的输出](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a>相关主题

- [包使用的概述和工作流](../consume-packages/overview-and-workflow.md)
- [查找和选择包](../consume-packages/finding-and-choosing-packages.md)
- [配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)
