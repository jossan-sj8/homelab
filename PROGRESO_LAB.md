# Progreso del laboratorio

## Proyecto actual

`homelab` — **cerrado**. Siguiente: `linux-baseline`.

## Estado

v0.1 entregado: construido, roto, recuperado y documentado.

## Hecho

- [x] Host Proxmox VE 9.2.26, kernel 7.0.14-28-pve, 0 unidades fallidas.
- [x] Repositorios enterprise desactivados; canal `pve-no-subscription` (E-001).
- [x] Repositorio clonado en el host; push por deploy key.
- [x] Imagen AlmaLinux 9.8 GenericCloud verificada por hash (D-005).
- [x] Plantilla con cloud-init, consola serie, firewall y agente (E-002, E-004, D-007).
- [x] `lab-control` y `lab-app` con IP fija, SSH por llave y SELinux enforcing.
- [x] nginx en 8080 servido como unidad Quadlet con reinicio automático (D-008).
- [x] Rotura y recuperación probadas con snapshot (D-010).
- [x] Diagrama, baseline, runbook y cuatro documentos de proyecto.

## Pendiente del proyecto

- [ ] Backup fuera del equipo con `vzdump` (D-010 lo deja explícito).

## Próximo proyecto

`linux-baseline`: Ansible desde `lab-control`, hardening de SSH, `auditd`,
firewall declarativo e idempotencia verificada.
