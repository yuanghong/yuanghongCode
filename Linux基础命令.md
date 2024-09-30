# 文件系统：

Linux 使用一种层次化的文件系统来组织和管理文件和目录。学习文件系统的结构、常见的目录和文件操作命令，例如 ls、cd、mkdir、rm 等。

\1.     列出文件和目录：使用 `ls` 命令列出当前目录下的文件和目录。例如：`ls` 或 `ls -l`。

\2.     切换目录：使用 `cd` 命令切换当前工作目录。例如：`cd /path/to/directory`。

\3.     创建目录：使用 `mkdir` 命令创建新目录。例如：`mkdir mydirectory`。

\4.     删除目录：使用 `rmdir` 命令删除空目录。例如：`rmdir mydirectory`。

\5.     删除文件：使用 `rm` 命令删除文件。例如：`rm myfile.txt`。

注意：`rm` 命令是非常强大和危险的，慎重使用。要永久删除文件而不提示警告，可以使用 `rm -f`。

\6.     复制文件和目录：使用 `cp` 命令复制文件或目录。例如：`cp myfile.txt /path/to/newlocation` 或 `cp -r mydirectory /path/to/newlocation`。

注意：`cp` 命令使用 `-r` 选项以递归方式复制目录。

\7.     移动文件和目录：使用 `mv` 命令移动文件或目录。例如：`mv myfile.txt /path/to/newlocation` 或 `mv mydirectory /path/to/newlocation`。

注意：`mv` 命令也可以用于重命名文件或目录。

\8.     查看文件内容：使用 `cat` 命令查看文件的内容。例如：`cat myfile.txt`。

如果文件很大，你可以使用 `less` 或 `more` 命令进行分页查看。例如：`less myfile.txt`。

\9.     创建空白文件：使用 `touch` 命令创建空白文件。例如：`touch myfile.txt`。

\10.  文件权限管理：使用 `chmod` 命令更改文件的权限。例如：`chmod 644 myfile.txt`。

注意：文件权限由三个组（所有者、所在组、其他人）的读、写、执行权限组成。

# 用户和权限管理：

Linux 是一个多用户系统，学习如何创建用户账户、设置密码和用户组，并了解不同用户对文件和目录的访问权限和权限管理命令，如 chmod 和 chown。

\1.     useradd：用于创建新用户账户。例如：useradd username。

\2.     passwd：用于设置或更改用户的密码。例如：passwd username。

\3.     usermod：用于修改用户账户的属性，如用户的组、家目录等。例如：usermod -aG groupname username。

\4.     userdel：用于删除用户账户。例如：userdel username。

\5.     groupadd：用于创建新用户组。例如：groupadd groupname。

\6.     groupdel：用于删除用户组。例如：groupdel groupname。

\7.     gpasswd：用于管理用户组的密码，添加或删除组成员。例如：gpasswd -a username groupname 和 gpasswd -d username groupname。

\8.     chown：用于更改文件或目录的所有者。例如：chown username filename。

\9.     chgrp：用于更改文件或目录的所属组。例如：chgrp groupname filename。

\10.  chmod：用于更改文件或目录的权限。例如：chmod 644 filename。

\11.  su：用于切换到其他用户账户。例如：su - username。

\12.  sudo：用于以超级用户权限执行命令。例如：sudo command。

# 命令行操作：

学习使用基本的命令行工具和使用命令行选项和参数来完成各种任务。例如，掌握文件和目录操作命令、文本处理命令（如 grep、sed、awk）以及包管理器（如 dpkg、apt、yum）等。

**文本处理命令：**

\1.     grep：在文本中搜索匹配的模式。

\2.     sed：流式文本编辑器，用于编辑和转换文本。

\3.     awk：用于处理和分析文本文件的强大工具。

**包管理器：**

\1.     dpkg：Debian 系统上的包管理器。可以通过 dpkg -i package.deb 安装软件包。

\2.     apt：Debian 系统上的高级包管理工具。可以使用 apt install package 安装软件包。

\3.     yum：Red Hat 系统上的包管理器。可以使用 yum install package 安装软件包。

四 远程访问和文件传输：了解如何使用 SSH 协议远程连接到 Linux 服务器或另一台 Linux 主机。学习使用 scp 或 sftp 命令来进行文件传输和管理。

**远程访问：**

\1.     SSH连接：使用 SSH（Secure Shell）协议连接到远程主机。可以使用以下命令连接到远程主机：

\2.  ssh username@remote_host

其中，username 是远程主机上的用户名，remote_host 是远程主机的 IP 地址或主机名。你需要提供正确的凭据（密码或 SSH 密钥）进行身份验证。

\3.     SSH配置：你可以编辑 SSH 配置文件来自定义连接。配置文件路径通常是 /etc/ssh/sshd_config。在进行任何更改之后，你需要重新加载 SSH 服务。

**文件传输和管理：**

\1.     scp命令：使用 scp 命令进行文件传输。以下是一些示例：

o    从本地复制文件到远程主机：scp local_file username@remote_host:/remote/path

o    从远程主机复制文件到本地：scp username@remote_host:/remote/path/file local_path

o    在远程主机之间复制文件：scp username@remote_host1:/remote/path username@remote_host2:/remote/path

\2.     sftp命令：sftp 是一个交互式的文件传输程序，类似于 FTP。以下是一些示例：

o    连接到远程主机：sftp username@remote_host

o    在本地和远程主机之间传输文件：例如，使用 put 命令上传文件，使用 get 命令下载文件。

使用 SSH 进行远程访问和 scp、sftp 进行文件传输是安全可靠的方式，可以方便地管理远程 Linux 主机和在主机之间传输文件。记住保持服务器和网络的安全，使用强密码或 SSH 密钥进行身份验证，以确保远程连接的安全。

#  进程管理：

学习如何查看正在运行的进程、启动和停止进程以及监控系统资源使用情况的命令，如 ps、top、kill 等。

\1.     ps：用于查看当前正在运行的进程。常用选项包括：

o    ps aux：显示所有用户的所有进程。

o    ps -ef：显示系统中所有进程。

o    ps -e --forest：显示进程以树状结构展示。

\2.     top：用于实时监视系统资源的使用情况和运行中的进程。它提供一个动态更新的展示，按 CPU 使用率或内存使用率等进行排序。

\3.     htop：类似于 top，但提供更多的交互式功能和更友好的用户界面。

\4.     kill：用于停止正在运行的进程。常用选项包括：

o    kill process_id：停止指定进程 ID 的进程。

o    killall process_name：停止指定进程名称的所有进程。

\5.     pgrep：根据进程名称查找匹配的进程 ID。

\6.     pkill：根据进程名称停止匹配的进程。

\7.     nohup：在后台运行命令，并且即使关闭终端也不会停止。用法：nohup command &。

\8.     jobs：显示当前会话中正在运行或挂起的作业。

\9.     fg：将作业调至前台运行。

\10.  bg：将作业调至后台运行。

这些命令可以让你查看系统上正在运行的进程，监控系统资源使用情况，以及启动和停止进程。请注意，某些进程可能需要 root 或特定用户的权限才能进行操作。在执行任何与进程相关的操作之前，请仔细阅读相关命令的文档，并确保了解其影响。

# 系统日志和故障排查：

了解 Linux 系统记录日志的方式和位置，学习日志查看工具和常用的故障排查技巧，如查看日志文件、分析报错信息等。

**日志文件位置：**

\1.     /var/log 目录包含了许多系统和应用程序的日志文件，其中一些常见的日志文件包括：

o    syslog 或 messages：记录系统级信息和错误。

o    auth.log 或 secure：记录用户认证和授权的信息。

o    kern.log：记录内核相关的信息。

o    daemon.log：记录守护进程的信息。

o    nginx/error.log：记录 Nginx 服务器的错误日志。

\2.     应用程序也可能有自己的日志文件，位置和命名可能因应用程序而异。通常在 /var/log 目录下或应用程序的安装目录中。

**日志查看工具：**

\1.     tail 命令：用于显示日志文件的末尾内容，常用选项：

o    tail -n 100 file.log：显示文件 file.log 的最后 100 行内容。

o    tail -f file.log：实时监视日志文件的新增内容。

\2.     cat 命令：用于显示整个日志文件的内容，常用选项：

o    cat file.log：显示文件 file.log 的全部内容。

\3.     less 或 more 命令：用于分页显示和查看日志文件的内容。

\4.     grep 命令：用于在日志文件中搜索指定的关键词，常用选项：

o    grep "keyword" file.log：在文件 file.log 中搜索关键词 “keyword” 并显示匹配的行。

**故障排查技巧：**

\1.     分析日志文件：查看日志文件以找出任何错误、警告或异常信息，这些信息通常有助于诊断问题的根源。

\2.     报错信息：对于系统或应用程序给出的报错信息，仔细阅读并理解其中的含义，可以提供有关问题的线索。

\3.     查看关联日志：查看与问题相关的其它日志文件，例如相关应用程序的日志、系统服务的日志等。

\4.     使用工具和命令：例如 dmesg 命令用于查看内核相关的信息，journalctl 命令用于查看系统日志（适用于使用 systemd 的发行版）。

\5.     记录问题：在排查过程中，记下所有重要的细节和步骤，便于日后参考和复现。

故障排查是一个复杂的过程，因此详细了解系统的日志记录方式和位置，并使用合适的工具和命令来分析日志，可以帮助你更有效地解决问题。

# 网络配置和管理：

学习如何配置网络接口、设置 IP 地址和 DNS 服务器，以及常用的网络管理命令，如 ifconfig、ping、route 等。

**配置网络接口：**

\1.     ifconfig：显示和配置网络接口的信息。然而，在新的 Linux 发行版中，ifconfig 可能已被废弃，推荐使用 ip 命令进行网络接口的配置和管理。

o    ip link show：显示所有网络接口。

o    ip address show：显示网络接口的 IP 地址。

\2.     nmcli：NetworkManager 的命令行界面，用于配置和管理网络。

o    nmcli connection show：显示当前配置的网络连接。

o    nmcli connection add type ethernet ifname eth0：添加以太网连接。

o    nmcli connection modify eth0 ipv4.addresses 192.168.0.2/24：设置 IP 地址。

o    nmcli connection modify eth0 ipv4.gateway 192.168.0.1：设置网关。

\3.     编辑网络配置文件：在 /etc/network/interfaces 文件中手动配置网络接口。这取决于你使用的 Linux 发行版和网络管理工具。

**设置** **IP** **地址和** **DNS** **服务器：**

\1.     ip 命令：用于设置 IP 地址、子网掩码、网关等。

o    ip address add 192.168.0.2/24 dev eth0：为 eth0 接口分配 IP 地址。

o    ip route add default via 192.168.0.1：设置默认网关。

\2.     编辑网络配置文件：可以编辑 /etc/network/interfaces 文件，添加如下行来配置 IP 地址、子网掩码和网关：

\3.  auto eth0

\4.  iface eth0 inet static

\5.  address 192.168.0.2

\6.  netmask 255.255.255.0

\7.  gateway 192.168.0.1

\8.     配置 DNS 服务器：修改 /etc/resolv.conf 文件来设置 DNS 服务器。例如：

\9.  nameserver 8.8.8.8

\10. nameserver 8.8.4.4

**常用网络管理命令：**

\1.     ping：用于测试与目标主机的网络连接。

o    ping google.com：发送 ICMP Echo 请求给 google.com，并接收回复。

\2.     ifconfig 或 ip：用于显示和配置网络接口的信息。

\3.     route：显示和配置路由表信息。

o    route -n：显示路由表信息，包括目标网络、网关和相关参数。

\4.     netstat：显示网络连接、路由表、接口统计信息等。

o    netstat -tuln：显示当前打开的 TCP 和 UDP 端口。