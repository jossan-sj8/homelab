# Decisiones

Formato: qué se decidió, por qué, y qué alternativa se descartó.

## D-001 — Proxmox VE como hipervisor

- **Decisión:** Proxmox VE 9.2.2 como sistema del host.
- **Motivo:** snapshots, clonado de plantillas y API; permite romper y revertir.
- **Alternativa descartada:** Ubuntu Server + Docker directo (menos capas, pero
  sin snapshots ni aislamiento entre servicios).

## D-002 — AlmaLinux 9 como sistema invitado

- **Decisión:** VMs sobre AlmaLinux 9.
- **Motivo:** compatible con RHEL (temario RHCSA/LFCS), mismo stack que el
  trabajo (dnf, firewalld, SELinux), repositorios libres.
- **Alternativa descartada:** Debian/Ubuntu; no practica SELinux.

## D-003 — Repositorio público

- **Decisión:** el repo `homelab` es público desde el primer commit.
- **Motivo:** es el entregable; no contiene datos reales ni secretos.
- **Regla asociada:** si un archivo necesita un secreto, no entra al repo.
