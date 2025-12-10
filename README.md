
-----


# 📺 Flussonic Media Server

![Flussonic Version](https://img.shields.io/badge/Flussonic-Latest-red?style=for-the-badge&logo=youtube)
![Platform](https://img.shields.io/badge/Platform-Linux-blue?style=for-the-badge&logo=linux)
![License](https://img.shields.io/badge/License-Commercial-green?style=for-the-badge)

**Flussonic Media Server** is a high-performance, carrier-grade streaming platform designed for live TV, VOD, IPTV, and OTT delivery. This repository provides quick deployment scripts, configuration guides, and community resources for system administrators and ISPs.

---

## 📋 Table of Contents

- [Features](#-features)
- [Prerequisites](#-prerequisites)
- [Installation Guide](#-installation-guide)
  - [Quick Install](#quick-install)
  - [Debian/Ubuntu](#debianubuntu)
  - [CentOS/RedHat](#centosredhat)
- [Configuration & Activation](#-configuration--activation)
- [Management Commands](#-management-commands)
- [Support & Community](#-support--community)

---

## ✨ Features

* **Multi-protocol Support:** HLS, DASH, RTMP, RTSP, SRT, and WebRTC.
* **DVR/Catchup:** Built-in recording and archive management.
* **Transcoding:** Hardware-accelerated transcoding (NVIDIA NVENC, Intel QuickSync).
* **Low Latency:** Optimized for sub-second latency streaming.
* **Clustering:** Scalable architecture for high-load environments.

---

## ⚙️ Prerequisites

Before installing, ensure your server meets the following requirements:

* **Operating System:** * Ubuntu 20.04 / 22.04 / 24.04 (LTS recommended)
    * CentOS 7 / 8 / Stream or RedHat equivalent
* **Architecture:** `amd64` (x86_64) or `arm64`
* **Network:** * **Port 80:** Must be open for the web interface and Let's Encrypt validation.
    * **Port 443:** For HTTPS playback.
    * **Port 1935:** If using RTMP.
* **Access:** Root or `sudo` privileges are required.

---

## 🚀 Installation Guide

### Quick Install
The fastest way to get running is using the official installer script:

```bash
curl -sSf [https://flussonic.com/public/install.sh](https://flussonic.com/public/install.sh) | sh
````

### Manual Installation

#### Debian/Ubuntu

```bash
# Add the GPG key and repository
wget -q -O - [https://flussonic.com/doc/install/binary/gpg.key](https://flussonic.com/doc/install/binary/gpg.key) | apt-key add -
echo "deb [https://flussonic.com/doc/install](https://flussonic.com/doc/install) binary/" > /etc/apt/sources.list.d/flussonic.list

# Update and Install
apt-get update
apt-get -y install flussonic flussonic-ffmpeg flussonic-python
```

#### CentOS/RedHat

```bash
# Import GPG Key
rpm --import [https://flussonic.com/doc/install/binary/gpg.key](https://flussonic.com/doc/install/binary/gpg.key)

# Add Repository
cat <<EOF > /etc/yum.repos.d/flussonic.repo
[flussonic]
name=Flussonic Repository
baseurl=[https://flussonic.com/doc/install/rpm/](https://flussonic.com/doc/install/rpm/)
enabled=1
gpgcheck=1
EOF

# Install
yum install flussonic flussonic-ffmpeg flussonic-python -y
```

-----

## 🔑 Configuration & Activation

1.  **Start the Service:**
    ```bash
    service flussonic start
    ```
2.  **Access Web UI:**
    Open your browser and navigate to `http://YOUR_SERVER_IP:80`.
3.  **Activate License:**
    Enter the license key provided by the Flussonic sales team.
4.  **Security Step:**
    ⚠️ **Important:** Change the default `admin` password immediately upon first login to secure your server.

-----

## 🛠 Management Commands

Keep your server healthy with these essential commands:

| Action | Command |
| :--- | :--- |
| **Start Server** | `service flussonic start` |
| **Stop Server** | `service flussonic stop` |
| **Restart Server** | `service flussonic restart` |
| **Check Status** | `service flussonic status` |
| **Update Server** | `apt-get update && apt-get install flussonic` |
| **View Logs** | `tail -f /var/log/flussonic/flussonic.log` |

-----

## 🌐 Support & Community

Join the discussion and get help from other professionals:

  * [**Official Documentation**](https://flussonic.com/doc/) - Full technical guides.
  * [**Telegram Community**](https://www.google.com/search?q=https://t.me/flussonic_help) - Real-time chat with other admins.
      * *Note: Please respect group rules. No buying/selling allowed.*

-----

**Disclaimer:** This is an unofficial repository for quick deployment scripts. Flussonic is a commercial product owned by Erlyvideo.



### Why this version is better:
1.  **Badges:** Adds visual appeal at the top (Status, Platform, License).
2.  **Table of Contents:** Makes navigation easier.
3.  **Code Blocks:** Uses syntax highlighting for bash commands, making them easier to read and copy.
4.  **Tables:** Uses a table for commands, which is much cleaner than a list.
5.  **Security Warning:** Explicitly mentions changing the password, which is a good practice.
6.  **Disclaimer:** Adds a professional touch by clarifying the nature of the repo.


