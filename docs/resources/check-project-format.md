---
title: 标识项目格式
description: 介绍如何标识项目格式
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488484"
---
# <a name="identify-the-project-format"></a><span data-ttu-id="27b3a-103">标识项目格式</span><span class="sxs-lookup"><span data-stu-id="27b3a-103">Identify the project format</span></span>

<span data-ttu-id="27b3a-104">NuGet 适用于所有 .NET 项目。</span><span class="sxs-lookup"><span data-stu-id="27b3a-104">NuGet works with all .NET projects.</span></span> <span data-ttu-id="27b3a-105">但是，项目格式（SDK 样式或非 SDK 样式）决定了使用和创建 NuGet 包所需的一些工具和方法。</span><span class="sxs-lookup"><span data-stu-id="27b3a-105">However, the project format (SDK-style or non-SDK-style) determines some of the tools and methods that you need to use to consume and create NuGet packages.</span></span> <span data-ttu-id="27b3a-106">SDK 样式的项目使用 [SDK 属性](/dotnet/core/tools/csproj#additions)。</span><span class="sxs-lookup"><span data-stu-id="27b3a-106">SDK-style projects use the [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span> <span data-ttu-id="27b3a-107">确定项目类型非常重要，因为用于使用和创建 NuGet 包的方法和工具都依赖于项目格式。</span><span class="sxs-lookup"><span data-stu-id="27b3a-107">It is important to identify your project type because the methods and tools you use to consume and create NuGet packages are dependent on the project format.</span></span> <span data-ttu-id="27b3a-108">对于非 SDK 样式的项目，方法和工具还取决于项目是否迁移到 `PackageReference` 格式。</span><span class="sxs-lookup"><span data-stu-id="27b3a-108">For non-SDK-style projects, the methods and tools are also dependent on whether or not the project has been migrated to `PackageReference` format.</span></span>

<span data-ttu-id="27b3a-109">项目是否为 SDK 样式取决于用于创建项目的方法。</span><span class="sxs-lookup"><span data-stu-id="27b3a-109">Whether your project is SDK-style or not depends on the method used to create the project.</span></span> <span data-ttu-id="27b3a-110">下表显示了使用 Visual Studio 2017 及更高版本创建项目时的默认项目格式和相关的 CLI 工具。</span><span class="sxs-lookup"><span data-stu-id="27b3a-110">The following table shows the default project format and the associated CLI tool for your project when you create it using Visual Studio 2017 and later versions.</span></span>

| <span data-ttu-id="27b3a-111">项目&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="27b3a-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="27b3a-112">默认项目格式</span><span class="sxs-lookup"><span data-stu-id="27b3a-112">Default project format</span></span> | <span data-ttu-id="27b3a-113">CLI 工具&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="27b3a-113">CLI tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="27b3a-114">说明</span><span class="sxs-lookup"><span data-stu-id="27b3a-114">Notes</span></span> |
|:------------- |:-------------|:-----|:-----|
| <span data-ttu-id="27b3a-115">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="27b3a-115">.NET Standard</span></span> | <span data-ttu-id="27b3a-116">SDK 样式</span><span class="sxs-lookup"><span data-stu-id="27b3a-116">SDK-style</span></span> | [<span data-ttu-id="27b3a-117">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="27b3a-117">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="27b3a-118">在 Visual Studio 2017 之前创建的项目为非 SDK 样式。</span><span class="sxs-lookup"><span data-stu-id="27b3a-118">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="27b3a-119">使用 `nuget.exe` CLI。</span><span class="sxs-lookup"><span data-stu-id="27b3a-119">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="27b3a-120">.NET Core</span><span class="sxs-lookup"><span data-stu-id="27b3a-120">.NET Core</span></span> | <span data-ttu-id="27b3a-121">SDK 样式</span><span class="sxs-lookup"><span data-stu-id="27b3a-121">SDK-style</span></span> | [<span data-ttu-id="27b3a-122">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="27b3a-122">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="27b3a-123">在 Visual Studio 2017 之前创建的项目为非 SDK 样式。</span><span class="sxs-lookup"><span data-stu-id="27b3a-123">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="27b3a-124">使用 `nuget.exe` CLI。</span><span class="sxs-lookup"><span data-stu-id="27b3a-124">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="27b3a-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="27b3a-125">.NET Framework</span></span> | <span data-ttu-id="27b3a-126">非 SDK 样式</span><span class="sxs-lookup"><span data-stu-id="27b3a-126">Non-SDK-style</span></span> | [<span data-ttu-id="27b3a-127">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="27b3a-127">nuget.exe CLI</span></span>](../install-nuget-client-tools.md#nugetexe-cli) | <span data-ttu-id="27b3a-128">使用其他方法创建的 .NET Framework 项目可能是 SDK 样式项目。</span><span class="sxs-lookup"><span data-stu-id="27b3a-128">.NET Framework projects created using other methods may be SDK-style projects.</span></span> <span data-ttu-id="27b3a-129">对于这种情况，请改为使用 [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli)。</span><span class="sxs-lookup"><span data-stu-id="27b3a-129">For these, use [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) instead.</span></span> |
| <span data-ttu-id="27b3a-130">[迁移的](../consume-packages/migrate-packages-config-to-package-reference.md) .NET 项目</span><span class="sxs-lookup"><span data-stu-id="27b3a-130">[Migrated](../consume-packages/migrate-packages-config-to-package-reference.md) .NET project</span></span> | <span data-ttu-id="27b3a-131">非 SDK 样式</span><span class="sxs-lookup"><span data-stu-id="27b3a-131">Non-SDK-style</span></span>| <span data-ttu-id="27b3a-132">要创建包，请使用 [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) 创建包。</span><span class="sxs-lookup"><span data-stu-id="27b3a-132">To create packages, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) to create packages.</span></span> | <span data-ttu-id="27b3a-133">要创建包，建议使用 `msbuild -t:pack`。</span><span class="sxs-lookup"><span data-stu-id="27b3a-133">To create packages, `msbuild -t:pack` is recommended.</span></span> <span data-ttu-id="27b3a-134">否则，使用 [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli)。</span><span class="sxs-lookup"><span data-stu-id="27b3a-134">Otherwise, use the [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span></span> <span data-ttu-id="27b3a-135">迁移的项目是非 SDK 样式的项目。</span><span class="sxs-lookup"><span data-stu-id="27b3a-135">Migrated projects are not SDK-style projects.</span></span> |

## <a name="check-the-project-format"></a><span data-ttu-id="27b3a-136">检查项目格式</span><span class="sxs-lookup"><span data-stu-id="27b3a-136">Check the project format</span></span>

<span data-ttu-id="27b3a-137">如果不确定该项目是否是 SDK 样式的格式，请在项目文件中的 `<Project>` 元素中查找 SDK 属性（对于 C#，这是 \*.csproj 文件）。</span><span class="sxs-lookup"><span data-stu-id="27b3a-137">If you're unsure whether the project is SDK-style format or not, look for the SDK attribute in the `<Project>` element in the project file (For C#, this is the \*.csproj file).</span></span> <span data-ttu-id="27b3a-138">如果存在，则该项目是一个 SDK 样式的项目。</span><span class="sxs-lookup"><span data-stu-id="27b3a-138">If it is present, the project is an SDK-style project.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a><span data-ttu-id="27b3a-139">在 Visual Studio 中检查项目格式</span><span class="sxs-lookup"><span data-stu-id="27b3a-139">Check the project format in Visual Studio</span></span>

<span data-ttu-id="27b3a-140">如果在 Visual Studio 中进行操作，可以使用以下方法之一快速检查项目格式：</span><span class="sxs-lookup"><span data-stu-id="27b3a-140">If you are working in Visual Studio, you can quickly check the project format using one of the following methods:</span></span>

- <span data-ttu-id="27b3a-141">在解决方案资源管理器中右键单击该项目，然后选择“编辑 myprojectname.csproj”  。</span><span class="sxs-lookup"><span data-stu-id="27b3a-141">Right-click the project in Solution Explorer and select **Edit myprojectname.csproj**.</span></span>

   <span data-ttu-id="27b3a-142">此选项从 Visual Studio 2017 开始仅对使用 SDK 样式属性的项目可用。</span><span class="sxs-lookup"><span data-stu-id="27b3a-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="27b3a-143">否则，请使用其他方法。</span><span class="sxs-lookup"><span data-stu-id="27b3a-143">Otherwise, use the other method.</span></span>

   ![编辑项目文件](media/edit-project-file.png)

   <span data-ttu-id="27b3a-145">一个 SDK 样式的项目会在项目文件中显示 [SDK 属性](/dotnet/core/tools/csproj#additions)。</span><span class="sxs-lookup"><span data-stu-id="27b3a-145">An SDK-style project shows the [SDK attribute](/dotnet/core/tools/csproj#additions) in the project file.</span></span>
   
- <span data-ttu-id="27b3a-146">在“项目”  菜单中选择“卸载项目”  （或右键单击项目并选择“卸载项目”  ）。</span><span class="sxs-lookup"><span data-stu-id="27b3a-146">From the **Project** menu, choose **Unload Project** (or right-click the project and choose **Unload Project**).</span></span>

   <span data-ttu-id="27b3a-147">该项目将不在项目文件中包含 SDK 属性。</span><span class="sxs-lookup"><span data-stu-id="27b3a-147">This project will not include the SDK attribute in the project file.</span></span> <span data-ttu-id="27b3a-148">它不是 SDK 样式的项目。</span><span class="sxs-lookup"><span data-stu-id="27b3a-148">It is not an SDK-style project.</span></span>

   ![卸载项目](media/unload-project.png)

   <span data-ttu-id="27b3a-150">然后，右键单击卸载的项目并选择“编辑 myprojectname.csproj”  。</span><span class="sxs-lookup"><span data-stu-id="27b3a-150">Then, right-click the unloaded project and choose **Edit myprojectname.csproj**.</span></span>

## <a name="see-also"></a><span data-ttu-id="27b3a-151">请参阅</span><span class="sxs-lookup"><span data-stu-id="27b3a-151">See also</span></span>

- [<span data-ttu-id="27b3a-152">使用 dotnet CLI 创建 .NET Standard 包</span><span class="sxs-lookup"><span data-stu-id="27b3a-152">Create .NET Standard Packages with dotnet CLI</span></span>](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [<span data-ttu-id="27b3a-153">使用 Visual Studio 创建 .NET Standard 包</span><span class="sxs-lookup"><span data-stu-id="27b3a-153">Create .NET Standard Packages with Visual Studio</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [<span data-ttu-id="27b3a-154">创建并发布 .NET Framework 包 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="27b3a-154">Create and publish a .NET Framework package (Visual Studio)</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [<span data-ttu-id="27b3a-155">作为 MSBuild 目标的 NuGet 包和还原</span><span class="sxs-lookup"><span data-stu-id="27b3a-155">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
