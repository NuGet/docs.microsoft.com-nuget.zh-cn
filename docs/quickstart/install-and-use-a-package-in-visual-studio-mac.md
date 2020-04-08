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
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a><span data-ttu-id="077bd-103">快速入门：在 Visual Studio for Mac 中安装和使用包</span><span class="sxs-lookup"><span data-stu-id="077bd-103">Quickstart: Install and use a package in Visual Studio for Mac</span></span>

<span data-ttu-id="077bd-104">NuGet 包包含其他开发人员提供的在项目中使用的可重用代码。</span><span class="sxs-lookup"><span data-stu-id="077bd-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="077bd-105">请参阅[什么是 NuGet？](../What-is-NuGet.md)，了解背景信息。</span><span class="sxs-lookup"><span data-stu-id="077bd-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="077bd-106">使用 NuGet 包管理器在 Visual Studio for Mac 项目中安装包。</span><span class="sxs-lookup"><span data-stu-id="077bd-106">Packages are installed into a Visual Studio for Mac project using the NuGet Package Manager.</span></span> <span data-ttu-id="077bd-107">本文介绍使用热门的 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 包和 .NET Core 控制台项目的过程。</span><span class="sxs-lookup"><span data-stu-id="077bd-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a .NET Core console project.</span></span> <span data-ttu-id="077bd-108">相同的过程适用于任何其他 Xamarin 或 .NET Core 项目。</span><span class="sxs-lookup"><span data-stu-id="077bd-108">The same process applies to any other Xamarin or .NET Core project.</span></span>

<span data-ttu-id="077bd-109">安装完成后，请引用具有 `using <namespace>` 的代码中的包，其中 \<namespace\> 特定于正在使用的包。</span><span class="sxs-lookup"><span data-stu-id="077bd-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="077bd-110">建立引用后，可通过相应的 API 调用包。</span><span class="sxs-lookup"><span data-stu-id="077bd-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="077bd-111">**nuget.org 入门**：为查找可在自己的应用程序中重用的组件，.NET 开发人员通常都会浏览 nuget.org  。</span><span class="sxs-lookup"><span data-stu-id="077bd-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="077bd-112">可以直接搜索 nuget.org 或根据本文中的介绍，在 Visual Studio 中查找和安装包  。</span><span class="sxs-lookup"><span data-stu-id="077bd-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="077bd-113">有关一般信息，请参阅[查找和评估 NuGet 包](../consume-packages/finding-and-choosing-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="077bd-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="077bd-114">先决条件</span><span class="sxs-lookup"><span data-stu-id="077bd-114">Prerequisites</span></span>

- <span data-ttu-id="077bd-115">Visual Studio 2019 for Mac。</span><span class="sxs-lookup"><span data-stu-id="077bd-115">Visual Studio 2019 for Mac.</span></span>

<span data-ttu-id="077bd-116">可以从 [visualstudio.com](https://www.visualstudio.com/) 免费安装 2019 Community 版，或者使用 Professional 或 Enterprise 版。</span><span class="sxs-lookup"><span data-stu-id="077bd-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="077bd-117">如果是在 Windows 上使用 Visual Studio，请参阅[在 Visual Studio 中安装并使用包（仅适用于 Windows）](install-and-use-a-package-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="077bd-117">If you're using Visual Studio on Windows, see [Install and use a package in Visual Studio (Windows Only)](install-and-use-a-package-in-visual-studio.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="077bd-118">创建项目</span><span class="sxs-lookup"><span data-stu-id="077bd-118">Create a project</span></span>

<span data-ttu-id="077bd-119">可将 NuGet 包安装到任何 .NET 项目，前提是包支持与项目相同的目标框架。</span><span class="sxs-lookup"><span data-stu-id="077bd-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="077bd-120">本演练使用简单的 .NET Core 控制台应用。</span><span class="sxs-lookup"><span data-stu-id="077bd-120">For this walkthrough, use a simple .NET Core Console app.</span></span> <span data-ttu-id="077bd-121">通过以下方式在 Visual Studio for Mac 中创建项目：选择“文件”>“新建解决方案...”，然后选择“.NET Core”>“应用”>“控制台应用程序”模板   。</span><span class="sxs-lookup"><span data-stu-id="077bd-121">Create a project in Visual Studio for Mac using **File > New Solution...**, select the **.NET Core > App > Console Application** template.</span></span> <span data-ttu-id="077bd-122">单击 **“下一步”** 。</span><span class="sxs-lookup"><span data-stu-id="077bd-122">Click **Next**.</span></span> <span data-ttu-id="077bd-123">出现提示时，接受“目标框架”  的默认值。</span><span class="sxs-lookup"><span data-stu-id="077bd-123">Accept the default values for **Target Framework** when prompted.</span></span>

<span data-ttu-id="077bd-124">Visual Studio 创建项目，该项目将在解决方案资源管理器中打开。</span><span class="sxs-lookup"><span data-stu-id="077bd-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="077bd-125">添加 Newtonsoft.Json Nuget 包</span><span class="sxs-lookup"><span data-stu-id="077bd-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="077bd-126">若要安装此包，请使用 NuGet 包管理器。</span><span class="sxs-lookup"><span data-stu-id="077bd-126">To install the package, you use the NuGet Package Manager.</span></span> <span data-ttu-id="077bd-127">安装包时，NuGet 会将依赖项记录在项目文件或 `packages.config` 文件中（具体位置取决于项目格式）。</span><span class="sxs-lookup"><span data-stu-id="077bd-127">When you install a package, NuGet records the dependency in  either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="077bd-128">有关详细信息，请参阅[包使用概述和工作流](../consume-packages/Overview-and-Workflow.md)。</span><span class="sxs-lookup"><span data-stu-id="077bd-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="077bd-129">NuGet 程序包管理器</span><span class="sxs-lookup"><span data-stu-id="077bd-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="077bd-130">在解决方案资源管理器中，右键单击“依赖项”，然后选择“添加包...”   。</span><span class="sxs-lookup"><span data-stu-id="077bd-130">In Solution Explorer, right-click **Dependencies** and choose **Add Packages...**.</span></span>

    ![管理项目引用的 NuGet 包命令](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. <span data-ttu-id="077bd-132">在对话框的左上角，选择“nuget.org”作为“包源”，并搜索“Newtonsoft.Json”，在列表中选择该包，然后选择“添加包...”    ：</span><span class="sxs-lookup"><span data-stu-id="077bd-132">Choose "nuget.org" as the **Package source** in the top left corner of the dialog, and search for **Newtonsoft.Json**, select that package in the list, and select **Add Packages...**:</span></span>

    ![定位 Newtonsoft.Json 包](media/QS_Use_Mac-03-NewtonsoftJson.png)

    <span data-ttu-id="077bd-134">若要了解有关 NuGet 包管理器的详细信息，请参阅[使用 Visual Studio for Mac 安装和管理包](../consume-packages/install-use-packages-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="077bd-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio for Mac](../consume-packages/install-use-packages-visual-studio.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="077bd-135">在应用中使用 Newtonsoft.Json API</span><span class="sxs-lookup"><span data-stu-id="077bd-135">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="077bd-136">使用项目中的 Newtonsoft.Json 包，可调用 `JsonConvert.SerializeObject` 方法将对象转换为可人工读取的字符串。</span><span class="sxs-lookup"><span data-stu-id="077bd-136">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="077bd-137">打开 `Program.cs` 文件（位于 Solution Pad 中），然后使用以下代码替换文件内容：</span><span class="sxs-lookup"><span data-stu-id="077bd-137">Open the `Program.cs` file (located in the Solution Pad) and replace the file contents with the following code:</span></span>

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

1. <span data-ttu-id="077bd-138">选择“运行”>“开始调试”，生成和运行应用  ：</span><span class="sxs-lookup"><span data-stu-id="077bd-138">Build and run the app by selecting **Run > Start Debugging**:</span></span>

1. <span data-ttu-id="077bd-139">应用运行后，你将看到控制台中显示的序列化的 JSON 输出：</span><span class="sxs-lookup"><span data-stu-id="077bd-139">Once the app runs, you'll see the serialized JSON output appear in the console:</span></span>

  ![控制台应用的输出](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a><span data-ttu-id="077bd-141">后续步骤</span><span class="sxs-lookup"><span data-stu-id="077bd-141">Next steps</span></span>
<span data-ttu-id="077bd-142">祝贺你安装并使用第一个 NuGet 包！</span><span class="sxs-lookup"><span data-stu-id="077bd-142">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="077bd-143">使用 Visual Studio for Mac 安装和管理包</span><span class="sxs-lookup"><span data-stu-id="077bd-143">Install and manage packages using Visual Studio for Mac</span></span>](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

<span data-ttu-id="077bd-144">若要了解更多 NuGet 产品，请选择以下链接。</span><span class="sxs-lookup"><span data-stu-id="077bd-144">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="077bd-145">包使用的概述和工作流</span><span class="sxs-lookup"><span data-stu-id="077bd-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="077bd-146">项目文件中的包引用</span><span class="sxs-lookup"><span data-stu-id="077bd-146">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
