---
lab:
    az204Title: '实验室 07: 以更安全地方式跨服务访问资源机密'
    az020Title: '实验室 07: 以更安全地方式跨服务访问资源机密'
    az204Module: '模块 07: 实现安全云解决方案'
    az020Module: '模块 07: 实现安全云解决方案'
    type: '答案要点'
---

# 实验室 07：以更安全地方式跨服务访问资源机密
# 学生实验室答案要点

## Microsoft Azure 用户界面

鉴于 Microsoft 云工具的动态特性，Azure 用户界面 (UI) 在此培训内容开发后可能会发生更改。这些更改可能会导致实验室说明和实验室步骤不一致。

当社区要求我们进行更改时，Microsoft 将更新此培训课程。但是，由于云更新频繁发生，因此在此培训内容更新之前，你可能会遇到 UI 更改情况。**如果发生这种情况，请适应这些更改，并根据需要在实验室中熟悉这些更改。**

## 说明

### 准备工作

#### 登录实验室虚拟机

使用以下凭据登录到 Windows 10 虚拟机 (VM)：

- 用户名：**Admin**
- 密码：**Pa55w.rd**

> **备注**：你的讲师将提供连接到虚拟实验室环境的说明。

#### 查看已安装的应用程序

在你的 Windows 10 桌面上找到任务栏。任务栏里有本实验室中你将使用的应用程序的图标：

- Microsoft Edge
- 文件资源管理器
- Windows 终端
- Visual Studio Code

### 练习 1：创建 Azure 资源

#### 任务 1：打开 Azure 门户

1. 在任务栏上，选择 **“Microsoft Edge”** 图标。
1. 在打开的浏览器窗口中，转到 **Azure 门户** (<https://portal.azure.com>)。
1. 输入你的 Microsoft 帐户的电子邮件地址，然后选择 **“下一步”**。
1. 输入 Microsoft 帐户的**密码**，然后选择 **“登录”**。
    > **备注**：你第一次登录 Azure 门户时会为你提供门户导览。如果想跳过该导览，请选择 **“开始使用”** 以开始使用门户。

#### 任务 2：创建 Azure 存储帐户

1. 在 Azure 门户的“导航”窗格中，选择 **“所有服务”**。
1. 在 **“所有服务”** 边栏选项卡中，选择 **“存储帐户”**。
1. 在 **“存储帐户”** 边栏选项卡中，找到 Storage 实例列表。
1. 在 **“存储帐户”** 边栏选项卡中，选择 **“新建”**。
1. 从 **“创建存储帐户”** 边栏选项卡中找到各选项卡，例如 **“基本”**。
    > **备注**：每个选项卡代表工作流中创建新存储帐户的一个步骤。你可以随时选择 **“查看 + 创建”** 跳过其余选项卡。
1. 在 **“基本信息”** 选项卡中，执行以下操作：
    1. 将 **“订阅”** 文本框设置为默认值。
    1. 在 **“资源组”** 部分，选择 **“新建”**，输入 **“ConfidentialStack”**，然后选择 **“确定”**。
    1. 在 **“存储帐户名称”** 文本框中，输入 **“securestor[yourname]”**。
    1. 在 **“位置”** 下拉列表中，选择 **“(美国)美国东部”** 区域。
    1. 在 **“性能”** 部分中，选择 **“标准”**。
    1. 在 **“帐户类型”** 下拉列表中，选择 **“StorageV2 (常规用途 v2)”**。
    1. 在 **“复制”** 下拉列表中，选择 **“本地冗余存储(LRS)”**。
    1. 选择 **“查看 + 创建”**。
1. 在 **“查看 + 创建”** 选项卡中，查看在先前步骤中选择的选项。
1. 选择 **“创建”**，使用指定的配置创建存储帐户。
    > **备注**：等待创建任务完成，再继续本实验室。
1. 在 Azure 门户的“导航”窗格中，选择 **“所有服务”**。
1. 在 **“所有服务”** 边栏选项卡中，选择 **“存储帐户”**。
1. 在 **“存储帐户”** 边栏选项卡中，选择你之前在本实验室中创建的 **“securestor[yourname]”** 存储帐户。
1. 在 **“存储帐户”** 边栏选项卡中，找到 **“设置”** 部分并选择 **“访问密钥”** 链接。
1. 在 **“访问密钥”** 边栏选项卡中，选择任意一个密钥并记录 **“连接字符串”** 框中的任意值。你稍后将在本实验室中使用此值。
    > **备注**：你选择哪个连接字符串无关紧要。它们可以互换。

#### 任务 3：创建 Azure Key Vault

1. 在 Azure 门户的“导航”窗格中，选择 **“创建资源”** 链接。
1. 在 **“新建”** 边栏选项卡，找到精选服务列表上方的 **“搜索市场”** 文本框。
1. 在搜索框中，输入 **“保管库”**，然后按 Enter。
1. 在 **“市场”** 搜索结果边栏选项卡中，选择 **“密钥保管库”** 结果。
1. 在 **“密钥保管库”** 边栏选项卡中，选择 **“创建”**。
1. 从 **“创建密钥保管库”** 边栏选项卡中找到各选项卡，例如 **“基本”**。
    > **备注**：每个选项卡都代表在工作流中新建密钥保管库的一个步骤。你可以随时选择 **“查看 + 创建”** 跳过其余选项卡。
1. 在 **“基本信息”** 选项卡中，执行以下操作：
    1. 将 **“订阅”** 文本框设置为默认值。
    1. 在 **“资源组”** 部分，选择 **“使用现有”**，然后从列表选择 **“ConfidentialStack”**。
    1. 在 **“密钥保管库名称”** 文本框中，输入 **“securevault[yourname]”**。
    1. 在 **“区域”** 下拉列表中，选择 **“美国东部”** 区域。
    1. 在 **“定价层”** 下拉列表中，选择 **“标准”**。
    1. 选择 **“查看 + 创建”**。
1. 在 **“查看 + 创建”** 选项卡中，查看在先前步骤中选择的选项。
1. 选择 **“创建”**，使用指定的配置创建密钥保管库。
    > **备注**：等待创建任务完成，再继续本实验室。

#### 任务 4：创建 Azure Functions 应用

1. 在 Azure 门户的“导航”窗格中，选择 **“创建资源”** 链接。
1. 在 **“新建”** 边栏选项卡，找到精选服务列表上方的 **“搜索市场”** 文本框。
1. 在搜索文本框中，输入 **“函数”**，然后按 Enter。
1. 在 **“市场”** 搜索结果边栏选项卡中，选择 **“函数应用”** 结果。
1. 在 **“函数应用”** 边栏选项卡中，选择 **“创建”**。
1. 从 **“函数应用”** 边栏选项卡中找到各选项卡，例如 **“基本”**。
    > **备注**：每个选项卡都代表在工作流中新建函数应用的一个步骤。你可以随时选择 **“查看 + 创建”** 跳过其余选项卡。
1. 在 **“基本信息”** 选项卡中，执行以下操作：
    1. 将 **“订阅”** 文本框设置为默认值。
    1. 在 **“资源组”** 部分，选择 **“使用现有”**，然后从列表选择 **“ConfidentialStack”**。
    1. 在 **“函数应用名称”** 文本框中，输入 **“securefunc[yourname]”**。
    1. 在 **“发布”** 部分，选择 **“代码”**。
    1. 在 **“运行时堆栈”** 下拉列表中选择 **“.NET”**。
    1. 在 **“版本”** 下拉列表中，选择 **“3.1”**。
    1. 在 **“区域”** 下拉列表中，选择 **“美国东部”** 区域。
    1. 选择 **“下一步: 托管”** 。
1. 在 **“托管”** 选项卡中，执行以下操作：
    1. 在 **“操作系统”** 部分，选择 **“Linux”**。
    1. 在 **“存储帐户”** 下拉列表中，选择你之前在本实验室中创建的 **“securestor[yourname]”** 存储帐户。
    1. 在 **“计划类型”** 下拉列表中，选择 **“消耗(无服务器)”** 选项。
    1. 选择 **“查看 + 创建”**。
1. 在 **“查看 + 创建”** 选项卡中，查看在先前步骤中选择的选项。
1. 选择 **“创建”**，使用指定的配置创建函数应用。
    > **备注**：等待创建任务完成，再继续本实验室。

> **回顾**：在本练习中，你创建了本实验室所需的所有资源。

### 练习 2：配置机密和标识

#### 任务 1：配置系统分配的托管服务标识

1. 在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。
1. 在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“ConfidentialStack”** 资源组。
1. 在 **“ConfidentialStack”** 边栏选项卡中，选择你之前在本实验室中创建的 **“securefunc[yourname]”** 函数应用。
1. 在 **“应用服务”** 边栏选项卡中，选择 **“设置”** 部分的 **“标识”** 选项。
1. 在 **“标识”** 窗格中，找到 **“系统分配”** 选项卡，然后执行以下操作：
    1. 在 **“状态”** 部分，选择 **“开启”**，然后选择 **“保存”**。
    1. 在确认对话框中，选择 **“是”**。
    > **备注**：等待系统分配的托管标识创建完成后再继续本实验。

#### 任务 2：创建密钥保管库机密

1. 在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。
1. 在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“ConfidentialStack”** 资源组。
1. 在 **“ConfidentialStack”** 边栏选项卡中，选择你之前在本实验室中创建的 **“securevault[yourname]”** 密钥保管库。
1. 在 **“密钥保管库”** 边栏选项卡中，选择位于 **“设置”** 部分的 **“机密”** 链接。
1. 在 **“机密”** 窗格中，选择 **“生成/导入”**。
1. 在 **“创建机密”** 边栏选项卡中，执行以下操作：
    1. 在 **“上传选项”** 下拉列表中，选择 **“手动”**。
    1. 在 **“名称”** 文本框中，输入 **“storagecredentials”**。
    1. 在 **“值”** 文本框中，输入之前在本实验室中记录的存储帐户连接字符串。
    1. 将 **“内容类型”** 文本框保留设置为默认值。
    1. 将 **“设置激活日期”** 文本框保留设置为默认值。
    1. 将 **“设置到期日期”** 文本框保留设置为默认值。
    1. 在 **“已启用”** 部分，选择 **“是”**，然后选择 **“创建”**。
    > **备注**：等待机密创建完成后再继续本实验。
1. 返回“机密”窗格，选择列表中的 **“storagecredentials”** 项。
1. 在“版本”窗格中，选择最新版本的 **“storagecredentials”** 机密。
1. 在“机密版本”窗格中，执行以下操作：
    1. 找到最新版本机密的元数据。
    1. 选择 **“显示机密值”** ，可以找到机密的值。
    1. 记录 **“机密标识符”** 文本框的值，因为你稍后将在本实验室中使用该值。
    > **备注**：是记录 **“机密标识符”** 文本框中的值，而不是 **“机密值”** 文本框中的值。

#### 任务 3：配置密钥保管库访问策略

1. 在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。
1. 在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“ConfidentialStack”** 资源组。
1. 在 **“ConfidentialStack”** 边栏选项卡中，选择你之前在本实验室中创建的 **“securevault[yourname]”** 密钥保管库。
1. 在 **“密钥保管库”** 边栏选项卡中，选择位于 **“设置”** 部分的 **“访问策略”** 链接。
1. 在“访问策略”窗格中，选择 **“添加访问策略”**。
1. 在 **“添加访问策略”** 边栏选项卡中，执行以下操作：
    1. 选择 **“选择主体”** 链接。
    1. 在 **“主体”** 边栏选项卡中，找到并选择名为 **“securefunc[yourname]”** 的服务主体，然后选择 **“选择”**。
        > **备注**：你之前在本实验室中创建的系统分配的托管标识将与 Azure Function 资源具有相同的名称。
    1. 将 **“密钥权限”** 列表保留设置为默认值。
    1. 在 **“机密权限”** 下拉列表中，选择 **“GET”** 权限。
    1. 将 **“证书权限”** 列表保留设置为默认值。
    1. 将 **“授权应用程序”** 文本框保留设置为默认值。
    1. 选择 **“添加”**。
1. 返回“访问策略”窗格，选择 **“保存”**。
    > **备注**：等待访问策略更改保存后再继续本实验室。

#### 任务 4：创建密钥保管库派生的应用程序设置

1. 在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。
1. 在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“ConfidentialStack”** 资源组。
1. 在 **“ConfidentialStack”** 边栏选项卡中，选择你之前在本实验室中创建的 **“securefunc[yourname]”** 函数应用。
1. 在 **“应用服务”** 边栏选项卡中，选择 **“设置”** 部分中的 **“配置”** 选项。
1. 在 **“配置”** 窗格中，执行以下操作：
    1. 选择 **“应用程序设置”** 选项卡，然后选择 **“新应用程序设置”**。
    1. 在出现的 **“添加/编辑应用程序设置”** 弹出窗口中，在 **“名称”** 字段，输入 **“StorageConnectionString”**。
    1. 在 **“值”** 文本框中，采用以下语法构造一个值：``@Microsoft.KeyVault(SecretUri=*Secret Identifier*)``
        > **备注**：你需要使用以上语法生成对***机密标识符***的引用。例如，如果机密标识符为 ``https://securevaultstudent.vault.azure.net/secrets/storagecredentials/17b41386df3e4191b92f089f5efb4cbf``，则值应为 ``@Microsoft.KeyVault(SecretUri=https://securevaultstudent.vault.azure.net/secrets/storagecredentials/17b41386df3e4191b92f089f5efb4cbf)``。
    1. 将 **“部署槽位设置”** 文本框保留设置为默认值。
    1. 选择 **“确定”** 关闭弹出窗口并返回到 **“配置”** 部分。
    1. 在边栏选项卡选择 **“保存”** 以保存设置。  
    1. 在 **“保存更改”** 确认弹出对话框中，选择 **“继续”**。
    > **备注**：等待应用程序设置保存后再继续本实验。

> **回顾**：在本练习中，你为函数应用创建了系统分配的托管服务标识，然后为该标识提供了相应的权限，以获取密钥保管库中的机密值。最后，你创建了函数应用的配置设置中所引用的机密。

### 练习 3：生成 Azure Functions 应用

#### 任务 1：初始化函数项目

1. 在任务栏上，选择 **“Windows 终端”** 图标。
1. 输入以下命令并按 Enter 以将当前目录更改为 **“Allfiles (F):\\Allfiles\\Labs\\07\\Starter\\func”** 空目录：

    ```powershell
    cd F:\Allfiles\Labs\07\Starter\func
    ```

1. 在打开的命令提示符处，输入以下命令然后按 Enter，以使用 **Azure Functions Core Tools** 在当前目录中创建使用 **dotnet** 运行时的新本地 Functions 项目：

    ```powershell
    func init --worker-runtime dotnet --force
    ```

    > **备注**：可以查看文档以使用 **Azure Functions Core Tools** [创建新项目][azure-functions-core-tools-new-project]。
1. 输入以下命令，然后按 Enter **生成** .NET Core 3.1 项目：

    ```powershell
    dotnet build
    ```

#### 任务 2：创建 HTTP 触发的函数

1. 同样在打开的命令提示符处，输入以下命令然后按 Enter，以使用 **Azure Functions Core Tools** 创建使用 **HTTP 触发**模板的新函数（名为 **“FileParser”**）：

    ```powershell
    func new --template "HTTP trigger" --name "FileParser"
    ```

    > **备注**：可以查看文档以使用 **Azure Functions Core Tools** [创建新函数][azure-functions-core-tools-new-function]。
1. 关闭当前运行的 **“Windows 终端”** 应用程序。

#### 任务 3：配置和读取应用程序设置

1. 在 **“启动”** 屏幕上，选择 **“Visual Studio Code”** 磁贴。
1. 在 **“文件”** 菜单上，选择 **“打开文件夹”**。
1. 在打开的 **“文件资源管理器”** 窗格中，浏览到 **“Allfiles (F):\\Allfiles\\Labs\\07\\Starter\\func”**，然后选择 **“选择文件夹”**。
1. 在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，打开 **local.settings.json** 文件。
1. 观察 **Values** 对象的当前值：

    ```json
    "Values": {
        "AzureWebJobsStorage": "UseDevelopmentStorage=true",
        "FUNCTIONS_WORKER_RUNTIME": "dotnet"
    }
    ```

1. 通过添加名为 **StorageConnectionString** 的新设置并将其设置为 **[TEST VALUE]** 的字符串值来更新 **Values** 对象的值：

    ```json
    "Values": {
        "AzureWebJobsStorage": "UseDevelopmentStorage=true",
        "FUNCTIONS_WORKER_RUNTIME": "dotnet",
        "StorageConnectionString": "[TEST VALUE]"
    }
    ```

1. **Local.settings.json** 文件现应包括：

    ```json
    {
        "IsEncrypted": false,
        "Values": {
            "AzureWebJobsStorage": "UseDevelopmentStorage=true",
            "FUNCTIONS_WORKER_RUNTIME": "dotnet",
            "StorageConnectionString": "[TEST VALUE]"
        }
    }
    ```

1. 在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，打开 **FileParser.cs** 文件。
1. 在代码编辑器中，观察示例实现：

    ```csharp
    using System;
    using System.IO;
    using System.Threading.Tasks;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Extensions.Http;
    using Microsoft.AspNetCore.Http;
    using Microsoft.Extensions.Logging;
    using Newtonsoft.Json;

    namespace func
    {
        public static class FileParser
        {
            [FunctionName("FileParser")]
            public static async Task<IActionResult> Run(
                [HttpTrigger(AuthorizationLevel.Function, "get", "post", Route = null)] HttpRequest req,
                ILogger log)
            {
                log.LogInformation("C# HTTP trigger function processed a request.");

                string name = req.Query["name"];

                string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
                dynamic data = JsonConvert.DeserializeObject(requestBody);
                name = name ?? data?.name;

                string responseMessage = string.IsNullOrEmpty(name)
                    ? "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response."
                    : $"Hello, {name}. This HTTP triggered function executed successfully.";

                return new OkObjectResult(responseMessage);
            }
        }
    }
    ```

1. 删除 **FileParser.cs** 文件中的所有内容。
1. 添加以下代码行，为 **Microsoft.AspNetCore.Mvc**、**Microsoft.Azure.WebJobs**、**Microsoft.AspNetCore.Http**、**System** 和 **System.Threading.Tasks** 命名空间添加 **using 指令**：

    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using System;
    using System.Threading.Tasks;
    ```

1. 创建名为 **FileParser** 的新**公共静态**类：

    ```csharp
    public static class FileParser
    { }
    ```

1. 再次观察 **FileParser.cs** 文件，该文件现在应包括：

    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using System;
    using System.Threading.Tasks;

    public static class FileParser
    { }
    ```

1. 在 **FileParser** 类中，添加以下代码块，创建名为 **Run** 的新**公共静态** *异步*方法，该方法返回类型为 **Task\<IActionResult\>** 的变量，并且还采用类型为 **HttpRequest** 的变量 *request*：

    ```csharp
    public static async Task<IActionResult> Run(
        HttpRequest request)
    { }
    ```

1. 添加以下代码，将属性追加到类型为 **FunctionNameAttribute** 的 **Run** 方法中，该方法的**名称**参数设置为 **FileParser** 的值：

    ```csharp
    [FunctionName("FileParser")]
    public static async Task<IActionResult> Run(
        HttpRequest request)
    { }
    ```

1. 添加以下代码，将属性追加到类型为 **HttpTriggerAttribute** 的 **request** 参数，该参数的 **methods** 参数数组设置为 **GET** 的一个值：

    ```csharp
    [FunctionName("FileParser")]
    public static async Task<IActionResult> Run(
        [HttpTrigger("GET")] HttpRequest request)
    { }
    ```

1. 再次观察 **FileParser.cs** 文件，该文件现在应包括：

    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using System;
    using System.Threading.Tasks;

    public static class FileParser
    {
        [FunctionName("FileParser")]
        public static async Task<IActionResult> Run(
            [HttpTrigger("GET")] HttpRequest request)
        { }
    }
    ```

1. 在 **Run** 方法中输入以下代码行，通过使用 **Environment.GetEnvironmentVariable** 方法并将结果存储在名为 **connectionString** 的字**符串**变量中来检索 **StorageConnectionString** 应用程序设置的值：

    ```csharp
    string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
    ```

1. 输入以下代码行以将 **connectionString** 变量的值作为 HTTP 响应返回：

    ```csharp
    return new OkObjectResult(connectionString);
    ```

1. 再次观察 **FileParser.cs** 文件，该文件现在应包括：

    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using System;
    using System.Threading.Tasks;

    public static class FileParser
    {
        [FunctionName("FileParser")]
        public static async Task<IActionResult> Run(
            [HttpTrigger("GET")] HttpRequest request)
        {
            string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
            return new OkObjectResult(connectionString);
        }
    }
    ```

1. 选择 **“保存”** 以保存对 **FileParser.cs** 文件的更改。

#### 任务 4：验证本地函数

1. 在任务栏上，选择 **“Windows 终端”** 图标。
1. 输入以下命令并按 Enter 以将当前目录更改为 **“Allfiles (F):\\Allfiles\\Labs\\07\\Starter\\func”** 空目录：

    ```powershell
    cd F:\Allfiles\Labs\07\Starter\func
    ```

1. 在打开的命令提示符处，输入以下命令并按 Enter，以运行函数应用项目：

    ```powershell
    func start --build
    ```

    > **备注**：可以查看文档以使用 **Azure Functions Core Tools** [在本地启动函数应用项目][azure-functions-core-tools-start-function]。
1. 在任务栏上再次选择 **“Windows 终端”** 图标以打开 **Windows Terminal** 应用程序的新实例。
1. 在收到打开的命令提示符时，输入以下命令，然后按 Enter 以启动 **httprepl** 工具，将基本统一资源标识符 (URI) 设置为 ``http://localhost:7071``：

    ```powershell
    httprepl http://localhost:7071
    ```

    > **备注**：httprepl 工具会显示一条错误消息。出现此消息的原因是该工具正在搜索用于“遍历”API 的 Swagger 定义文件。由于函数项目不会生成 Swagger 定义文件，因此你需要手动遍历该 API。
1. 在收到工具提示符时，输入以下命令，然后按 Enter 浏览到相关的 **api** 目录：

    ```powershell
    cd api
    ```

1. 输入以下命令，然后按 Enter 浏览到相关的的 **fileparser** 目录：

    ```powershell
    cd fileparser
    ```

1. 输入以下命令，然后按 Enter 运行 **get** 命令：

    ```powershell
    get
    ```

1. 查看作为 HTTP 请求结果返回的 **StorageConnectionString** 的 **[TEST VALUE]** 值：

    ```powershell
    HTTP/1.1 200 OK
    Content-Type: text/plain; charset=utf-8
    Date: Tue, 01 Sep 2020 23:35:39 GMT
    Server: Kestrel
    Transfer-Encoding: chunked

    [TEST VALUE]

    ```

1. 输入以下命令，然后按 Enter 退出 **“httprepl”** 应用程序：

    ```powershell
    exit
    ```

1. 关闭 **“Windows 终端”** 应用程序上所有当前运行的实例。

#### 任务 5：使用 Azure Functions Core Tools 进行部署

1. 在任务栏上，选择 **“Windows 终端”** 图标。
1. 输入以下命令并按 Enter 以将当前目录更改为 **“Allfiles (F):\\Allfiles\\Labs\\07\\Starter\\func”** 空目录：

    ```powershell
    cd F:\Allfiles\Labs\07\Starter\func
    ```

1. 在打开的命令提示符中，输入以下命令并按 Enter 以登录 Azure 命令行接口 (CLI)：

    ```powershell
    az login
    ```

1. 在 **Microsoft Edge** 浏览器窗口中，执行以下操作：
    1. 输入你的 Microsoft 帐户的电子邮件地址，然后选择 **“下一步”**。
    1. 输入 Microsoft 帐户的密码，然后选择 **“登录”**。
1. 返回当前打开的 **Windows Terminal** 窗口。等待登录过程完成。
1. 输入以下命令，然后按 Enter 发布函数应用项目：

    ```powershell
    func azure functionapp publish <function-app-name>
    ```

    > **备注**：例如，如果**函数应用名称**为 **securefuncstudent**，则命令将为 ``func azure functionapp publish securefuncstudent``。可以查看文档以使用 **Azure Functions Core Tools** [发布本地函数应用项目][azure-functions-core-tools-publish-azure]。
1. 等待部署完成后，再继续本实验室。
1. 关闭当前运行的 **“Windows 终端”** 应用程序。

#### 任务 6：测试密钥保管库派生的应用程序设置

1. 在任务栏上，选择 **“Microsoft Edge”** 图标。
1. 在打开的浏览器窗口中，转到 Azure 门户 (<https://portal.azure.com>)。
1. 在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。
1. 在 **“资源组”** 边栏选项卡上，找到并选择你之前在本实验室中创建的 **“ConfidentialStack”** 资源组。
1. 在 **“ConfidentialStack”** 边栏选项卡上，选择你之前在本实验室中创建的 **“securefunc[yourname]”** 函数应用。
1. 在 **“应用服务”** 边栏选项卡中，从 **“函数”** 部分选择 **“函数”** 选项。
1. 在 **“函数** ”窗格中选择现有的“ **FileParser”** 函数。
1. 在 **“函数”** 边栏选项卡上的 **“开发人员”** 部分中选择 **“代码 + 测试”** 选项。
1. 在函数编辑器中，选择 **“测试/运行”**。
1. 在显示的弹出对话框中，执行以下操作：
    - 在 **“HTTP 方法”** 列表中，选择 **“GET”**。
1. 选择 **“运行”** 以测试函数。
1. 观察运行测试的结果。结果应为 Azure 存储连接字符串。

> **回顾**：在本练习中，你使用了服务标识来读取存储在密钥保管库中的机密值，并返回该值作为函数应用的结果。

### 练习 4：访问 Azure Blob 存储数据

#### 任务 1：上传示例存储 blob

1. 在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。
1. 在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“ConfidentialStack”** 资源组。
1. 在 **“ConfidentialStack”** 边栏选项卡中，选择你之前在本实验室中创建的 **“securestor[yourname]”** 存储帐户。
1. 在 **“存储帐户”** 边栏选项卡中，选择 **“Blob 服务”** 部分的 **“容器”** 链接。
1. 在 **“容器”** 部分，选择 **“+ 容器”**。
1. 在 **“新建容器”** 弹出窗口中，执行以下操作：
    1. 在 **“名称”** 文本框中，输入 **“drop”**。
    1. 从 **“公共访问级别”** 下拉列表中，选择 **“Blob (仅限 Blob 的匿名读取访问)”**，然后选择 **“创建”**。
1. 返回 **“容器”** 部分，然后选择新创建的 **drop** 容器。
1. 在 **“容器”** 边栏选项卡中，选择 **“上传”**。
1. 在 **“上传 Blob”** 弹出窗口中，执行以下操作：
    1. 在 **“文件”** 部分，选择 **“文件夹”** 图标。
    1. 在 **“文件资源管理器”** 窗口中，浏览到 **“Allfiles (F):\\Allfiles\\Labs\\07\\Starter”**，选择 **“records.json”** 文件，然后选择 **“打开”**。
    1. 确保 **“如果文件已存在，则覆盖”** 已选中，然后选择 **“上传”**。  
    > **备注**：等待 Blob 上传完成，然后再继续本实验室。
1. 返回 **“容器”** 边栏选项卡，选择 Blob 列表中的 **“records.json”** Blob。
1. 在 **“Blob”** 边栏选项卡中，找到 Blob 元数据，然后复制该 Blob 的 URL。
1. 在任务栏上，右键单击 **“Microsoft Edge”** 图标或激活快捷菜单，然后选择 **“新建窗口”**。
1. 在新的浏览器窗口中，前往你为 Blob 复制的 URL。
1. 现在应该显示 Blob 的 JavaScript 对象表示法 (JSON) 内容。关闭显示 JSON 内容的浏览器窗口。
1. 返回显示 Azure 门户的浏览器窗口，然后关闭 **“Blob”** 边栏选项卡。
1. 返回 **“容器”** 边栏选项卡，然后选择 **“更改访问级别策略”**。
1. 在 **“更改访问级别”** 弹出窗口中，执行以下操作：
    1. 在 **“公共访问级别”** 下拉列表中，选择 **“专用(非匿名访问)”**。
    1. 选择 **“确定”**。
1. 在任务栏上，右键单击 **“Microsoft Edge”** 图标或激活快捷菜单，然后选择 **“新建窗口”**。
1. 在新的浏览器窗口中，前往你为 Blob 复制的 URL。
1. 现在应该显示一条表示未找到资源的错误消息。
    > **备注**：如果没有显示该错误消息，则浏览器可能缓存了该文件。按 Ctrl+F5 刷新页面，直到出现错误提示。

#### 任务 2：请求并配置用于 .NET 的 Azure SDK

1. 在任务栏上，选择 **“Windows 终端”** 图标。
1. 输入以下命令并按 Enter 以将当前目录更改为 **“Allfiles (F):\\Allfiles\\Labs\\07\\Starter\\func”** 空目录：

    ```powershell
    cd F:\Allfiles\Labs\07\Starter\func
    ```

1. 在打开的命令提示符中，输入以下命令并按 Enter，从 NuGet 添加 **12.6.0** 版本的 **Azure.Storage.Blobs** 包：

    ```powershell
    dotnet add package Azure.Storage.Blobs --version 12.6.0
    ```

    > **备注**：[Azure.Storage.Blobs](https://www.nuget.org/packages/Azure.Storage.Blobs/12.6.0) NuGet 包引用为 Azure Blob 存储编写代码所需的用于 .NET 的 Azure SDK 的子集。
1. 关闭当前运行的 **“Windows 终端”** 应用程序。
1. 在 **“启动”** 屏幕上，选择 **“Visual Studio Code”** 磁贴。
1. 在 **“文件”** 菜单上，选择 **“打开文件夹”**。
1. 在打开的 **“文件资源管理器”** 窗格中，浏览到 **“Allfiles (F):\\Allfiles\\Labs\\07\\Starter\\func”**，然后选择 **“选择文件夹”**。
1. 在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，打开 **FileParser.cs** 文件。
1. 为 **Azure.Storage.Blobs** 命名空间添加 **using 指令**：

    ```csharp
    using Azure.Storage.Blobs;
    ```

1. 观察 **FileParser.cs** 文件，该文件现在应包括：

    ```csharp
    using Azure.Storage.Blobs;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using System;
    using System.Threading.Tasks;

    public static class FileParser
    {
        [FunctionName("FileParser")]
        public static async Task<IActionResult> Run(
            [HttpTrigger("GET")] HttpRequest request)
        {
            string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
            return new OkObjectResult(connectionString);
        }
    }
    ```

#### 任务 3：使用用于 .NET 的 Azure SDK 编写 Azure Blob 存储代码

1. 在 **FileParser** 类的 **Run** 方法中，删除以下代码行：

    ```csharp
    return new OkObjectResult(connectionString);
    ```

1. 同样是在 **Run** 方法中，添加以下代码块，通过将 *connectionString* 变量、``"drop"``字符串值和``"records.json"``字符串值传递给构造函数来创建 **BlobClient** 类的新实例：

    ```csharp
    BlobClient blob = new BlobClient(connectionString, "drop", "records.json");
    ```

1. 同样是在 **Run** 方法中，添加以下代码块，使用 **BlobClient.DownloadAsync** 方法异步下载引用的 Blob 的内容，并将结果存储在名为 *response* 的变量中：

    ```csharp
    var response = await blob.DownloadAsync();
    ```

1. 同样是在 **Run** 方法中，添加以下代码块，使用 **FileStreamResult** 类构造函数返回存储在 *content* 变量中的各种内容的值：

    ```csharp
    return new FileStreamResult(response?.Value?.Content, response?.Value?.ContentType);
    ```

1. 再次观察 **FileParser.cs** 文件，该文件现在应包括：

    ```csharp
    using Azure.Storage.Blobs;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using System;
    using System.Threading.Tasks;

    public static class FileParser
    {
        [FunctionName("FileParser")]
        public static async Task<IActionResult> Run(
            [HttpTrigger("GET")] HttpRequest request)
        {
            string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
            BlobClient blob = new BlobClient(connectionString, "drop", "records.json");
            var response = await blob.DownloadAsync();
            return new FileStreamResult(response?.Value?.Content, response?.Value?.ContentType);
        }
    }
    ```

1. 选择 **“保存”** 以保存对 **FileParser.cs** 文件的更改。

#### 任务 4：部署和验证 Azure Functions 应用

1. 在任务栏上，选择 **“Windows 终端”** 图标。
1. 输入以下命令并按 Enter 以将当前目录更改为 **“Allfiles (F):\\Allfiles\\Labs\\07\\Starter\\func”** 空目录：

    ```powershell
    cd F:\Allfiles\Labs\07\Starter\func
    ```

1. 在打开的命令提示符中，输入以下命令并按 Enter 以登录 Azure CLI：

    ```powershell
    az login
    ```

1. 在 **Microsoft Edge** 浏览器窗口中，执行以下操作：
    1. 输入你的 Microsoft 帐户的电子邮件地址，然后选择 **“下一步”**。
    1. 输入 Microsoft 帐户的密码，然后选择 **“登录”**。
1. 返回当前打开的 **Windows Terminal** 窗口。等待登录过程完成。
1. 输入以下命令，然后按 Enter 再次发布函数应用项目：

    ```powershell
    func azure functionapp publish <function-app-name>
    ```

    > **备注**：例如，如果**函数应用名称**为 **securefuncstudent**，则命令将为 ``func azure functionapp publish securefuncstudent``。可以查看文档以使用 **Azure Functions Core Tools** [发布本地函数应用项目][azure-functions-core-tools-publish-azure]。
1. 等待部署完成后，再继续本实验室。
1. 关闭当前运行的 **“Windows 终端”** 应用程序。
1. 在任务栏上，选择 **“Microsoft Edge”** 图标。
1. 在打开的浏览器窗口中，转到 Azure 门户 (<https://portal.azure.com>)。
1. 在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。
1. 在 **“资源组”** 边栏选项卡上，找到并选择你之前在本实验室中创建的 **“ConfidentialStack”** 资源组。
1. 在 **“ConfidentialStack”** 边栏选项卡上，选择你之前在本实验室中创建的 **“securefunc[yourname]”** 函数应用。
1. 在 **“应用服务”** 边栏选项卡中，从 **“函数”** 部分选择 **“函数”** 选项。
1. 在 **“函数”** 窗格中选择现有的 **“FileParser”** 函数。
1. 在 **“函数”** 边栏选项卡上的 **“开发人员”** 部分中选择 **“代码 + 测试”** 选项。
1. 在函数编辑器中，选择 **“测试/运行”**。
1. 在显示的弹出对话框中，执行以下操作：
    - 在 **“HTTP 方法”** 列表中，选择 **“GET”**。
1. 选择 **“运行”** 以测试函数。
1. 观察运行测试的结果。输出将包含存储在 Azure 存储帐户中的 **$/drop/records.json** Blob 的内容。

> **回顾**：在本练习中，你使用了 C\# 代码来访问存储帐户，然后下载了 Blob 的内容。

### 练习 5：清理订阅

#### 任务 1：打开 Azure Cloud Shell 并列出资源组

1. 在 Azure 门户的“导航”窗格中，选择 **“Cloud Shell”** 图标以打开一个新的 shell 实例。

    > **备注**：**“Cloud Shell”** 图标使用大于符号 (\>) 和下划线字符 (\_) 表示。

1. 如果这是你第一次使用订阅打开 Cloud Shell，则可以使用 **“欢迎使用 Azure Cloud Shell 向导”** 来配置 Cloud Shell，以便首次使用。在向导中执行以下操作：

    1. 对话框提示你配置 shell。选择 **“Bash”**，查看选定的订阅，然后选择 **“创建存储”**。

    > **备注**：等待 Cloud Shell 完成首次设置过程后，再继续本实验室。如果 Cloud Shell 配置选项未显示，这很可能是因为你在本课程实验室中使用的是现有订阅。实验室是在你使用的是新订阅的假设下编写的。

#### 任务 2：删除资源组

1. 系统显示命令提示符时，输入以下命令，然后按 Enter 删除 **ConfidentialStack** 资源组：

    ```powershell
    az group delete --name ConfidentialStack --no-wait --yes
    ```

1. 关闭门户中的 Cloud Shell 窗格。

#### 任务 3：关闭活动的应用程序

1. 关闭当前正在运行的 Microsoft Edge 应用程序。

> **回顾**：在本练习中，你通过删除本实验室中使用的资源组清理订阅。
