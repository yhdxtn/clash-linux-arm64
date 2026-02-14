# clash-linux-arm64（Debian ARM 随身 WiFi / Android 13 可用）

Clash **ARM64** 可执行文件，已在以下环境实测通过：
- ✅ **Debian ARM 的随身 WiFi**（可当路由器/网关设备使用）
- ✅ **Android 13（Termux）**

> 配置文件 `config.yaml` / `*.yaml` 请从你其它 Clash 客户端导出（完整 YAML 配置），本项目不提供订阅/节点内容。

---

## 关键文件放置（Country.mmdb 放哪？）

`Country.mmdb`（GeoIP 数据库）请放到 **Clash 工作目录**（也就是你运行时 `-d` 指向的目录）里。

推荐结构：

```bash
clash/
├── clash                 # clash-linux-arm64-latest 重命名为 clash
├── config.yaml           # 从其它客户端导出的 Clash 配置
└── Country.mmdb          # GeoIP 数据库（必须与 config.yaml 同目录）
启动时使用 -d 指定该目录，Clash 会在该目录内读取 config.yaml 与 Country.mmdb。

运行前权限（必须）
1) Linux / Debian ARM（随身 WiFi）
给二进制可执行权限：

chmod +x clash
2) Android 13（Termux）
给二进制可执行权限：

chmod +x clash
让 Termux 拥有存储访问权限（便于拷贝/读取 yaml）：

termux-setup-storage
建议在系统设置中给 Termux 允许后台运行/关闭电池优化，避免锁屏被杀导致断连。

Debian ARM 随身 WiFi（推荐路径）
以 /etc/clash 为例：

mkdir -p /etc/clash
# 把 clash、config.yaml、Country.mmdb 放入 /etc/clash
cd /etc/clash
chmod +x clash
./clash -d /etc/clash
后台运行（可选）：

nohup ./clash -d /etc/clash >/tmp/clash.log 2>&1 &
Android 13（Termux）
mkdir -p ~/clash
cd ~/clash
# 放入 clash、config.yaml、Country.mmdb
chmod +x clash
./clash -d ~/clash
后台运行（可选）：

nohup ./clash -d ~/clash > ~/clash/run.log 2>&1 &
