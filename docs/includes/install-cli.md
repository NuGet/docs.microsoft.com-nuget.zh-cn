#### <a name="windows"></a>Windows
1. 请访问[nuget.org/downloads](https://nuget.org/downloads)和选择 NuGet 3.3 或更高版本 （2.8.6 不与 Mono 兼容）。 始终建议的最新版本，并且将包发布到 nuget.org 所需的 4.1.0+。
2. 每个下载`nuget.exe`直接文件。 指示您的浏览器将文件保存到所选的文件夹。 该文件是*不*的安装程序; 如果直接从浏览器运行不会看到任何内容。
3. 将你的放置位置的文件夹添加`nuget.exe`到你的 PATH 环境变量，从任意位置使用 CLI 工具。

#### <a name="macoslinux"></a>macOS/Linux
行为可能通过操作系统分配略有不同。

1. 安装[Mono 4.4.2 或更高版本](http://www.mono-project.com/docs/getting-started/install/)。
2. 执行以下命令外壳提示符：
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. 通过将以下脚本添加到相应的文件，为您的操作系统创建别名 (通常`~/.bash_aliases`或`~/.bash_profile`):
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. 重新加载 shell。  通过输入测试安装`nuget`不带任何参数。 应显示 NuGet CLI 帮助。