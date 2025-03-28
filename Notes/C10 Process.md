## 进程管理

### 1. 进程基础
- 进程：正在执行的程序实例
- PID（进程ID）：操作系统中每个进程的唯一标识符
- 前台/后台进程管理：
  - `jobs` 查看后台进程
  - `Ctrl+C` 终止前台进程

### 2. 守护进程（Daemon）
- 特性：
  - 系统启动时自动运行
  - 长期驻留的后台服务进程
  - 命名惯例通常以"d"结尾（如`sshd`对应`/etc/ssh/sshd_config`）
- 管理工具：`systemd`（新一代初始化系统）

### 3. 系统监控命令
| 命令/组合 | 功能描述 |
|---------|---------|
| `top`   | 实时系统资源监控 |
| `ps aux` | 显示所有运行中的进程 |
| `ps aux \| grep <进程名>` | 进程快速定位 |
| `pidof`/`pgrep` | 获取进程PID |

### 4. 用户权限管理
```bash
su <用户名>    # 切换用户身份
sudo <命令>    # 以root权限执行命令
```

### 5. systemd服务管理
```systemd
systemctl start/stop/status <服务名>  # 服务生命周期管理
配置文件路径：/etc/systemd/system/
```

### 6. 实用工具集
- **日志管理**：
  - `logrotate` 日志轮转（自动压缩/删除旧日志）
- **任务调度**：
  - `cron` 实现周期性任务
- **文本处理**：
  - `grep` 强大的文本搜索工具


