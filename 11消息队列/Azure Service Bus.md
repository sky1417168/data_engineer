Azure Service Bus 是 Microsoft Azure 提供的一个全面的消息传递服务，用于构建可靠、可扩展的分布式应用程序。Service Bus 支持多种消息传递模式，包括队列、主题和中继服务，适用于各种应用场景。下面详细介绍 Azure Service Bus 的核心特点、使用场景和操作示例。

### Azure Service Bus 概述

#### 核心特点

1. **多种消息传递模式**：
   - **队列 (Queues)**：支持点对点 (Point-to-Point) 消息传递，消息发送到队列，只有一个消费者可以接收消息。
   - **主题 (Topics)**：支持发布/订阅 (Publish-Subscribe) 模式，消息发送到主题，多个订阅者可以接收消息。
   - **中继服务 (Relays)**：支持混合云场景，允许本地应用程序与 Azure 云服务之间进行双向通信。

2. **高可用性和可扩展性**：
   - **分区**：支持分区队列和主题，提高吞吐量和可扩展性。
   - **自动缩放**：根据负载自动调整资源，确保高性能和低延迟。

3. **安全性**：
   - **身份验证和授权**：支持 Azure Active Directory (AAD) 和共享访问签名 (SAS) 进行身份验证和授权。
   - **消息加密**：支持传输层安全 (TLS) 加密，确保消息传输的安全性。

4. **灵活的消息模型**：
   - **消息大小**：支持大消息（最大 1 MB），适用于复杂的数据传输场景。
   - **消息过滤**：支持消息过滤和选择性接收，提高消息处理的灵活性。

5. **管理和监控**：
   - **Azure 门户**：通过 Azure 门户进行配置和管理。
   - **Azure Monitor**：集成 Azure Monitor，提供详细的监控和诊断信息。

### 使用场景

1. **异步通信**：
   - **示例**：订单系统中，前端应用将订单信息发送到消息队列，后端服务异步处理订单。
   - **优势**：提高系统的响应速度和吞吐量，解耦前后端服务。

2. **解耦系统**：
   - **示例**：微服务架构中，不同服务通过消息队列进行通信，降低服务间的耦合度。
   - **优势**：提高系统的可维护性和可扩展性。

3. **事件驱动架构**：
   - **示例**：用户注册时，发送注册事件到消息主题，触发邮件发送、日志记录等后续操作。
   - **优势**：实现松耦合的事件驱动系统，提高系统的灵活性和响应速度。

4. **混合云场景**：
   - **示例**：本地应用程序通过中继服务与 Azure 云服务进行双向通信。
   - **优势**：支持混合云架构，实现本地和云端的无缝集成。

### 操作示例

#### 创建 Service Bus 命名空间

1. **登录 Azure 门户**：
   - 打开 Azure 门户 (https://portal.azure.com) 并登录。

2. **创建命名空间**：
   - 导航到“创建资源” > “企业集成” > “Service Bus”。
   - 填写必要的信息，如命名空间名称、资源组、位置等。
   - 选择 SKU（免费、基本、标准、高级）。
   - 点击“创建”按钮。

3. **获取连接字符串**：
   - 创建完成后，导航到 Service Bus 命名空间。
   - 在左侧菜单中选择“共享访问策略”。
   - 选择默认的“RootManageSharedAccessKey”，复制连接字符串。

#### 创建队列和主题

1. **创建队列**：
   - 在 Service Bus 命名空间中，选择“队列”。
   - 点击“+ 队列”按钮，填写队列名称和其他配置。
   - 点击“创建”按钮。

2. **创建主题**：
   - 在 Service Bus 命名空间中，选择“主题”。
   - 点击“+ 主题”按钮，填写主题名称和其他配置。
   - 点击“创建”按钮。

3. **创建订阅**：
   - 在创建的主题中，选择“+ 订阅”按钮，填写订阅名称和其他配置。
   - 点击“创建”按钮。

#### 发送和接收消息

1. **发送消息到队列**：
   - 使用 .NET SDK 发送消息：
     ```csharp
     using Azure.Messaging.ServiceBus;

     string connectionString = "<your-connection-string>";
     string queueName = "myqueue";

     async Task SendMessagesAsync()
     {
         await using var client = new ServiceBusClient(connectionString);
         ServiceBusSender sender = client.CreateSender(queueName);

         for (int i = 0; i < 5; i++)
         {
             string messageBody = $"Message {i}";
             ServiceBusMessage message = new ServiceBusMessage(messageBody);

             await sender.SendMessageAsync(message);
             Console.WriteLine($"Sent message: {messageBody}");
         }

         await sender.CloseAsync();
     }

     SendMessagesAsync().GetAwaiter().GetResult();
     ```

2. **接收消息从队列**：
   - 使用 .NET SDK 接收消息：
     ```csharp
     using Azure.Messaging.ServiceBus;

     string connectionString = "<your-connection-string>";
     string queueName = "myqueue";

     async Task ReceiveMessagesAsync()
     {
         await using var client = new ServiceBusClient(connectionString);
         ServiceBusReceiver receiver = client.CreateReceiver(queueName);

         while (true)
         {
             ServiceBusReceivedMessage receivedMessage = await receiver.ReceiveMessageAsync();
             if (receivedMessage != null)
             {
                 Console.WriteLine($"Received message: {receivedMessage.Body}");
                 await receiver.CompleteMessageAsync(receivedMessage);
             }
             else
             {
                 break;
             }
         }

         await receiver.CloseAsync();
     }

     ReceiveMessagesAsync().GetAwaiter().GetResult();
     ```

3. **发送消息到主题**：
   - 使用 .NET SDK 发送消息：
     ```csharp
     using Azure.Messaging.ServiceBus;

     string connectionString = "<your-connection-string>";
     string topicName = "mytopic";

     async Task SendMessagesToTopicAsync()
     {
         await using var client = new ServiceBusClient(connectionString);
         ServiceBusSender sender = client.CreateSender(topicName);

         for (int i = 0; i < 5; i++)
         {
             string messageBody = $"Message {i}";
             ServiceBusMessage message = new ServiceBusMessage(messageBody);

             await sender.SendMessageAsync(message);
             Console.WriteLine($"Sent message to topic: {messageBody}");
         }

         await sender.CloseAsync();
     }

     SendMessagesToTopicAsync().GetAwaiter().GetResult();
     ```

4. **接收消息从订阅**：
   - 使用 .NET SDK 接收消息：
     ```csharp
     using Azure.Messaging.ServiceBus;

     string connectionString = "<your-connection-string>";
     string topicName = "mytopic";
     string subscriptionName = "mysubscription";

     async Task ReceiveMessagesFromSubscriptionAsync()
     {
         await using var client = new ServiceBusClient(connectionString);
         ServiceBusReceiver receiver = client.CreateReceiver(topicName, subscriptionName);

         while (true)
         {
             ServiceBusReceivedMessage receivedMessage = await receiver.ReceiveMessageAsync();
             if (receivedMessage != null)
             {
                 Console.WriteLine($"Received message from subscription: {receivedMessage.Body}");
                 await receiver.CompleteMessageAsync(receivedMessage);
             }
             else
             {
                 break;
             }
         }

         await receiver.CloseAsync();
     }

     ReceiveMessagesFromSubscriptionAsync().GetAwaiter().GetResult();
     ```

### 高级功能

1. **分区**：
   - **分区队列和主题**：启用分区，提高吞吐量和可扩展性。
   - **配置**：在创建队列或主题时，选择“分区”选项。

2. **消息过滤**：
   - **规则和操作**：在订阅中配置消息过滤规则，实现选择性接收。
   - **示例**：
     ```csharp
     string connectionString = "<your-connection-string>";
     string topicName = "mytopic";
     string subscriptionName = "mysubscription";

     await using var client = new ServiceBusAdministrationClient(connectionString);
     var ruleOptions = new CreateRuleOptions("myrule")
     {
         Filter = new SqlFilter("color = 'red'"),
         Action = new SqlRuleAction("SET label = 'important'")
     };

     await client.CreateRuleAsync(topicName, subscriptionName, ruleOptions);
     ```

3. **死信队列**：
   - **配置**：在队列或订阅中启用死信队列，处理无法成功处理的消息。
   - **示例**：
     ```csharp
     string connectionString = "<your-connection-string>";
     string queueName = "myqueue";

     await using var client = new ServiceBusAdministrationClient(connectionString);
     var options = new CreateQueueOptions(queueName)
     {
         EnableDeadLetteringOnMessageExpiration = true,
         MaxDeliveryCount = 10
     };

     await client.CreateQueueAsync(options);
     ```

4. **事务**：
   - **事务性消息处理**：支持事务性消息发送和接收，确保消息的一致性和可靠性。
   - **示例**：
     ```csharp
     using Azure.Messaging.ServiceBus;

     string connectionString = "<your-connection-string>";
     string queueName = "myqueue";

     async Task TransactionalSendAndReceiveAsync()
     {
         await using var client = new ServiceBusClient(connectionString);
         ServiceBusSender sender = client.CreateSender(queueName);
         ServiceBusReceiver receiver = client.CreateReceiver(queueName);

         using ServiceBusTransactionContext transaction = await client.BeginTransactionAsync();

         ServiceBusMessage message = new ServiceBusMessage("Transactional message");
         await sender.SendMessageAsync(message, transaction);

         ServiceBusReceivedMessage receivedMessage = await receiver.ReceiveMessageAsync();
         await receiver.CompleteMessageAsync(receivedMessage, transaction);

         await transaction.CommitAsync();
     }

     TransactionalSendAndReceiveAsync().GetAwaiter().GetResult();
     ```

