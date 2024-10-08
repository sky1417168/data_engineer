MongoDB 是一个开源的、面向文档的 NoSQL 数据库，设计用于处理大量非结构化或半结构化数据。它使用 BSON（Binary JSON）格式存储数据，并支持丰富的查询语言和索引功能。MongoDB 在高并发读写、实时数据分析、内容管理等领域有广泛的应用。

### 主要特点

1. **面向文档**：
   - **BSON 格式**：数据以 BSON 格式存储，类似于 JSON，但更高效。
   - **灵活的模式**：文档可以有不同的结构，不需要预定义的模式。

2. **高性能**：
   - **内存中的数据处理**：支持将数据加载到内存中进行快速处理。
   - **索引**：支持多种类型的索引，包括单字段索引、复合索引、文本索引等。

3. **高可用性和容错性**：
   - **复制集**：支持多主复制，确保高可用性和容错性。
   - **自动故障转移**：自动检测和恢复故障节点，确保系统的稳定运行。

4. **水平扩展**：
   - **分片**：支持数据分片，通过多个分片节点来线性扩展系统的处理能力和存储容量。
   - **负载均衡**：支持负载均衡，确保请求均匀分布到各个节点。

5. **丰富的查询语言**：
   - **聚合框架**：支持复杂的聚合查询，用于数据分析和统计。
   - **地理空间查询**：支持地理空间索引和查询，适用于地理位置相关的应用。

6. **安全性**：
   - **身份验证和授权**：支持多种身份验证机制，如 SCRAM、LDAP 等。
   - **加密**：支持数据传输和存储的加密。

### 使用场景

1. **内容管理**：
   - **博客和新闻网站**：存储和管理大量文档和内容。
   - **媒体库**：存储和管理多媒体文件及其元数据。

2. **实时数据分析**：
   - **业务分析**：实时分析业务数据，提供决策支持。
   - **用户行为分析**：分析用户行为和偏好，优化产品和服务。

3. **物联网（IoT）**：
   - **设备数据存储**：存储和管理大量设备产生的数据。
   - **实时数据处理**：支持实时数据处理和分析，如设备状态监控。

4. **电子商务**：
   - **商品目录**：存储和管理商品信息及其属性。
   - **订单管理**：处理和管理订单数据。

### 基本操作示例

#### 安装 MongoDB

1. **在 Ubuntu 上安装 MongoDB**：
   ```sh
   sudo apt update
   sudo apt install mongodb
   ```

2. **启动 MongoDB 服务**：
   ```sh
   sudo systemctl start mongodb
   ```

3. **访问 MongoDB Shell**：
   ```sh
   mongo
   ```

#### 基本命令

1. **创建数据库**：
   ```sh
   use mydatabase
   ```

2. **插入文档**：
   ```sh
   db.mycollection.insertOne({ name: "Alice", age: 30, email: "alice@example.com" })
   ```

3. **查询文档**：
   ```sh
   db.mycollection.find({ name: "Alice" })
   ```

4. **更新文档**：
   ```sh
   db.mycollection.updateOne({ name: "Alice" }, { $set: { age: 31 } })
   ```

5. **删除文档**：
   ```sh
   db.mycollection.deleteOne({ name: "Alice" })
   ```

#### 通过编程语言使用 MongoDB

1. **JavaScript 示例**（使用 Node. js 和 `mongodb` 库）：
   ```javascript
   const { MongoClient } = require('mongodb');

   const uri = 'mongodb://localhost:27017';
   const client = new MongoClient(uri, { useNewUrlParser: true, useUnifiedTopology: true });

   async function run() {
       try {
           await client.connect();
           const database = client.db('mydatabase');
           const collection = database.collection('mycollection');

           // 插入文档
           const insertResult = await collection.insertOne({ name: 'Alice', age: 30, email: 'alice@example.com' });
           console.log(`Inserted document with _id: ${insertResult.insertedId}`);

           // 查询文档
           const findResult = await collection.findOne({ name: 'Alice' });
           console.log(`Found document: ${JSON.stringify(findResult, null, 2)}`);

           // 更新文档
           const updateResult = await collection.updateOne({ name: 'Alice' }, { $set: { age: 31 } });
           console.log(`Updated ${updateResult.modifiedCount} document(s)`);

           // 删除文档
           const deleteResult = await collection.deleteOne({ name: 'Alice' });
           console.log(`Deleted ${deleteResult.deletedCount} document(s)`);
       } finally {
           await client.close();
       }
   }

   run().catch(console.error);
   ```

2. **Python 示例**（使用 `pymongo` 库）：
   ```python
   from pymongo import MongoClient

   client = MongoClient('mongodb://localhost:27017/')
   db = client['mydatabase']
   collection = db['mycollection']

   def insert_document():
       doc = { 'name': 'Alice', 'age': 30, 'email': 'alice@example.com' }
       result = collection.insert_one(doc)
       print(f'Inserted document with _id: {result.inserted_id}')

   def find_document():
       result = collection.find_one({ 'name': 'Alice' })
       print(f'Found document: {result}')

   def update_document():
       result = collection.update_one({ 'name': 'Alice' }, { '$set': { 'age': 31 } })
       print(f'Updated {result.modified_count} document(s)')

   def delete_document():
       result = collection.delete_one({ 'name': 'Alice' })
       print(f'Deleted {result.deleted_count} document(s)')

   if __name__ == '__main__':
       insert_document()
       find_document()
       update_document()
       find_document()
       delete_document()
   ```

### 高级功能示例

#### 聚合查询

1. **基本聚合**：
   ```sh
   db.mycollection.aggregate([
       { $match: { age: { $gte: 30 } } },
       { $group: { _id: "$name", totalAge: { $sum: "$age" } } }
   ])
   ```

2. **地理空间查询**：
   ```sh
   db.places.createIndex({ location: "2dsphere" })

   db.places.insertMany([
       { name: "Central Park", location: { type: "Point", coordinates: [ -73.9712, 40.7831 ] } },
       { name: "Times Square", location: { type: "Point", coordinates: [ -73.9855, 40.7580 ] } }
   ])

   db.places.find({
       location: {
           $near: {
               $geometry: { type: "Point", coordinates: [ -73.9712, 40.7831 ] },
               $maxDistance: 1000
           }
       }
   })
   ```

#### 分片

1. **启用分片**：
   ```sh
   mongod --configsvr --replSet configReplSet --dbpath /data/configdb --port 27019 --bind_ip localhost --fork --logpath /var/log/mongodb/config.log
   mongod --shardsvr --replSet shardReplSet --dbpath /data/shard1 --port 27018 --bind_ip localhost --fork --logpath /var/log/mongodb/shard1.log
   mongod --shardsvr --replSet shardReplSet --dbpath /data/shard2 --port 27017 --bind_ip localhost --fork --logpath /var/log/mongodb/shard2.log
   mongos --configdb configReplSet/localhost:27019 --port 27017 --fork --logpath /var/log/mongodb/mongos.log
   ```

2. **初始化分片**：
   ```sh
   mongo --port 27019
   rs.initiate()
   ```

3. **添加分片**：
   ```sh
   mongo --port 27017
   sh.addShard("shardReplSet/localhost:27018,localhost:27017")
   ```

4. **启用数据库分片**：
   ```sh
   sh.enableSharding("mydatabase")
   ```

5. **启用集合分片**：
   ```sh
   sh.shardCollection("mydatabase.mycollection", { _id: "hashed" })
   ```

