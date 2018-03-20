---
title: "从 Visual Studio 中使用 NuGet 包的介绍性指南 | Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "有关如何在 Visual Studio 项目中安装并使用 NuGet 包的演练教程。"
keywords: "安装 NuGet, NuGet包使用, 安装 NuGet 包, NuGet 包引用, 使用 NuGet 包"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ff905fec6d6af4fa40fd4331cb970121b6eb0879
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="817df-104">在 Visual Studio 中安装和使用包</span><span class="sxs-lookup"><span data-stu-id="817df-104">Install and use a package in Visual Studio</span></span>

<span data-ttu-id="817df-105">NuGet 包包含其他开发人员提供的在项目中使用的可重用代码。</span><span class="sxs-lookup"><span data-stu-id="817df-105">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="817df-106">请参阅[什么是 NuGet？](../What-is-NuGet.md)，了解背景信息。</span><span class="sxs-lookup"><span data-stu-id="817df-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="817df-107">如本文中针对流行的 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 包和通用 Windows 平台 (UWP) 项目的内容所述，使用程序包管理器 UI 或程序包管理器控制台将程序包安装到 Visual Studio 项目中。</span><span class="sxs-lookup"><span data-stu-id="817df-107">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console, as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span>

<span data-ttu-id="817df-108">安装完成后，请引用具有 `using <namespace>` 的代码中的包，其中 \<namespace\> 特定于正在使用的包。</span><span class="sxs-lookup"><span data-stu-id="817df-108">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="817df-109">建立引用后，可通过相应的 API 调用包。</span><span class="sxs-lookup"><span data-stu-id="817df-109">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="817df-110">**nuget.org 入门**：浏览 nuget.org 是 .NET 开发人员通常在自己的应用程序中查找可重用组件的方式。</span><span class="sxs-lookup"><span data-stu-id="817df-110">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="817df-111">你可以直接搜索 nuget.org 或根据本文中的介绍，在 Visual Studio 中查找和安装包。</span><span class="sxs-lookup"><span data-stu-id="817df-111">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="817df-112">系统必备</span><span class="sxs-lookup"><span data-stu-id="817df-112">Prerequisites</span></span>

- <span data-ttu-id="817df-113">具有通用 Windows 平台开发工作负载的 Visual Studio 2017，或</span><span class="sxs-lookup"><span data-stu-id="817df-113">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="817df-114">适用于通用 Windows 应用的 Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="817df-114">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="817df-115">可以从 [visualstudio.com](https://www.visualstudio.com/) 免费安装 2017 Community 版，或者使用 Professional 或 Enterprise 版。</span><span class="sxs-lookup"><span data-stu-id="817df-115">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="817df-116">创建项目</span><span class="sxs-lookup"><span data-stu-id="817df-116">Create a project</span></span>

<span data-ttu-id="817df-117">可以将 NuGet 包安装到某种类型的 .NET 项目。</span><span class="sxs-lookup"><span data-stu-id="817df-117">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="817df-118">对于本演练，将使用简单的通用 Windows (UWP) 应用。</span><span class="sxs-lookup"><span data-stu-id="817df-118">For this walkthrough, you use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="817df-119">要在 Visual Studio 中创建项目，请使用“文件 > 新建项目...”，然后选择“Windows 通用 > 空白应用(通用 Windows)”。</span><span class="sxs-lookup"><span data-stu-id="817df-119">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="817df-120">出现提示时，接受“目标版本”和“最低版本”的默认值。</span><span class="sxs-lookup"><span data-stu-id="817df-120">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="817df-121">添加 Newtonsoft.Json Nuget 包</span><span class="sxs-lookup"><span data-stu-id="817df-121">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="817df-122">若要安装此程序包，可以使用程序包管理器 UI 或程序包管理器控制台。</span><span class="sxs-lookup"><span data-stu-id="817df-122">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="817df-123">安装包时，NuGet 会将依赖项记录在项目文件或 `packages.config` 文件中。</span><span class="sxs-lookup"><span data-stu-id="817df-123">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file.</span></span> <span data-ttu-id="817df-124">有关详细信息，请参阅[包使用概述和工作流](../consume-packages/Overview-and-Workflow.md)。</span><span class="sxs-lookup"><span data-stu-id="817df-124">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="817df-125">包管理器 UI</span><span class="sxs-lookup"><span data-stu-id="817df-125">Package Manager UI</span></span>

1. <span data-ttu-id="817df-126">在解决方案资源管理器中，右键单击“引用”，选择“管理 NuGet 包”。</span><span class="sxs-lookup"><span data-stu-id="817df-126">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![管理项目引用的 NuGet 包命令](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="817df-128">将“nuget.org”选择为“包源”，选择“浏览”选项卡并搜索“Newtonsoft.Json”，在列表中选择该包，然后选择“安装”：</span><span class="sxs-lookup"><span data-stu-id="817df-128">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![定位 Newtonsoft.Json 包](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="817df-130">接受任何许可证提示。</span><span class="sxs-lookup"><span data-stu-id="817df-130">Accept any license prompts.</span></span>

1. <span data-ttu-id="817df-131">(Visual Studio 2017) 如果系统提示选择程序包管理格式，请选择“项目文件中的 PackageReference”：</span><span class="sxs-lookup"><span data-stu-id="817df-131">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![选择包引用格式](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="817df-133">如果系统提示查看更改，请选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="817df-133">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="817df-134">程序包管理器控制台</span><span class="sxs-lookup"><span data-stu-id="817df-134">Package Manager Console</span></span>

1. <span data-ttu-id="817df-135">选择“工具”>“NuGet 包管理器”>“程序包管理器控制台”菜单命令。</span><span class="sxs-lookup"><span data-stu-id="817df-135">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="817df-136">控制台打开后，检查“默认项目”下拉列表中是否显示在程序包中要安装的项目。</span><span class="sxs-lookup"><span data-stu-id="817df-136">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="817df-137">如果在解决方案中有一个项目，则它已被选中。</span><span class="sxs-lookup"><span data-stu-id="817df-137">If you have a single project in the solution, it is already selected.</span></span>

    ![定位 Newtonsoft.Json 包](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="817df-139">输入命令 `Install-Package Newtonsoft.json`（请参阅 [Install-Package](../tools/ps-ref-install-package.md)）。</span><span class="sxs-lookup"><span data-stu-id="817df-139">Enter the command `Install-Package Newtonsoft.json` (see [Install-Package](../tools/ps-ref-install-package.md)).</span></span> <span data-ttu-id="817df-140">控制台窗口会显示该命令的输出。</span><span class="sxs-lookup"><span data-stu-id="817df-140">The console window shows output for the command.</span></span> <span data-ttu-id="817df-141">错误通常指示程序包与项目的目标框架不兼容。</span><span class="sxs-lookup"><span data-stu-id="817df-141">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="817df-142">在应用中使用 Newtonsoft.Json API</span><span class="sxs-lookup"><span data-stu-id="817df-142">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="817df-143">使用项目中的 Newtonsoft.Json 包，可调用 `JsonConvert.SerializeObject` 方法将对象转换为可人工读取的字符串。</span><span class="sxs-lookup"><span data-stu-id="817df-143">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="817df-144">打开 `MainPage.xaml` 并将现有 `Grid` 元素替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="817df-144">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="817df-145">打开 `MainPage.xaml.cs` 文件（位于 `MainPage.xaml` 节点下的解决方案资源管理器中），然后在 `MainPage` 构造函数中插入以下代码：</span><span class="sxs-lookup"><span data-stu-id="817df-145">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

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

1. <span data-ttu-id="817df-146">尽管已将 Newtonsoft.Json 包添加到项目中，因为你需要使用代码文件最上方的 `using` 语句，所以 `JsonConvert` 下仍会出现红色波形曲线：</span><span class="sxs-lookup"><span data-stu-id="817df-146">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.json;
    ```

1. <span data-ttu-id="817df-147">若要生成并运行应用，请按 F5 或选择“调试”>“启动调试”：</span><span class="sxs-lookup"><span data-stu-id="817df-147">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![UWP 应用的初始输出](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="817df-149">选择按钮，查看替换为某些 JSON 文本的 TextBlock 的内容：</span><span class="sxs-lookup"><span data-stu-id="817df-149">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![选择按钮后 UWP 应用的输出](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a><span data-ttu-id="817df-151">相关文章</span><span class="sxs-lookup"><span data-stu-id="817df-151">Related articles</span></span>

- [<span data-ttu-id="817df-152">包使用的概述和工作流</span><span class="sxs-lookup"><span data-stu-id="817df-152">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="817df-153">查找和选择包</span><span class="sxs-lookup"><span data-stu-id="817df-153">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="817df-154">安装包的方式</span><span class="sxs-lookup"><span data-stu-id="817df-154">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="817df-155">配置 NuGet 行为</span><span class="sxs-lookup"><span data-stu-id="817df-155">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
