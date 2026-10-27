# Hi, welcome to my profile! 👋

**Aspiring Systems Integrator | Self-Hosting Enthusiast | Homelab Builder**

I like to understand how things work by building them myself. My homelab is my playground for infrastructure, networking, containers and automation, and it's where most of my practical IT skills come from.

---

## 🎯 Current Focus

- 🎓 **Finishing my retraining as an IT Specialist for System Integration (FISI)**, covering networking, server administration, security and IT project work
- 🔎 **Looking for an 8.5-month internship in IT** (system integration, system administration, infrastructure or support). If you have an opening or know someone who does, I'd love to connect!
- 🧪 **Homelab projects:** hardening and documenting my setup, improving backup and monitoring, and migrating workloads to my own hardware
- 📚 **Learning:** more automation, cybersecurity fundamentals, and clean, reproducible infrastructure

---

## 🛠️ Skills & Tech Stack

### Virtualization & Operating Systems
![Proxmox](https://img.shields.io/badge/Proxmox_VE-E57000?style=for-the-badge&logo=proxmox&logoColor=white)
![Debian](https://img.shields.io/badge/Debian-A81D33?style=for-the-badge&logo=debian&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![ZFS](https://img.shields.io/badge/ZFS-0072C6?style=for-the-badge)

### Networking & Security
![Nginx Proxy Manager](https://img.shields.io/badge/Nginx_Proxy_Manager-F15833?style=for-the-badge&logo=nginxproxymanager&logoColor=white)
![WireGuard](https://img.shields.io/badge/WireGuard-88171A?style=for-the-badge&logo=wireguard&logoColor=white)
![Pi-hole](https://img.shields.io/badge/Pi--hole-96060C?style=for-the-badge&logo=pihole&logoColor=white)

### Containers & Self-Hosting
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![AMP](https://img.shields.io/badge/AMP-Game_Server_Panel-4C9BE8?style=for-the-badge)

### Development
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![VS Code](https://img.shields.io/badge/VS_Code-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white)

### AI-Assisted Workflows
![Local LLMs](https://img.shields.io/badge/Local_LLMs-Self--Hosted-8A2BE2?style=for-the-badge)
![AI Pair Programming](https://img.shields.io/badge/AI_Assisted-Coding-1F8A70?style=for-the-badge)

---

## 🏗️ Homelab Architecture

Everything runs on a single Proxmox VE hypervisor with ZFS-backed storage. External access goes through a reverse proxy and a WireGuard VPN, while Pi-hole handles DNS filtering for the local network. Workloads are containerized with Docker.

```mermaid
flowchart TB
    Internet(["🌐 Internet"])

    subgraph Edge["Network Edge & Routing"]
        direction TB
        WG["WireGuard VPN<br/>secure remote access"]
        NPM["Nginx Proxy Manager<br/>reverse proxy + TLS"]
        PH["Pi-hole<br/>DNS filtering"]
    end

    subgraph PVE["Proxmox VE Hypervisor (Debian-based)"]
        direction TB

        ZFS[("ZFS Storage Pool<br/>snapshots + data integrity")]

        subgraph DockerHost["Docker Host (VM / LXC)"]
            direction TB
            subgraph Portal["Learning Portal"]
                Node["Node.js App"]
                SQLite[("SQLite")]
                Node --> SQLite
            end
            subgraph Games["Game Servers"]
                AMP["AMP Panel"]
                MC["Minecraft Modpack Server<br/>Docker container"]
                AMP --> MC
            end
        end

        DockerHost -. "persistent volumes" .-> ZFS
    end

    LAN(["💻 Local Clients"])

    Internet -- "HTTPS" --> NPM
    Internet -- "UDP / VPN" --> WG
    LAN -- "DNS queries" --> PH
    NPM -- "proxy" --> Node
    NPM -- "proxy" --> AMP
    WG -- "admin access" --> PVE
```

**Highlights**

- 🔐 **Secure by default:** services are published through a reverse proxy, and administration is done over VPN
- 💾 **Data integrity first:** ZFS provides snapshots and checksummed storage for persistent data
- 🐳 **Reproducible workloads:** services run in Docker containers with persistent volumes
- 🎮 **Performance tuning:** resource-hungry Minecraft modpack servers (profiling, JVM and mod optimization) run in containers managed via AMP

---

## 🚀 What I Build & Run

| Project | What it is | Tech |
|---|---|---|
| **Self-hosted learning portal** | A web app with exercises and user accounts for fellow learners | Node.js, SQLite, Docker |
| **Game server hosting** | Dedicated, heavily modded Minecraft servers with performance profiling | AMP, Docker, Java |
| **Client-side mods** | Custom client-side mods and addons | Java |
| **Network services** | Ad/tracker blocking, VPN access, reverse proxy with TLS | Pi-hole, WireGuard, Nginx Proxy Manager |
| **Storage management** | Pool design, snapshots and data integrity | ZFS |

---

## 🧰 How I Work

- **Hands-on first:** I learn fastest by building, breaking and fixing real systems
- **Documentation matters:** if I can't explain a setup, I don't consider it finished
- **Tooling:** VS Code, Git, and local LLMs as a coding companion (I review and understand what I ship)
- **Mindset:** troubleshoot systematically, automate repetitive work, and keep things simple and maintainable

---

## 📫 Let's Connect

I'm actively looking for an **IT internship (8.5 months)** in system integration or administration. Feel free to reach out via GitHub, or open an issue or discussion on one of my repositories.

---

<sub>Built with Markdown, Mermaid and a lot of curiosity. 🛠️</sub>
