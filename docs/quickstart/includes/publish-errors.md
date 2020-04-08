---
ms.openlocfilehash: b0af2000b1f43cd0b91f2c95dfc0c11540a94cab
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495943"
---
`push` 命令中的错误通常表示存在问题。 例如，你可能会忘记更新项目中的版本号，因此尝试发布已存在的包。

尝试使用主机上已存在的标识符发布包时，你也会看到错误。 例如，名称“AppLogger”已经存在。 在这种情况下，`push` 命令会给出以下错误：

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

如果你使用的是刚刚创建的有效 API 密钥，则此消息表明存在命名冲突，并未从错误的“权限”部分中将其完全清除。 更改包标识符，重建项目，重新创建 `.nupkg` 文件，然后重试 `push` 命令。