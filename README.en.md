# homelab

[Versión en español](README.md)

Personal infrastructure lab for practicing Linux systems operations,
virtualization and automation. Everything runs on a private network, with no
internet exposure and no real data.

## Status

Under construction — phase 0 (host in a known state).

## Hardware

| Component | Value |
|---|---|
| Host | HP, Intel 9th-gen i5 |
| RAM | _pending: `free -h`_ |
| Disk | _pending: `df -h`_ |
| Hypervisor | Proxmox VE 9.2.2 |
| Network | Private LAN, `192.168.1.0/24` |

## Architecture

_pending: diagram and VM table_

## v0.1 scope

- Proxmox host with correct repositories and fully updated.
- Reusable AlmaLinux 9 template with cloud-init.
- Two VMs: `lab-control` and `lab-app`, with static IPs.
- One containerized service on `lab-app`, verified from `lab-control`.
- One induced failure, diagnosed and documented.

## How to run

_pending: written once the first VM exists._

## Security

- The lab is **not** exposed to the internet.
- No credentials, keys or public IPs in this repository.
- Administrative access over SSH keys, not passwords.

## Documents

- [PROGRESO_LAB.md](PROGRESO_LAB.md) — current state and next step.
- [DECISIONES.md](DECISIONES.md) — what was chosen and why.
- [ERRORES.md](ERRORES.md) — failures, root cause, prevention.
