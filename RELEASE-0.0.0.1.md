[English](#english) | [简体中文](#简体中文)

## English

First community release (alpha) of TENY SafeShield for Linux.

**Supported kernels** — the package refuses to install on any other kernel:

| System | Kernel | Package |
|---|---|---|
| Ubuntu 26.04 | 7.0.0-38-generic | `ssfwl_0.0.0.1_amd64.deb` |
| Ubuntu 24.04 (HWE) | 7.0.0-38-generic | `ssfwl_0.0.0.1_amd64.deb` |
| Debian 13 | 6.12.107+deb13-amd64 | `ssfwl_0.0.0.1_amd64.deb` |
| Rocky Linux 10 | 6.12.0-211.68.1.el10_2.x86_64 | `ssfwl-0.0.0.1-1.el10.x86_64.rpm` |

**Included**

- Blacklist and whitelist, driver-level protection
- HTTP and HTTPS protection
- Automatic protection
- Web console
- deb and rpm packages with a systemd service

**Known issues**

- Fully tested on Ubuntu 26.04 only. The Ubuntu 24.04, Debian 13 and Rocky Linux 10 drivers are built and checked against those kernels but have not been run on them yet — reports are welcome.
- IPv4 only; one certificate in the Community Edition.

See the README on the repository home page for installation and first steps.

## 简体中文

腾亿安全盾 for Linux 第一个社区版（Alpha）。

**支持的内核**（其他内核上安装包会拒绝安装）：

| 系统 | 内核 | 安装包 |
|---|---|---|
| Ubuntu 26.04 | 7.0.0-38-generic | `ssfwl_0.0.0.1_amd64.deb` |
| Ubuntu 24.04（HWE） | 7.0.0-38-generic | `ssfwl_0.0.0.1_amd64.deb` |
| Debian 13 | 6.12.107+deb13-amd64 | `ssfwl_0.0.0.1_amd64.deb` |
| Rocky Linux 10 | 6.12.0-211.68.1.el10_2.x86_64 | `ssfwl-0.0.0.1-1.el10.x86_64.rpm` |

**包含功能**

- 黑白名单、驱动防护
- 支持 HTTP 与 HTTPS 防护
- 自动防护
- 管理后台
- deb、rpm 安装包，systemd 服务

**已知问题**

- 只在 Ubuntu 26.04 上完整测试过。Ubuntu 24.04、Debian 13、Rocky Linux 10 的驱动已针对各自内核编译和检查，还没有实际运行过，欢迎反馈。
- 只支持 IPv4；社区版只保护一张证书。

安装和使用见仓库首页的 README（可切换简体中文）。
