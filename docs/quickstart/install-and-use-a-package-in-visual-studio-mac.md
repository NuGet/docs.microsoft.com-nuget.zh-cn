---
title: 在 Visual Studio for Mac 中安装和使用 NuGet 包
description: 有关如何在 Visual Studio for Mac 项目中安装并使用 NuGet 包的演练教程。
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238473"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a>快速入门：在 Visual Studio for Mac 中安装和使用包

NuGet 包包含其他开发人员提供的在项目中使用的可重用代码。 请参阅[什么是 NuGet？](../What-is-NuGet.md)，了解背景信息。 使用 NuGet 包管理器在 Visual Studio for Mac 项目中安装包。 本文介绍使用热门的 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 包和 .NET Core 控制台项目的过程。 相同的过程适用于任何其他 Xamarin 或 .NET Core 项目。

安装完成后，请引用具有 `using <namespace>` 的代码中的包，其中 \<namespace\> 特定于正在使用的包。 建立引用后，可通过相应的 API 调用包。

> [!Tip]
> **nuget.org 入门**：为查找可在自己的应用程序中重用的组件，.NET 开发人员通常都会浏览 nuget.org  。 可以直接搜索 nuget.org 或根据本文中的介绍，在 Visual Studio 中查找和安装包  。 有关一般信息，请参阅[查找和评估 NuGet 包](../consume-packages/finding-and-choosing-packages.md)。

## <a name="prerequisites"></a>先决条件

- Visual Studio 2019 for Mac。

可以从 [visualstudio.com](https://www.visualstudio.com/) 免费安装 2019 Community 版，或者使用 Professional 或 Enterprise 版。

如果是在 Windows 上使用 Visual Studio，请参阅[在 Visual Studio 中安装并使用包（仅适用于 Windows）](install-and-use-a-package-in-visual-studio.md)。

## <a name="create-a-project"></a>创建项目

可将 NuGet 包安装到任何 .NET 项目，前提是包支持与项目相同的目标框架。

本演练使用简单的 .NET Core 控制台应用。 通过以下方式在 Visual Studio for Mac 中创建项目：选择“文件”>“新建解决方案...”，然后选择“.NET Core”>“应用”>“控制台应用程序”模板   。 单击 **“下一步”** 。 出现提示时，接受“目标框架”  的默认值。

Visual Studio 创建项目，该项目将在解决方案资源管理器中打开。

## <a name="add-the-newtonsoftjson-nuget-package"></a>添加 Newtonsoft.Json Nuget 包

若要安装此包，请使用 NuGet 包管理器。 安装包时，NuGet 会将依赖项记录在项目文件或 `packages.config` 文件中（具体位置取决于项目格式）。 有关详细信息，请参阅[包使用概述和工作流](../consume-packages/Overview-and-Workflow.md)。

### <a name="nuget-package-manager"></a>NuGet 程序包管理器

1. 在解决方案资源管理器中，右键单击“依赖项”，然后选择“添加包...”   。

    ![管理项目引用的 NuGet 包命令](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. 在对话框的左上角，选择“nuget.org”作为“包源”，并搜索“Newtonsoft.Json”，在列表中选择该包，然后选择“添加包...”    ：

    ![定位 Newtonsoft.Json 包](media/QS_Use_Mac-03-NewtonsoftJson.png)

    若要了解有关 NuGet 包管理器的详细信息，请参阅[使用 Visual Studio for Mac 安装和管理包](../consume-packages/install-use-packages-visual-studio.md)。

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>在应用中使用 Newtonsoft.Json API

使用项目中的 Newtonsoft.Json 包，可调用 `JsonConvert.SerializeObject` 方法将对象转换为可人工读取的字符串。

1. 打开 `Program.cs` 文件（位于 Solution Pad 中），然后使用以下代码替换文件内容：

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. 选择“运行”>“开始调试”，生成和运行应用  ：

1. 应用运行后，你将看到控制台中显示的序列化的 JSON 输出：

  ![控制台应用的输出](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a>后续步骤
祝贺你安装并使用第一个 NuGet 包！

> [!div class="nextstepaction"]
> [使用 Visual Studio for Mac 安装和管理包](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

若要了解更多 NuGet 产品，请选择以下链接。

- [包使用的概述和工作流](../consume-packages/overview-and-workflow.md)
- [项目文件中的包引用](../consume-packages/package-references-in-project-files.md)
