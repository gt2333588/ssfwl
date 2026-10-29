**English** | [简体中文](README.zh-CN.md)

# TENY SafeShield for Linux (ssfwl) — Community Edition

TENY SafeShield is a CC / HTTP flood firewall for Linux web servers.

> **Alpha.** Test it on a non-critical server first.

## Features

- **Blacklist and whitelist**
- **Driver-level protection**
- **HTTP and HTTPS protection**
- **SYN protection**
- **TCP and UDP flood protection**
- **Automatic protection**
- **Packet capture**
- **Web console**

## Supported systems

The driver is prebuilt for each kernel. **Only the kernels below are supported**; on any other kernel the package refuses to install.

| System | Kernel (`uname -r`) | Package |
|---|---|---|
| Ubuntu 26.04 | 7.0.0-38-generic | `.deb` |
| Ubuntu 24.04 (HWE kernel) | 7.0.0-38-generic | `.deb` |
| Ubuntu 24.04 (GA kernel) | 6.8.0-147-generic | `.deb` |
| Debian 13 | 6.12.107+deb13-amd64 | `.deb` |
| Rocky Linux 10 | 6.12.0-211.68.1.el10_2.x86_64 | `.rpm` |

x86_64 only. Check your system with:

```sh
. /etc/os-release; echo "$ID $VERSION_ID"; uname -r
```

## Install

Download the package for your system from the [latest release](../../releases/latest), then:

**Ubuntu / Debian**

```sh
sudo apt install ./ssfwl_0.0.0.2_amd64.deb
```

The installer asks for the console port; press Enter for the default 8800.

**Rocky Linux**

```sh
sudo dnf install ./ssfwl-0.0.0.2-1.el10.x86_64.rpm
```

The console port is 8800. If firewalld is running, the installer prints the command that opens the port.

When installation finishes, the console address, the connection key and the config file location are printed. The driver, the XDP program and the service start automatically and come back after a reboot. **Protection is off until you turn it on in the console.**

## First steps

1. Open `https://<server address>:8800` and log in with the connection key. The console uses a self-signed certificate until you configure one, so the browser warns once.
2. Add a protection rule for your web ports (for example 443 HTTPS and 80 HTTP).
3. HTTPS protection needs your site's certificate: pick one on the Certificates page.
4. Turn protection on, or enable automatic protection in Settings.

Lost the key? It is `admin_key` in `/etc/ssfwl/ssfwl.conf`; `admin_listen` is the port. After editing the file run `sudo systemctl restart ssfwl`.

## Files

| Path | Contents |
|---|---|
| `/etc/ssfwl/ssfwl.conf` | Configuration, including the console port and connection key |
| `/etc/ssfwl/rules/` | Protection rules |
| `/usr/sbin/ssfwl` | Main program |
| `/usr/lib/modules/<kernel>/` | Driver `ssfwlnf.ko` |
| `/usr/lib/ssfwl/ssfwlxdp.o` | XDP program |
| `/usr/share/ssfwl/` | Console pages and challenge page templates |

Logs: `journalctl -u ssfwl`

## Uninstall

```sh
sudo apt remove ssfwl     # Ubuntu / Debian, keeps /etc/ssfwl
sudo apt purge ssfwl      # Ubuntu / Debian, also deletes /etc/ssfwl
sudo dnf remove ssfwl     # Rocky Linux, keeps /etc/ssfwl (delete it by hand if you want)
```

Uninstalling stops the service, detaches the XDP program and unloads the driver.

## Limitations

- IPv4 only.
- The Community Edition protects one certificate. If your server hosts several domains on different certificates, browsers will warn on the other domains while HTTPS protection is on.
- HTTPS protection requires TLS 1.3 clients (all current browsers).
- After a kernel update, the new kernel needs a new package; until then protection does not start after a reboot. Install the matching release before rebooting into a new kernel.

---

© TENY INTERNATIONAL PTY LTD (Australia)
