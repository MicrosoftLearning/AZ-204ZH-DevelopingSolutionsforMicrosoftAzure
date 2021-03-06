---
lab:
    az204Title: '实验室 05: 使用映像和容器部署计算工作负载'
    az204Module: '模块 05: 实现 IaaS 解决方案'
    type: '答案要点'
---

# 实验室 05：使用映像和容器部署计算工作负载
# 学生实验室答案要点

## Microsoft Azure 用户界面

鉴于 Microsoft 云工具的动态特性，Azure UI 在此培训内容开发后可能会发生更改。这些更改可能会导致实验室说明和实验室步骤不一致。

当社区要求我们进行更改时，Microsoft 将更新此培训课程。但是，由于云更新频繁发生，因此在此培训内容更新之前，你可能会遇到 UI 更改情况。**如果发生这种情况，请适应这些更改，并根据需要在实验室中熟悉这些更改。**

## 说明

### 准备工作

#### 登录到实验室虚拟机

使用以下凭据登录到 Windows 10 虚拟机 (VM)：
    
-   用户名：**Admin**

-   密码： **Pa55w.rd**

> **备注**：你的讲师将提供连接到虚拟实验室环境的说明。

#### 查看已安装的应用程序

在你的 Windows 10 桌面上找到任务栏。任务栏里有本实验室中你将使用的应用程序的图标：
    
-   Microsoft Edge

-   文件资源管理器

### 练习 1：使用 Azure 命令行接口 (CLI) 创建 VM

#### 任务 1：打开 Azure 门户

1.  在任务栏上，选择 **“Microsoft Edge”** 图标。

1.  在打开的浏览器窗口中，转到 Azure 门户 (<https://portal.azure.com>)。

1.  输入你的 Microsoft 帐户的电子邮件地址，然后选择 **“下一步”**。

1.  输入 Microsoft 帐户的密码，然后选择 **“登录”**。

    > **备注**：你第一次登录 Azure 门户时会为你提供门户导览。选择 **“开始使用”**，开始使用门户。

#### 任务 2：创建资源组

1.  在 Azure 门户的“导航”窗格中，选择 **“创建资源”** 链接。

    > **备注**：如果你找不到 **“创建资源”** 链接的话，门户中的加号 (+) 就是 **“创建资源”** 的图标。

1.  在 **“新建”** 边栏选项卡，找到精选服务列表上方的 **“搜索市场”** 文本框。

1.  在搜索框中，输入文本 **“资源组”**，然后按 Enter 键。

1.  在 **“市场”** 搜索结果边栏选项卡中，选择 **“资源组”** 结果。

1.  在 **“资源组”** 边栏选项卡中，选择 **“创建”**。

1.  在附加 **“资源组”** 边栏选项卡中，找到边栏选项卡的选项卡，如 **“基本”**。

    > **备注**：每个选项卡代表工作流中创建新资源组的一个步骤。你可以随时选择 **“查看 + 创建”** 跳过其余选项卡。

1.  在 **“基本信息”** 选项卡中，执行以下操作：
    
    1.  将 **“订阅”** 文本框设置为默认值。
    
    1.  在 **“资源组”** 文本框中，输入值 **“ContainerCompute”**。
    
    1.  在 **“区域”** 下拉列表中，选择 **“（美国）美国东部”** 位置。
    
    1.  选择 **“查看 + 创建”**。

1.  在 **“查看 + 创建”** 选项卡中，查看在先前步骤中选择的选项。

1.  选择 **“创建”** 以使用指定的配置创建资源组。  

    > **备注**：等待创建任务完成后再继续本实验室。

#### 任务 3：打开 Azure Cloud Shell

1.  在 Azure 门户中，选择 **“Cloud Shell”** 图标以打开一个新的 shell 实例。

    > **备注**：**“Cloud Shell”** 图标使用大于符号 () 和下划线字符 (\_) 表示。

1.  如果这是你第一次使用订阅打开 Cloud Shell，则可以使用 **“欢迎使用 Azure Cloud Shell 向导”** 来配置 Cloud Shell，以便首次使用。在向导中执行以下操作：
    
    1.  对话框提示你配置 shell。选择 **“Bash”**，查看选定的订阅，然后选择 **“创建存储”**。 

    > **备注**：等待 Cloud Shell 完成首次设置过程后，再继续本实验室。如果 **Cloud Shell** 配置选项未显示，很可能是因为你使用的是本课程实验室中的现有订阅。实验是假设你使用的是新订阅的情况下编写的。

1.  在门户的 **Cloud Shell** 命令提示符处，输入以下命令，然后按 Enter 键以查看 Azure CLI 工具的版本：

    ```
    az --version
    ```

#### 任务 4：使用 Azure CLI 命令

1.  输入以下命令并按 Enter 以获取 CLI 根级别的子组和命令列表：

    ```
    az --help
    ```

1.  输入以下命令，然后选择 Enter，以获取 Azure 虚拟机的子组和命令列表：

    ```
    az vm --help
    ```

1.  输入以下命令并按 Enter 键以查看 **“创建虚拟机”** 命令的参数和示例列表：

    ```
    az vm create --help
    ```

1.  输入以下命令并按 Enter 键以使用以下设置创建新的 **“虚拟机”**：
    
    - 资源组：**ContainerCompute**

    - 名称：**quickvm**

    - 映像：**Debian**

    - 用户名：**学生**

    - 密码： **StudentPa55w.rd**

    ```
    az vm create --resource-group ContainerCompute --name quickvm --image Debian --admin-username student --admin-password StudentPa55w.rd
    ```

    > **备注**：等待 VM 创建过程完成。该过程完成后，命令将返回一个包含计算机相关详细信息的 JSON 文件。

1.  输入以下命令并按 Enter 键以查看包含有关新创建 VM 的各种元数据的更详细 JavaScript 对象表示法 (JSON) 文件：

    ```
    az vm show --resource-group ContainerCompute --name quickvm
    ```

1.  输入以下命令并按 Enter 键以列出与 VM 关联的所有 IP 地址：

    ```
    az vm list-ip-addresses --resource-group ContainerCompute --name quickvm
    ```

1.  输入以下命令并按 Enter 键以筛选输出，以便只返回第一个 IP 地址值：

    ```
    az vm list-ip-addresses --resource-group ContainerCompute --name quickvm --query '[].{ip:virtualMachine.network.publicIpAddresses[0].ipAddress}' --output tsv
    ```

1.  输入以下命令并按 Enter 键以将上一个命令的结果存储在名为 *ipAddress* 的新 Bash Shell 变量中：

    ```
    ipAddress=$(az vm list-ip-addresses --resource-group ContainerCompute --name quickvm --query '[].{ip:virtualMachine.network.publicIpAddresses[0].ipAddress}' --output tsv)
    ```

1.  输入以下命令，然后按 Enter 以呈现 Bash Shell 变量 *ipAddress* 的值：

    ```
    echo $ipAddress
    ```

1.  输入以下命令并按 Enter 键以通过使用 Secure Shell (SSH) 工具和存储在 Bash Shell 变量 *ipAddress* 中的 IP 地址连接到之前在本实验室中创建的 VM：

    ```
    ssh student@$ipAddress
    ```

1.  SSH 工具首先将通知你无法建立主机的真实性，然后询问是否要继续连接。输入 **“yes”**，然后按 Enter 键以继续连接到 VM。

1.  然后 SSH 工具会要求你输入密码。输入 **“StudentPa55w.rd”**，然后选择 “Enter” 对 VM 进行身份验证。

1.  使用 SSH 连接到 VM 后，输入以下命令并按 Enter 键以获取描述 Linux VM 的元数据：

    ```
    uname -a
    ```

1.  使用**出口**命令结束 SSH 会话：

    ```
    exit
    ```

1.  关闭门户中的 Cloud Shell 窗格。

#### 回顾

在本练习中，你使用了 Cloud Shell 作为自动脚本的一部分创建 VM。

### 练习 2：创建 Docker 容器映像并部署到 Azure 容器注册表

#### 任务 1：打开 Cloud Shell 和编辑器

1.  在 Azure 门户的“导航”窗格中，选择 **“Cloud Shell”** 图标以打开一个新的 shell 实例。  

    > **备注**：等待 Cloud Shell 完成连接到实例，再继续进行本实验室。

1.  在门户的 **Cloud Shell** 命令提示符中，输入以下命令并按 Enter 键以从根目录移动至 **\~/clouddrive** 目录：

    ```
    cd ~/clouddrive
    ```

1.  输入以下命令并按 Enter 键，以在 **\~/clouddrive** 目录中创建名为 **ipcheck** 的新目录：

    ```
    mkdir ipcheck
    ```

1.  输入以下命令并按 Enter 键以将活动目录从 **\~/clouddrive** 更改为 **\~/clouddrive/ipcheck**：

    ```
    cd ~/clouddrive/ipcheck
    ```

1.  输入以下命令并，按 Enter 键以在当前目录中创建新的 .NET Core 控制台应用程序：

    ```
    dotnet new console --output . --name ipcheck
    ```

1.  输入以下命令，并按 Enter 键，以便在名为 **Dockerfile** 的 **\~/clouddrive/ipcheck** 目录中创建一个新文件：

    ```
    touch Dockerfile
    ```

1.  输入以下命令并按 Enter 以在当前目录打开嵌入式图形编辑器：

    ```
    code .
    ```

#### 任务 2：创建并测试 .NET 应用程序

1.  在图形编辑器中，找到“文件”窗格，然后打开 **“Program.cs”** 文件，以在编辑器中打开该文件。

1.  删除 **“Program.cs”** 文件的全部内容。

1.  将以下代码复制并粘贴到 **“Program.cs”** 文件中：

    ```
    public class Program
    {
        public static void Main(string[] args)
        {        
            // 检查网络是否可用
            if (System.Net.NetworkInformation.NetworkInterface.GetIsNetworkAvailable())
            {
                System.Console.WriteLine("Current IP Addresses:");

                // 获取当前主机名的主机条目
                string hostname = System.Net.Dns.GetHostName();
                System.Net.IPHostEntry host = System.Net.Dns.GetHostEntry(hostname);
                
                // 循环访问每个 IP 地址并呈现其值
                foreach(System.Net.IPAddress address in host.AddressList)
                {
                    System.Console.WriteLine($"\t{address}");
                }
            }
            else
            {
                System.Console.WriteLine("No Network Connection");
            }
        }
    }
    ```

1.  使用图形编辑器中的菜单或 Ctrl+S 键盘快捷键保存 **Program.cs** 文件。  不要关闭图形编辑器。

1.  返回命令提示符，输入以下命令，然后按 Enter 以运行应用程序：

    ```
    dotnet run
    ```

1.  查找运行结果。应该为 Cloud Shell 实例列出至少一个 IP 地址。

1.  在图形编辑器中，找到编辑器上的“文件”窗格，然后在编辑器中打开 **“Dockerfile”** 文件。

1.  将以下代码复制并粘贴到 **“Dockerfile”** 文件中：

    ```
    ＃开始使用 .NET Core 3.1 SDK 容器映像
    FROM mcr.microsoft.com/dotnet/sdk:3.1-alpine AS build

    # 更改当前工作目录
    WORKDIR /app

    ＃从主机复制现有文件
    COPY . ./

    ＃将应用程序发布到“out”文件夹
    RUN dotnet publish --configuration Release --output out

    ＃通过运行应用程序 DLL 启动容器
    ENTRYPOINT ["dotnet", "out/ipcheck.dll"]
    ```

1.  使用图形编辑器中的菜单或 Ctrl+S 键盘快捷键保存 **Dockerfile** 文件。

1.  关闭门户中的 Cloud Shell 窗格。

#### 任务 3：创建 Azure 容器注册表资源

1.  在 Azure 门户的“导航”窗格中，选择 **“创建资源”** 链接。

1.  在 **“新建”** 边栏选项卡，找到精选服务列表上方的 **“搜索市场”** 文本框。

1.  在搜索文本框中，输入 **Container Registry**，然后按 Enter 键。

1.  在 **“市场”** 搜索结果边栏选项卡中，选择 **“容器注册表”** 结果。

1.  在 **“容器注册表”** 边栏选项卡中，选择 **“创建”**。

1.  在 **“创建容器注册表”** 边栏选项卡中，执行以下操作：

    1.  在 **“注册表名称”** 文本框中，为注册表提供全局唯一名称。

        > **备注**：边栏选项卡将自动检查名称的唯一性，并在需要选择其他名称时通知你。

    1.  将 **“订阅”** 文本框设置为默认值。

    1.  在 **“资源组”** 下拉列表中，选择现有的 **ContainerCompute** 选项。

    1.  在 **“位置”** 文本框中，选择 **“美国东部”**。

    1.  在 **“SKU”** 下拉列表中，选择 **“基本设置”**。

    1.  选择 **“创建”**。  

    > **备注**：等待创建任务完成后再继续本实验室。

#### 任务 4：打开 Azure Cloud Shell 并存储容器注册表元数据

1.  在 Azure 门户中，选择 **“Cloud Shell”** 图标以打开一个新的 shell 实例。  

    > **备注**：等待 Cloud Shell 完成连接到实例，再继续进行本实验室。

1.  在门户的 **Cloud Shell** 命令提示符中，输入以下命令，然后按 Enter 键以查看订阅中的所有容器注册表列表：

    ```
    az acr list
    ```

1.  输入以下命令，然后按 Enter 键：

    ```
    az acr list --query "max_by([], &creationDate).name" --output tsv
    ```

1.  输入以下命令，然后按 Enter 键：

    ```
    acrName=$(az acr list --query "max_by([], &creationDate).name" --output tsv)
    ```

1.  输入以下命令，然后按 Enter 键：

    ```
    echo $acrName
    ```

#### 任务 5：将 Docker 容器映像部署到容器注册表

1.  输入以下命令并选择 Enter 键以将活动目录从 **\~/** 更改为 **\~/clouddrive/ipcheck**：

    ```
    cd ~/clouddrive/ipcheck
    ```

1.  输入以下命令并按 Enter 键，获取当前目录的内容：

    ```
    dir
    ```

1.  输入以下命令并按 Enter 以将源代码上传到容器注册表并将容器映像构建为容器注册表任务：

    ```
    az acr build --registry $acrName --image ipcheck:latest .
    ```

    > **备注**：等待生成任务完成后再继续本实验室。

1.  关闭门户中的 Cloud Shell 窗格。

#### 任务 6：在容器注册表中验证容器映像

1.  在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“ContainerCompute”** 资源组。

1.  在 **“ContainerCompute”** 边栏选项卡中，选择你之前在本实验室中创建的容器注册表。

1.  在 **“容器注册表”** 边栏选项卡中，找到 **“服务”** 部分并选择 **“存储库”** 链接。

1.  在 **“存储库”** 部分，选择 **“ipcheck”** 容器映像存储库。

1.  在 **“存储库”** 边栏选项卡中，选择 **“最新”** 标记。

1.  查找具有 **“最新”** 标记的容器映像版本的元数据。

    > **备注**：你也可以选择 **“运行 ID”** 链接以查看有关生成任务的元数据。

#### 回顾

在本练习中，你创建了一个 .NET 控制台应用程序来显示计算机的当前 IP 地址。然后，你将 **Dockerfile** 文件添加到应用程序，以便将其转换为 Docker 容器映像。最后，你将容器映像部署到容器注册表。

### 练习 3：部署 Azure 容器实例 

#### 任务 1：在容器注册表中启用管理员用户

1.  在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“ContainerCompute”** 资源组。

1.  在 **“ContainerCompute”** 边栏选项卡中，选择你之前在本实验室中创建的容器注册表。

1.  在 **“容器注册表”** 边栏选项卡中，选择 **“更新”**。

1.  在 **“更新容器注册表”** 边栏选项卡中，执行以下操作：
    
    1.   在“**管理员用户**”部分，选择“**启用**”。
    
    1.   选择“**保存**”。

    1.   关闭边栏选项卡。
    
1.  关闭 **“更新容器注册表”** 边栏选项卡。

#### 任务 2：自动将容器映像部署到 Azure 容器实例

1.  在 **“容器注册表”** 边栏选项卡中，找到 **“服务”** 部分并选择 **“存储库”** 链接。

1.  在 **“存储库”** 部分，选择 **“ipcheck”** 容器映像存储库。

1.  在 **“存储库”** 边栏选项卡中，选择与 **“最新”** 标记条目关联的省略号菜单。

1.  在弹出菜单中，选择 **“运行实例”** 链接。

1.  在 **“创建容器实例”** 边栏选项卡中，执行以下操作：
    
    1.  在 **“容器名称”** 文本框中，输入 **“manualcompute”**。
    
    1.  将 **“容器映像”** 文本框保留设置为默认值。
    
    1.  在 **“OS 类型”** 部分，选择 **“Linux”**。
    
    1.  将 **“订阅”** 文本框设置为默认值。
    
    1.  在 **“资源组”** 下拉列表中，选择 **“ContainerCompute”**。
    
    1.  在 **“位置”** 下拉列表中，选择 **“美国东部”**。
    
    1.  在 **“核心数量”** 下拉列表中，选择 **“2”**。
    
    1.  在 **“内存 (GB)”** 文本框中，输入 **“4”**。
    
    1.  在 **“公共 IP 地址”** 部分，选择 **“否”**。
    
    1.  选择 **“确定”**。

    > **备注**：等待创建任务完成后再继续本实验室。

#### 任务 3：手动将容器映像部署到容器实例

1.  在 Azure 门户的“导航”窗格中，选择 **“创建资源”** 链接。

1.  在 **“新建”** 边栏选项卡，找到精选服务列表上方的 **“搜索市场”** 文本框。

1.  在搜索文本框中，输入 **“容器实例”**，然后按 Enter 键。

1.  在 **“市场”** 搜索结果边栏选项卡中，选择 **“容器实例”** 结果。

1.  在 **“容器实例”** 边栏选项卡中，选择 **“创建”**。

1.  在 **“创建容器实例”** 边栏选项卡查找选项卡，例如 **“基本设置”**、**“网络”** 和 **“高级”**。

    > **备注**：每个选项卡代表工作流中创建新容器实例的一步。

1.  在 **“基本信息”** 选项卡中，执行以下操作：

    1.  将 **“订阅”** 文本框设置为默认值。

    1.  在 **“资源组”** 下拉列表中，选择 **“ContainerCompute”**。
    
    1.  在 **“容器名称”** 文本框中，输入 **manualcompute**。

    1.  在 **“区域”** 下拉列表中，选择 **“（美国）美国东部”**。
    
    1.  在 **“映像源”** 部分，选择 **“Azure 容器注册表”**。
    
    1.  在 **“注册表”** 下拉列表中，选择你之前在本实验室中创建的 **“Azure 容器注册表”** 资源。
    
    1.  在 **“映像”** 下拉列表中，选择 **“ipcheck”**。
    
    1.  在 **“映像标记”** 下拉列表中，选择 **“最新”**。

    1.  选择 **“查看 + 创建”**。

1.  在 **“查看 + 创建”** 选项卡中，查看选定的选项。

1.  选择 **“创建”** 以使用指定配置创建容器实例。  

    > **备注**：等待创建任务完成后再继续本实验室。

#### 任务 4：验证容器实例是否成功运行

1.  在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“ContainerCompute”** 资源组。

1.  在 **“ContainerCompute”** 边栏选项卡中，选择你之前在本实验室中创建的 **“manualcompute”** 容器实例。

1.  在 **“容器实例”** 边栏选项卡中，找到 **“设置”** 部分，然后选择 **“容器”** 链接。

1.  在 **“容器”** 部分，查找 **“事件”** 列表。

1.  选择 **“日志”** 选项卡，然后找到容器实例中的短信日志。

> **备注**：你也可以选择查看 **managedcompute** 容器实例中的 **“事件”** 和 **“日志”**。

> **备注**：应用程序完成运行后，容器因为已完成工作而终止。对于手动创建的容器实例，你表示可以接受成功退出，因此该容器只运行一次。自动创建的实例没有提供此选项，并且假定该容器应始终处于运行状态，因此该容器会反复重启。

#### 回顾

在本练习中，你使用了多种方法将容器映像部署到 Azure 容器实例。通过使用手动方法，你还可以进一步自定义部署，并将基于任务的应用程序作为容器运行的一部分运行。

### 练习 4：清理订阅 

#### 任务 1：打开 Azure Cloud Shell 并列出资源组

1.  在 Azure 门户的“导航”窗格中，选择 **“Cloud Shell”** 图标以打开一个新的 shell 实例。

    > **备注**：**“Cloud Shell”** 图标使用大于符号 () 和下划线字符 (\_) 表示。

1.  如果这是你第一次使用订阅打开 Cloud Shell，则可以使用 **“欢迎使用 Azure Cloud Shell 向导”** 来配置 Cloud Shell，以便首次使用。在向导中执行以下操作：
    
    1.  对话框提示你配置 shell。选择 **“Bash”**，查看选定的订阅，然后选择 **“创建存储”**。 

    > **备注**：等待 Cloud Shell 完成首次设置过程后，再继续本实验室。如果 Cloud Shell 配置选项未显示，这很可能是因为你在本课程实验室中使用的是现有订阅。实验室是在你使用的是新订阅的假设下编写的。

#### 任务 2：删除资源组

1.  输入以下命令，然后按 Enter 键以删除 **ContainerCompute** 资源组：

    ```
    az group delete --name ContainerCompute --no-wait --yes
    ```

1.  关闭门户中的 Cloud Shell 窗格。

#### 任务 3：关闭活动应用程序

-   关闭当前正在运行的 Microsoft Edge 应用程序。

#### 回顾

在本练习中，你通过删除本实验室中使用的资源组清理订阅。
