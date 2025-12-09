

---

📖 Flussonic Media Server – Installation & Activation Guide

⚙️ Prerequisites
- Supported OS: Ubuntu LTS 24.04, 22.04, 20.04, CentOS/RedHat, and other RPM-based distros  
- Architectures: amd64, arm64  
- Ensure HTTP port 80 is free (Flussonic uses it by default)  
- Root or sudo privileges required  

---

🚀 Installation Methods

1. Quick Install via Script
`bash
curl -sSf https://flussonic.com/public/install.sh | sh
`
This script automatically configures repositories and installs Flussonic.

---

2. Manual Install (Debian/Ubuntu)
`bash
wget -q -O - https://flussonic.com/doc/install/binary/gpg.key | apt-key add -
echo "deb https://flussonic.com/doc/install binary/" > /etc/apt/sources.list.d/flussonic.list
apt-get update
apt-get -y install flussonic flussonic-ffmpeg flussonic-python
`
This method gives you more control over package sources.

---

3. CentOS/RedHat (RPM-based)
`bash
rpm --import https://flussonic.com/doc/install/binary/gpg.key
cat <<EOF > /etc/yum.repos.d/flussonic.repo
[flussonic]
name=Flussonic Repository
baseurl=https://flussonic.com/doc/install/rpm/
enabled=1
gpgcheck=1
EOF

yum install flussonic flussonic-ffmpeg flussonic-python -y
`

---

🔑 Activation
1. Start the service:
   `bash
   service flussonic start
   `
2. Open the web interface:  
   http://localhost  
3. Enter your license key (provided by Flussonic).  

---

🔄 Updating Flussonic
To update to the latest version:
`bash
apt-get update
apt-get -y install flussonic
service flussonic restart
`
For RPM-based systems, use yum update flussonic.  

---

🧩 Useful Commands
- Start service: service flussonic start  
- Stop service: service flussonic stop  
- Restart service: service flussonic restart  
- Check status: service flussonic status  

---

📌 Notes
- Default admin login is set during installation; change the password immediately for security.  
- Flussonic can also run inside Docker containers for isolated deployments.  
- Supports Live TV, VOD, IPTV, OTT streaming platforms.  

---

Sources: Flussonic Official Manual GitHub – Flussonic Media Server Guide GeeksforGeeks – Flussonic Install Guide

---

