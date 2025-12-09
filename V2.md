
---

📺 Flussonic Media Server

Flussonic Media Server is a powerful streaming platform for live TV, VOD, IPTV, and OTT delivery.  
This README provides installation instructions, activation steps, and community support links.

---

⚙️ Prerequisites
- OS: Ubuntu 24.04 / 22.04 / 20.04, CentOS/RedHat  
- Architecture: amd64, arm64  
- Ports: Ensure port 80 is free for the web interface  
- Privileges: Root or sudo access  

---

🚀 Installation

Quick Install (Recommended)
`bash
curl -sSf https://flussonic.com/public/install.sh | sh
`

Manual Install (Debian/Ubuntu)
`bash
wget -q -O - https://flussonic.com/doc/install/binary/gpg.key | apt-key add -
echo "deb https://flussonic.com/doc/install binary/" > /etc/apt/sources.list.d/flussonic.list
apt-get update
apt-get -y install flussonic flussonic-ffmpeg flussonic-python
`

CentOS/RedHat
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
2. Open the web interface: http://localhost  
3. Enter your license key provided by Flussonic.  

---

🔄 Updating
`bash
apt-get update
apt-get -y install flussonic
service flussonic restart
`
For RPM-based systems:  
`bash
yum update flussonic
`

---

🧩 Useful Commands
- Start: service flussonic start  
- Stop: service flussonic stop  
- Restart: service flussonic restart  
- Status: service flussonic status  

---

🌐 Community & Support
- Telegram Group: Flussonic Help 📡💻  
  - 360+ members, active discussions  
  - Rules: Group Rules  
  - ❌ Do not buy/sell inside the group  
- Official Docs: Flussonic Documentation  

---

📌 Notes
- Change the default admin password immediately after installation.  
- Flussonic supports Docker deployment for isolated environments.  
- Ideal for ISP, OTT, IPTV, and enterprise streaming solutions.  

---

Sources: Flussonic official documentation

---
