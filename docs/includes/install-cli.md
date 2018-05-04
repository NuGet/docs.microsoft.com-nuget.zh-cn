#### <a name="windows"></a><span data-ttu-id="7b485-101">Windows</span><span class="sxs-lookup"><span data-stu-id="7b485-101">Windows</span></span>

1. <span data-ttu-id="7b485-102">请访问 [nuget.org/downloads](https://nuget.org/downloads)，并选择 NuGet 3.3 或更高版本（2.8.6 与 Mono 不兼容）。</span><span class="sxs-lookup"><span data-stu-id="7b485-102">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="7b485-103">始终建议使用最新版。若要将包发布到 nuget.org，版本至少必须是 4.1.0。</span><span class="sxs-lookup"><span data-stu-id="7b485-103">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="7b485-104">每次下载都直接下载 `nuget.exe` 文件。</span><span class="sxs-lookup"><span data-stu-id="7b485-104">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="7b485-105">让浏览器将文件保存到选定文件夹。</span><span class="sxs-lookup"><span data-stu-id="7b485-105">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="7b485-106">此文件不是安装程序；如果直接在浏览器中运行，就不会看到任何内容。</span><span class="sxs-lookup"><span data-stu-id="7b485-106">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="7b485-107">将文件夹添加到 `nuget.exe` 中放置 PATH 环境变量的位置，这样就可以从任意位置使用 CLI 工具。</span><span class="sxs-lookup"><span data-stu-id="7b485-107">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="7b485-108">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="7b485-108">macOS/Linux</span></span>

<span data-ttu-id="7b485-109">行为可能因 OS 分发版本略有不同。</span><span class="sxs-lookup"><span data-stu-id="7b485-109">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="7b485-110">安装 [Mono 4.4.2 或更高版本](http://www.mono-project.com/docs/getting-started/install/)。</span><span class="sxs-lookup"><span data-stu-id="7b485-110">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="7b485-111">在 shell 提示符处，执行下列命令：</span><span class="sxs-lookup"><span data-stu-id="7b485-111">Execute the following commands at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```

1. <span data-ttu-id="7b485-112">通过将以下脚本添加到 OS 的相应文件来创建别名（通常为 `~/.bash_aliases` 或 `~/.bash_profile`）：</span><span class="sxs-lookup"><span data-stu-id="7b485-112">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="7b485-113">重载 shell。</span><span class="sxs-lookup"><span data-stu-id="7b485-113">Reload the shell.</span></span>  <span data-ttu-id="7b485-114">通过输入 `nuget`（而不使用任何参数）来测试安装。</span><span class="sxs-lookup"><span data-stu-id="7b485-114">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="7b485-115">应该会看到 NuGet CLI 帮助。</span><span class="sxs-lookup"><span data-stu-id="7b485-115">NuGet CLI help should display.</span></span>