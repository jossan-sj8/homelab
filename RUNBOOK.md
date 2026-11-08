# Runbook

Procedimientos operativos. Formato: síntoma, diagnóstico, acción, verificación.
Escritos antes de necesitarlos.

## R1 — Una VM no responde por SSH

- **Síntoma:** `qm start` devuelve éxito, pero `ssh` no conecta.
- **Diagnóstico:** `qm status <vmid>` (¿está `running`?); `qm terminal <vmid>` y
  leer el arranque (se sale con `Ctrl+O`). Si dice "no bootable device", el disco
  no está conectado o el orden de arranque es incorrecto.
- **Acción:** `qm config <vmid> | grep -E '^(boot|scsi0|ide2)'`.
- **Verificación:** la consola llega a un login y `ssh` responde.

## R2 — El servicio de `lab-app` no responde

- **Síntoma:** `curl -I http://192.168.1.51:8080` falla desde otra máquina.
- **Diagnóstico, en este orden:**
  1. `curl -I http://localhost:8080` dentro de `lab-app`. Si funciona, el
     problema es de red, no del servicio.
  2. `systemctl --user status web --no-pager`.
  3. `sudo firewall-cmd --list-ports` (debe incluir `8080/tcp`).
  4. `podman ps` (el contenedor debe llamarse `systemd-web`).
- **Acción:** `systemctl --user restart web`; si el puerto no está, `sudo
  firewall-cmd --add-port=8080/tcp --permanent && sudo firewall-cmd --reload`.
- **Verificación:** `200 OK` desde `lab-control`.

## R3 — Recuperar una VM desde un snapshot

- **Cuándo:** se rompió un archivo o una configuración y no hay tiempo de
  diagnosticar.
- **Advertencia:** el rollback descarta **todo** lo escrito desde el snapshot.
- **Acción:**
  ```bash
  qm listsnapshot <vmid>
  qm stop <vmid>
  qm rollback <vmid> <nombre-del-snapshot>
  qm start <vmid>
  ```
- **Verificación:** `qm listsnapshot` muestra `current` bajo el snapshot
  restaurado, y el servicio responde como antes.

## R4 — No hay acceso SSH a una VM

- **Diagnóstico:** `qm terminal <vmid>` desde el host; dentro, `systemctl status
  sshd`, `ip -br a`, `sudo firewall-cmd --list-services` (debe incluir `ssh`).
- **Acción:** `sudo systemctl restart sshd`; `sudo firewall-cmd
  --add-service=ssh --permanent && sudo firewall-cmd --reload`.
- **Verificación:** nueva sesión SSH acepta la llave y no pide contraseña.
