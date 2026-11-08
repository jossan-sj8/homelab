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

## D-004 — Canal `pve-no-subscription`, no enterprise

- **Decisión:** desactivar los repositorios enterprise y usar el canal gratuito.
- **Motivo:** no hay suscripción; el canal gratuito recibe los mismos paquetes
  con algo menos de retraso en pruebas.
- **Riesgo asumido:** es el canal de pruebas de Proxmox; en producción se paga.
- **Nota:** los repos enterprise quedan definidos con `Enabled: false` como
  registro de la decisión, no borrados.
