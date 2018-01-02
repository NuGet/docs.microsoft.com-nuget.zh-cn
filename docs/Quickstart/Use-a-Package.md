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
ms.openlocfilehash: bcccc7139de31a8d07e9ed52abfd12fe9e6d687b
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="install-and-use-a-package"></a><span data-ttu-id="e71f0-104">安装并使用包</span><span class="sxs-lookup"><span data-stu-id="e71f0-104">Install and use a package</span></span>

[!INCLUDE [install-methods](../includes/install-methods.md)]

<span data-ttu-id="e71f0-105">安装完成后，请引用具有 `using <namespace>` 的代码中的包，其中 \<namespace\> 特定于正在使用的包。</span><span class="sxs-lookup"><span data-stu-id="e71f0-105">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="e71f0-106">建立引用后，可通过相应的 API 调用包。</span><span class="sxs-lookup"><span data-stu-id="e71f0-106">Once the reference is made, you can call the package through its API.</span></span>

<span data-ttu-id="e71f0-107">本主题的其余部分介绍如何使用包管理器 UI 在通用 Windows 平台 (UWP) 项目中安装常用的 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 包。</span><span class="sxs-lookup"><span data-stu-id="e71f0-107">The remainder of this topic walks through the process of using the Package Manager UI to install the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package in a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="e71f0-108">然后会显示使用包的示例。</span><span class="sxs-lookup"><span data-stu-id="e71f0-108">It then shows an example of using the package.</span></span> <span data-ttu-id="e71f0-109">对项目中使用的几乎每个 NuGet 包使用类似的工作流。</span><span class="sxs-lookup"><span data-stu-id="e71f0-109">You use a similar same workflow for virtually every NuGet package you use in a project.</span></span>

- [<span data-ttu-id="e71f0-110">安装必备组件</span><span class="sxs-lookup"><span data-stu-id="e71f0-110">Install pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="e71f0-111">创建项目</span><span class="sxs-lookup"><span data-stu-id="e71f0-111">Create a project</span></span>](#create-a-project)
- [<span data-ttu-id="e71f0-112">添加 Newtonsoft.Json Nuget 包</span><span class="sxs-lookup"><span data-stu-id="e71f0-112">Add the Newtonsoft.Json NuGet package</span></span>](#add-the-newtonsoftjson-nuget-package)
- [<span data-ttu-id="e71f0-113">在应用中使用 Newtonsoft.Json API</span><span class="sxs-lookup"><span data-stu-id="e71f0-113">Use the Newtonsoft.Json API in the app</span></span>](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> <span data-ttu-id="e71f0-114">**nuget.org 入门**：从 nuget.org 安装包是常见的工作流，.NET 开发人员使用此工作流查找可在自己的应用程序中重复使用的组件。</span><span class="sxs-lookup"><span data-stu-id="e71f0-114">**Start with nuget.org**: Installing packages from nuget.org is a common workflow that .NET developers use to find components they can reuse in their own applications.</span></span> <span data-ttu-id="e71f0-115">始终可以直接搜索 nuget.org 或根据本主题中的介绍，在 Visual Studio 中查找和安装包。</span><span class="sxs-lookup"><span data-stu-id="e71f0-115">You can always search nuget.org directly or find and install packages within Visual Studio as shown in this topic.</span></span>

## <a name="install-pre-requisites"></a><span data-ttu-id="e71f0-116">安装必备组件</span><span class="sxs-lookup"><span data-stu-id="e71f0-116">Install pre-requisites</span></span>

<span data-ttu-id="e71f0-117">本教程需要具有适用于通用 Windows 应用的工具的 Visual Studio 2015 Update 3 或具有通用 Windows 平台开发工作负荷的 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="e71f0-117">This tutorial requires Visual Studio 2015 Update 3 with Tools for Universal Windows Apps, or Visual Studio 2017 with the Universal Windows Platform development workload.</span></span> <span data-ttu-id="e71f0-118">如果已安装 Visual Studio，可再次运行安装程序以添加 UWP 工具。</span><span class="sxs-lookup"><span data-stu-id="e71f0-118">If you already have Visual Studio installed, you can run the installer again to add the UWP tools.</span></span>

<span data-ttu-id="e71f0-119">可以从 [visualstudio.com](https://www.visualstudio.com/) 免费安装 Community 版，或者使用 Professional 或 Enterprise 版。</span><span class="sxs-lookup"><span data-stu-id="e71f0-119">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span> 

## <a name="create-a-project"></a><span data-ttu-id="e71f0-120">创建项目</span><span class="sxs-lookup"><span data-stu-id="e71f0-120">Create a project</span></span>

<span data-ttu-id="e71f0-121">若要安装 NuGet 包，需要使用 Visual Studio 中某些基于 .NET 的项目。</span><span class="sxs-lookup"><span data-stu-id="e71f0-121">To install a NuGet package, you need some kind of .NET-based project in Visual Studio.</span></span> <span data-ttu-id="e71f0-122">在本演练中，可使用简单的 Windows Presentation Foundation (WPF) 或通用 Windows (UWP) 应用：</span><span class="sxs-lookup"><span data-stu-id="e71f0-122">For this walkthrough, you can use use a simple Windows Presentation Foundation (WPF) or Universal Windows (UWP) app:</span></span>

- <span data-ttu-id="e71f0-123">在 WPF (Windows 7+) 中，选择“文件”>“新建”>“项目”，展开“Visual C#”，选择“Windows 经典桌面”>“WPF 应用(.NET Framework)”，然后选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="e71f0-123">For WPF (Windows 7+), choose **File > New > Project**, expand **Visual C#**, select **Windows Classic Desktop > WPF App (.NET Framework)**, and select **OK**.</span></span>
- <span data-ttu-id="e71f0-124">在 UWP (Windows 10) 中，请改用“Windows 通用”>“空白应用(通用 Windows)”。</span><span class="sxs-lookup"><span data-stu-id="e71f0-124">For UWP (Windows 10), use the **Windows Universal > Blank App (Universal Windows)** instead.</span></span> <span data-ttu-id="e71f0-125">出现提示时，接受“目标版本”和“最低版本”的默认值。</span><span class="sxs-lookup"><span data-stu-id="e71f0-125">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="e71f0-126">添加 Newtonsoft.Json Nuget 包</span><span class="sxs-lookup"><span data-stu-id="e71f0-126">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="e71f0-127">在解决方案资源管理器中，右键单击“引用”，选择“管理 NuGet 包”。</span><span class="sxs-lookup"><span data-stu-id="e71f0-127">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![管理项目引用的 NuGet 包命令](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="e71f0-129">将“nuget.org”选择为“包源”，选择“浏览”选项卡并搜索“Newtonsoft.Json”，在列表中选择该包，然后选择“安装”：</span><span class="sxs-lookup"><span data-stu-id="e71f0-129">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![定位 Newtonsoft.Json 包](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="e71f0-131">如果系统提示选择包管理格式，请选择 PackageReference（推荐）或 `packages.config`：</span><span class="sxs-lookup"><span data-stu-id="e71f0-131">If prompted to select a package management format, choose between PackageReference (recommended) and `packages.config`:</span></span>

    ![选择包引用格式](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="e71f0-133">如果系统提示查看更改，请选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="e71f0-133">If prompted to review changes, select **OK**.</span></span>

1. <span data-ttu-id="e71f0-134">在解决方案资源管理器中右键单击解决方案，然后选择“生成解决方案”。</span><span class="sxs-lookup"><span data-stu-id="e71f0-134">Right-click the solution in Solution Explorer and select **Build Solution**.</span></span> <span data-ttu-id="e71f0-135">此操作还原“引用”下列出的任何 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="e71f0-135">This restores any NuGet packages listed under **References**.</span></span> <span data-ttu-id="e71f0-136">有关更多详细信息，请参阅[包还原](../consume-packages/package-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="e71f0-136">For more details, see [Package Restore](../consume-packages/package-restore.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="e71f0-137">在应用中使用 Newtonsoft.Json API</span><span class="sxs-lookup"><span data-stu-id="e71f0-137">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="e71f0-138">使用项目中的 Newtonsoft.Json 包，可调用 `JsonConvert.SerializeObject` 方法将对象转换为可人工读取的字符串。</span><span class="sxs-lookup"><span data-stu-id="e71f0-138">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="e71f0-139">打开 `MainWindow.xaml` (WPF) 或 `MainPage.xaml` (UWP)，将现有 `Grid` 元素替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="e71f0-139">Open `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="e71f0-140">在解决方案资源管理器中展开 `MainWindow.xaml` (WPF) 或 `MainPage.xaml` (UWP) 节点，打开 `.cs` 文件，然后在 `MainWindow` 或 `MainPage` 类中的构造函数后插入以下代码：</span><span class="sxs-lookup"><span data-stu-id="e71f0-140">Expand the `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) node in Solution Explorer, open the `.cs` file, and insert the following code inside the `MainWindow` or `MainPage` class, after the constructor:</span></span>

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

1. <span data-ttu-id="e71f0-141">尽管已将 Newtonsoft.Json 包添加到项目中，`JsonConvert` 下仍出现红色波形曲线，因为需要使用 `using` 语句。</span><span class="sxs-lookup"><span data-stu-id="e71f0-141">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement.</span></span> <span data-ttu-id="e71f0-142">将鼠标悬停在有下划线的 `JsonConvert` 上方，将出现灯泡图标和“显示可能的修补程序”选项：</span><span class="sxs-lookup"><span data-stu-id="e71f0-142">Hover over the underlined `JsonConvert` and you'll see the Lightbulb and the option to **Show potential fixes**:</span></span>

    ![灯泡图标和“显示可能的修补程序”命令](media/QS_Use-04-ShowPotentialFixes.png)


1. <span data-ttu-id="e71f0-144">单击“显示可能的修补程序”（或 灯泡图标），然后选择第一个推荐修补程序 `using Newtonsoft.Json;`。</span><span class="sxs-lookup"><span data-stu-id="e71f0-144">Click on **Show potential fixes** (or the Lightbulb) and select the first suggested fix, `using Newtonsoft.Json;`.</span></span> <span data-ttu-id="e71f0-145">此操作将必要的行添加到文件顶部。</span><span class="sxs-lookup"><span data-stu-id="e71f0-145">This adds the necessary line to the top of the file.</span></span>

    ![提供添加 using 语句选项的灯泡图标](media/QS_Use-05-AddUsing.png)

1. <span data-ttu-id="e71f0-147">若要生成并运行应用，请按 F5 或选择“调试”>“启动调试”（此处显示的是 UWP 中的操作；WPF 中的操作与之相似）：</span><span class="sxs-lookup"><span data-stu-id="e71f0-147">Build and run the app by pressing F5 or selecting **Debug > Start Debugging** (UWP shown here; WPF is similar):</span></span>

    ![UWP 应用的初始输出](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="e71f0-149">选择按钮，查看替换为某些 JSON 文本的 TextBlock 的内容：</span><span class="sxs-lookup"><span data-stu-id="e71f0-149">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![选择按钮后 UWP 应用的输出](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a><span data-ttu-id="e71f0-151">相关主题</span><span class="sxs-lookup"><span data-stu-id="e71f0-151">Related topics</span></span>

- [<span data-ttu-id="e71f0-152">包使用的概述和工作流</span><span class="sxs-lookup"><span data-stu-id="e71f0-152">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="e71f0-153">查找和选择包</span><span class="sxs-lookup"><span data-stu-id="e71f0-153">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="e71f0-154">配置 NuGet 行为</span><span class="sxs-lookup"><span data-stu-id="e71f0-154">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
