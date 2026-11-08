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

## E-002 — Plantilla creada sin disco de arranque

- **Estado:** resuelto.
- **Síntoma:** `qm config 9000` mostró `boot: order=net0` y ninguna línea
  `scsi0`; el disco importado seguía en `unused0`.
- **Impacto:** los clones habrían arrancado con "no bootable device" y el
  diagnóstico se habría buscado en cloud-init.
- **Causa raíz:** se ejecutó `qm set --ide2 local-lvm:cloudinit` y `qm template`
  sin ejecutar antes el `qm set --scsi0 --boot order=scsi0`; el paso se omitió y
  no se leyó la salida del `qm config`.
- **Solución:** ejecutar el `qm set` con `--scsi0`, `--boot order=scsi0`,
  `--serial0 socket` y `--vga serial0`; verificar las cuatro líneas antes de
  convertir en plantilla.
- **Cómo evitarlo:** la verificación es parte del paso, no un extra; un paso no
  está cerrado hasta que su salida se leyó.
