Azure Cosmos DB 是微软 Azure 提供的一个全球分布式、多模型的 NoSQL 数据库服务。它支持多种数据模型，包括文档、键值对、图形和列族存储，旨在提供高可用性、低延迟和无限的可扩展性。Cosmos DB 适用于处理大规模数据集和高并发读写操作的应用场景。

### 主要特点

1. **多模型支持**：
   - **文档数据库**：支持 MongoDB、Cassandra、SQL API 等文档数据库模型。
   - **键值对存储**：支持 Table API，类似于 Azure Table Storage。
   - **图形数据库**：支持 Gremlin API，适用于图形数据模型。
   - **列族存储**：支持 Cassandra API，适用于列族数据模型。

2. **全球分布**：
   - **多区域复制**：数据可以在多个 Azure 区域之间复制，确保全球范围内的低延迟访问。
   - **自动故障转移**：支持自动故障转移，确保高可用性和容错性。

3. **高性能**：
   - **低延迟**：支持毫秒级的读写操作，适用于实时数据访问。
   - **高吞吐量**：支持高并发读写操作，适用于大规模数据集。

4. **无限可扩展性**：
   - **水平扩展**：通过增加分区和区域来线性扩展系统的处理能力和存储容量。
   - **自动分区**：数据自动分区到多个节点，确保数据的均匀分布。

5. **灵活的定价模式**：
   - **按需定价**：根据实际使用的请求单位（RU/s）和存储容量进行计费。
   - **预留容量**：可以预购请求单位以获得折扣。

6. **强大的安全性和合规性**：
   - **身份验证和授权**：支持 Azure Active Directory 身份验证和细粒度的权限控制。
   - **加密**：数据在传输和静止状态下都进行加密。

### 使用场景

1. **Web 应用**：
   - **内容管理系统**：存储和管理大量文档和内容，如博客、新闻网站等。
   - **实时协作应用**：支持多用户实时协作编辑文档，如在线文档编辑器。

2. **移动应用**：
   - **离线同步**：支持离线数据存储和同步，适用于移动应用。
   - **数据同步**：在多个设备之间同步数据，确保数据的一致性。

3. **物联网（IoT）**：
   - **设备数据存储**：存储和管理大量设备产生的数据。
   - **实时数据处理**：支持实时数据处理和分析，如设备状态监控。

4. **数据分析**：
   - **数据聚合**：使用 SQL 查询和分析工具进行数据聚合和分析。
   - **实时报表**：生成实时报表和统计信息。

### 基本操作示例

#### 创建和管理 Cosmos DB 账户

1. **通过 Azure Portal**：
   - 登录 Azure Portal。
   - 导航到“创建资源”。
   - 选择“数据库” > “Azure Cosmos DB”。
   - 输入账户名称、API 类型、资源组等配置。
   - 点击“创建”。

2. **通过 Azure CLI**：
   ```sh
   az cosmosdb create --name mycosmosdbaccount --resource-group myresourcegroup --kind GlobalDocumentDB --locations "East US"=0 "West US"=1
   ```

#### 创建和管理数据库和集合

1. **通过 Azure Portal**：
   - 导航到 Cosmos DB 账户。
   - 选择“数据资源管理器”。
   - 点击“新建数据库”，输入数据库名称和吞吐量。
   - 点击“新建集合”，输入集合名称、分区键和吞吐量。

2. **通过 Azure CLI**：
   ```sh
   az cosmosdb sql database create --name mycosmosdbaccount --resource-group myresourcegroup --db-name mydatabase
   az cosmosdb sql container create --name mycosmosdbaccount --resource-group myresourcegroup --db-name mydatabase --container-name mycontainer --partition-key-path /partitionKey --throughput 400
   ```

#### 基本命令

1. **创建文档**：
   - **通过 Azure Portal**：
     - 导航到集合。
     - 点击“新建项”，输入文档内容。

   - **通过 Azure CLI**：
     ```sh
     az cosmosdb sql item create --account-name mycosmosdbaccount --resource-group myresourcegroup --database-name mydatabase --container-name mycontainer --item-file @item.json
     ```

2. **查询文档**：
   - **通过 Azure Portal**：
     - 导航到集合。
     - 点击“查询资源”，输入查询语句。

   - **通过 Azure CLI**：
     ```sh
     az cosmosdb sql query --account-name mycosmosdbaccount --resource-group myresourcegroup --database-name mydatabase --query-text "SELECT * FROM c"
     ```

3. **更新文档**：
   - **通过 Azure Portal**：
     - 导航到文档。
     - 修改文档内容，点击“保存”。

   - **通过 Azure CLI**：
     ```sh
     az cosmosdb sql item replace --account-name mycosmosdbaccount --resource-group myresourcegroup --database-name mydatabase --container-name mycontainer --item-file @updated-item.json
     ```

4. **删除文档**：
   - **通过 Azure Portal**：
     - 导航到文档。
     - 点击“删除”。

   - **通过 Azure CLI**：
     ```sh
     az cosmosdb sql item delete --account-name mycosmosdbaccount --resource-group myresourcegroup --database-name mydatabase --container-name mycontainer --id <document-id> --partition-key <partition-key>
     ```

#### 通过编程语言使用 Cosmos DB

1. **JavaScript 示例**（使用 Node. js 和 `@azure/cosmos` 库）：
   ```javascript
   const { CosmosClient } = require('@azure/cosmos');

   const endpoint = 'https://mycosmosdbaccount.documents.azure.com:443/';
   const key = 'your-primary-key';
   const client = new CosmosClient({ endpoint, key });

   const databaseId = 'mydatabase';
   const containerId = 'mycontainer';

   async function createDatabaseIfNotExists() {
       const { database } = await client.databases.createIfNotExists({ id: databaseId });
       console.log(`Created database:\n${database.id}\n`);
   }

   async function createContainerIfNotExists() {
       const { container } = await client.database(databaseId).containers.createIfNotExists({ id: containerId, partitionKey: { paths: ['/partitionKey'], kind: 'Hash' } });
       console.log(`Created container:\n${container.id}\n`);
   }

   async function createItem(item) {
       const { resource: createdItem } = await client.database(databaseId).container(containerId).items.create(item);
       console.log(`Created item:\n${createdItem.id}\n`);
   }

   async function queryItems() {
       const { resources: items } = await client.database(databaseId).container(containerId).items.query({
           query: 'SELECT * FROM c'
       }).fetchAll();
       console.log(`Found items:\n${JSON.stringify(items, null, 2)}\n`);
   }

   async function updateItem(id, partitionKey, updatedItem) {
       const { resource: updatedItem } = await client.database(databaseId).container(containerId).item(id, partitionKey).replace(updatedItem);
       console.log(`Updated item:\n${updatedItem.id}\n`);
   }

   async function deleteItem(id, partitionKey) {
       await client.database(databaseId).container(containerId).item(id, partitionKey).delete();
       console.log(`Deleted item:\n${id}\n`);
   }

   async function main() {
       await createDatabaseIfNotExists();
       await createContainerIfNotExists();
       const item = { id: '1', partitionKey: 'value1', name: 'Alice', age: 30 };
       await createItem(item);
       await queryItems();
       const updatedItem = { id: '1', partitionKey: 'value1', name: 'Alice', age: 31 };
       await updateItem('1', 'value1', updatedItem);
       await deleteItem('1', 'value1');
   }

   main().catch(console.error);
   ```

2. **Python 示例**（使用 `azure-cosmos` 库）：
   ```python
   from azure.cosmos import exceptions, CosmosClient, PartitionKey

   endpoint = 'https://mycosmosdbaccount.documents.azure.com:443/'
   key = 'your-primary-key'
   client = CosmosClient(endpoint, key)

   database_name = 'mydatabase'
   container_name = 'mycontainer'

   def create_database_if_not_exists():
       try:
           database = client.create_database(database_name)
           print(f'Created database: {database.id}')
       except exceptions.CosmosResourceExistsError:
           database = client.get_database_client(database_name)
           print(f'Database {database.id} already exists')

   def create_container_if_not_exists():
       try:
           container = database.create_container(id=container_name, partition_key=PartitionKey(path='/partitionKey'))
           print(f'Created container: {container.id}')
       except exceptions.CosmosResourceExistsError:
           container = database.get_container_client(container_name)
           print(f'Container {container.id} already exists')

   def create_item(item):
       container.upsert_item(body=item)
       print(f'Created item: {item["id"]}')

   def query_items():
       items = list(container.query_items(
           query='SELECT * FROM c',
           enable_cross_partition_query=True
       ))
       print(f'Found items: {items}')

   def update_item(id, partition_key, updated_item):
       container.replace_item(item=id, body=updated_item, partition_key=partition_key)
       print(f'Updated item: {id}')

   def delete_item(id, partition_key):
       container.delete_item(item=id, partition_key=partition_key)
       print(f'Deleted item: {id}')

   database = client.get_database_client(database_name)
   create_database_if_not_exists()
   create_container_if_not_exists()

   item = {
       'id': '1',
       'partitionKey': 'value1',
       'name': 'Alice',
       'age': 30
   }

   create_item(item)
   query_items()

   updated_item = {
       'id': '1',
       'partitionKey': 'value1',
       'name': 'Alice',
       'age': 31
   }

   update_item('1', 'value1', updated_item)
   delete_item('1', 'value1')
   ```

### 高级功能示例

#### 全球分布

1. **添加区域**：
   - **通过 Azure Portal**：
     - 导航到 Cosmos DB 账户。
     - 选择“复制数据”。
     - 添加新的区域。

   - **通过 Azure CLI**：
     ```sh
     az cosmosdb update --name mycosmosdbaccount --resource-group myresourcegroup --locations "East US"=0 "West US"=1 "North Europe"=2
     ```

2. **配置一致性级别**：
   - **通过 Azure Portal**：
     - 导航到 Cosmos DB 账户。
     - 选择“设置” > “一致性级别”。
     - 选择合适的一致性级别。

   - **通过 Azure CLI**：
     ```sh
     az cosmosdb update --name mycosmosdbaccount --resource-group myresourcegroup --default-consistency-level BoundedStaleness
     ```

#### 数据建模

1. **文档数据库**：
   - **使用 SQL API**：
     - 创建文档集合：
       ```sh
       az cosmosdb sql container create --name mycosmosdbaccount --resource-group myresourcegroup --db-name mydatabase --container-name mycontainer --partition-key-path /partitionKey --throughput 400
       ```
     - 插入文档：
       ```sh
       az cosmosdb sql item create --account-name mycosmosdbaccount --resource-group myresourcegroup --database-name mydatabase --container-name mycontainer --item-file @item.json
       ```

2. **图形数据库**：
   - **使用 Gremlin API**：
     - 创建图形数据库：
       ```sh
       az cosmosdb gremlin database create --name mycosmosdbaccount --resource-group myresourcegroup --db-name mydatabase
       ```
     - 创建图形集合：
       ```sh
       az cosmosdb gremlin graph create --name mycosmosdbaccount --resource-group myresourcegroup --db-name mydatabase --graph-name mygraph --partition-key-path /partitionKey --throughput 400
       ```
     - 插入顶点和边：
       ```sh
       az cosmosdb gremlin query --account-name mycosmosdbaccount --resource-group myresourcegroup --db-name mydatabase --graph-name mygraph --query-text "g.addV('person').property('id', '1').property('name', 'Alice')"
       az cosmosdb gremlin query --account-name mycosmosdbaccount --resource-group myresourcegroup --db-name mydatabase --graph-name mygraph --query-text "g.V('1').addE('knows').to(g.addV('person').property('id', '2').property('name', 'Bob'))"
       ```

