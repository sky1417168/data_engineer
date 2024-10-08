
Linux 是一个开源的操作系统内核，最初由 Linus Torvalds 在 1991 年开发。Linux 通常与各种开源软件一起打包成发行版（如 Ubuntu、CentOS、Debian 等），形成一个完整的操作系统。Linux 在服务器、嵌入式系统、移动设备（如 Android）和个人计算机上广泛使用。

### 1. Linux 基本概念

#### 1.1 **内核（Kernel）**
- **内核**：Linux 的核心部分，负责管理系统的资源，如 CPU、内存和 I/O 设备。
- **功能**：进程管理、内存管理、文件系统、网络协议栈等。

#### 1.2 **发行版（Distribution）**
- **发行版**：基于 Linux 内核的完整操作系统，包括内核、用户空间工具、库、图形界面等。
- **常见发行版**：
  - **Ubuntu**：用户友好，适合初学者。
  - **CentOS**：企业级，稳定性高。
  - **Debian**：社区驱动，稳定性高。
  - **Fedora**：创新性强，经常引入新技术。
  - **Arch Linux**：高度可定制，适合高级用户。

#### 1.3 **Shell**
- **Shell**：用户与操作系统交互的命令解释器。
- **常见 Shell**：
  - **Bash**：最常用的 Shell，功能丰富。
  - **Zsh**：Bash 的增强版本，提供更多自定义选项。
  - **Fish**：用户友好的 Shell，自动补全功能强大。

### 2. Linux 常用命令

#### 2.1 **文件和目录操作**
- **列出目录内容**：
  ```sh
  ls
  ```
- **切换目录**：
  ```sh
  cd <directory>
  ```
- **创建目录**：
  ```sh
  mkdir <directory>
  ```
- **删除文件或目录**：
  ```sh
  rm <file>
  rm -r <directory>
  ```
- **复制文件或目录**：
  ```sh
  cp <source> <destination>
  cp -r <source-directory> <destination-directory>
  ```
- **移动或重命名文件或目录**：
  ```sh
  mv <source> <destination>
  ```

#### 2.2 **文件查看和编辑**
- **查看文件内容**：
  ```sh
  cat <file>
  less <file>
  head <file>
  tail <file>
  ```
- **编辑文件**：
  ```sh
  nano <file>
  vim <file>
  ```

#### 2.3 **文件权限管理**
- **查看文件权限**：
  ```sh
  ls -l
  ```
- **更改文件权限**：
  ```sh
  chmod <permissions> <file>
  ```
- **更改文件所有者**：
  ```sh
  chown <user>:<group> <file>
  ```

#### 2.4 **进程管理**
- **查看进程**：
  ```sh
  ps aux
  top
  htop
  ```
- **杀死进程**：
  ```sh
  kill <pid>
  killall <process-name>
  ```

#### 2.5 **网络操作**
- **查看网络接口**：
  ```sh
  ifconfig
  ip a
  ```
- **查看网络连接**：
  ```sh
  netstat -tuln
  ss -tuln
  ```
- **测试网络连接**：
  ```sh
  ping <hostname>
  curl <url>
  wget <url>
  ```

#### 2.6 **系统管理**
- **查看系统信息**：
  ```sh
  uname -a
  lsb_release -a
  ```
- **更新系统**：
  ```sh
  sudo apt update && sudo apt upgrade  # Debian/Ubuntu
  sudo yum update                      # CentOS/RHEL
  sudo dnf update                      # Fedora
  ```
- **安装软件**：
  ```sh
  sudo apt install <package>           # Debian/Ubuntu
  sudo yum install <package>           # CentOS/RHEL
  sudo dnf install <package>           # Fedora
  ```

### 3. Linux 文件系统

#### 3.1 **文件系统层次结构标准（FHS）**
- **/**：根目录
- **/bin**：基本命令和可执行文件
- **/boot**：启动所需的文件
- **/dev**：设备文件
- **/etc**：配置文件
- **/home**：用户主目录
- **/lib**：共享库
- **/media**：可移动媒体挂载点
- **/mnt**：临时挂载点
- **/opt**：可选软件包
- **/proc**：进程信息
- **/root**：root 用户的主目录
- **/run**：运行时数据
- **/sbin**：系统管理员命令
- **/srv**：服务数据
- **/sys**：系统设备和内核信息
- **/tmp**：临时文件
- **/usr**：用户程序和文件
- **/var**：可变数据

### 4. Linux 系统管理

#### 4.1 **用户和组管理**
- **添加用户**：
  ```sh
  sudo useradd <username>
  sudo passwd <username>
  ```
- **删除用户**：
  ```sh
  sudo userdel <username>
  ```
- **添加组**：
  ```sh
  sudo groupadd <groupname>
  ```
- **删除组**：
  ```sh
  sudo groupdel <groupname>
  ```
- **查看用户和组**：
  ```sh
  cat /etc/passwd
  cat /etc/group
  ```

#### 4.2 **服务管理**
- **查看服务状态**：
  ```sh
  systemctl status <service>
  ```
- **启动服务**：
  ```sh
  sudo systemctl start <service>
  ```
- **停止服务**：
  ```sh
  sudo systemctl stop <service>
  ```
- **重启服务**：
  ```sh
  sudo systemctl restart <service>
  ```
- **设置服务开机启动**：
  ```sh
  sudo systemctl enable <service>
  ```
- **禁止服务开机启动**：
  ```sh
  sudo systemctl disable <service>
  ```

### 5. Linux 脚本编程

#### 5.1 **Shell 脚本**
- **创建脚本文件**：
  ```sh
  nano myscript.sh
  ```
- **编写脚本**：
  ```sh
  #!/bin/bash
  echo "Hello, World!"
  ```
- **赋予执行权限**：
  ```sh
  chmod +x myscript.sh
  ```
- **运行脚本**：
  ```sh
  ./myscript.sh
  ```

#### 5.2 **常用命令**
- **条件判断**：
  ```sh
  if [ condition ]; then
    # do something
  else
    # do something else
  fi
  ```
- **循环**：
  ```sh
  for i in {1..5}; do
    echo $i
  done
  ```
- **函数**：
  ```sh
  myfunction() {
    echo "This is a function"
  }
  myfunction
  ```

### 6. Linux 安全

#### 6.1 **防火墙管理**
- **iptables**：
  ```sh
  sudo iptables -L
  sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
  sudo iptables-save > /etc/iptables/rules.v4
  ```
- **firewalld**：
  ```sh
  sudo firewall-cmd --list-all
  sudo firewall-cmd --add-port=22/tcp --permanent
  sudo firewall-cmd --reload
  ```

#### 6.2 **SELinux**
- **查看 SELinux 状态**：
  ```sh
  sestatus
  ```
- **临时设置 SELinux 模式**：
  ```sh
  sudo setenforce 0  # 设置为宽容模式
  sudo setenforce 1  # 设置为强制模式
  ```
- **永久设置 SELinux 模式**：
  ```sh
  sudo vi /etc/selinux/config
  ```

### 7. Linux 性能监控

#### 7.1 **系统监控工具**
- **top**：实时显示系统进程和资源使用情况。
- **htop**：增强版的 top，支持交互式操作。
- **vmstat**：显示虚拟内存统计信息。
- **iostat**：显示 I/O 统计信息。
- **netstat**：显示网络连接和端口信息。
- **iftop**：显示网络带宽使用情况。

### 8. Linux 虚拟化和容器

#### 8.1 **虚拟化**
- **KVM**：基于内核的虚拟机。
- **VirtualBox**：开源虚拟化软件。

#### 8.2 **容器**
- **Docker**：轻量级的容器化平台。
- **LXC**：Linux 容器。
