# Hey, welcome to my profile! 👋

**Future sysadmin | Self-hosting nerd | Homelab tinkerer**

I love building stuff myself and seeing how it all fits together. My homelab is my playground for Linux, networking, containers and automation, and honestly it's where I've learned most of my practical IT skills.

> 🎮 **All of this is just for fun.** I'm a vibe coder: I build things together with AI and I don't have deep code knowledge. Where I actually shine is infrastructure (Linux, Docker, networking), and that's the career I'm training for.

---

## 🎯 What I'm Up To Right Now

- 🎓 **Retraining as an IT Specialist for System Integration (FISI)**: networking, servers, security and IT projects
- 🔎 **Hunting for an 8.5-month internship in IT** (system integration, sysadmin, infrastructure or support). If you've got an opening or know someone who does, hit me up!
- 🏠 **Building out my homelab:** Proxmox VE on refurbished Intel mini PCs running a Debian VM with Docker plus an LXC container for Pi-hole, plus a media stack and remote access via Tailscale
- 📦 **Moving house (for my servers):** migrating services from a rented Hetzner server to my own hardware at home
- 📚 **Learning:** more automation, cybersecurity basics, and keeping my setups clean and reproducible

---

## 🛠️ Skills & Tech Stack

### Operating Systems & Hardware
![Proxmox](https://img.shields.io/badge/Proxmox_VE-E57000?style=for-the-badge&logo=proxmox&logoColor=white)
![Debian](https://img.shields.io/badge/Debian-A81D33?style=for-the-badge&logo=debian&logoColor=white)
![Ubuntu Server](https://img.shields.io/badge/Ubuntu_Server-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Raspberry Pi](https://img.shields.io/badge/Raspberry_Pi-A22846?style=for-the-badge&logo=raspberrypi&logoColor=white)

### Containers & Self-Hosting
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Jellyfin](https://img.shields.io/badge/Jellyfin-00A4DC?style=for-the-badge&logo=jellyfin&logoColor=white)
![Immich](https://img.shields.io/badge/Immich-4250AF?style=for-the-badge&logo=immich&logoColor=white)
![Home Assistant](https://img.shields.io/badge/Home_Assistant-18BCF2?style=for-the-badge&logo=homeassistant&logoColor=white)
![Dockge](https://img.shields.io/badge/Dockge-Compose_Manager-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Nodvard Deck](https://img.shields.io/badge/Nodvard_Deck-Homelab_Dashboard-5B5BD6?style=for-the-badge)
![AMP](https://img.shields.io/badge/AMP-Game_Server_Panel-4C9BE8?style=for-the-badge)

### Networking & Security
![Nginx Proxy Manager](https://img.shields.io/badge/Nginx_Proxy_Manager-F15833?style=for-the-badge&logo=nginxproxymanager&logoColor=white)
![Tailscale](https://img.shields.io/badge/Tailscale-242424?style=for-the-badge&logo=tailscale&logoColor=white)
![Pi-hole](https://img.shields.io/badge/Pi--hole-96060C?style=for-the-badge&logo=pihole&logoColor=white)
![Fail2ban](https://img.shields.io/badge/Fail2ban-Hardening-2E7D32?style=for-the-badge)

### Development (vibe coded with AI, not hand-written)
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![VS Code](https://img.shields.io/badge/VS_Code-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white)

### AI-Assisted Workflows
![AI Pair Programming](https://img.shields.io/badge/AI_Assisted-Coding-1F8A70?style=for-the-badge)

---

## 🏗️ Homelab Architecture

My homelab runs on **refurbished Intel mini PCs** (**Proxmox VE** as the hypervisor, with a Debian VM running Docker and an LXC container running Pi-hole) plus a **Raspberry Pi 400** for smart home stuff. I manage my containers with Dockge and run everything through [Nodvard Deck](https://github.com/nodvard/deck), a self-hosted homelab dashboard that lives on my home server and also keeps an eye on my Raspberry Pi and my Hetzner server. My home router doesn't let me forward ports, so **remote access goes through Tailscale** instead of exposed ports. I've worked with WireGuard before and know my way around it a bit, but Tailscale is what I use these days.

```mermaid
flowchart TB
    Remote(["📱 Remote Devices<br/>phone / laptop"])
    TS["Tailscale<br/>mesh VPN, no open ports"]

    subgraph Home["🏠 Home Network"]
        direction TB
        Router["FRITZ!Box<br/>home router"]

        subgraph Mini["Intel Mini PC (Proxmox VE)"]
            direction TB
            subgraph VM["Debian VM (Docker)"]
                direction TB
                Mgmt["Management<br/>Dockge"]
                Deck["Nodvard Deck<br/>management dashboard"]
                subgraph Media["Media Stack"]
                    JF["Jellyfin"]
                    IM["Immich"]
                end
                Disk[("2 TB media disk")]
                JF --> Disk
                IM --> Disk
            end
            subgraph LXC["LXC Container"]
                PH["Pi-hole<br/>DNS filtering"]
            end
        end

        subgraph Pi["Raspberry Pi 400 (Ubuntu Server + CasaOS)"]
            direction TB
            HA["Home Assistant"]
        end

        Clients(["💻 Local Clients"])
    end

    Remote --> TS
    TS --> Mini
    TS --> Pi
    Clients --> Router
    Router -- "DNS" --> PH
    Mgmt -. "manages" .-> Media
    Deck -. "manages" .-> Media
    Deck -. "manages" .-> LXC
    Deck -. "manages" .-> Pi
```

---

## ☁️ Bonus: My Rented Server (Hetzner)

Separate from the homelab, I also run an unmanaged **dedicated server at Hetzner** (Debian + Docker). It's home to the stuff that needs a public face, and I'm slowly moving its workloads over to my own hardware.

```mermaid
flowchart TB
    Internet(["🌐 Internet"])

    subgraph HZ["Hetzner Dedicated Server (Debian)"]
        direction TB
        F2B["SSH + Fail2ban<br/>hardened access"]
        NPM2["Nginx Proxy Manager<br/>reverse proxy + HTTPS"]
        Panel["1Panel<br/>server management"]

        subgraph Dock["Docker Workloads"]
            direction TB
            Apps["Self-hosted Apps"]
            Games["AMP Game Servers<br/>Minecraft modpacks"]
        end

        NPM2 --> Apps
        NPM2 --> Games
        Panel -. "manages" .-> Dock
    end

    Deck2["Nodvard Deck<br/>hosted on my home server"]
    Backup[("Off-site Backups<br/>planned")]

    Deck2 -. "manages" .-> HZ
    Internet -- "HTTPS" --> NPM2
    Internet -- "SSH" --> F2B
    Dock -. "scheduled dumps" .-> Backup
```

**The fun bits**

- 🔐 **No open ports at home:** Tailscale for remote access instead of exposed ports
- 🧱 **Virtualized base:** Proxmox VE underneath, a Debian VM with Docker and a Pi-hole LXC on top
- 🎮 **Squeezing performance:** profiling and tuning hungry Minecraft modpack servers
- 🔁 **Migration mode:** planning and moving services, data and media between hosts step by step

---

## 🖥️ Hardware

| Machine | Role | Specs |
|---|---|---|
| **Hetzner dedicated server** | Rented server for public-facing services and game servers | Intel Core i7-6700 (4C/8T), Intel HD 530 iGPU, ~62 GiB RAM, ~3.5 TB storage |
| **Home server (mini PCs)** | Main homelab nodes (Proxmox VE host with a Debian Docker VM and a Pi-hole LXC) | Refurbished Acer Veriton N4660G mini PC, Intel Core i5-9500T, 16 GB RAM, 512 GB SSD, 1 TB Netac NVMe, 2 TB media disk |
| **Raspberry Pi 400** | Smart home | Ubuntu Server + CasaOS, Home Assistant |
| **Gaming PC** | Gaming and everyday driver | AMD Ryzen 7 5700X, MSI MPG B550 Gaming Plus, AMD Radeon RX 9060 XT 16 GB, 32 GB RAM |

---

## 🚀 What I Build & Run

| Project | What it is | Tech |
|---|---|---|
| **Home media & photos** | My own media server and photo library | Jellyfin, Immich, Docker |
| **Game server hosting** | Heavily modded Minecraft servers, tuned with profiling | AMP, Docker, Java |
| **Client-side mods** | Hobby mods and addons for games, built with AI help | Java |
| **Network services** | DNS-level ad/tracker blocking, mesh VPN, reverse proxy with TLS | Pi-hole, Tailscale, Nginx Proxy Manager |
| **Smart home** | Home automation running on a Raspberry Pi | Home Assistant, Docker, Raspberry Pi |

---

## 🧰 How I Roll

- **Fun first:** this is my hobby. I build things because it's enjoyable, not because I have to
- **Hands-on:** I learn fastest by building, breaking and fixing real systems
- **Vibe coding, honestly:** I use AI assistants to write code, and I'm upfront that I don't have deep programming knowledge. Code is a tool for me; my focus is getting systems running and understanding the infrastructure around them
- **Tooling:** VS Code, Git and AI assistance
- **Mindset:** troubleshoot step by step, automate the boring stuff, keep things simple

---

## 📫 Let's Connect

I'm actively looking for an **IT internship (8.5 months)** in system integration or administration. Feel free to reach out via GitHub, or open an issue or discussion on one of my repos.

---

<sub>Built with Markdown, Mermaid and way too much curiosity. 🛠️</sub>
