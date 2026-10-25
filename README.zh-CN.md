[English](README.md) | **简体中文**

# 腾亿安全盾 for Linux（ssfwl）社区版

腾亿安全盾是给 Linux Web 服务器用的 CC / HTTP 洪水防火墙。

> **Alpha 版。** 0.0.0.1 是第一个社区版，请先在不重要的服务器上试用。

## 功能

- **黑白名单**
- **驱动防护**
- **支持 HTTP 与 HTTPS 防护**
- **自动防护**
- **管理后台**

## 支持的系统

驱动按内核预编译，**只支持下表列出的内核**，其他内核上安装包会拒绝安装。

| 系统 | 内核（`uname -r`） | 安装包 |
|---|---|---|
| Ubuntu 26.04 | 7.0.0-38-generic | `.deb` |
| Ubuntu 24.04（HWE 内核） | 7.0.0-38-generic | `.deb` |
| Debian 13 | 6.12.107+deb13-amd64 | `.deb` |
| Rocky Linux 10 | 6.12.0-211.68.1.el10_2.x86_64 | `.rpm` |

只支持 x86_64。查看本机系统和内核：

```sh
. /etc/os-release; echo "$ID $VERSION_ID"; uname -r
```

## 安装

从[最新版本](../../releases/latest)下载对应系统的安装包，然后：

**Ubuntu / Debian**

```sh
sudo apt install ./ssfwl_0.0.0.1_amd64.deb
```

安装时会问管理后台端口，直接回车用默认的 8800。

**Rocky Linux**

```sh
sudo dnf install ./ssfwl-0.0.0.1-1.el10.x86_64.rpm
```

管理后台端口为 8800。开着 firewalld 时，安装完会打印放行端口的命令。

安装完成时会打印管理后台地址、连接密钥和配置文件位置。驱动、XDP 程序和服务自动启动，重启后也会自动运行。**防护默认关闭，要在管理后台里开启。**

## 开始使用

1. 打开 `https://<服务器地址>:8800`，用连接密钥登录。没配置证书前管理后台用自签证书，浏览器会提示一次不安全。
2. 给网站端口添加防护规则（比如 443 用 HTTPS、80 用 HTTP）。
3. HTTPS 防护需要网站证书：在“证书”页选择。
4. 开启防护，或在“设置”里打开自动防护。

忘了密钥？它是 `/etc/ssfwl/ssfwl.conf` 里的 `admin_key`，`admin_listen` 是端口。改完配置执行 `sudo systemctl restart ssfwl`。

## 文件位置

| 位置 | 内容 |
|---|---|
| `/etc/ssfwl/ssfwl.conf` | 配置文件，含管理后台端口和连接密钥 |
| `/etc/ssfwl/rules/` | 防护规则 |
| `/usr/sbin/ssfwl` | 主程序 |
| `/usr/lib/modules/<内核>/` | 驱动 `ssfwlnf.ko` |
| `/usr/lib/ssfwl/ssfwlxdp.o` | XDP 程序 |
| `/usr/share/ssfwl/` | 管理后台页面和挑战页模板 |

日志：`journalctl -u ssfwl`

## 卸载

```sh
sudo apt remove ssfwl     # Ubuntu / Debian，保留 /etc/ssfwl
sudo apt purge ssfwl      # Ubuntu / Debian，连 /etc/ssfwl 一起删
sudo dnf remove ssfwl     # Rocky Linux，保留 /etc/ssfwl（不要了就手动删）
```

卸载时会停止服务、摘掉 XDP 程序、卸载驱动。

## 限制

- 只支持 IPv4。
- 社区版只保护一张证书。服务器上多个域名用不同证书时，开启 HTTPS 防护后其他域名会被浏览器报不安全。
- HTTPS 防护要求客户端支持 TLS 1.3（现在的浏览器都支持）。
- 内核升级后要装支持新内核的版本，否则重启后防护起不来。重启进新内核前，先装好对应的版本。

---

© TENY INTERNATIONAL PTY LTD（澳大利亚）
