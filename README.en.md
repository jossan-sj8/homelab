# homelab

[Versión en español](README.md)

Personal infrastructure lab for practicing Linux systems operations,
virtualization and automation. Everything runs on a private network, with no
internet exposure and no real data.

## Status

Phase 2 — AlmaLinux 9 template and first working VM.

## Hardware

| Component | Value |
|---|---|
| Host | HP, Intel 9th-gen i5 |
| RAM | 16 GB |
| Disk | 256 GB NVMe (68 GB root + LVM thin pool) |
| Hypervisor | Proxmox VE 9.2.26 |
| Network | Private LAN, `192.168.1.0/24` |

## Architecture

| VMID | Name | RAM | IP | Role |
|---|---|---|---|---|
| 9000 | `tpl-alma9` | 2 GB | — | AlmaLinux 9.8 template |
| 100 | `lab-control` | 2 GB | `192.168.1.50` | Control: Ansible, kubectl |
| 101 | `lab-app` | 3 GB | `192.168.1.51` | Containerized services (pending) |

VMs are cloned from the template and configure themselves with cloud-init: user,
SSH key, hostname and static IP.

## v0.1 scope

- [x] Proxmox host with correct repositories and fully updated.
- [x] Reusable AlmaLinux 9 template with cloud-init.
- [x] `lab-control` with static IP and key-based access.
- [ ] `lab-app` with a containerized service.
- [ ] One induced failure, diagnosed and documented.

## How to run

    qm clone 9000 101 --name lab-app --full
    qm set 101 --memory 3072 --ipconfig0 ip=192.168.1.51/24,gw=192.168.1.1 --nameserver 192.168.1.1
    qm start 101

## Security

- The lab is **not** exposed to the internet.
- No credentials, keys or public IPs in this repository.
- Administrative access over SSH keys, not passwords.
- Passwordless `sudo` for the cloud-init user: lab convenience, not a production
  setting.

## Documents

- [PROGRESO_LAB.md](PROGRESO_LAB.md) — current state and next step.
- [DECISIONES.md](DECISIONES.md) — what was chosen and why.
- [ERRORES.md](ERRORES.md) — failures, root cause, prevention.
