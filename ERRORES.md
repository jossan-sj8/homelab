# Errores

Formato: síntoma, causa raíz, solución, cómo evitarlo.

## E-001 — `apt-get update` falla desde la instalación

- **Estado:** resuelto.
- **Síntoma:** tareas `Update package database` en rojo, con
  `Error: command 'apt-get update' failed`, repetidas desde el 7 de octubre.
- **Impacto:** el host no recibía actualizaciones ni parches de seguridad; no se
  podían instalar paquetes nuevos, incluido `git`.
- **Causa raíz:** el instalador dejó activos los canales de pago
  `pve-enterprise` y `ceph-squid` (`enterprise.proxmox.com`). Sin suscripción,
  el servidor responde `401 Unauthorized` y apt aborta la actualización completa
  con `The repository ... is not signed`.
- **Solución:** `Enabled: false` en `pve-enterprise.sources` y `ceph.sources`;
  se agregó `pve-no-subscription.sources` apuntando a
  `download.proxmox.com` con la misma llave (`Signed-By`). `apt update` queda
  sin errores y ve 212 paquetes actualizables.
- **Cómo evitarlo:** verificar `apt update` inmediatamente después de instalar
  el hipervisor, y no seguir tutoriales de otra versión mayor (Proxmox 9 usa
  Debian 13 y el formato deb822 `.sources`, no `sources.list`).
