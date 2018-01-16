---
title: "NuGet 项目治理 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 94c088ce-ec96-4876-a210-fbdae743942c
description: "NuGet 的治理模型，包括提交者、参与者和用户的角色和职责。"
keywords: "NuGet 治理, NuGet 仁慈独裁者, 提交者职责, 参与者职责, 用户职责"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0437b7d41f965da6a7ad44a7d0675916ed655fe1
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-governance"></a><span data-ttu-id="a2987-104">NuGet 治理</span><span class="sxs-lookup"><span data-stu-id="a2987-104">NuGet governance</span></span>

> <span data-ttu-id="a2987-105">本文档基于牛津大学的[仁慈独裁者治理模型](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel)。</span><span class="sxs-lookup"><span data-stu-id="a2987-105">This document is based upon the [Benevolent Dictator Governance Model](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) by the University of Oxford.</span></span> <span data-ttu-id="a2987-106">它根据 [Creative Commons Attribution-ShareAlike 2.0 UK: England & Wales License](http://creativecommons.org/licenses/by-sa/2.0/uk/) 获得许可。</span><span class="sxs-lookup"><span data-stu-id="a2987-106">It is licensed under a [Creative Commons Attribution-ShareAlike 2.0 UK: England & Wales License](http://creativecommons.org/licenses/by-sa/2.0/uk/).</span></span>

<span data-ttu-id="a2987-107">NuGet 项目由仁慈独裁者领导并由社区进行管理。</span><span class="sxs-lookup"><span data-stu-id="a2987-107">The NuGet project is led by a Benevolent Dictator and managed by the community.</span></span> <span data-ttu-id="a2987-108">也就是说，社区积极参与项目的日常维护，但总体策略规划由仁慈独裁者制定。</span><span class="sxs-lookup"><span data-stu-id="a2987-108">That is, the community actively contributes to the day-to-day maintenance of the project, but the general strategic line is drawn by the benevolent dictator.</span></span> <span data-ttu-id="a2987-109">如果出现争议，仁慈独裁者拥有最终裁量权。</span><span class="sxs-lookup"><span data-stu-id="a2987-109">In case of disagreement, the benevolent dictator has the last word.</span></span>

<span data-ttu-id="a2987-110">仁慈独裁者的职责是解决社区内部争议，并确保项目能够协调开展。</span><span class="sxs-lookup"><span data-stu-id="a2987-110">It is the benevolent dictator’s job to resolve disputes within the community and to ensure that the project is able to progress in a coordinated way.</span></span> <span data-ttu-id="a2987-111">而社区的职责是通过积极参与和贡献来指导仁慈独裁者的决策。</span><span class="sxs-lookup"><span data-stu-id="a2987-111">In turn, it's the community’s job to guide the decisions of the benevolent dictator through active engagement and contribution.</span></span>

## <a name="roles-and-responsibilities"></a><span data-ttu-id="a2987-112">角色和职责</span><span class="sxs-lookup"><span data-stu-id="a2987-112">Roles and responsibilities</span></span>

<span data-ttu-id="a2987-113">此处介绍四种角色：仁慈独裁者、提交者、参与者和用户。</span><span class="sxs-lookup"><span data-stu-id="a2987-113">There are four roles described here: Benevolent Dictator, Committers, Contributors, and Users.</span></span>

### <a name="benevolent-dictator"></a><span data-ttu-id="a2987-114">仁慈独裁者</span><span class="sxs-lookup"><span data-stu-id="a2987-114">Benevolent Dictator</span></span>

<span data-ttu-id="a2987-115">NuGet 核心团队自任命为仁慈独裁者或项目领导。</span><span class="sxs-lookup"><span data-stu-id="a2987-115">The NuGet core team is self-appointed as Benevolent Dictator or project lead.</span></span> <span data-ttu-id="a2987-116">但是，由于社区总是会出现分歧，因此团队应完全对社区负责。</span><span class="sxs-lookup"><span data-stu-id="a2987-116">However, because the community always has the ability to fork, the team is fully answerable to the community.</span></span> <span data-ttu-id="a2987-117">项目领导应了解整个社区，并努力尽量满足发生冲突的需求，同时确保项目长期开展下去。</span><span class="sxs-lookup"><span data-stu-id="a2987-117">The project lead is expected to understand the community as a whole and strive to satisfy as many conflicting needs as possible, while ensuring that the project survives in the long term.</span></span>

<span data-ttu-id="a2987-118">在许多方面，仁慈独裁者的角色更偏向协调，而不是独裁。</span><span class="sxs-lookup"><span data-stu-id="a2987-118">In many ways, the role of the benevolent dictator is less about dictatorship and more about diplomacy.</span></span> <span data-ttu-id="a2987-119">关键的一点是，随着项目展开，确保相关人员受到积极影响，社区在项目领导的愿景下共同协作。</span><span class="sxs-lookup"><span data-stu-id="a2987-119">The key is to ensure that, as the project expands, the right people are given influence over it and the community rallies behind the vision of the project lead.</span></span> <span data-ttu-id="a2987-120">领导的职责是确保提交者（见下文）代表项目做出正确的决策。</span><span class="sxs-lookup"><span data-stu-id="a2987-120">The lead’s job is then to ensure that the committers (see below) make the right decisions on behalf of the project.</span></span> <span data-ttu-id="a2987-121">一般而言，只要提交者与项目的策略保持一致，项目领导会允许他们按自己的方式行事。</span><span class="sxs-lookup"><span data-stu-id="a2987-121">Generally speaking, as long as the committers are aligned with the project’s strategy, the project lead will allow them to proceed as they desire.</span></span>

<span data-ttu-id="a2987-122">此外，.NET Foundation 员工将项目领导视为 NuGet 的主要或首个联系点，用于域注册和技术服务（如代码签名）等业务操作。</span><span class="sxs-lookup"><span data-stu-id="a2987-122">Additionally, .NET Foundation staff consider the project lead the primary or first point of contact for NuGet for purposes of business operations including domain registrations, and technical services (e.g. code-signing).</span></span>

### <a name="committers"></a><span data-ttu-id="a2987-123">提交者</span><span class="sxs-lookup"><span data-stu-id="a2987-123">Committers</span></span>

<span data-ttu-id="a2987-124">提交者是为 NuGet 持续做出有价值贡献的参与者，由仁慈独裁者任命。</span><span class="sxs-lookup"><span data-stu-id="a2987-124">Committers are contributors who have made sustained valuable contributions to NuGet and are appointed by the Benevolent Dictator.</span></span> <span data-ttu-id="a2987-125">经任命后，将代码直接写入存储库及筛选其他人的贡献均依赖于提交者。</span><span class="sxs-lookup"><span data-stu-id="a2987-125">One appointed, committers are relied upon to both write code directly to the repository and screen the contributions of others.</span></span> <span data-ttu-id="a2987-126">提交者通常是开发人员，但可以通过其他方式参与。</span><span class="sxs-lookup"><span data-stu-id="a2987-126">Committers are often developers but can contribute in other ways.</span></span>

<span data-ttu-id="a2987-127">通常，提交者专注于项目的特定方面，其具有一定的专业知识和经验，因此受到社区和项目领导的尊重。</span><span class="sxs-lookup"><span data-stu-id="a2987-127">Typically, a committer focuses on a specific aspect of the project, and brings a level of expertise and understanding that earns them the respect of the community and the project lead.</span></span> <span data-ttu-id="a2987-128">提交者并非一种正式角色，它仅仅是有影响力的社区成员在项目领导向其寻求指导和支持时担当的职位。</span><span class="sxs-lookup"><span data-stu-id="a2987-128">The role of committer is not an official one, it's simply a position that influential members of the community assume as the project lead looks to them for guidance and support.</span></span>

<span data-ttu-id="a2987-129">从 NuGet 的总体方向来看，提交者不具备权威。</span><span class="sxs-lookup"><span data-stu-id="a2987-129">Committers have no authority where the overall direction of NuGet is concerned.</span></span> <span data-ttu-id="a2987-130">但项目领导会听取他们的意见。</span><span class="sxs-lookup"><span data-stu-id="a2987-130">However, they do have the ear of the project lead.</span></span> <span data-ttu-id="a2987-131">提交者的职责是确保领导了解社区的需求和集体目标，并帮助开发或引导对项目的适当贡献。</span><span class="sxs-lookup"><span data-stu-id="a2987-131">It is a committer’s job to ensure that the lead is aware of the community’s needs and collective objectives, and to help develop or elicit appropriate contributions to the project.</span></span> <span data-ttu-id="a2987-132">通常，提交者可对其特定负责部分进行非正式管理，并且分配有可直接修改源代码的特定部分的权限。</span><span class="sxs-lookup"><span data-stu-id="a2987-132">Often, committers are given informal control over their specific areas of responsibility, and are assigned rights to directly modify certain areas of the source code.</span></span> <span data-ttu-id="a2987-133">也就是说，尽管提交者没有明确的决策权，但他们通常会发现其操作与领导做出的决策一致。</span><span class="sxs-lookup"><span data-stu-id="a2987-133">That is, although committers do not have explicit decision-making authority, they will often find that their actions are synonymous with the decisions made by the lead.</span></span>

### <a name="contributors"></a><span data-ttu-id="a2987-134">参与者</span><span class="sxs-lookup"><span data-stu-id="a2987-134">Contributors</span></span>

<span data-ttu-id="a2987-135">参与者是向 NuGet 提交修补程序的社区成员。</span><span class="sxs-lookup"><span data-stu-id="a2987-135">Contributors are community members who submit patches to NuGet.</span></span> <span data-ttu-id="a2987-136">这些修补程序可能只发生一次或者不断发生。</span><span class="sxs-lookup"><span data-stu-id="a2987-136">These patches may be a one-time occurrence or occur over time.</span></span> <span data-ttu-id="a2987-137">根据预期，参与者提交的修补程序起初很小，随着参与者、提交者和项目领导对其质量树立起信心而逐渐变大。</span><span class="sxs-lookup"><span data-stu-id="a2987-137">Expectations are that contributors submit patches that are small at first and grow larger when the contributor, committers, and the project lead have built confidence in the quality of a contributor's patches.</span></span> <span data-ttu-id="a2987-138">参与者在关联的产品发布说明文档中获得认可。</span><span class="sxs-lookup"><span data-stu-id="a2987-138">Contributors are recognized in the associated product release notes document.</span></span>

<span data-ttu-id="a2987-139">将参与者的第一个修补程序放入存储库前，他们必须向 .NET Foundation 签署[参与者许可协议](http://en.wikipedia.org/wiki/Contributor_License_Agreement)或分配协议。</span><span class="sxs-lookup"><span data-stu-id="a2987-139">Before a contributor’s first patch is put into the repository, they must sign a [Contributor License Agreement](http://en.wikipedia.org/wiki/Contributor_License_Agreement) or an assignment agreement to the .NET Foundation.</span></span> <span data-ttu-id="a2987-140">修补程序可提交和讨论，但如果没有相应的书面批准，实际上不能提交到存储库。</span><span class="sxs-lookup"><span data-stu-id="a2987-140">The patch can be submitted and discussed but it can’t actually be committed to the repository without the appropriate paperwork in place.</span></span> <span data-ttu-id="a2987-141">若要获取参与者许可协议，请通过电子邮件将请求发送至 [contributions@nuget.org](mailto:contributions@nuget.org)。</span><span class="sxs-lookup"><span data-stu-id="a2987-141">To obtain a contributor license agreement, please send a request in email to [contributions@nuget.org](mailto:contributions@nuget.org).</span></span>

<span data-ttu-id="a2987-142">若要成为参与者，请向以下存储库之一提交拉取请求：</span><span class="sxs-lookup"><span data-stu-id="a2987-142">To become a contributor, submit a pull request to one of the following repositories:</span></span>

- [<span data-ttu-id="a2987-143">NuGet 客户端</span><span class="sxs-lookup"><span data-stu-id="a2987-143">NuGet Client</span></span>](https://github.com/NuGet/NuGet.Client)
- [<span data-ttu-id="a2987-144">NuGet 库</span><span class="sxs-lookup"><span data-stu-id="a2987-144">NuGet Gallery</span></span>](https://github.com/nuget/nugetgallery)
- [<span data-ttu-id="a2987-145">NuGet Docs</span><span class="sxs-lookup"><span data-stu-id="a2987-145">NuGet Docs</span></span>](https://github.com/nuget/nugetdocs)

<span data-ttu-id="a2987-146">提交拉取请求的详细过程因存储库而异：</span><span class="sxs-lookup"><span data-stu-id="a2987-146">The detailed process for submitting a pull request varies by repository:</span></span>

- [<span data-ttu-id="a2987-147">NuGet 客户端和 NuGet 库的参与说明</span><span class="sxs-lookup"><span data-stu-id="a2987-147">Contribution instructions for NuGet Client and NuGet Gallery</span></span>](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [<span data-ttu-id="a2987-148">NuGet Docs 的参与说明</span><span class="sxs-lookup"><span data-stu-id="a2987-148">Contribution instructions for NuGet Docs</span></span>](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a><span data-ttu-id="a2987-149">用户</span><span class="sxs-lookup"><span data-stu-id="a2987-149">Users</span></span>

<span data-ttu-id="a2987-150">用户是作为包使用者和/或创建者需要并使用 NuGet 的社区成员。</span><span class="sxs-lookup"><span data-stu-id="a2987-150">Users are community members who have a need for and use NuGet, as package consumers and/or authors.</span></span> <span data-ttu-id="a2987-151">用户是社区最重要的成员：没有他们，项目就没有用。</span><span class="sxs-lookup"><span data-stu-id="a2987-151">Users are the most important members of the community: without them, the project would have no purpose.</span></span> <span data-ttu-id="a2987-152">任何人都可成为用户；没有特定要求。</span><span class="sxs-lookup"><span data-stu-id="a2987-152">Anyone can be a user; there are no specific requirements.</span></span>

<span data-ttu-id="a2987-153">应鼓励用户尽量参与 NuGet 和社区的活动。</span><span class="sxs-lookup"><span data-stu-id="a2987-153">Users should be encouraged to participate in the life of NuGet and the community as much as possible.</span></span> <span data-ttu-id="a2987-154">用户的参与使项目团队确保满足用户的需求。</span><span class="sxs-lookup"><span data-stu-id="a2987-154">User contributions enable the project team to ensure that they are satisfying the needs of those users.</span></span> <span data-ttu-id="a2987-155">常见的用户活动包括但不限于以下几种：</span><span class="sxs-lookup"><span data-stu-id="a2987-155">Common user activities include but are not limited to the following:</span></span>

- <span data-ttu-id="a2987-156">提倡使用该项目</span><span class="sxs-lookup"><span data-stu-id="a2987-156">Advocating for use of the project</span></span>
- <span data-ttu-id="a2987-157">从新用户的角度告知开发人员项目的优缺点</span><span class="sxs-lookup"><span data-stu-id="a2987-157">Informing developers of project strengths and weaknesses from a new user’s perspective</span></span>
- <span data-ttu-id="a2987-158">提供精神支持（感谢的话语为开发人员带来工作的动力）</span><span class="sxs-lookup"><span data-stu-id="a2987-158">Providing moral support (a thank you goes a long way)</span></span>
- <span data-ttu-id="a2987-159">编写文档和教程</span><span class="sxs-lookup"><span data-stu-id="a2987-159">Writing documentation and tutorials</span></span>
- <span data-ttu-id="a2987-160">填写 bug 报告和功能请求</span><span class="sxs-lookup"><span data-stu-id="a2987-160">Filing bug reports and feature requests</span></span>
- <span data-ttu-id="a2987-161">参与社区活动，如 bug 清除</span><span class="sxs-lookup"><span data-stu-id="a2987-161">Participating in community events, such as bug bashes</span></span>
- <span data-ttu-id="a2987-162">参与讨论板或论坛</span><span class="sxs-lookup"><span data-stu-id="a2987-162">Participating on discussion boards or forums</span></span>

<span data-ttu-id="a2987-163">通常，持续参与项目及其社区的用户的参与度会不断提高。</span><span class="sxs-lookup"><span data-stu-id="a2987-163">Users who continue to engage with the project and its community will often find themselves becoming more and more involved.</span></span> <span data-ttu-id="a2987-164">这类用户以后可以成为参与者，如上文所述。</span><span class="sxs-lookup"><span data-stu-id="a2987-164">Such users may then go on to become contributors, as described above.</span></span>

## <a name="package-succession-under-special-circumstances"></a><span data-ttu-id="a2987-165">特殊情况下的包继承</span><span class="sxs-lookup"><span data-stu-id="a2987-165">Package succession under special circumstances</span></span>
<span data-ttu-id="a2987-166">在 NuGet 帐户持有者无行为能力或死亡等不幸情况下，我们将与社区协作，将适当的所有者添加到包，其中上述帐户对包具有唯一所有权，并且包根据 [OSI 批准许可](https://opensource.org/licenses/alphabetical)发布。</span><span class="sxs-lookup"><span data-stu-id="a2987-166">In the unfortunate situation where a NuGet account holder is incapacitated or deceased, we’ll work with the community to add appropriate owner/s to the package where the said account has sole ownership and the package is published under an [OSI approved license](https://opensource.org/licenses/alphabetical).</span></span> <span data-ttu-id="a2987-167">若要请求所有权，必须向我们发送以下文档：</span><span class="sxs-lookup"><span data-stu-id="a2987-167">To request ownership you must send us the following documents:</span></span>

1.  <span data-ttu-id="a2987-168">政府颁发的带照片身份证复印件。</span><span class="sxs-lookup"><span data-stu-id="a2987-168">A photocopy of your government-issued photo ID.</span></span>
2.  <span data-ttu-id="a2987-169">可证明以前帐户持有者状态的以下文档之一：</span><span class="sxs-lookup"><span data-stu-id="a2987-169">One of the following documents proving the previous account holder’s status:</span></span> 
    - <span data-ttu-id="a2987-170">政府颁发的官方死亡证明（如果以前的帐户持有者已死亡），或</span><span class="sxs-lookup"><span data-stu-id="a2987-170">An official, government-issued death certificate if the previous account holder is deceased, or,</span></span>
    - <span data-ttu-id="a2987-171">公证文件，例如负责照顾无行为能力帐户持有者的医疗专业人员签名的证明。</span><span class="sxs-lookup"><span data-stu-id="a2987-171">A certified document such as a certificate signed by a medical professional in charge of the care of an incapacitated account holder.</span></span>
3.  <span data-ttu-id="a2987-172">可证明你拥有所有权的以下文档之一：</span><span class="sxs-lookup"><span data-stu-id="a2987-172">One of the following documents proving your right to ownership:</span></span> 
    - <span data-ttu-id="a2987-173">可证明你是帐户持有者的依然健在的配偶的结婚证，</span><span class="sxs-lookup"><span data-stu-id="a2987-173">Marriage certificate showing that you are the surviving spouse of the account holder,</span></span>
    - <span data-ttu-id="a2987-174">签名委托书，</span><span class="sxs-lookup"><span data-stu-id="a2987-174">Signed power of attorney,</span></span>
    - <span data-ttu-id="a2987-175">将你命名为执行人或受益人的遗嘱或信托文件复印件，</span><span class="sxs-lookup"><span data-stu-id="a2987-175">Copy of a will or trust document naming you as executor or beneficiary,</span></span>
    - <span data-ttu-id="a2987-176">帐户持有者的出生证明（如果你是其父母），或</span><span class="sxs-lookup"><span data-stu-id="a2987-176">Birth certificate for the account holder, if you are their parent, or,</span></span>
    - <span data-ttu-id="a2987-177">监护人身份书面证明（如果你是帐户持有者的法定监护人）。</span><span class="sxs-lookup"><span data-stu-id="a2987-177">Guardianship paperwork if you are a legal guardian of the account holder.</span></span>
    
<span data-ttu-id="a2987-178">如果你发现自己需要使用此政策，请通过电子邮件将包的 ID 和版本发送至 [support@nuget.org](mailto:support@nuget.org)。</span><span class="sxs-lookup"><span data-stu-id="a2987-178">If you find yourself in need of invoking this policy, please send us an email at [support@nuget.org](mailto:support@nuget.org) with the ID and version of the package.</span></span>
    
## <a name="transparency"></a><span data-ttu-id="a2987-179">透明度</span><span class="sxs-lookup"><span data-stu-id="a2987-179">Transparency</span></span>

<span data-ttu-id="a2987-180">在开放源代码项目治理中构建社区信任对其成功至关重要。</span><span class="sxs-lookup"><span data-stu-id="a2987-180">Building community trust in the governance of an open-source project is vital to its success.</span></span> <span data-ttu-id="a2987-181">为此，决策制定必须采取透明、开放的方式。</span><span class="sxs-lookup"><span data-stu-id="a2987-181">To that end, decision making must be done in a transparent, open fashion.</span></span> <span data-ttu-id="a2987-182">有关项目方向的讨论必须公开进行。</span><span class="sxs-lookup"><span data-stu-id="a2987-182">Discussion about the project’s direction must be done publicly.</span></span> <span data-ttu-id="a2987-183">社区不应对仁慈独裁者的决策措手不及。</span><span class="sxs-lookup"><span data-stu-id="a2987-183">The community should never be caught off-guard by a decision by the Benevolent Dictator.</span></span> <span data-ttu-id="a2987-184">此外，有关项目决策的讨论必须存档，以便社区成员可了解决策及其上下文的整个历史记录。</span><span class="sxs-lookup"><span data-stu-id="a2987-184">Additionally, discussion about project decisions must be archived so that community members can understand the entire history of a decision and its context.</span></span>
