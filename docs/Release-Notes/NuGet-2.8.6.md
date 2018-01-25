---
title: "NuGet 2.8.6 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 920c551c-18a7-40f4-a32b-ce84de6ea766
description: "发行说明，了解 NuGet 2.8.6 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。"
keywords: "NuGet 2.8.6 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4dfd0a76967280cc6a16b37fe2b2a3362231fce5
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="30574-104">NuGet 2.8.6 发行说明</span><span class="sxs-lookup"><span data-stu-id="30574-104">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="30574-105">[NuGet 2.8.5 发行说明](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 发行说明](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="30574-105">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="30574-106">发布 NuGet 2.8.6 2015 年 7 月 20 日作为一项次要更新到我们 2.8.5 VSIX 一些针对修补程序和改进，可使用支持 Windows 10 UWP 开发模型支持可能会发送的包。</span><span class="sxs-lookup"><span data-stu-id="30574-106">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="30574-107">此版本的 NuGet 包管理器扩展提供仅支持 32 位 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="30574-107">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="30574-108">在此版本中，NuGet 包管理器对话框必须添加对支持：</span><span class="sxs-lookup"><span data-stu-id="30574-108">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="30574-109">引入了 UAP 目标框架名字对象以支持 Windows 10 应用程序开发。</span><span class="sxs-lookup"><span data-stu-id="30574-109">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="30574-110">NuGet 协议版本 3 终结点</span><span class="sxs-lookup"><span data-stu-id="30574-110">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="30574-111">支持[Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion 属性存储库源。</span><span class="sxs-lookup"><span data-stu-id="30574-111">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="30574-112">默认值为"2"</span><span class="sxs-lookup"><span data-stu-id="30574-112">Default value is "2"</span></span>
* <span data-ttu-id="30574-113">回退到远程存储库如果所需的程序包版本在本地缓存中不可用</span><span class="sxs-lookup"><span data-stu-id="30574-113">Falling back to remote repository if a required package version is not available in the local cache</span></span>