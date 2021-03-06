---
lab:
    az204Title: '实验室 10: 使用 Azure 队列存储异步处理消息'
    az020Title: '实验室 10: 使用 Azure 队列存储异步处理消息'
    az204Module: '模块 10: 开发基于消息的解决方案'
    az020Module: '模块 10: 开发基于消息的解决方案'
    type: '答案要点'
---

# 实验室 10：使用 Azure 队列存储异步处理消息
# 学生实验室答案要点

## Microsoft Azure 用户界面

鉴于 Microsoft 云工具的动态特性，Azure UI 在此培训内容开发后可能会发生更改。这些更改可能会导致实验室说明和实验室步骤不一致。

当社区要求我们进行更改时，Microsoft 将更新此培训课程。但是，由于云更新频繁发生，因此在此培训内容更新之前，你可能会遇到 UI 更改情况。**如果发生这种情况，请适应这些更改，并根据需要在实验室中熟悉这些更改。**

## 说明

### 准备工作

#### 登录到实验室虚拟机

使用以下凭据登录到 Windows 10 虚拟机 (VM)：
    
-   用户名： **Admin**

-   密码： **Pa55w.rd**

> **备注**：你的讲师将提供连接到虚拟实验室环境的说明。

#### 查看已安装的应用程序

在你的 Windows 10 桌面上找到任务栏。任务栏里有本实验室中你将使用的应用程序的图标：
    
-   Microsoft Edge

-   Visual Studio Code

-   Azure 存储资源管理器

### 练习 1：创建 Azure 资源

#### 任务 1：打开 Azure 门户

1.  在任务栏上，选择 **“Microsoft Edge”** 图标。

1.  在打开的浏览器窗口中，转到 Azure 门户 (<https://portal.azure.com>)。

1.  输入你的 Microsoft 帐户的电子邮件地址，然后选择 **“下一步”**。

1.  输入 Microsoft 帐户的密码，然后选择 **“登录”**。

    > **备注**：第一次登录 Azure 门户时，你会看到一个门户教程。选择 **“开始使用”**，以跳过导览并开始使用门户。

#### 任务 2：创建存储帐户

1.  在 Azure 门户的“导航”窗格中，选择 **“所有服务”**。

1.  在 **“所有服务”** 边栏选项卡中，选择 **“存储帐户”**。

1.  在 **“存储帐户”** 边栏选项卡上，获取存储帐户实例列表。

1.  在 **“存储帐户”** 边栏选项卡上，选择 **“新建”**。

1.  在 **“创建存储帐户”** 边栏选项卡上，查看边栏选项卡上的选项卡，如 **“基本”**、**“标记”** 和 **“查看 + 创建”**。

    > **备注**：每个选项卡代表工作流中创建新存储帐户的一个步骤。你可以随时选择 **“查看 + 创建”** 跳过其余选项卡。

1.  选择 **“基本信息”** 选项卡，然后在选项卡区域内执行以下操作：
    
    1.  将 **“订阅”** 文本框设置为默认值。
    
    1.  在 **“资源组”** 部分，选择 **“新建”**，输入 **“AsyncProcessor”**，然后选择 **“确定”**。
    
    1.  在 **“存储帐户名称”** 文本框中，输入 **“asyncstor[yourname]”**。
    
    1.  在 **“位置”** 列表中，选择 **“(美国)美国东部”** 区域。
    
    1.  在 **“性能”** 部分中，选择 **“标准”**。
    
    1.  在 **“帐户类型”** 列表中，选择 **“StorageV2(常规用途 v2)”**。
    
    1.  在 **“复制”** 列表中，选择 **“本地冗余存储(LRS)”**。
        
    1.  选择 **“查看 + 创建”**。

1.  在 **“查看 + 创建”** 选项卡中，查看在之前步骤中指定的选项。

1.  选择 **“创建”**，使用指定的配置创建存储帐户。

    > **备注**：在 **“部署”** 边栏选项卡中，等待创建任务完成后再继续本实验室。

1.	选择 **“部署”** 边栏选项卡中的 **“前往资源”** 按钮，以转到新创建的存储帐户。

1.	在 **“储存帐户”** 边栏选项卡上，找到 **“设置”** 部分，然后选择 **“访问密钥”**。

1.	在 **“访问密钥”** 边栏选项卡中，选择任意一个密钥并记录 **“连接字符串”** 框中的任意一个值。你稍后将在本实验室中使用此值。

    > **备注**：你选择哪个连接字符串无关紧要。它们可以互换。

#### 回顾

在本练习中，你创建了一个新的 Azure 存储帐户，将在实验室的其余部分使用该帐户。

### 练习 2：在 .NET 项目中配置 Azure 存储 SDK 

#### 任务 1：创建 .NET 项目

1.  在 **“启动”** 屏幕上，选择 **“Visual Studio Code”** 磁贴。

1.  在 **“文件”** 菜单中，选择 **“打开文件夹”**。

1.  在打开的 **“文件资源管理器”** 窗格中，浏览到 **“Allfiles (F):\\Allfiles\\Labs\\10\\Starter\\MessageProcessor”**，然后选择 **“选择文件夹”**。

1.  在 **“Visual Studio Code”** 窗口中，右键单击或激活“资源管理器”窗格的快捷菜单，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令并按 Enter，在当前文件夹中创建一个名为 **MessageProcessor** 的新 .NET 项目：

    ```
    dotnet new console --name MessageProcessor --output .
    ```

    > **备注**：**dotnet new** 命令将在与项目同名的文件夹中创建一个新的 **“控制台”** 项目。

1.  在命令提示符处，输入以下命令并按 Enter，从 NuGet 添加 12.0.0 版本的 **“Azure.Storage.Queues”**：

    ```
    dotnet add package Azure.Storage.Queues --version 12.0.0
    ```

    > **备注**：**dotnet add package** 命令将从 NuGet 添加 **Azure.Storage.Queues** 包。有关详细信息，请转到 [“Azure.Storage.Queues”](https://www.nuget.org/packages/Azure.Storage.Queues/12.0.0)。

1.  在命令提示符处，输入以下命令，然后按 Enter 以生成 .NET Web 应用程序：

    ```
    dotnet build
    ```

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 2：编写代码以访问 Azure 存储

1.  在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，打开 **Program.cs** 文件。

1.  在 **Program.cs** 文件的代码编辑器选项卡中，删除现有文件中的所有代码。

1.  添加以下代码行，通过从 NuGet 导入的 **“Azure.Storage.Queues”** 包导入 **“Azure”**、**“Azure.Storage.Queues”** 和 **“Azure.Storage.Queues.Models”** 命名空间：

    ```
    using Azure;
    using Azure.Storage.Queues;
    using Azure.Storage.Queues.Models;
    ```
    
1.  添加以下代码行，为此文件将使用的内置命名空间添加 **using** 指令：

    ```
    using System;
    using System.Text;
    using System.Threading.Tasks;
    ```

1.  输入以下代码，创建一个新的 **Program** 类：

    ```
    public class Program
    {
    }
    ``` 

1.  在 **Program** 类中，输入以下代码行，创建一个名为 **“storageConnectionString”** 的新字符串常量：

    ```
    private const string storageConnectionString = "";
    ```

1.  通过将 **storageConnectionString** 字符串常量的值设置为你之前在本实验室中记录的存储帐户的**连接字符串**来更新该字符串常量。

1.  在 **Program** 类中，输入以下代码行，创建一个名为 **queueName** 且值为 **“messagequeue”** 的新字符串常量：

    ```
    private const string queueName = "messagequeue";
    ```

1.  在 **Program** 类中，输入以下代码以创建新的异步 **Main** 方法：

    ```
    public static async Task Main(string[] args)
    {
    }
    ```

1.  查看 **Program.cs** 文件，该文件现在应包括：

    ```
    using Azure;
    using Azure.Storage.Queues;
    using Azure.Storage.Queues.Models;
    using System;
    using System.Text;
    using System.Threading.Tasks;

    public class Program
    {
        private const string storageConnectionString = "<storage-connection-string>";
        private const string queueName = "messagequeue";

        public static async Task Main(string[] args)
        {
        }
    }
    ```

#### 任务 3：验证 Azure 存储访问

1.  在 **Main** 方法中，通过创建类型为 **“QueueClient”** 的新变量 *client*，添加以下代码行以连接到存储帐户：

    ```
    QueueClient client = new QueueClient(storageConnectionString, queueName);  
    ```

1.  在 **Main** 方法中，添加以下代码行，通过异步方式创建队列（如果尚不存在）：

    ```        
    await client.CreateAsync();
    ```

1.  在 **Main** 方法中，添加以下代码行以呈现“帐户元数据”部分的标题：

    ```
    Console.WriteLine($"---Account Metadata---");
    ```
    
1.  在 **Main** 方法中，添加以下代码行以呈现队列终结点的统一资源标识符 (URI)：

    ```
    Console.WriteLine($"Account Uri:\t{client.Uri}");
    ```

1.  查看 **Main** 方法，该方法现在应包括：

    ```
    public static async Task Main(string[] args)
    {
        QueueClient client = new QueueClient(storageConnectionString, queueName);        
        await client.CreateAsync();

        Console.WriteLine($"---Account Metadata---");
        Console.WriteLine($"Account Uri:\t{client.Uri}");
    }
    ```

1.  保存 **Program.cs** 文件。

1.  在 **“Visual Studio Code”** 窗口中，右键单击或激活“资源管理器”窗格的快捷菜单，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令并按 “Enter” 键，以运行 .NET Web 应用程序：

    ```
    dotnet run
    ```

    > **备注**：如果出现任何生成错误，请查看位于 **“Allfiles (F):\\Allfiles\\Labs\\10\\Solution\\MessageProcessor”** 文件夹中的 **“Program.cs”** 文件。

1.  观察当前运行的控制台应用程序的输出。输出包含队列端点的元数据。

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 回顾

在本练习中，你将 .NET 项目配置为访问存储服务并处理通过该服务提供的队列。

### 练习 3：从队列中读取消息

#### 任务 1：编写代码以访问队列消息

1.  在 **Main** 方法中，添加以下代码行以呈现“现有消息”部分的标题：

    ```
    Console.WriteLine($"---Existing Messages---");
    ```

1.  在 **Main** 方法中，执行以下操作，以创建在检索队列消息时将使用的变量：

    1.  添加以下代码行，以创建一个类型为 **int**、值为 **10** 的变量 *batchSize*：

        ```
        int batchSize = 10;
        ```

    1.  添加以下代码行，以创建一个类型为 **TimeSpan**、值为 **“2.5 秒”** 的变量 *visibilityTimeout*：

        ```
        TimeSpan visibilityTimeout = TimeSpan.FromSeconds(2.5d);
        ```

1.  在 **Main** 方法中，执行以下操作，从队列服务中异步检索一批消息：

    1.  添加以下代码行，以调用 **“QueueClient”** 类的 **“ReceiveMessagesAsync”** 异步方法，并将 *“batchSize”* 和 *“visibilityTimeout”* 变量作为参数传入：

        ```
        client.ReceiveMessagesAsync(batchSize, visibilityTimeout);
        ```

    1.  通过添加更多代码来更新上一行代码，以使用 **await** 关键字异步处理表达式：

        ```
        await client.ReceiveMessagesAsync(batchSize, visibilityTimeout);
        ```

    1.  通过添加更多代码来更新上一行代码，将表达式的结果存储在类型为 **[Response<QueueMessage[]>](https://docs.microsoft.com/dotnet/api/azure.response-1)** 的 *messages* 新变量中：

        ```
        Response<QueueMessage[]> messages = await client.ReceiveMessagesAsync(batchSize, visibilityTimeout);
        ```

1.  在 **Main** 方法中，执行以下操作以迭代并呈现每个消息的属性：

    1.  添加以下代码行以创建一个 **foreach** 循环，该循环遍历存储在类型为 **[QueueMessage[]](https://docs.microsoft.com/dotnet/api/azure.storage.queues.models.queuemessage)** 的 *messages* 变量的 **[Value](https://docs.microsoft.com/dotnet/api/azure.response-1.value)** 属性中的每条消息：

        ```
        foreach(QueueMessage message in messages?.Value)
        {
        }
        ```

    1.  在 **foreach** 循环中，添加另一行代码以呈现每个 **QueueMessage** 实例的 **“MessageId”** 和 **“MessageText”** 属性：
    
        ```
        Console.WriteLine($"[{message.MessageId}]\t{message.MessageText}");
        ```

1.  查看 **Main** 方法，该方法现在应包括：

    ```
    public static async Task Main(string[] args)
    {
        // Existing code removed for brevity

        Console.WriteLine($"---Existing Messages---");
        int batchSize = 10;
        TimeSpan visibilityTimeout = TimeSpan.FromSeconds(2.5d);
        
        Response<QueueMessage[]> messages = await client.ReceiveMessagesAsync(batchSize, visibilityTimeout);

        foreach(QueueMessage message in messages?.Value)
        {
            Console.WriteLine($"[{message.MessageId}]\t{message.MessageText}");
        }
    }
    ```

1.  保存 **Program.cs** 文件。

1.  在 **“Visual Studio Code”** 窗口中，右键单击或激活“资源管理器”窗格的快捷菜单，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符中，输入以下命令并选择 Enter 以生成 .NET Web 应用程序：

    ```
    dotnet build
    ```

    > **备注**：如果出现任何生成错误，请查看位于 **“Allfiles (F):\\Allfiles\\Labs\\10\\Solution\\MessageProcessor”** 文件夹中的 **“Program.cs”** 文件。

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 2：测试消息队列访问

1.  在 **“Visual Studio Code”** 窗口中，右键单击或激活“资源管理器”窗格的快捷菜单，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令并按 “Enter” 键，以运行 .NET Web 应用程序：

    ```
    dotnet run
    ```

    > **备注**：如果出现任何生成错误，请查看位于 **“Allfiles (F):\\Allfiles\\Labs\\10\\Solution\\MessageProcessor”** 文件夹中的 **“Program.cs”** 文件。

1.  观察当前运行的控制台应用程序的输出。输出表明队列中没有消息。

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

1.  在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“AsyncProcessor”** 资源组。

1.  在 **“AsyncProcessor”** 边栏选项卡中，选择你之前在本实验室中创建的 “**asyncstor[yourname]**” 存储帐户。

1.  在 **“存储帐户”** 边栏选项卡中，选择 **“概述”**。 

1.  在 **“概述”** 部分，选择 **“在资源管理器中打开”**。

1.  在 **“Azure 存储资源管理器”** 窗口中，选择 **“打开 Azure 存储资源管理器”**。

    > **备注**：如果这是你第一次使用门户打开存储资源管理器，可能会提示你允许门户未来打开这些类型的链接。你应接受该提示。

1.  在 **“Azure 存储资源管理器”** 应用程序中，你会注意到要求登录到 Azure 帐户的提示。通过执行以下操作登录：

    1.  在弹出对话框中，选择 **“登录”**。

    1.  在 **“连接到 Azure 存储”** 窗口中，选择 **“添加 Azure 帐户”**，在 **“Azure 环境”** 列表中选择 **“Azure”**，然后选择 **“下一步”**。

    1.  在 **“登录到你的帐户”** 弹出窗口中，输入你的 Microsoft 帐户的电子邮件地址，然后选择 **“下一步”**。

    1.  仍在 **“登录到你的帐户”** 弹出窗口，输入 Microsoft 帐户的密码，然后选择 **“登录”**。

    1.  在 **“帐户管理”** 窗格中，选择 **“应用”**。

    1.  你发现你已返回到填充了订阅信息的 **“资源管理器”** 窗格。

1.  在 **“Azure 存储资源管理器”** 应用程序的 **“资源管理器”** 窗格中，找到并展开之前在本实验室中创建的 “**asyncstor[yourname]**” 存储帐户。

1.  在 “**asyncstor[yourname]**” 存储帐户中，找到并展开 **“队列”** 节点。

1.  在 **“队列”** 节点中，使用 .NET 代码打开之前在本实验室中创建的 **messagequeue** 队列。

1.  在 **“messagequeue”** 选项卡中，选择 **“添加消息”**。

1.  在 **“添加消息”** 弹出窗口中，执行以下操作：

    1.  在 **“消息正文”** 文本框中输入值 **“Hello World”**。

    1.  在 **“到期时间”** 文本框中，输入值 **“12”**。

    1.  在 **“到期时间”** 下拉列表中，选择 **“小时”**。

    1.  确保未选中 **“以 Base 64 格式编码消息正文”** 复选框。

    1.  选择 **“确定”**。

1.  返回到 **“Visual Studio Code”** 窗口，右键单击或激活“资源管理器”窗格的快捷菜单，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令并按 “Enter” 键，以运行 .NET Web 应用程序：

    ```
    dotnet run
    ```

    > **备注**：如果出现任何生成错误，请查看位于 **“Allfiles (F):\\Allfiles\\Labs\\10\\Solution\\MessageProcessor”** 文件夹中的 **“Program.cs”** 文件。

1.  观察当前运行的控制台应用程序的输出。输出包括你创建的新消息。

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 3：删除加入队列的消息

1.  在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，打开 **Program.cs** 文件。

1.  在 **Program.cs** 文件的代码编辑器选项卡上，找到 **Main** 方法中现有的 **foreach** 循环：

    ```
    foreach(QueueMessage message in messages?.Value)
    {
        Console.WriteLine($"[{message.MessageId}]\t{message.MessageText}");
    }
    ```

1.  在 **foreach** 循环中，添加一行新代码以调用 **QueueMessage** 类的 **DeleteMessageAsync** 方法，并传递 *message* 变量的 **MessageId** 和 **PopReceipt** 属性：

    ```
    await client.DeleteMessageAsync(message.MessageId, message.PopReceipt);
    ```

1.  查看 **Main** 方法，该方法现在应包括：

    ```
    public static async Task Main(string[] args)
    {
        // Existing code removed for brevity
        
        foreach(QueueMessage message in messages?.Value)
        {
            Console.WriteLine($"[{message.MessageId}]\t{message.MessageText}");
            await client.DeleteMessageAsync(message.MessageId, message.PopReceipt);
        }
    }
    ```

1.  **保存** **Program.cs** 文件。

1.  在 **“Visual Studio Code”** 窗口中，右键单击或激活“资源管理器”窗格的快捷菜单，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令并按 “Enter” 键，以运行 .NET Web 应用程序：

    ```
    dotnet run
    ```

    > **备注**：如果出现任何生成错误，请查看位于 **“Allfiles (F):\\Allfiles\\Labs\\10\\Solution\\MessageProcessor”** 文件夹中的 **“Program.cs”** 文件。

1.  观察当前运行的控制台应用程序的输出。之前在实验室中创建的消息仍然存在，因为先前没有将其删除。

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

1.  返回“存储资源管理器”，然后查找之前在本实验室中创建的 “**asyncstor[yourname]**” 存储帐户。

1.  在 “**asyncstor[yourname]**” 存储帐户中，找到并展开 **“队列”** 节点。

1.  在 **“队列”** 节点中，使用 .NET 代码打开之前在本实验室中创建的 **messagequeue** 队列。

1.  观察队列中的空消息列表。

    > **备注**：可能需要刷新队列。

#### 回顾

在本练习中，使用 .NET 库从存储队列中读取和删除了现有消息。

### 练习 4：使用 .NET 对新消息进行排队

#### 任务 1：编写代码以创建队列消息

1.  在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，打开 **Program.cs** 文件。

1.  在 **Program.cs** 文件的代码编辑器选项卡上，找到现有 **Main** 方法。

1.  在 **Main** 方法中，添加一行新代码以呈现“新消息”部分的标题：

    ```
    Console.WriteLine($"---New Messages---");
    ```

1.  在 **Main** 方法中，执行以下操作，通过异步方式创建和发送消息：

    1.  添加以下代码行，以创建一个值为 **Hi, Developer!** 的新字符串变量 *greeting*：

        ```
        string greeting = "Hi, Developer!";        
        ```

    1.  添加以下代码行，以使用 *greeting* 变量作为参数来调用 **QueueClient** 类的 **SendMessageAsync** 方法

        ```
        await client.SendMessageAsync(Convert.ToBase64String(Encoding.UTF8.GetBytes(greeting)));        
        ```

    1.  添加以下代码行以呈现发送的消息内容：

        ```
        Console.WriteLine($"Sent Message:\t{greeting}");        
        ```

1.  查看 **Main** 方法，该方法现在应包括：

    ```
    public static async Task Main(string[] args)
    {
        // Existing code removed for brevity
        
        Console.WriteLine($"---New Messages---");
        string greeting = "Hi, Developer!";
        await client.SendMessageAsync(Convert.ToBase64String(Encoding.UTF8.GetBytes(greeting)));
        
        Console.WriteLine($"Sent Message:\t{greeting}");
    }
    ```

1.  **保存** **Program.cs** 文件。

1.  在 **“Visual Studio Code”** 窗口中，右键单击或激活“资源管理器”窗格的快捷菜单，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令并按 “Enter” 键，以运行 .NET Web 应用程序：

    ```
    dotnet run
    ```

    > **备注**：如果出现任何生成错误，请查看位 于 **“Allfiles (F):\\Allfiles\\Labs\\10\\Solution\\MessageProcessor”** 文件夹中的 **“Program.cs”** 文件。

1.  观察当前运行的控制台应用程序的输出。发送的新消息内容应该会在输出中。

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 2：使用存储资源管理器查看排队的消息

1.  返回“存储资源管理器”，然后查找之前在本实验室中创建的 “**asyncstor[yourname]**” 存储帐户。

1.  在 “**asyncstor[yourname]**” 存储帐户中，找到并展开 **“队列”** 节点。

1.  在 **“队列”** 节点中，使用 .NET 代码打开之前在本实验室中创建的 **messagequeue** 队列。

1.  查看队列消息列表中的单条新消息。

    > **备注**：可能需要刷新队列。

#### 回顾

在本练习中，通过使用存储队列的 .NET 库在队列中创建了新消息。

### 练习 5：清理订阅 

#### 任务 1：打开 Azure Cloud Shell 并列出资源组

1.  在 Azure 门户的“导航”窗格中，选择 **“Cloud Shell”** 图标以打开一个新的 shell 实例。

    > **备注**：**“Cloud Shell”** 图标使用大于符号 (\>) 和下划线字符 (\_) 表示。

1.  如果这是你第一次使用订阅打开 Cloud Shell，则可以使用 **“欢迎使用 Azure Cloud Shell 向导”** 来配置 Cloud Shell，以便首次使用。在向导中执行以下操作：
    
    -   对话框提示你配置 shell。选择 **“Bash”**，查看选定的订阅，然后选择 **“创建存储”**。 

    > **备注**：等待 Cloud Shell 完成首次设置过程后，再继续本实验室。如果 Cloud Shell 配置选项未显示，这很可能是因为你在本课程实验室中使用的是现有订阅。实验是假设你使用的是新订阅的情况下编写的。

#### 任务 2：删除资源组

1.  在命令提示符处，输入以下命令，然后按 Enter 删除 **AsyncProcessor** 资源组：

    ```
    az group delete --name AsyncProcessor --no-wait --yes
    ```
    
1.  关闭门户中的 Cloud Shell 窗格。

#### 任务 3：关闭活动的应用程序

1.  关闭当前正在运行的 Microsoft Edge 应用程序。

1.  关闭当前正在运行的 “Visual Studio Code” 应用程序。

1.  关闭当前正在运行的 “Azure 存储资源管理器”应用程序。

#### 回顾

在本练习中，你通过删除本实验室中曾经使用的资源组来清理订阅。
