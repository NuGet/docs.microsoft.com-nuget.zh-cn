---
title: 使用 dotnet CLI 安装并使用 NuGet 包
description: 有关如何在 .NET Core 项目中安装并使用 NuGet 包的演练教程。
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 47593cc65ad707b8880d854dc43824b9234fd44a
ms.sourcegitcommit: ba8ad1bd13a4bba3df94374e34e20c425a05af2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2019
ms.locfileid: "68833311"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="26bea-103">快速入门：使用 dotnet CLI 安装并使用包</span><span class="sxs-lookup"><span data-stu-id="26bea-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="26bea-104">NuGet 包包含其他开发人员提供的在项目中使用的可重用代码。</span><span class="sxs-lookup"><span data-stu-id="26bea-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="26bea-105">请参阅[什么是 NuGet？](../What-is-NuGet.md)，了解背景信息。</span><span class="sxs-lookup"><span data-stu-id="26bea-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="26bea-106">使用如本文所述的适用于常用 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) 包的 `dotnet add package` 命令将包安装到 .NET Core 项目中。</span><span class="sxs-lookup"><span data-stu-id="26bea-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="26bea-107">安装完成后，请引用具有 `using <namespace>` 的代码中的包，其中 \<namespace\> 特定于正在使用的包。</span><span class="sxs-lookup"><span data-stu-id="26bea-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="26bea-108">然后，可以使用包的 API。</span><span class="sxs-lookup"><span data-stu-id="26bea-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="26bea-109">**nuget.org 入门**：若要查找可在自己的应用程序中重用的组件，.NET 开发人员通常都会浏览 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="26bea-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="26bea-110">你可以直接搜索 nuget.org 或根据本文中的介绍，在 Visual Studio 中查找和安装包。</span><span class="sxs-lookup"><span data-stu-id="26bea-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26bea-111">系统必备</span><span class="sxs-lookup"><span data-stu-id="26bea-111">Prerequisites</span></span>

- <span data-ttu-id="26bea-112">[.NET Core SDK](https://www.microsoft.com/net/download/)，提供 `dotnet` 命令行工具。</span><span class="sxs-lookup"><span data-stu-id="26bea-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="26bea-113">从 Visual Studio 2017 开始，dotnet CLI 将自动随任何与 .NET Core 相关的工作负载一起安装。</span><span class="sxs-lookup"><span data-stu-id="26bea-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="26bea-114">创建项目</span><span class="sxs-lookup"><span data-stu-id="26bea-114">Create a project</span></span>

<span data-ttu-id="26bea-115">可以将 NuGet 包安装到某种类型的 .NET 项目。</span><span class="sxs-lookup"><span data-stu-id="26bea-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="26bea-116">在本演练中，如下所示创建一个简单的 .NET Core 控制台项目：</span><span class="sxs-lookup"><span data-stu-id="26bea-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="26bea-117">为项目创建文件夹。</span><span class="sxs-lookup"><span data-stu-id="26bea-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="26bea-118">打开命令提示符并切换到新文件夹。</span><span class="sxs-lookup"><span data-stu-id="26bea-118">Open a command prompt and switch to the new folder.</span></span>

1. <span data-ttu-id="26bea-119">请使用以下命令创建项目：</span><span class="sxs-lookup"><span data-stu-id="26bea-119">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="26bea-120">使用 `dotnet run` 来测试已正确创建的应用。</span><span class="sxs-lookup"><span data-stu-id="26bea-120">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="26bea-121">添加 Newtonsoft.Json Nuget 包</span><span class="sxs-lookup"><span data-stu-id="26bea-121">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="26bea-122">运行以下命令安装 `Newtonsoft.json` 包：</span><span class="sxs-lookup"><span data-stu-id="26bea-122">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="26bea-123">该命令完成后，打开 `.csproj` 文件以查看所添加的引用：</span><span class="sxs-lookup"><span data-stu-id="26bea-123">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="26bea-124">在应用中使用 Newtonsoft.Json API</span><span class="sxs-lookup"><span data-stu-id="26bea-124">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="26bea-125">打开 `Program.cs` 文件，然后在文件的顶部添加以下行：</span><span class="sxs-lookup"><span data-stu-id="26bea-125">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="26bea-126">在 `class Program` 行的前面添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="26bea-126">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="26bea-127">使用以下代码替换 `Main` 函数：</span><span class="sxs-lookup"><span data-stu-id="26bea-127">Replace the `Main` function with the following:</span></span>

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. <span data-ttu-id="26bea-128">使用 `dotnet run` 命令生成并运行应用。</span><span class="sxs-lookup"><span data-stu-id="26bea-128">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="26bea-129">输出应是 `Account` 对象在代码中的 JSON 表示形式：</span><span class="sxs-lookup"><span data-stu-id="26bea-129">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="26bea-130">后续步骤</span><span class="sxs-lookup"><span data-stu-id="26bea-130">Next steps</span></span>

<span data-ttu-id="26bea-131">祝贺你安装并使用第一个 NuGet 包！</span><span class="sxs-lookup"><span data-stu-id="26bea-131">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="26bea-132">使用 dotnet CLI 安装并使用包</span><span class="sxs-lookup"><span data-stu-id="26bea-132">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)

<span data-ttu-id="26bea-133">若要了解更多 NuGet 产品，请选择以下链接。</span><span class="sxs-lookup"><span data-stu-id="26bea-133">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="26bea-134">包使用的概述和工作流</span><span class="sxs-lookup"><span data-stu-id="26bea-134">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="26bea-135">查找和选择包</span><span class="sxs-lookup"><span data-stu-id="26bea-135">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="26bea-136">项目文件中的包引用</span><span class="sxs-lookup"><span data-stu-id="26bea-136">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
