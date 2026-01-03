# 简单FTP服务器
<img width="993" height="660" alt="image" src="https://github.com/user-attachments/assets/1ffc2f96-ec72-4b62-91f3-aa3712ff216f" />
<img width="961" height="770" alt="图片" src="https://github.com/user-attachments/assets/d66e5d86-fdb0-4c6d-9847-56d7924314ca" />


🚀 简单的FTP/FTPS服务器
一个轻量级、全交互式、支持加密传输的 FTP 服务器，适用于 Windows 环境。无需复杂配置，首次运行即引导你完成所有设置，并自动保存用户信息。内置 Web 管理面板和日志轮转功能。

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)
![平台](https://img.shields.io/badge/平台-Windows-浅灰色)
![许可证](https://img.shields.io/badge/License-MIT-green)

✨ 特性
✅ 全交互式配置向导：首次运行自动引导设置端口、用户、目录、FTPS 等
✅ 支持 FTPS（FTP over TLS）：自动生成自签名证书，保障传输安全
✅ 多用户隔离：每个用户拥有独立根目录，权限可控
✅ 可选匿名访问（只读）
✅ Web 管理界面：实时查看用户、日志、目录结构（仅本地访问）
✅ 日志自动轮转：按天分割日志，保留最近 7 天
✅ 配置自动保存：用户信息写入 users.txt，下次启动可复用
✅ 支持打包成 .exe：无需 Python 环境即可运行

📦 快速开始
方法一：直接运行（需 Python）

1. 安装依赖：
巴什
使用pip安装pyftpdlib、flask和cryptography。

2. 下载 simple_ftp_server.py 到任意目录（如桌面）

3. 双击运行或在终端执行：
巴什
python simple_ftp_server.py

4. 按提示完成配置（示例）：

🔧 欢迎使用高级 FTP 服务器配置向导！

请输入 FTP 控制端口 [默认: 2121]: 2121
是否启用匿名访问？(y/N) [匿名用户只能只读]: 否
请输入用户（格式：用户名:密码，留空结束）: admin:secure123
请输入用户（格式：用户名:密码，留空结束）:
请输入 FTP 根目录 [默认: C:\wwwftp]:
是否启用 FTPS 加密传输？(y/N): y

5. 启动成功后：
FTP 地址：ftp://localhost:2121
Web 管理：[http://127.0.0.1:8080/admin](http://127.0.0.1:8080/admin)

方法二：使用编译好的 .exe（推荐无 Python 环境）

1. 下载 SimpleFTPServer.exe（或自行打包，见下文）
2. 双击运行
3. 按交互提示操作
4. 所有文件（日志、证书、配置）将生成在同目录
💡 首次运行会自动创建：
users.txt：用户账户（明文存储，请妥善保管）
server.pem：FTPS 证书
ftp.log：运行日志

⚙️ 命令行参数（高级用户）

虽然本程序主打交互，但也支持部分命令行选项：

巴什
python simple_ftp_server.py -h

输出：

用法: simple_ftp_server.py [-h] [--config CONFIG] [--ftps] [--web-port WEB_PORT]

全交互式 FTP/FTPS 服务器（支持 Web 管理、日志轮转、自动保存配置）

optional arguments:
-h, --help 显示此帮助信息并退出
--config CONFIG 用户配置文件路径（默认：users.txt）
--ftps 快速启用 FTPS（跳过部分交互）
--web-port WEB_PORT Web 管理界面端口（默认：8080）
📌 注意：若存在 users.txt，程序会优先加载；否则强制进入交互模式。

🔒 安全提示
不要在生产环境使用明文密码：当前版本密码以明文保存在 users.txt 中，仅适合内网或测试。
FTPS 是必须的：强烈建议启用 --ftps，避免密码在网络中明文传输。
防火墙设置：请开放以下端口：
控制端口（如 2121）
被动数据端口范围（默认 50000–50100）

🛠️ 打包成 .exe（分发给他人）
步骤：

1. 安装 PyInstaller：
bash
pip install pyinstaller

2. 在脚本目录执行：
bash
pyinstaller --onefile --console --name "SimpleFTPServer" simple_ftp_server.py

3. 打包完成后，可执行文件位于：

dist/SimpleFTPServer.exe

4. 将该 .exe 文件复制到目标机器，双击即可运行！
💡 打包后体积约 20–30 MB（因包含 Python 解释器和依赖库）。

❓ 常见问题
Q1: 启动时报错 [WinError 10013] 以一种访问权限不允许的方式...？

原因：Windows 系统保留了你指定的端口（如 47001），普通用户无法绑定。

解决：
使用推荐端口：2121, 2122, 8021
避免使用 49152–65535 范围内的高位端口
不要以管理员身份运行（除非必要）

Q2: Web 管理界面打不开？
确保地址是：[http://127.0.0.1:8080/admin](http://127.0.0.1:8080/admin)
该界面仅限本地访问，出于安全考虑不对外暴露
如果端口被占用，可通过 --web-port 8081 修改

Q3: 如何添加新用户？

1. 编辑 users.txt，按 用户名:密码 格式添加
2. 重启服务器使配置生效
示例：
txt
alice:pass123
bob:secret456

Q4: 日志文件太大？

日志已配置为每天轮转，保留 7 天，旧日志自动删除，无需手动清理。

📄 许可证

本项目采用 [MIT License](LICENSE) — 免费用于个人或商业用途。

👨‍💻 作者
编写 & 维护：LIQI
邮箱：tian_ko@163.com
💬 欢迎提交 Issue 或 PR！

✅ 现在就试试吧！只需 1 分钟，你就能拥有一个安全、易用的 FTP 服务器！
