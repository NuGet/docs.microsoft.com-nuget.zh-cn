---
title: 使用 dotnet CLI 安装并使用 NuGet 包
description: 有关如何在 .NET Core 项目中安装并使用 NuGet 包的演练教程。
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 006fff8360ac62393e4b88c1a253514591d22f4c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231265"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="47d63-103">快速入门：使用 dotnet CLI 安装并使用包</span><span class="sxs-lookup"><span data-stu-id="47d63-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="47d63-104">NuGet 包包含其他开发人员提供的在项目中使用的可重用代码。</span><span class="sxs-lookup"><span data-stu-id="47d63-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="47d63-105">请参阅[什么是 NuGet？](../What-is-NuGet.md)，了解背景信息。</span><span class="sxs-lookup"><span data-stu-id="47d63-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="47d63-106">使用如本文所述的适用于常用 `dotnet add package`Newtonsoft.Json[ 包的 ](https://www.nuget.org/packages/Newtonsoft.Json/) 命令将包安装到 .NET Core 项目中。</span><span class="sxs-lookup"><span data-stu-id="47d63-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="47d63-107">安装完成后，请引用具有 `using <namespace>` 的代码中的包，其中 \<namespace\> 特定于正在使用的包。</span><span class="sxs-lookup"><span data-stu-id="47d63-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="47d63-108">然后，可以使用包的 API。</span><span class="sxs-lookup"><span data-stu-id="47d63-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="47d63-109">**nuget.org 入门**：浏览 nuget.org 是 .NET 开发人员通常在自己的应用程序中查找可重用组件的方式。</span><span class="sxs-lookup"><span data-stu-id="47d63-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="47d63-110">你可以直接搜索 nuget.org 或根据本文中的介绍，在 Visual Studio 中查找和安装包。</span><span class="sxs-lookup"><span data-stu-id="47d63-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47d63-111">必备条件</span><span class="sxs-lookup"><span data-stu-id="47d63-111">Prerequisites</span></span>

- <span data-ttu-id="47d63-112">[.NET Core SDK](https://www.microsoft.com/net/download/)，提供 `dotnet` 命令行工具。</span><span class="sxs-lookup"><span data-stu-id="47d63-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="47d63-113">从 Visual Studio 2017 开始，dotnet CLI 将自动随任何与 .NET Core 相关的工作负载一起安装。</span><span class="sxs-lookup"><span data-stu-id="47d63-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="47d63-114">创建一个项目</span><span class="sxs-lookup"><span data-stu-id="47d63-114">Create a project</span></span>

<span data-ttu-id="47d63-115">可以将 NuGet 包安装到某种类型的 .NET 项目。</span><span class="sxs-lookup"><span data-stu-id="47d63-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="47d63-116">在本演练中，如下所示创建一个简单的 .NET Core 控制台项目：</span><span class="sxs-lookup"><span data-stu-id="47d63-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="47d63-117">为项目创建文件夹。</span><span class="sxs-lookup"><span data-stu-id="47d63-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="47d63-118">打开命令提示符并切换到新文件夹。</span><span class="sxs-lookup"><span data-stu-id="47d63-118">Open a command prompt and switch to the new folder.</span></span>

1. <span data-ttu-id="47d63-119">请使用以下命令创建项目：</span><span class="sxs-lookup"><span data-stu-id="47d63-119">Create the project using the following command:</span></span>

    ```dotnetcli
    dotnet new console
    ```

1. <span data-ttu-id="47d63-120">使用 `dotnet run` 来测试已正确创建的应用。</span><span class="sxs-lookup"><span data-stu-id="47d63-120">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="47d63-121">添加 Newtonsoft.Json Nuget 包</span><span class="sxs-lookup"><span data-stu-id="47d63-121">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="47d63-122">运行以下命令安装 `Newtonsoft.json` 包：</span><span class="sxs-lookup"><span data-stu-id="47d63-122">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="47d63-123">该命令完成后，打开 `.csproj` 文件以查看所添加的引用：</span><span class="sxs-lookup"><span data-stu-id="47d63-123">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="47d63-124">在应用中使用 Newtonsoft.Json API</span><span class="sxs-lookup"><span data-stu-id="47d63-124">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="47d63-125">打开 `Program.cs` 文件，然后在文件的顶部添加以下行：</span><span class="sxs-lookup"><span data-stu-id="47d63-125">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="47d63-126">在 `class Program` 行的前面添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="47d63-126">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="47d63-127">使用以下代码替换 `Main` 函数：</span><span class="sxs-lookup"><span data-stu-id="47d63-127">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="47d63-128">使用 `dotnet run` 命令生成并运行应用。</span><span class="sxs-lookup"><span data-stu-id="47d63-128">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="47d63-129">输出应是 `Account` 对象在代码中的 JSON 表示形式：</span><span class="sxs-lookup"><span data-stu-id="47d63-129">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a><span data-ttu-id="47d63-130">相关视频</span><span class="sxs-lookup"><span data-stu-id="47d63-130">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

<span data-ttu-id="47d63-131">在[第 9 频道](https://channel9.msdn.com/Series/NuGet-101)和 [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_) 上查找更多 NuGet 视频。</span><span class="sxs-lookup"><span data-stu-id="47d63-131">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="47d63-132">后续步骤</span><span class="sxs-lookup"><span data-stu-id="47d63-132">Next steps</span></span>

<span data-ttu-id="47d63-133">祝贺你安装并使用第一个 NuGet 包！</span><span class="sxs-lookup"><span data-stu-id="47d63-133">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="47d63-134">使用 dotnet CLI 安装并使用包</span><span class="sxs-lookup"><span data-stu-id="47d63-134">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)

<span data-ttu-id="47d63-135">若要了解更多 NuGet 产品，请选择以下链接。</span><span class="sxs-lookup"><span data-stu-id="47d63-135">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="47d63-136">包使用的概述和工作流</span><span class="sxs-lookup"><span data-stu-id="47d63-136">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="47d63-137">查找和选择包</span><span class="sxs-lookup"><span data-stu-id="47d63-137">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="47d63-138">项目文件中的包引用</span><span class="sxs-lookup"><span data-stu-id="47d63-138">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
