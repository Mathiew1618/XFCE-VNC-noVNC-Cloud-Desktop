# 📌 Project Overview

This repository provides a complete, reproducible setup for running an XFCE desktop environment on a cloud server using:

- **XFCE Desktop** — lightweight, fast, ideal for remote use
- **VNC Server** — remote desktop protocol
- **noVNC** — browser-based VNC client
- **Websockify** — websocket bridge for noVNC
- **Systemd services** — automatic startup and reliability
- **Firewall rules** — secure network exposure

This project is ideal for:

- Cloud engineering
- Linux administration
- Remote desktop architecture
- Security engineering
- Lightweight GUI environments
- Portfolio demonstration

---

# 🖥️ Architecture

```text
[User Browser]
      ↓  HTTPS
   [noVNC Web UI]
      ↓  WebSockets
   [Websockify Proxy]
      ↓  TCP
   [VNC Server :5901]
      ↓
   [XFCE Desktop Session]
      ↓
   [Linux VPS]

This architecture allows you to access a full Linux desktop from any browser, without installing a VNC client.

🚀 Features
Lightweight XFCE desktop
VNC access (TigerVNC or TightVNC)
Browser-based access via noVNC
Systemd services for auto-start
Secure firewall configuration
Works on any KVM-based VPS
Ideal for cloud desktops and remote GUI apps
📂 Repository Structure
XFCE-VNC-noVNC/
│
├── scripts/
│   ├── install_xfce.sh
│   ├── install_vnc.sh
│   ├── install_novnc.sh
│   └── start_all.sh
│
├── systemd/
│   ├── vncserver.service
│   └── novnc.service
│
├── screenshots/
│   ├── xfce_desktop.png
│   └── novnc_login.png
│
├── security-notes.md
└── README.md
📦 Installation
1. Install XFCE
sudo apt update
sudo apt install -y xfce4 xfce4-goodies
2. Install VNC Server
sudo apt install -y tigervnc-standalone-server

Create ~/.vnc/xstartup:

#!/bin/sh
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
startxfce4 &
3. Start VNC
vncserver :1 -geometry 1280x800 -depth 24
4. Install noVNC + Websockify
sudo apt install -y novnc websockify

Start noVNC:

websockify --web=/usr/share/novnc/ 6080 localhost:5901
5. Open firewall ports
5901 (VNC) — optional
6080 (noVNC) — required

Example (UFW):

sudo ufw allow 6080/tcp
🔧 Systemd Services

This repo includes:

vncserver.service
novnc.service

These ensure the desktop environment starts automatically on boot.

🔐 Security Considerations

See security-notes.md for details, including:

Restricting VNC to localhost
Using SSH tunnels
Adding TLS termination (Caddy or Nginx)
Hardening the VPS
Using strong VNC passwords
Avoiding root login
Limiting exposed ports
🌐 Accessing the Desktop
Via Browser (noVNC)

Open:

http://<your-server-ip>:6080
Via VNC Client

Connect to:

<your-server-ip>:5901
📸 Screenshots

Add screenshots of:

XFCE desktop
noVNC login page
Terminal inside XFCE

This makes the repo visually appealing and professional.

📘 What This Project Demonstrates

This project shows proficiency in:

Linux system administration
Remote desktop protocols
Websocket tunneling
Cloud networking
Security hardening
Automation with systemd

This is exactly the kind of hands-on work cloud security and cloud engineering roles look for.

📄 License MIT License
