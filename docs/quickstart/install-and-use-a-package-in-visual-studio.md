---
title: 在 Visual Studio 中安装和使用 NuGet 包
description: 有关如何在 Visual Studio 项目中安装并使用 NuGet 包的演练教程。
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 96e138561390984d9def495ba5e091c43023cc92
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231326"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a><span data-ttu-id="9d8dc-103">快速入门：在 Visual Studio 中安装和使用包（仅适用于 Windows）</span><span class="sxs-lookup"><span data-stu-id="9d8dc-103">Quickstart: Install and use a package in Visual Studio (Windows only)</span></span>

<span data-ttu-id="9d8dc-104">NuGet 包包含其他开发人员提供的在项目中使用的可重用代码。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="9d8dc-105">请参阅[什么是 NuGet？](../What-is-NuGet.md)，了解背景信息。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="9d8dc-106">使用 NuGet 包管理器或包管理器控制台在 Visual Studio 项目中安装包。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-106">Packages are installed into a Visual Studio project using the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="9d8dc-107">本文介绍使用热门的 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 包和 Windows Presentation Foundation (WPF) 项目的过程。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Windows Presentation Foundation (WPF) project.</span></span> <span data-ttu-id="9d8dc-108">相同的过程适用于任何其他 .NET 或 .NET Core 项目。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="9d8dc-109">安装完成后，请引用具有 `using <namespace>` 的代码中的包，其中 \<namespace\> 特定于正在使用的包。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="9d8dc-110">建立引用后，可通过相应的 API 调用包。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="9d8dc-111">**nuget.org 入门**：为查找可在自己的应用程序中重用的组件，.NET 开发人员通常都会浏览 nuget.org  。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="9d8dc-112">可以直接搜索 nuget.org 或根据本文中的介绍，在 Visual Studio 中查找和安装包  。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="9d8dc-113">有关一般信息，请参阅[查找和评估 NuGet 包](../consume-packages/finding-and-choosing-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d8dc-114">先决条件</span><span class="sxs-lookup"><span data-stu-id="9d8dc-114">Prerequisites</span></span>

- <span data-ttu-id="9d8dc-115">Visual Studio 2019 .NET 桌面开发工作流。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-115">Visual Studio 2019 with the .NET Desktop Development workload.</span></span>

<span data-ttu-id="9d8dc-116">可以从 [visualstudio.com](https://www.visualstudio.com/) 免费安装 2019 Community 版，或者使用 Professional 或 Enterprise 版。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="9d8dc-117">如果使用的是 Visual Studio for Mac，请参阅[在 Visual Studio for Mac 中安装并使用包](install-and-use-a-package-in-visual-studio-mac.md)。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-117">If you're using Visual Studio for Mac, see [Install and use a package in Visual Studio for Mac](install-and-use-a-package-in-visual-studio-mac.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="9d8dc-118">创建项目</span><span class="sxs-lookup"><span data-stu-id="9d8dc-118">Create a project</span></span>

<span data-ttu-id="9d8dc-119">可将 NuGet 包安装到任何 .NET 项目，前提是包支持与项目相同的目标框架。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="9d8dc-120">本演练使用简单的 WPF 应用。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-120">For this walkthrough, use a simple WPF app.</span></span> <span data-ttu-id="9d8dc-121">使用以下方法在 Visual Studio 中创建项目：单击“文件” > “新建项目”，在搜索框中键入“.NET”，然后选择“WPF 应用(.NET Framework)”     。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-121">Create a project in Visual Studio using **File** > **New Project**, typing **.NET** in the search box, and then selecting the **WPF App (.NET Framework)**.</span></span> <span data-ttu-id="9d8dc-122">单击 **“下一步”** 。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-122">Click **Next**.</span></span> <span data-ttu-id="9d8dc-123">出现提示时，接受 Framework  的默认值。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-123">Accept the default values for **Framework** when prompted.</span></span>

<span data-ttu-id="9d8dc-124">Visual Studio 创建项目，该项目将在解决方案资源管理器中打开。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="9d8dc-125">添加 Newtonsoft.Json Nuget 包</span><span class="sxs-lookup"><span data-stu-id="9d8dc-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="9d8dc-126">若要安装此包，可以使用 NuGet 包管理器或包管理器控制台。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-126">To install the package, you can use either the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="9d8dc-127">安装包时，NuGet 会将依赖项记录在项目文件或 `packages.config` 文件中（具体位置取决于项目格式）。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-127">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="9d8dc-128">有关详细信息，请参阅[包使用概述和工作流](../consume-packages/Overview-and-Workflow.md)。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="9d8dc-129">NuGet 程序包管理器</span><span class="sxs-lookup"><span data-stu-id="9d8dc-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="9d8dc-130">在解决方案资源管理器中，右键单击“引用”，选择“管理 NuGet 包”   。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-130">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![管理项目引用的 NuGet 包命令](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="9d8dc-132">将“nuget.org”选择为“包源”，选择“浏览”选项卡并搜索“Newtonsoft.Json”，在列表中选择该包，然后选择“安装”     ：</span><span class="sxs-lookup"><span data-stu-id="9d8dc-132">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![定位 Newtonsoft.Json 包](media/QS_Use-03-NewtonsoftJson.png)

    <span data-ttu-id="9d8dc-134">若要了解有关 NuGet 包管理器的详细信息，请参阅[使用 Visual Studio 安装和管理包](../consume-packages/install-use-packages-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span></span>

1. <span data-ttu-id="9d8dc-135">接受任何许可证提示。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-135">Accept any license prompts.</span></span>

1. <span data-ttu-id="9d8dc-136">（仅适用于 Visual Studio 2017）如果系统提示选择包管理格式，请选择  “项目文件中的 PackageReference”：</span><span class="sxs-lookup"><span data-stu-id="9d8dc-136">(Visual Studio 2017 only) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![选择包管理格式](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="9d8dc-138">如果系统提示查看更改，请选择“确定”  。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-138">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="9d8dc-139">程序包管理器控制台</span><span class="sxs-lookup"><span data-stu-id="9d8dc-139">Package Manager Console</span></span>

1. <span data-ttu-id="9d8dc-140">选择“工具” > “NuGet 包管理器” > “包管理器控制台”菜单命令    。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-140">Select the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="9d8dc-141">控制台打开后，检查  “默认项目”下拉列表中是否显示在程序包中要安装的项目。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-141">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="9d8dc-142">如果在解决方案中有一个项目，则它已被选中。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-142">If you have a single project in the solution, it is already selected.</span></span>

    ![定位 Newtonsoft.Json 包](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="9d8dc-144">输入命令 `Install-Package Newtonsoft.Json`（请参阅 [Install-Package](../reference/ps-reference/ps-ref-install-package.md)）。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-144">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="9d8dc-145">控制台窗口会显示该命令的输出。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-145">The console window shows output for the command.</span></span> <span data-ttu-id="9d8dc-146">错误通常指示程序包与项目的目标框架不兼容。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-146">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

   <span data-ttu-id="9d8dc-147">若要了解有关包管理器控制台的详细信息，请参阅[使用包管理器控制台安装和管理包](../consume-packages/install-use-packages-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-147">If you want more information on the Package Manager Console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="9d8dc-148">在应用中使用 Newtonsoft.Json API</span><span class="sxs-lookup"><span data-stu-id="9d8dc-148">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="9d8dc-149">使用项目中的 Newtonsoft.Json 包，可调用 `JsonConvert.SerializeObject` 方法将对象转换为可人工读取的字符串。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-149">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="9d8dc-150">打开 `MainWindow.xaml` 并将现有 `Grid` 元素替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="9d8dc-150">Open `MainWindow.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="9d8dc-151">打开 `MainWindow.xaml.cs` 文件（位于 `MainWindow.xaml` 节点下的解决方案资源管理器中），然后在 `MainWindow` 类中插入以下代码：</span><span class="sxs-lookup"><span data-stu-id="9d8dc-151">Open the `MainWindow.xaml.cs` file (located in Solution Explorer under the `MainWindow.xaml` node), and insert the following code inside the `MainWindow` class:</span></span>

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

1. <span data-ttu-id="9d8dc-152">尽管已将 Newtonsoft.Json 包添加到项目中，因为你需要使用代码文件最上方的 `using` 语句，所以 `JsonConvert` 下仍会出现红色波形曲线：</span><span class="sxs-lookup"><span data-stu-id="9d8dc-152">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="9d8dc-153">要构建并运行应用，请按 F5 或选择“调试” > “启动调试”   ：</span><span class="sxs-lookup"><span data-stu-id="9d8dc-153">Build and run the app by pressing F5 or selecting **Debug** > **Start Debugging**:</span></span>

    ![WPF 应用的初始输出](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="9d8dc-155">选择按钮，查看替换为某些 JSON 文本的 TextBlock 的内容：</span><span class="sxs-lookup"><span data-stu-id="9d8dc-155">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![选择按钮后 WPF 应用的输出](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a><span data-ttu-id="9d8dc-157">相关视频</span><span class="sxs-lookup"><span data-stu-id="9d8dc-157">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

<span data-ttu-id="9d8dc-158">在[第 9 频道](https://channel9.msdn.com/Series/NuGet-101)和 [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_) 上查找更多 NuGet 视频。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-158">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d8dc-159">后续步骤</span><span class="sxs-lookup"><span data-stu-id="9d8dc-159">Next steps</span></span>

<span data-ttu-id="9d8dc-160">祝贺你安装并使用第一个 NuGet 包！</span><span class="sxs-lookup"><span data-stu-id="9d8dc-160">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9d8dc-161">使用 Visual Studio 安装和管理包</span><span class="sxs-lookup"><span data-stu-id="9d8dc-161">Install and manage packages using Visual Studio</span></span>](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="9d8dc-162">使用包管理器控制台安装和管理包</span><span class="sxs-lookup"><span data-stu-id="9d8dc-162">Install and manage packages using Package Manager Console</span></span>](../consume-packages/install-use-packages-powershell.md)

<span data-ttu-id="9d8dc-163">若要了解更多 NuGet 产品，请选择以下链接。</span><span class="sxs-lookup"><span data-stu-id="9d8dc-163">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="9d8dc-164">包使用的概述和工作流</span><span class="sxs-lookup"><span data-stu-id="9d8dc-164">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="9d8dc-165">查找和选择包</span><span class="sxs-lookup"><span data-stu-id="9d8dc-165">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="9d8dc-166">项目文件中的包引用</span><span class="sxs-lookup"><span data-stu-id="9d8dc-166">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
