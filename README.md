# Self-Hosted Private Cloud & Direct Storage Stack

A comprehensive guide for transforming a host machine or laptop into a secure, private cloud server accessible remotely across mobile and desktop devices—without exposing any ports to the open internet.

---

## Simple Concept Overview

Both setup methods use **Tailscale** to create an encrypted, invisible tunnel between your mobile phone and your home server. This bypasses port forwarding and keeps your server hidden from internet hackers.

                ┌─────────────────────────────────────┐
                │            MOBILE PHONE             │
                │   (Nextcloud App / Mobile SFTP)     │
                └──────────────────┬──────────────────┘
                                   │
                 [ Tailscale Encrypted WireGuard Tunnel ]
                                   │
                ┌──────────────────┴──────────────────┐
                │            LAPTOP SERVER            │
                │                                     │
                │  ┌──────────────┐ ┌──────────────┐  │
                │  │ Nextcloud    │ │ FileZilla    │  │
                │  │ Docker Stack │ │ SFTP Server  │  │
                │  └──────┬───────┘ └──────┬───────┘  │
                │         │                │          │
                │  ┌──────▼────────────────▼───────┐  │
                │  │   Local Storage (C: / D:)     │  │
                │  └───────────────────────────────┘  │
                └─────────────────────────────────────┘
---

## 🛠️ Choose Your Access Method

| Feature | Method 1: Direct SFTP Access | Method 2: Nextcloud AIO Cloud |
| :--- | :--- | :--- |
| **Best For** | Ultra-fast direct file browsing & media streaming | Google Drive / Photos alternative with auto-sync |
| **Interface** | Mobile File Managers (Solid Explorer, CX File) | Web Dashboard & Official Nextcloud Apps |
| **Resource Usage** | Lightweight (~10–20 MB RAM) | Medium (~1.5–2 GB RAM via Docker) |
| **Backups** | Manual copy / sync | Automated 3-2-1 BorgBackup + Rclone Cloud Sync |
| **Detailed Guide** | [`1.Direct SFTP Access via FileZilla Server.md`](./1.Direct%20SFTP%20Access%20via%20FileZilla%20Server.md) | [`2.Self-Hosted-Private-Cloud-AIO.md`](./2.Self-Hosted-Private-Cloud-AIO.md) |

---

## 📁 Repository Documentation Paths

* **Method 1: Direct File System Access**  
   Path: [`./1.Direct SFTP Access via FileZilla Server.md`](./1.Direct%20SFTP%20Access%20via%20FileZilla%20Server.md)  
  *Setup FileZilla Server natively on Windows to browse raw drive partitions (`C:\`, `D:\`) over Tailscale SSH/SFTP.*

* **Method 2: All-in-One Personal Cloud Engine**  
   Path: [`./2.Self-Hosted-Private-Cloud-AIO.md`](./2.Self-Hosted-Private-Cloud-AIO.md)  
  *Deploy Nextcloud AIO via Docker Desktop, configure Tailscale HTTPS certificates, and enable 3-2-1 automated cloud backups using BorgBackup and Rclone.*

---

## 🛡️ Quick Security Principles

* **Zero Port Forwarding:** Router ports remain closed. All traffic passes strictly through private Tailscale mesh network addresses (`100.x.y.z`).
* **Root Partition Guard:** Avoid mapping root `C:\` in SFTP to protect critical Windows OS files (`C:\Windows`). Scope access to secondary partitions or dedicated folders (e.g., `D:\PersonalCloud`).
* **Power Management:** Configure Windows Power Settings to `Never Sleep` when plugged in to ensure continuous 24/7 file availability.
