- **包管理器 UI** (Visual Studio)：右键单击“解决方案资源管理器”中的解决方案，选择“还原 NuGet 包”。 如果一个或多个独立包仍未正确安装（即“解决方案资源管理器”显示错误图标），请使用包管理器 UI 卸载受影响的包并重新安装。 请参阅[重新安装和更新包](../Consume-Packages/Reinstalling-and-Updating-Packages.md)

- **命令行**：使用 [nuget restore](../tools/cli-ref-restore.md) 命令。 运行项目文件夹中的 `nuget restore` 即可尝试还原项目的依赖项。
