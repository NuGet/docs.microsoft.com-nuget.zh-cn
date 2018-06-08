---
title: NuGet 项目治理
description: NuGet 的治理模型，包括提交者、参与者和用户的角色和职责。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 658901a86b42d6451e41c2c26906a6b6f444faf6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818057"
---
# <a name="nuget-governance"></a>NuGet 治理

> 本文档基于牛津大学的[仁慈独裁者治理模型](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel)。 它根据 [Creative Commons Attribution-ShareAlike 2.0 UK: England & Wales License](http://creativecommons.org/licenses/by-sa/2.0/uk/) 获得许可。

NuGet 项目由仁慈独裁者领导并由社区进行管理。 也就是说，社区积极参与项目的日常维护，但总体策略规划由仁慈独裁者制定。 如果出现争议，仁慈独裁者拥有最终裁量权。

仁慈独裁者的职责是解决社区内部争议，并确保项目能够协调开展。 而社区的职责是通过积极参与和贡献来指导仁慈独裁者的决策。

## <a name="roles-and-responsibilities"></a>角色和职责

此处介绍四种角色：仁慈独裁者、提交者、参与者和用户。

### <a name="benevolent-dictator"></a>仁慈的独裁者

NuGet 核心团队自任命为仁慈独裁者或项目领导。 但是，由于社区总是会出现分歧，因此团队应完全对社区负责。 项目领导应了解整个社区，并努力尽量满足发生冲突的需求，同时确保项目长期开展下去。

在许多方面，仁慈独裁者的角色更偏向协调，而不是独裁。 关键的一点是，随着项目展开，确保相关人员受到积极影响，社区在项目领导的愿景下共同协作。 领导的职责是确保提交者（见下文）代表项目做出正确的决策。 一般而言，只要提交者与项目的策略保持一致，项目领导会允许他们按自己的方式行事。

此外，.NET Foundation 员工将项目领导视为 NuGet 的主要或首个联系点，用于域注册和技术服务（如代码签名）等业务操作。

### <a name="committers"></a>提交者

提交者是为 NuGet 持续做出有价值贡献的参与者，由仁慈独裁者任命。 经任命后，将代码直接写入存储库及筛选其他人的贡献均依赖于提交者。 提交者通常是开发人员，但可以通过其他方式参与。

通常，提交者专注于项目的特定方面，其具有一定的专业知识和经验，因此受到社区和项目领导的尊重。 提交者并非一种正式角色，它仅仅是有影响力的社区成员在项目领导向其寻求指导和支持时担当的职位。

从 NuGet 的总体方向来看，提交者不具备权威。 但项目领导会听取他们的意见。 提交者的职责是确保领导了解社区的需求和集体目标，并帮助开发或引导对项目的适当贡献。 通常，提交者可对其特定负责部分进行非正式管理，并且分配有可直接修改源代码的特定部分的权限。 也就是说，尽管提交者没有明确的决策权，但他们通常会发现其操作与领导做出的决策一致。

### <a name="contributors"></a>参与者

参与者是向 NuGet 提交修补程序的社区成员。 这些修补程序可能只发生一次或者不断发生。 根据预期，参与者提交的修补程序起初很小，随着参与者、提交者和项目领导对其质量树立起信心而逐渐变大。 参与者在关联的产品发布说明文档中获得认可。

将参与者的第一个修补程序放入存储库前，他们必须向 .NET Foundation 签署[参与者许可协议](http://en.wikipedia.org/wiki/Contributor_License_Agreement)或分配协议。 修补程序可提交和讨论，但如果没有相应的书面批准，实际上不能提交到存储库。 若要获取参与者许可协议，请通过电子邮件将请求发送至 [contributions@nuget.org](mailto:contributions@nuget.org)。

若要成为参与者，请向以下存储库之一提交拉取请求：

- [NuGet 客户端](https://github.com/NuGet/NuGet.Client)
- [NuGet 库](https://github.com/nuget/nugetgallery)
- [NuGet Docs](https://github.com/nuget/nugetdocs)

提交拉取请求的详细过程因存储库而异：

- [NuGet 客户端和 NuGet 库的参与说明](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [NuGet Docs 的参与说明](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>用户

用户是作为包使用者和/或创建者需要并使用 NuGet 的社区成员。 用户是社区最重要的成员：没有他们，项目就没有用。 任何人都可成为用户；没有特定要求。

应鼓励用户尽量参与 NuGet 和社区的活动。 用户的参与使项目团队确保满足用户的需求。 常见的用户活动包括但不限于以下几种：

- 提倡使用该项目
- 从新用户的角度告知开发人员项目的优缺点
- 提供精神支持（感谢的话语为开发人员带来工作的动力）
- 编写文档和教程
- 填写 bug 报告和功能请求
- 参与社区活动，如 bug 清除
- 参与讨论板或论坛

通常，持续参与项目及其社区的用户的参与度会不断提高。 这类用户以后可以成为参与者，如上文所述。

## <a name="package-succession-under-special-circumstances"></a>特殊情况下的包继承

在 NuGet 帐户持有者无行为能力或死亡等不幸情况下，我们将与社区协作，将适当的所有者添加到包，其中上述帐户对包具有唯一所有权，并且包根据 [OSI 批准许可](https://opensource.org/licenses/alphabetical)发布。 若要请求所有权，必须向我们发送以下文档：

1. 政府颁发的带照片身份证复印件。
1. 可证明以前帐户持有者状态的以下文档之一： 
    - 政府颁发的官方死亡证明（如果以前的帐户持有者已死亡），或
    - 公证文件，例如负责照顾无行为能力帐户持有者的医疗专业人员签名的证明。
1. 可证明你拥有所有权的以下文档之一： 
    - 可证明你是帐户持有者的依然健在的配偶的结婚证，
    - 签名委托书，
    - 将你命名为执行人或受益人的遗嘱或信托文件复印件，
    - 帐户持有者的出生证明（如果你是其父母），或
    - 监护人身份书面证明（如果你是帐户持有者的法定监护人）。

如果你发现自己需要使用此政策，请通过电子邮件将包的 ID 和版本发送至 [support@nuget.org](mailto:support@nuget.org)。

## <a name="transparency"></a>透明度

在开放源代码项目治理中构建社区信任对其成功至关重要。 为此，决策制定必须采取透明、开放的方式。 有关项目方向的讨论必须公开进行。 社区不应对仁慈独裁者的决策措手不及。 此外，有关项目决策的讨论必须存档，以便社区成员可了解决策及其上下文的整个历史记录。
