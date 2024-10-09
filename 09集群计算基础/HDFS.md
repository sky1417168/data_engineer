Hadoop Distributed File System (HDFS) 是 Apache Hadoop 的核心组件之一，专门设计用于存储大规模数据集。HDFS 是一个分布式文件系统，具有高容错性、高可靠性和高扩展性，适用于处理 TB 到 PB 级别的数据。以下是对 HDFS 的详细介绍，包括其架构、特点、操作示例和常见问题解决方法。

### HDFS 架构

1. **NameNode**：
   - **功能**：管理文件系统的命名空间，维护文件系统树及文件目录的元数据信息。
   - **职责**：
     - 维护文件系统的目录树。
     - 记录文件的块信息及其所在的数据节点。
     - 处理客户端的文件元数据请求。
   - **高可用性**：通过配置备用 NameNode（Secondary NameNode 或 Standby NameNode）实现高可用性。

2. **DataNode**：
   - **功能**：存储实际的数据块。
   - **职责**：
     - 存储和检索数据块。
     - 定期向 NameNode 报告存储状态。
     - 执行数据块的创建、删除和复制操作。
   - **扩展性**：通过增加更多的 DataNode 来扩展存储容量和处理能力。

3. **Block**：
   - **定义**：文件被分割成固定大小的块（默认 128 MB），每个块作为一个独立的单元存储在 DataNode 上。
   - **复制**：为了提高数据的可靠性和容错性，每个块通常会被复制到多个 DataNode 上，默认复制因子为 3。

### HDFS 特点

1. **高容错性**：
   - **数据复制**：每个数据块在多个 DataNode 上复制，确保数据的可靠性和可用性。
   - **故障检测**：NameNode 定期检查 DataNode 的健康状况，发现故障节点后会重新分配数据块。

2. **水平扩展**：
   - **增加节点**：可以通过增加更多的 DataNode 来扩展存储容量和处理能力。
   - **动态调整**：支持动态添加和删除节点，不影响现有数据的存储和访问。

3. **大文件支持**：
   - **适合大文件**：HDFS 适合存储和处理大型文件，支持 TB 到 PB 级别的数据。
   - **块存储**：文件被分割成固定大小的块，每个块独立存储，提高了数据的并行处理能力。

4. **数据一致性**：
   - **写入一致性**：保证数据写入的一致性，客户端在写入数据时会收到确认信息。
   - **读取一致性**：客户端读取数据时，总是能够获取到最新的数据。

### 基本操作示例

#### 配置 HDFS

1. **编辑 `core-site.xml`**：
   ```xml
   <configuration>
     <property>
       <name>fs.defaultFS</name>
       <value>hdfs://localhost:9000</value>
     </property>
   </configuration>
   ```

2. **编辑 `hdfs-site.xml`**：
   ```xml
   <configuration>
     <property>
       <name>dfs.replication</name>
       <value>3</value>
     </property>
     <property>
       <name>dfs.namenode.http-address</name>
       <value>localhost:50070</value>
     </property>
     <property>
       <name>dfs.datanode.http.address</name>
       <value>0.0.0.0:50075</value>
     </property>
   </configuration>
   ```

#### 格式化 HDFS

1. **格式化 NameNode**：
   ```sh
   hdfs namenode -format
   ```

#### 启动和停止 HDFS

1. **启动 HDFS**：
   ```sh
   start-dfs.sh
   ```

2. **停止 HDFS**：
   ```sh
   stop-dfs.sh
   ```

#### 常用命令

1. **创建目录**：
   ```sh
   hdfs dfs -mkdir /user/yourusername
   ```

2. **上传文件**：
   ```sh
   hdfs dfs -put /path/to/local/file.txt /user/yourusername/
   ```

3. **下载文件**：
   ```sh
   hdfs dfs -get /user/yourusername/file.txt /path/to/local/
   ```

4. **列出目录内容**：
   ```sh
   hdfs dfs -ls /user/yourusername/
   ```

5. **删除文件**：
   ```sh
   hdfs dfs -rm /user/yourusername/file.txt
   ```

6. **查看文件内容**：
   ```sh
   hdfs dfs -cat /user/yourusername/file.txt
   ```

### 常见问题解决方法

1. **NameNode 无法启动**：
   - **检查日志**：查看 `logs` 目录下的日志文件，查找错误信息。
   - **格式化 NameNode**：如果配置文件有误或数据损坏，尝试重新格式化 NameNode。

2. **DataNode 无法启动**：
   - **检查网络**：确保 DataNode 能够与 NameNode 通信。
   - **检查磁盘空间**：确保 DataNode 上有足够的磁盘空间。
   - **检查日志**：查看 `logs` 目录下的日志文件，查找错误信息。

3. **文件上传失败**：
   - **检查路径**：确保目标路径存在且有写权限。
   - **检查磁盘空间**：确保 DataNode 上有足够的磁盘空间。
   - **检查网络**：确保客户端能够与 NameNode 和 DataNode 通信。

4. **文件读取失败**：
   - **检查路径**：确保文件路径正确且文件存在。
   - **检查权限**：确保有读取权限。
   - **检查 DataNode 状态**：确保 DataNode 正常运行。
