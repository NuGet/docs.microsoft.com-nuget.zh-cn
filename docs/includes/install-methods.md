可通过 3 种方式安装包：

| 方法 | 描述 | 参考 |
| --- | --- | --- |
| nuget.exe CLI：`nuget install <package_name>` | 下载按 \<package_name\> 识别的包，并将其内容展开到当前目录中的文件夹。 如果未指定任何包，则安装项目的 `packages.config` 文件中列出的所有包。 所有项目文件均不会发生任何更改。 还将下载和展开依赖项。 | [CLI 引用](../tools/nuget-exe-CLI-Reference.md) |
| 包管理器控制台 (Visual Studio)：`Install-Package <package_name>` | 下载包并将其安装到当前项目中，然后更新项目文件，以将包作为依赖项列出。 | [包管理器控制台指南](../tools/Package-Manager-Console.md) |
| 包管理器 UI (Visual Studio) | 提供 UI，通过此 UI 你可以浏览、选择包并将包安装到项目中。 更新项目文件以将包作为依赖项列出。 | [包管理器 UI 引用](../tools/Package-Manager-UI.md) |