---
title: "使用 Visual Studio 2017 创建 .NET Standard 2.0 NuGet 包 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: "从头到尾演练如何使用 NuGet 4.x 和 Visual Studio 2017 创建 .NET Standard 2.0 NuGet 包。"
keywords: "创建包, .NET Standard 包, .NET Core"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82e413119b12503336becd6019e4fa3e4ac0b1f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a>使用 Visual Studio 2017 创建 .NET Standard 2.0 包

*在提供 Visual Studio 2017 Update 3 的情况下适用于 NuGet 4.x+ 和 MSBuild 15.3+。对于更早版本的 Visual Studio 2017，可以更改 \<TargetFramework\> 属性使这些说明适用于 .NET Standard 1.4 到 1.6。还可参阅[使用 Visual Studio 2015 创建 .NET Standard 包](../guides/create-net-standard-packages-vs2015.md)，了解如何使用 NuGet 3.x+。*

[.NET Standard 库](https://docs.microsoft.com/dotnet/articles/standard/library)是一套正式的 .NET API 规范，有望在所有 .NET 运行时推出，借此在 .NET 生态系统中建立更强的一致性。 .NET Standard 库为要实现的所有 .NET 平台定义一组统一的、与工作负荷无关的 BCL（基类库）API。 它使得开发人员可以生成跨所有 .NET 运行时可用的 PCL，并减少（如果不能消除）共享代码中平台特定的条件编译指令。

本指南将指导你使用 Visual Studio 2017 Update 3 和 NuGet 4.0 创建面向 .NET Standard 2.0 库的 NuGet 包。

1. [先决条件](#pre-requisites)
1. [创建类库项目](#create-the-netstandard-class-library-project)
1. [在 .csproj 文件中编辑元数据](#edit-metadata-in-the-csproj-file)
1. [打包组件](#package-the-component)
1. [相关主题](#related-topics)

## <a name="pre-requisites"></a>先决条件

本演练需要带“.NET Core 跨平台开发”工作负荷的 Visual Studio 2017 Update 3。 可以从 [visualstudio.com](https://www.visualstudio.com/) 免费安装 Community 版，也可以使用 Professional 和 Enterprise 版。

所需工作负荷在 Visual Studio 安装程序中显示为：

![Visual Studio 安装程序中的 .NET Core 跨平台开发工作负荷](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a>创建 .NET Standard 类库项目

1. 在 Visual Studio 中，单击“文件”>“新建”>“项目”，展开“Visual C#”>“.NET Standard”节点，选择“类库(Net Standard)”，将名称更改为 AppLogger，然后单击“确定”。

    ![创建新类库项目](media/NuGet4-02-NewProject.png)

1. 将生成配置更改为“Release”。
1. 右键单击解决方案资源管理器中的 `AppLogger` 项目，选择“属性”，选择“生成”选项卡，选中“XML 文档文件”框，然后将文件名设为 `AppLogger.xml`。 然后保存项目。

1. 将代码添加到组件，如以下内容（这些内容明显只是到控制台的输出消息）：

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. 生成项目（使用 Release 配置）并检查 `bin\Release\netstandard2.0` 文件夹中生成了 DLL 和 XML 文件。

## <a name="edit-metadata-in-the-csproj-file"></a>在 .csproj 文件中编辑元数据

有了 NuGet 4.0 和 .NET Core 项目，包元数据直接包含在 `.csproj` 文件中，而不是 `.nuspec` 等外部文件中。 可以在[作为 MSBuild 目标的 NuGet 包和还原](../schema/msbuild-targets.md#pack-target)中找到该元数据的完整说明。

1. 右键单击解决方案资源管理器中的项目，选择“编辑 AppLogger.csproj”，然后将第一个属性组编辑为包含如下包信息：

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. 保存项目，然后右键单击解决方案并选择“生成解决方案”再次为包生成所有文件，这一次使用正确的元数据。


## <a name="package-the-component"></a>打包组件

项目包含必要包元数据时（如上一部分所添加），NuGet 4.0 支持包目标使用 MSBuild 版本 15.1+（包括作为 Visual Studio 2017 Update 3 一部分的 MSBuild 15.3）。 若要使用此方法调用 MSBuild，只需在与 `.csproj` 文件相同的文件夹的命令行上指定包目标：

    msbuild /t:pack /p:Configuration=Release

有关 `msbuild /t:pack` 的其他选项，例如包含内容文件、符号和源代码，请参阅[作为 MSBuild 目标的 NuGet 包和还原](../schema/msbuild-targets.md#pack-target)。

在任何情况下，上述命令都会默认在 `bin\Release` 文件夹中生成 `AppLogger.YOUR_NAME.1.0.0.nupkg`，因为它生成该配置。 如果忽略 `/p` 开关，默认配置将为 `Debug`。 

在 [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)（NuGet 包资源管理器）之类的工具中打开此文件，并展开所有节点，随即将看到以下内容：

![显示 AppLogger 包的 NuGet 包资源管理器](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> `.nupkg` 文件实际上是具有其他扩展名的 ZIP 文件。 然后，也可通过将 `.nupkg` 更改为 `.zip` 来检查包内容，但将包上传到 nuget.org 之前，请记得恢复扩展名。

若要使你的包可供其他开发人员使用，请按照[发布包](../create-packages/publish-a-package.md)中的说明进行操作。

## <a name="related-topics"></a>相关主题

- [项目文件中的包引用](../consume-packages/package-references-in-project-files.md)介绍直接在项目文件中描述包的所有详细信息。
- [作为 MSBuild 目标的 NuGet 包和还原](../schema/msbuild-targets.md)介绍使用 `msbuild /t:pack` 创建包的所有选项。
- [.NET Standard 库文档](https://docs.microsoft.com/dotnet/articles/standard/library)
- [从 .NET Framework 移植到 .NET Core](https://docs.microsoft.com/dotnet/articles/core/porting/index)
