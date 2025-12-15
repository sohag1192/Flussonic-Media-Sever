![Badge](https://hitscounter.dev/api/hit?url=https%3A%2F%2Fgithub.com%2Fsohag1192%2FFlussonic-Media-Sever&label=Hit&icon=github&color=%23198754&message=&style=flat&tz=UTC)

- 💬 Join our [Telegram Group](https://t.me/+uQucOgx51IMzM2E1) for support and updates  
-----
<div align="center">

# 🎬 Flussonic Media Server (ISP Edition)

[![Flussonic Version](https://img.shields.io/badge/Flussonic-23.x-red?style=for-the-badge&logo=youtube&logoColor=white)](https://flussonic.com)
[![Platform](https://img.shields.io/badge/Platform-Ubuntu_22.04-orange?style=for-the-badge&logo=ubuntu&logoColor=white)](https://ubuntu.com)
[![Uptime](https://img.shields.io/badge/Uptime-99.9%25-green?style=for-the-badge&logo=activity&logoColor=white)](https://github.com/sohag1192)
[![License](https://img.shields.io/badge/License-Commercial-blue?style=for-the-badge&logo=files&logoColor=white)](https://flussonic.com/pricing)

**High-Performance Streaming Core for IPTV, OTT & Cable Operators.**
<br/>
*Optimized for High Concurrency & Low Latency Streaming.*

[Installation](#-installation) • [Configuration](#-configuration-examples) • [Performance Tuning](#-isp-performance-tuning) • [Troubleshooting](#-troubleshooting-&-commands)

</div>

---

## 🏗 System Architecture

Flussonic serves as the central heart of the streaming network, ingesting feeds from Satellites/IRDs and delivering them to end-users via HLS/DASH.

```mermaid
graph LR
    A[Satellite / IRD] -->|UDP Multicast| B(Flussonic Edge)
    B -->|Transcoding| B
    B -->|HLS / DASH| C{Load Balancer}
    C -->|Smart TV| D[End User]
    C -->|Mobile App| D
    B -->|Archive| E[(DVR Storage)]
    style B fill:#f96,stroke:#333,stroke-width:2px
    style E fill:#bbf,stroke:#333,stroke-width:2px
````

-----

## ⚡ Key Capabilities

| Feature | Description |
| :--- | :--- |
| **📡 Universal Ingest** | Supports UDP, HTTP, RTMP, RTSP, SRT, and WebRTC inputs. |
| **📼 Infinite DVR** | Seamless catchup TV and recording with timeline export. |
| **🔐 DRM & Security** | Token-based auth, AES-128 encryption, and backend integration. |
| **🚀 Ultra Low Latency** | LL-HLS and WebRTC for sub-second delay (Sports/Betting). |
| **🎬 Transcoding** | Hardware acceleration via NVIDIA NVENC and Intel QuickSync. |

-----

## 🚀 Installation

### 1\. Automated Install (Recommended)

Installs dependencies, configures the repo, and starts the service in one go.

```bash
curl -sSf [https://flussonic.com/public/install.sh](https://flussonic.com/public/install.sh) | sh
```

### 2\. Manual Install (Ubuntu/Debian)

For environments requiring specific version control.

```bash
wget -q -O - [https://flussonic.com/doc/install/binary/gpg.key](https://flussonic.com/doc/install/binary/gpg.key) | apt-key add -
echo "deb [https://flussonic.com/doc/install](https://flussonic.com/doc/install) binary/" > /etc/apt/sources.list.d/flussonic.list
apt-get update && apt-get -y install flussonic flussonic-ffmpeg flussonic-python
```
### 1. **Online License Key**
- Obtain a trial or purchased license from [Flussonic Licensing Portal](https://flussonic.com/doc/admin/licensing/#admin-licensing-online-key).  
- Enter the license key in either:
  - `/etc/flussonic/license.txt`  
  - Flussonic Web UI → **Config → License**  
- Ensure your server allows outbound HTTP/HTTPS connections on ports **80** and **443** for validation.  
- Example license format ( That is Only Demo license :  
  ```
  l4|WXHMkfXhFHeNmvDz-M_tb4|r6BzpmVPpjgKpn9IunpFp5lLbCZOp3
  ```
- Licenses are **not tied to hardware**. You can migrate to another server by stopping Flussonic on the old machine and starting it on the new one with the same key.

-----

## ⚙️ Configuration Examples

<details> <summary><b>🔹 Example 1: Auth Backend (Billing Integration)</b></summary>

This configuration sets up a premium channel that checks a viewer's subscription status against your billing system before playing.****

```erlang
# Global settings
http 80;
rtmp 1935;
pulse_db /var/lib/flussonic;

# Stream with authentication
stream premium_channel {
  url [http://provider.com/live/premium.m3u8](http://provider.com/live/premium.m3u8);

  # Require authentication via external backend
  auth backend {
    url [http://billing.example.com/auth](http://billing.example.com/auth);
    timeout 5s;
    cache 30s;   # Cache successful auth for 30 seconds
  }

  # Optional: deny access if backend fails
  deny_backend_fail;
}
```

#### 📝 Explanation

  * **auth backend**: Flussonic queries your billing/CRM system to validate each viewer.
  * **timeout**: Maximum wait time for backend response.
  * **cache**: Reduces load by caching successful responses.
  * **deny\_backend\_fail**: Ensures strict access control if the backend is unreachable.

</details>



<details> <summary><b>🔹 Example 2: Simple Global Auth</b></summary>

Connect your entire server to a PHP/Python billing panel.

```erlang
# Connect to your PHP/Python billing panel
auth_backend [http://127.0.0.1/billing_api/auth.php](http://127.0.0.1/billing_api/auth.php);
```

</details>

-----

## 🔧 ISP Performance Tuning

For high-traffic servers (**10Gbps+**), apply these kernel optimizations to `/etc/sysctl.conf` to prevent packet loss and buffer overflows.

```ini
# Maximize Network Buffers
net.core.rmem_max = 16777216
net.core.wmem_max = 16777216
net.ipv4.tcp_rmem = 4096 87380 16777216
net.ipv4.tcp_wmem = 4096 65536 16777216

# Congestion Control
net.ipv4.tcp_congestion_control = htcp
net.core.netdev_max_backlog = 30000

# Connection Handling
net.ipv4.tcp_max_syn_backlog = 4096
net.ipv4.tcp_tw_reuse = 1
```

> **Note:** Apply changes immediately by running:
>
> ```bash
> sysctl -p
> ```

-----

## 🛠 Troubleshooting & Commands

| Action | Command | Note |
| :--- | :--- | :--- |
| **Start Service** | `service flussonic start` | Starts the daemon |
| **Check Logs** | `tail -f /var/log/flussonic/flussonic.log` | Real-time error monitoring |
| **Validate Config** | `/opt/flussonic/bin/validate_conf` | Check for syntax errors |
| **Reset Password** | `/opt/flussonic/bin/passwd admin newpass` | Emergency password reset |

-----

## 🤝 Community & Resources

### Official

  * **Docs:** [flussonic.com/doc](https://flussonic.com/doc)
  * **Support:** support@flussonic.com

### Unofficial Community

  * **Telegram Group:** [Flussonic Help](https://www.google.com/search?q=https://t.me/flussonic_help) *(Search for group)*

-----

<div align="center">

Maintained by sohag1192


Unofficial Repository for Deployment Scripts & Custom Configs

</div>



