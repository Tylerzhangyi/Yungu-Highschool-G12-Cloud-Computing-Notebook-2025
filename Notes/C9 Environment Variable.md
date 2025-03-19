# 环境变量笔记

## 1. 什么是环境变量
环境变量（Environment Variables）是操作系统用于存储配置信息的键值对，影响系统和应用程序的运行。例如，`$PATH` 变量定义了可执行文件的搜索路径，而 `$TZ` 变量决定了系统的时区设置。

---

## 2. 配置文件（Config）
配置文件（Config）是存储系统或应用程序设置信息的文件，环境变量通常是其中的一部分。操作系统启动时，会从配置文件中读取环境变量并加载到当前会话。例如：
- `/etc/environment`：系统级环境变量配置文件。
- `~/.bashrc` 或 `~/.zshrc`：用户级环境变量配置文件，用于 Bash 或 Zsh。
- `/etc/profile`：全局 shell 配置文件，影响所有用户。

计算机启动时，首先加载的配置文件通常是 Bash 相关的，如 `/etc/profile` 和 `~/.bashrc`，然后 shell 会话会根据这些文件初始化环境变量。

---

## 3. $PATH 变量

### 3.1 $PATH 作用
`$PATH` 变量用于存储可执行文件的搜索路径。当在终端中输入一个命令时，系统会在 `$PATH` 指定的目录中查找对应的可执行文件。

### 3.2 `$PATH` 配置

#### 3.2.1 暂存配置（仅对当前终端会话有效）
```sh
export PATH="/new/path:$PATH"
```
上述命令会将 `/new/path` 添加到 `$PATH` 的前面，仅对当前终端有效。

#### 3.2.2 永久配置（对所有终端会话有效）
可以将 `$PATH` 配置写入 shell 配置文件，如 `~/.bashrc`（针对 Bash）或 `~/.zshrc`（针对 Zsh）：
```sh
echo 'export PATH="/new/path:$PATH"' >> ~/.bashrc
source ~/.bashrc  # 使更改生效
```
对于 macOS 用户，可能需要修改 `~/.zshrc`。

---

## 4. $TZ 变量（Time Zone 时区）

### 4.1 $TZ 作用
`$TZ` 变量用于设置系统的时区，影响 `date` 命令和其他基于时间的应用程序。

### 4.2 配置 `$TZ`

#### 4.2.1 暂存配置（仅当前终端会话有效）
```sh
export TZ="Asia/Shanghai"
```
#### 4.2.2 永久配置（对所有终端会话有效）
```sh
echo 'export TZ="Asia/Shanghai"' >> ~/.bashrc
source ~/.bashrc  # 使更改生效
```
对于 macOS 用户，可能需要修改 `~/.zshrc`。

### 4.3 时间校准方式
时间校准通常有三种方式：

1. **网络时间服务器（Time Server）**：通过 NTP（Network Time Protocol）从互联网同步时间。
   ```sh
   sudo ntpdate time.nist.gov  # 通过 NTP 服务器校准时间
   ```
2. **卫星授时（GPS）**：通过 GPS 卫星获取精准时间，通常用于科研或高精度时间同步。
3. **本地硬件时钟（RTC, Real-Time Clock）**：依赖计算机主板上的实时时钟（RTC），适用于无法联网的设备，但可能存在漂移。
   ```sh
   sudo hwclock --systohc  # 将系统时间同步到硬件时钟
   ```

---



