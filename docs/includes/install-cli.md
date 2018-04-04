#### <a name="windows"></a><span data-ttu-id="965cc-101">Windows</span><span class="sxs-lookup"><span data-stu-id="965cc-101">Windows</span></span>
1. <span data-ttu-id="965cc-102">请访问[nuget.org/downloads](https://nuget.org/downloads)和选择 NuGet 3.3 或更高版本 （2.8.6 不与 Mono 兼容）。</span><span class="sxs-lookup"><span data-stu-id="965cc-102">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="965cc-103">始终建议的最新版本，并且将包发布到 nuget.org 所需的 4.1.0+。</span><span class="sxs-lookup"><span data-stu-id="965cc-103">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
2. <span data-ttu-id="965cc-104">每个下载`nuget.exe`直接文件。</span><span class="sxs-lookup"><span data-stu-id="965cc-104">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="965cc-105">指示您的浏览器将文件保存到所选的文件夹。</span><span class="sxs-lookup"><span data-stu-id="965cc-105">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="965cc-106">该文件是*不*的安装程序; 如果直接从浏览器运行不会看到任何内容。</span><span class="sxs-lookup"><span data-stu-id="965cc-106">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
3. <span data-ttu-id="965cc-107">将你的放置位置的文件夹添加`nuget.exe`到你的 PATH 环境变量，从任意位置使用 CLI 工具。</span><span class="sxs-lookup"><span data-stu-id="965cc-107">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="965cc-108">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="965cc-108">macOS/Linux</span></span>
<span data-ttu-id="965cc-109">行为可能通过操作系统分配略有不同。</span><span class="sxs-lookup"><span data-stu-id="965cc-109">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="965cc-110">安装[Mono 4.4.2 或更高版本](http://www.mono-project.com/docs/getting-started/install/)。</span><span class="sxs-lookup"><span data-stu-id="965cc-110">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>
2. <span data-ttu-id="965cc-111">执行以下命令外壳提示符：</span><span class="sxs-lookup"><span data-stu-id="965cc-111">Execute the following commands at a shell prompt:</span></span>
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. <span data-ttu-id="965cc-112">通过将以下脚本添加到相应的文件，为您的操作系统创建别名 (通常`~/.bash_aliases`或`~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="965cc-112">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. <span data-ttu-id="965cc-113">重新加载 shell。</span><span class="sxs-lookup"><span data-stu-id="965cc-113">Reload the shell.</span></span>  <span data-ttu-id="965cc-114">通过输入测试安装`nuget`不带任何参数。</span><span class="sxs-lookup"><span data-stu-id="965cc-114">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="965cc-115">应显示 NuGet CLI 帮助。</span><span class="sxs-lookup"><span data-stu-id="965cc-115">NuGet CLI help should display.</span></span>