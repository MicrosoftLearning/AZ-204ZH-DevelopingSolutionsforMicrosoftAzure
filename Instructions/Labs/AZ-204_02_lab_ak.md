---
lab:
    az204Title: '实验室 02: 使用 Azure Functions 实现任务处理操作逻辑'
    az020Title: '实验室 02: 使用 Azure Functions 实现任务处理操作逻辑'
    az204Module: '模块 02: 实现 Azure Functions'
    az020Module: '模块 02: 实现 Azure Functions'
    type: '答案要点'
---

# 实验室 02： 使用 Azure Functions 实现任务处理操作逻辑
# 学生实验室答案要点

## Microsoft Azure 用户界面

鉴于 Microsoft 云工具的动态特性，Azure 用户界面 (UI) 在此培训内容开发后可能会发生更改。这些更改可能会导致实验室说明和实验室步骤不一致。

当社区要求我们进行更改时，Microsoft 将更新此培训课程。但是，由于云更新频繁发生，因此在此培训内容更新之前，你可能会遇到 UI 更改情况。**如果发生这种情况，请适应这些更改，并根据需要在实验室中熟悉这些更改。**

## 说明

### 准备工作

#### 登录到实验室虚拟机

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
1. 在打开的浏览器窗口中，转到 Azure 门户 (<https://portal.azure.com>)。
1. 输入你的 Microsoft 帐户的电子邮件地址，然后选择 **“下一步”**。
1. 输入 Microsoft 帐户的密码，然后选择 **“登录”**。
    > **备注**：第一次登录 Azure 门户时，你会看到一个门户教程。如果想跳过该导览，请选择 **“开始使用”** 以开始使用门户。

#### 任务 2：创建 Azure 存储帐户

1. 在 Azure 门户的“导航”窗格中，选择 **“所有服务”**。
1. 在 **“所有服务”** 边栏选项卡中，选择 **“存储帐户”**。
1. 在 **“存储帐户”** 边栏选项卡上，获取存储帐户实例列表。
1. 在 **“存储帐户”** 边栏选项卡上，选择 **“新建”**。
1. 在 **“创建存储帐户”** 边栏选项卡上，查看边栏选项卡上的选项卡，如 **“基本”**、**“标记”** 和 **“查看 + 创建”**。
    > **备注**：每个选项卡代表工作流中创建新存储帐户的一个步骤。你可以随时选择 **“查看 + 创建”** 跳过其余选项卡。
1. 选择 **“基本信息”** 选项卡，然后在选项卡区域内执行以下操作：
    1. 将 **“订阅”** 文本框设置为默认值。
    1. 在 **“资源组”** 部分，选择 **“新建”**，输入 **“Serverless”**，然后选择 **“确定”**。
    1. 在 **“存储帐户名称”** 文本框中，输入 **“funcstor[yourname]”**。
    1. 在 **“位置”** 列表中，选择 **“(美国)美国东部”** 区域。
    1. 在 **“性能”** 部分中，选择 **“标准”**。
    1. 在 **“帐户类型”** 列表中，选择 **“StorageV2(常规用途 v2)”**。
    1. 在 **“复制”** 列表中，选择 **“本地冗余存储(LRS)”**。
    1. 选择 **“查看 + 创建”**。
1. 在 **“查看 + 创建”** 选项卡中，查看在之前步骤中指定的选项。
1. 选择 **“创建”**，使用指定的配置创建存储帐户。
    > **备注**：在 **“部署”** 边栏选项卡中，等待创建任务完成后再继续本实验室。
1. 在 Azure 门户的“导航”窗格中，选择 **“所有服务”**。
1. 在 **“所有服务”** 边栏选项卡中，选择 **“存储帐户”**。
1. 在 **“存储帐户”** 边栏选项卡，选择 **funcstor[yourname]** 存储帐户实例。
1. 在 **“储存帐户”** 边栏选项卡上，找到 **“设置”** 部分，然后选择 **“访问密钥”**。
1. 在 **“访问密钥”** 边栏选项卡中，选择任意一个密钥并记录 **“连接字符串”** 框中的任意一个值。
    > **备注**：你将在稍后的实验室中使用此值。你选择哪个连接字符串无关紧要。它们可以互换。

#### 任务 3：创建一个函数应用

1. 在 Azure 门户的“导航”窗格中，选择 **“创建资源”** 链接。
1. 在 **“新建”** 边栏选项卡上，找到 **“搜索市场”** 文本框。
1. 在搜索文本框中，输入 **“函数”**，然后按 Enter。
1. 在 **“全部内容”** 搜索结果边栏选项卡中，选择 **“函数应用”** 结果。
1. 在 **“函数应用”** 边栏选项卡中，选择 **“创建”**。
1. 查看 **“函数应用”** 边栏选项卡的选项卡，例如 **“基本”**。
    > **备注**：每个选项卡都代表在工作流中新建函数应用的一个步骤。你可以随时选择 **“查看 + 创建”** 跳过其余选项卡。
1. 在 **“基本信息”** 选项卡上，执行以下操作：
    1. 将 **“订阅”** 文本框设置为默认值。
    1. 在 **“资源组”** 部分，选择 **“使用现有”**，然后从列表选择 **“无服务器”**。
    1. 在 **“函数应用名称”** 文本框中，输入 **“funclogic[yourname]”**。
    1. 在 **“发布”** 部分，选择 **“代码”**。
    1. 在 **“运行时堆栈”** 下拉列表中选择 **“.NET”**。
    1. 在 **“版本”** 下拉列表中，选择 **“3.1”**。
    1. 在 **“区域”** 下拉列表中，选择 **“美国东部”** 区域。
    1. 选择 **“下一步: 托管”**。
1. 在 **“托管”** 选项卡中，执行以下操作：
    1. 在 **“操作系统”** 部分，选择 **“Linux”**。
    1. 在 **“存储帐户”** 下拉列表中，选择你之前在本实验室中创建的 **“funcstor[yourname]”** 存储帐户。
    1. 在 **“计划类型”** 下拉列表中，选择 **“使用”** 选项。
    1. 选择 **“查看 + 创建”**。
1. 在 **“查看 + 创建”** 选项卡中，查看在上述步骤中选择的选项。
1. 选择 **“创建”**，使用指定的配置创建函数应用。
    > **备注**：等待创建任务完成，再继续本实验室。

> **回顾**：在本练习中，你创建了本实验室所需的所有资源。

### 练习 2： 配置本地 Azure Functions 项目

#### 任务 1：初始化函数项目

1. 在任务栏上，选择 **“Windows 终端”** 图标。
1. 输入以下命令并按 Enter 以将当前目录更改为 **“Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func”** 空目录：

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 在打开的命令提示符处，输入以下命令然后按 Enter，以使用 **Azure Functions Core Tools** 在当前目录中创建使用 **dotnet** 运行时的新本地 Azure Functions 项目：

    ```powershell
    func init --worker-runtime dotnet --force
    ```

    > **备注**：可以查看文档以使用 **Azure Functions Core Tools** [创建新项目][azure-functions-core-tools-new-project]。
1. 关闭当前运行的 **“Windows 终端”** 应用程序。

#### 任务 2：配置连接字符串

1. 在 **“启动”** 屏幕上，选择 **“Visual Studio Code”** 磁贴。
1. 在 **“文件”** 菜单上，选择 **“打开文件夹”**。
1. 在打开的 **“文件资源管理器”** 窗格中，浏览到 **“Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func”**，然后选择 **“选择文件夹”**。
1. 在 **“Visual Studio Code”** 窗口的 **“资源管理器”** 窗格中，打开 **local.settings.json** 文件。
1. 观察 **AzureWebJobsStorage** 设置的当前值：

    ```json
    "AzureWebJobsStorage": "UseDevelopmentStorage=true",
    ```

1. 通过将 **“AzureWebJobsStorage”** 的值设置为你之前在本实验室中记录的存储帐户的 **“连接字符串”** 来更新该值。

#### 任务 3：生成和验证项目

1. 在任务栏上，选择 **“Windows 终端”** 图标。
1. 输入以下命令并按 Enter 以将当前目录更改为 **“Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func”** 空目录：

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 在打开的命令提示符处，输入以下命令并选择 Enter 以**生成** .NET Core 3.1 项目：

    ```powershell
    dotnet build
    ```

> **回顾**：在本练习中，你创建了用于 Azure Functions 开发的本地项目。

### 练习 3：创建被 HTTP 申请触发的函数

#### 任务 1：创建 HTTP 触发的函数

1. 在任务栏上，选择 **“Windows 终端”** 图标。
1. 输入以下命令并按 Enter 以将当前目录更改为 **“Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func”** 空目录：

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 在打开的命令提示符处，输入以下命令然后按 Enter，以使用 **Azure Functions Core Tools** 创建使用 **HTTP 触发**模板的新函数（名为 **“Echo”**）：

    ```powershell
    func new --template "HTTP trigger" --name "Echo"
    ```

    > **备注**：可以查看文档以使用 **Azure Functions Core Tools** [创建新函数][azure-functions-core-tools-new-function]。
1. 关闭当前运行的 **“Windows 终端”** 应用程序。

#### 任务 2：编写 HTTP 触发的函数代码

1. 在 **“启动”** 屏幕上，选择 **“Visual Studio Code”** 磁贴。
1. 在 **“文件”** 菜单上，选择 **“打开文件夹”**。
1. 在打开的 **“文件资源管理器”** 窗格中，浏览到 **“Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func”**，然后选择 **“选择文件夹”**。
1. 在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，打开 **Echo.cs** 文件。
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
        public static class Echo
        {
            [FunctionName("Echo")]
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

1. 删除 **Echo.cs** 文件中的所有内容。
1. 添加以下代码行，为 **Microsoft.AspNetCore.Mvc**、**Microsoft.Azure.WebJobs**、**Microsoft.AspNetCore.Http** 和 **Microsoft.Extensions.Logging** 命名空间添加 **using 指令**：

    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using Microsoft.Extensions.Logging;
    ```

1. 创建名为 **Echo** 的新**公共静态**类：

    ```csharp
    public static class Echo
    { }
    ```

1. 再次观察 **Echo.cs** 文件，该文件现在应包括：

    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using Microsoft.Extensions.Logging;

    public static class Echo
    { }
    ```

1. 在 **Echo** 类中，添加以下代码块，创建名为 **Run** 的新**公共静态**方法，该方法返回类型为 **IActionResult** 的变量，并且还将 **HttpRequest** 和 **ILogger** 类型的变量分别作为名为 *request* 和 *logger* 的参数：

    ```csharp
    public static IActionResult Run(
        HttpRequest request,
        ILogger logger)
    { }
    ```

1. 添加以下代码，将属性追加到类型为 **FunctionNameAttribute** 的 **Run** 方法中，该方法的**名称**参数设置为 **Echo** 的值：

    ```csharp
    [FunctionName("Echo")]
    public static IActionResult Run(
        HttpRequest request,
        ILogger logger)
    { }
    ```

1. 添加以下代码，将属性追加到类型为 **HttpTriggerAttribute** 的 **request** 参数，该参数的 **methods** 参数数组设置为 **POST** 的一个值：

    ```csharp
    [FunctionName("Echo")]
    public static IActionResult Run(
        [HttpTrigger("POST")] HttpRequest request,
        ILogger logger)
    { }
    ```

1. 再次观察 **Echo.cs** 文件，该文件现在应包括：

    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using Microsoft.Extensions.Logging;

    public static class Echo
    {
        [FunctionName("Echo")]
        public static IActionResult Run(
            [HttpTrigger("POST")] HttpRequest request,
            ILogger logger)
        { }
    }
    ```

1. 在 **Run** 方法中，输入以下代码行，记录固定消息：

    ```csharp
    logger.LogInformation("Received a request");
    ```

1. 输入以下代码行以将 HTTP 请求的正文作为 HTTP 响应进行回显：

    ```csharp
    return new OkObjectResult(request.Body);
    ```

1. 再次观察 **Echo.cs** 文件，该文件现在应包括：

    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using Microsoft.Extensions.Logging;

    public static class Echo
    {
        [FunctionName("Echo")]
        public static IActionResult Run(
            [HttpTrigger("POST")] HttpRequest request,
            ILogger logger)
        {
            logger.LogInformation("Received a request");
            return new OkObjectResult(request.Body);
        }
    }
    ```

1. 选择 **“保存”** 以保存对 **Echo.cs** 文件的更改。

#### 任务 3： 使用 httprepl 测试 HTTP 触发的函数

1. 在任务栏上，选择 **“Windows 终端”** 图标。
1. 输入以下命令并按 Enter 以将当前目录更改为 **“Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func”** 空目录：

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 在打开的命令提示符处，输入以下命令并按 Enter，以运行函数应用项目：

    ```powershell
    func start --build
    ```

    > **备注**：可以查看文档以使用 **Azure Functions Core Tools** [在本地启动函数应用项目][azure-functions-core-tools-start-function]。
1. 在任务栏上再次选择 **“Windows 终端”** 图标以打开 **Windows Terminal** 应用程序的新实例。
1. 在收到打开的命令提示符时，输入以下命令，然后按 Enter 以启动 **httprel** 工具，将基本统一资源标识符 (URI) 设置为 ``http://localhost:7071``：

    ```powershell
    httprepl http://localhost:7071
    ```

    > **备注**： httprepl 工具会显示一条错误消息。出现此消息的原因是该工具正在搜索用于“遍历”API 的 Swagger 定义文件。由于函数项目不会生成 Swagger 定义文件，因此你需要手动遍历该 API。
1. 在收到工具提示符时，输入以下命令，然后按 Enter 浏览到相关的 **api** 目录：

    ```powershell
    cd api
    ```

1. 输入以下命令，然后按 Enter 浏览到相对的 **“echo”** 目录：

    ```powershell
    cd echo
    ```

1. 输入以下命令，然后按 Enter 来使用 **\-\-content** 选项运行 **post** 命令，以提交数值设为 **3** 的 HTTP 请求正文：

    ```powershell
    post --content 3
    ```

1. 输入以下命令，然后按 Enter 来使用 **\-\-content** 选项运行 **post** 命令，以提交数值设为 **5** 的 HTTP 请求正文：

    ```powershell
    post --content 5
    ```

1. 输入以下命令，然后按 Enter 来使用 **\-\-content** 选项运行 **post** 命令，以提交字符串值设为 **Hello** 的 HTTP 请求正文：

    ```powershell
    post --content "Hello"
    ```

1. 输入以下命令，然后按 Enter 来使用 **\-\-content** 选项运行 **post** 命令，以发送 JavaScript 对象表示法 (JSON) 值设为 **{"msg": "Successful"}** 的 HTTP 请求正文：

    ```powershell
    post --content "{"msg": "Successful"}"
    ```

1. 输入以下命令，然后按 Enter 退出 **“httprepl”** 应用程序：

    ```powershell
    exit
    ```

1. 关闭 **“Windows 终端”** 应用程序上所有当前运行的实例。

> **回顾**：在本练习中，你成功创建了一个基本函数。该函数可回响通过 HTTP POST 申请所发送的内容。

### 练习 4：创建一个按计划触发的函数

#### 任务 1：创建由计划触发的函数

1. 在任务栏上，选择 **“Windows 终端”** 图标。
1. 输入以下命令并按 Enter 以将当前目录更改为 **“Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func”** 空目录：

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 在打开的命令提示符处，输入以下命令然后按 Enter，以使用 **Azure Functions Core Tools** 创建使用**计时器触发**模板的新函数（名为 **“Recurring”**）：

    ```powershell
    func new --template "Timer trigger" --name "Recurring"
    ```

    > **备注**：可以查看文档以使用 **Azure Functions Core Tools** [创建新函数][azure-functions-core-tools-new-function]。
1. 关闭当前运行的 **“Windows 终端”** 应用程序。

#### 任务 2：观察函数代码

1. 在 **“启动”** 屏幕上，选择 **“Visual Studio Code”** 磁贴。
1. 在 **“文件”** 菜单上，选择 **“打开文件夹”**。
1. 在打开的 **“文件资源管理器”** 窗格中，浏览到 **“Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func”**，然后选择 **“选择文件夹”**。
1. 在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，打开 **Recurring.cs** 文件。
1. 在代码编辑器中，观察实现：

    ```csharp
    using System;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Host;
    using Microsoft.Extensions.Logging;

    namespace func
    {
        public static class Recurring
        {
            [FunctionName("Recurring")]
            public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, ILogger log)
            {
                log.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");
            }
        }
    }
    ```

#### 任务 3：观察函数运行

1. 在任务栏上，选择 **“Windows 终端”** 图标。
1. 输入以下命令并按 Enter 以将当前目录更改为 **“Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func”** 空目录：

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 在打开的命令提示符处，输入以下命令并按 Enter，以运行函数应用项目：

    ```powershell
    func start --build
    ```

    > **备注**：可以查看文档以使用 **Azure Functions Core Tools** [在本地启动函数应用项目][azure-functions-core-tools-start-function]。
1. 观察大约每 5 分钟运行一次的函数。每次运行函数都应向日志呈现一条简单的消息。
1. 关闭当前运行的 **“Windows 终端”** 应用程序。

#### 任务 4：更新函数集成配置

1. 在 **“启动”** 屏幕上，选择 **“Visual Studio Code”** 磁贴。
1. 在 **“文件”** 菜单上，选择 **“打开文件夹”**。
1. 在打开的 **“文件资源管理器”** 窗格中，浏览到 **“Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func”**，然后选择 **“选择文件夹”**。
1. 在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，打开 **Recurring.cs** 文件。
1. 在代码编辑器中，观察现有的 **Run** 方法签名：

    ```csharp
    [FunctionName("Recurring")]
    public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, ILogger log)
    ```

1. 更新 **Run** 方法签名代码块以将计划更改为每 **30 秒**执行一次：

    ```csharp
    [FunctionName("Recurring")]
    public static void Run([TimerTrigger("*/30 * * * * *")]TimerInfo myTimer, ILogger log)
    ```

1. 选择 **“保存”** 以保存对 **Recurring.cs** 文件的更改。

#### 任务 5：观察函数运行

1. 在任务栏上，选择 **“Windows 终端”** 图标。
1. 输入以下命令并按 Enter 以将当前目录更改为 **“Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func”** 空目录：

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 在打开的命令提示符处，输入以下命令并按 Enter，以运行函数应用项目：

    ```powershell
    func start --build
    ```

    > **备注**：可以查看文档以使用 **Azure Functions Core Tools** [在本地启动函数应用项目][azure-functions-core-tools-start-function]。
1. 观察大约每 30 秒运行一次的函数。每次运行函数都应向日志呈现一条简单的消息。
1. 关闭当前运行的 **“Windows 终端”** 应用程序。

> **回顾**：在本练习中，你创建了一个按照固定计划自动运行的函数。

### 练习 5：创建与其他服务集成的函数

#### 任务 1：将示例内容上传到 Azure Blob 存储

1. 在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。
1. 在 **“资源组”** 边栏选项卡上，找到并选择你之前在本实验室中创建的 **“无服务器”** 资源组。
1. 在 **“无服务器”** 边栏选项卡中，选择你之前在本实验室中创建的 **“funcstor[yourname]”** 存储帐户。
1. 在 **“存储帐户”** 边栏选项卡中，选择 **“Blob 服务”** 部分的 **“容器”** 链接。
1. 在 **“容器”** 部分，选择 **“+ 容器”**。
1. 在 **“新建容器”** 弹出窗口中，执行以下操作：
    1. 在 **“名称”** 文本框中，输入 **“内容”**。
    1. 在 **“公共访问级别”** 下拉列表中，选择 **“专用(非匿名访问)”**。
    1. 选择 **“确定”**。
1. 返回到 **“容器”** 部分，然后选择最近创建的 **“内容”** 容器。
1. 在 **“容器”** 边栏选项卡中，选择 **“上传”**。
1. 在 **“上传 Blob”** 窗口中，执行以下操作：
    1. 在 **“文件”** 部分，选择 **“文件夹”** 图标。
    1. 在 **“文件资源管理器”** 窗口中，浏览到 **“Allfiles (F):\\Allfiles\\Labs\\02\\Starter”**，选择 **“settings.json”** 文件，然后选择 **“打开”**。
    1. 确保选中 **“如果文件存储已经存在，则覆盖”** 复选框，然后选择 **“上传”**。
      > **备注**： 等待 Blob 上传完成，然后再继续本实验室。

#### 任务 2：创建 HTTP 触发的函数

1. 在任务栏上，选择 **“Windows 终端”** 图标。
1. 输入以下命令并按 Enter 以将当前目录更改为 **“Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func”** 空目录：

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 在打开的命令提示符处，输入以下命令然后按 Enter，以使用 **Azure Functions Core Tools** 创建使用 **HTTP 触发模**板的新函数（名为 **“GetSettingInfo”**）：

    ```powershell
    func new --template "HTTP trigger" --name "GetSettingInfo"
    ```

    > **备注**：可以查看文档以使用 **Azure Functions Core Tools** [创建新函数][azure-functions-core-tools-new-function]。
1. 关闭当前运行的 **“Windows 终端”** 应用程序。

#### 任务 3：编写 HTTP 触发且 Blob 输入的函数代码

1. 在 **“启动”** 屏幕上，选择 **“Visual Studio Code”** 磁贴。
1. 在 **“文件”** 菜单上，选择 **“打开文件夹”**。
1. 在打开的 **“文件资源管理器”** 窗格中，浏览到 **“Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func”**，然后选择 **“选择文件夹”**。
1. 在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，打开 **GetSettingInfo.cs** 文件。
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
        public static class GetSettingInfo
        {
            [FunctionName("GetSettingInfo")]
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

1. 删除 **GetSettingInfo.cs** 文件中的所有内容。

1. 添加以下代码行，为 **Microsoft.AspNetCore.Http**、**Microsoft.AspNetCore.Mvc** 和 **Microsoft.Azure.WebJobs** 命名空间添加 **using 指令**：

    ```csharp
    using Microsoft.AspNetCore.Http;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    ```

1. 创建名为 **GetSettingInfo** 的新**公共静态**类：

    ```csharp
    public static class GetSettingInfo
    { }
    ```

1. 再次观察 **GetSettingInfo.cs** 文件，该文件现在应包括：

    ```csharp
    using Microsoft.AspNetCore.Http;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;

    public static class GetSettingInfo
    { }
    ```

1. 在 **GetSettingInfo** 类中，添加以下代码块，创建名为 **Run** 且以表达式为主体的新**公共静态**方法，该方法返回类型为 **IActionResult** 的变量，并且还将 **HttpRequest** 和**字符串**类型的变量分别作为名为 *request* 和 *json* 的参数：

    ```csharp
    public static IActionResult Run(
        HttpRequest request,
        string json)
        => null;
    ```

    > **备注**：你只是将返回值暂时设置为 **null**。

1. 添加以下代码，将属性追加到类型为 **FunctionNameAttribute** 的 **Run** 方法中，该方法的**名称**参数设置为 **GetSettingInfo** 的值：

    ```csharp
    [FunctionName("GetSettingInfo")]
    public static IActionResult Run(
        HttpRequest request,
        string json)
        => null;
    ```

1. 添加以下代码，将属性追加到类型为 **HttpTriggerAttribute** 的 **request** 参数，该参数的 **methods** 参数数组设置为 **GET** 的一个值：

    ```csharp
    [FunctionName("GetSettingInfo")]
    public static IActionResult Run(
        [HttpTrigger("GET")] HttpRequest request,
        string json)
        => null;
    ```

1. 添加以下代码将属性添加到类型为 **BlobAttribute** 的 **json** 参数中，该方法的 **blobPath** 参数设置为 **content/settings.json** 的值：

    ```csharp
    [FunctionName("GetSettingInfo")]
    public static IActionResult Run(
        [HttpTrigger("GET")] HttpRequest request,
        [Blob("content/settings.json")] string json)
        => null;
    ```

1. 添加以下代码，更新以表达式为主体的 **Run** 方法来返回类型为 **OkObjectResult** 的新实例，以将 **json** 方法参数的值作为唯一的构造函数参数传入：

    ```csharp
    [FunctionName("GetSettingInfo")]
    public static IActionResult Run(
        [HttpTrigger("GET")] HttpRequest request,
        [Blob("content/settings.json")] string json)
        => new OkObjectResult(json);
    ```

1. 再次观察 **GetSettingInfo.cs** 文件，该文件现在应包括：

    ```csharp
    using Microsoft.AspNetCore.Http;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;

    public static class GetSettingInfo
    {
        [FunctionName("GetSettingInfo")]
        public static IActionResult Run(
            [HttpTrigger("GET")] HttpRequest request,
            [Blob("content/settings.json")] string json)
            => new OkObjectResult(json);
    }
    ```

1. 选择 **“保存”** 以保存对 **GetSettingInfo.cs** 文件的更改。

#### 任务 4： 注册 Azure 存储 Blob 扩展

1. 在任务栏上，选择 **“Windows 终端”** 图标。
1. 输入以下命令并按 Enter 以将当前目录更改为 **“Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func”** 空目录：

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 在打开的命令提示符处，输入以下命令并按 Enter，以**注册** [Microsoft.Azure.WebJobs.Extensions.Storage](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Storage/4.0.4) 扩展：

    ```powershell
    func extensions install --package Microsoft.Azure.WebJobs.Extensions.Storage --version 4.0.4
    ```

1. 输入以下命令并按 Enter，通过**生成** .NET 项目来验证是否正确安装了扩展：

    ```powershell
    dotnet build
    ```

1. 关闭 **“Windows 终端”** 应用程序上所有当前运行的实例。

#### 任务 5： 使用 httprepl 测试函数

1. 在任务栏上，选择 **“Windows 终端”** 图标。
1. 输入以下命令并按 Enter 以将当前目录更改为 **“Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func”** 空目录：

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
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

    > **备注**： httprepl 工具会显示一条错误消息。出现此消息的原因是该工具正在搜索用于“遍历”API 的 Swagger 定义文件。由于函数项目不会生成 Swagger 定义文件，因此你需要手动遍历该 API。
1. 在收到工具提示符时，输入以下命令，然后按 Enter 浏览到相关的 **api** 终结点：

    ```powershell
    cd api
    ```

1. 输入以下命令，然后按 Enter 浏览到相对的 **“getsettinginfo”** 终结点：

    ```powershell
    cd getsettinginfo
    ```

1. 输入以下命令，然后按 Enter 来对当前终结点运行 **“get”** 命令：

    ```powershell
    get
    ```

1. 查看函数应用响应的 JSON 内容，该内容现在应包括：

    ```json
    {
        "version": "0.2.4",
        "root": "/usr/libexec/mews_principal/",
        "device": {
            "id": "21e46d2b2b926cba031a23c6919"
        },
        "notifications": {
            "email": "joseph.price@contoso.com",
            "phone": "(425) 555-0162 x4151"
        }
    }
    ```

1. 输入以下命令，然后按 Enter 退出 **“httprepl”** 应用程序：

    ```powershell
    exit
    ```

1. 关闭 **“Windows 终端”** 应用程序上所有当前运行的实例。

> **回顾**：在本练习中，你在 Storage 里创建了能退回 JSON 文件内容的函数。

### 练习 6：将本地函数项目部署到 Azure Functions 应用

#### 任务 1：使用 Azure Functions Core Tools 进行部署

1. 在任务栏上，选择 **“Windows 终端”** 图标。
1. 输入以下命令并按 Enter 以将当前目录更改为 **“Allfiles (F):\\Allfiles\\Labs\\02\\Starter\\func”** 空目录：

    ```powershell
    cd F:\Allfiles\Labs\02\Starter\func
    ```

1. 在打开的命令提示符处，输入以下命令并按 Enter 以登录 Azure 命令行接口 (CLI)：

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

    > **备注**：例如，如果**函数应用名称**为 **funclogicstudent**，则命令将为 ``func azure functionapp publish funclogicstudent``。可以查看文档以使用 **Azure Functions Core Tools** [发布本地函数应用项目][azure-functions-core-tools-publish-azure]。
1. 等待部署完成后，再继续本实验室。
1. 关闭当前运行的 **“Windows 终端”** 应用程序。

#### 任务 2：验证部署

1. 在任务栏上，选择 **“Microsoft Edge”** 图标。
1. 在打开的浏览器窗口中，转到 Azure 门户 (<https://portal.azure.com>)。
1. 在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。
1. 在 **“资源组”** 边栏选项卡上，找到并选择你之前在本实验室中创建的 **“无服务器”** 资源组。
1. 在 **“无服务器”** 边栏选项卡上，选择你之前在本实验室中创建的 **“funclogic[yourname]”** 函数应用。
1. 在 **“应用服务”** 边栏选项卡中，从 **“函数”** 部分选择 **“函数”** 选项。
1. 在 **“函数”** 窗格中选择现有的 **“GetSettingInfo”** 函数。
1. 在 **“函数”** 边栏选项卡上的 **“开发人员”** 部分中选择 **“代码 + 测试”** 选项。
1. 在函数编辑器中，选择 **“测试/运行”**。
1. 在显示的弹出窗口中，执行以下操作：
    - 在 **“HTTP 方法”** 列表中，选择 **“GET”**。
1. 选择 **“运行”** 以测试函数。
1. 观察运行测试的结果。JSON 内容现应包括：

    ```json
    {
        "version": "0.2.4",
        "root": "/usr/libexec/mews_principal/",
        "device": {
            "id": "21e46d2b2b926cba031a23c6919"
        },
        "notifications": {
            "email": "joseph.price@contoso.com",
            "phone": "(425) 555-0162 x4151"
        }
    }
    ```

> **回顾**：在本练习中，你将本地函数项目部署到了 Azure Functions，并验证了这些函数在 Azure 中是否能够正常工作。

### 练习 7：清理订阅

#### 任务 1：打开 Azure Cloud Shell 并列出资源组

1.  在 Azure 门户中，选择 **“Cloud Shell”** 图标以打开一个新的 shell 实例。
    > **备注**： **“Cloud Shell”** 图标使用大于符号 (\>) 和下划线字符 (\_) 表示。
1. 如果这是你第一次使用订阅打开 Cloud Shell，则可以使用 **“欢迎使用 Azure Cloud Shell 向导”** 来配置 Cloud Shell，以便首次使用。在向导中执行以下操作：
    1. 对话框提示你配置 shell。选择 **“Bash”**，查看选定的订阅，然后选择 **“创建存储”**。
    > **备注**：等待 Cloud Shell 完成首次设置过程后，再继续本实验室。如果 Cloud Shell 配置选项未显示，这很可能是因为你在本课程实验室中使用的是现有订阅。实验是假设你使用的是新订阅的情况下编写的。

#### 任务 2：删除资源组

1. 收到命令提示符处时，输入以下命令，然后按 Enter 删除 **“无服务器”** 资源组：

    ```powershell
    az group delete --name Serverless --no-wait --yes
    ```

1. 关闭门户中的 Cloud Shell 窗格。

#### 任务 3：关闭活动的应用程序

1. 关闭当前正在运行的 Microsoft Edge 应用程序。

> **回顾**：在本练习中，你通过删除本实验室中曾经使用的资源组来清理订阅。

[azure-functions-core-tools-new-function]: https://docs.microsoft.com/azure/azure-functions/functions-run-local#create-func
[azure-functions-core-tools-new-project]: https://docs.microsoft.com/azure/azure-functions/functions-run-local#create-a-local-functions-project
[azure-functions-core-tools-start-function]: https://docs.microsoft.com/azure/azure-functions/functions-run-local#start
[azure-functions-core-tools-publish-azure]: https://docs.microsoft.com/azure/azure-functions/functions-run-local#publish
