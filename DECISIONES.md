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

## D-005 — Imagen AlmaLinux 9 GenericCloud, fijada por hash

- **Decisión:** usar la imagen cloud, no la ISO, y registrarla por hash.
- **Motivo:** cloud-init permite plantilla y clones sin instalador manual.
- **Registro:** `AlmaLinux-9-GenericCloud-latest.x86_64.qcow2`, sha256
  `6f94881458dfe966474544b12e86d078d81a600457188045d317b0ce3c3bdca7`.

## D-006 — Direcciones IP fijas documentadas

- **Decisión:** `lab-control` = `192.168.1.50`, `lab-app` = `192.168.1.51`.
- **Motivo:** la tabla de direcciones vive en el repositorio y es reproducible.
- **Alternativa descartada:** DHCP con reserva en el router; la reserva no está
  versionada ni se ve en Git.

## D-007 — Firewall declarado en la plantilla, vía vendor-data

- **Decisión:** declarar `firewalld` y `qemu-guest-agent` en un archivo
  vendor-data de cloud-init, aplicado a `tpl-alma9`.
- **Motivo:** el defecto está en el molde. Corregir `lab-app` a mano arregla una
  VM; corregir la plantilla arregla todas las futuras.
- **Por qué vendor-data y no user-data:** Proxmox genera el user-data con
  `ciuser`, `sshkeys` e `ipconfig0`; el vendor-data se **fusiona** encima y no
  lo reemplaza, así que no se pierde la configuración de cada clon.
- **Alternativa descartada:** hornear `firewalld` en el disco de la plantilla;
  la imagen deja de ser la del vendor y se complica actualizarla.

## D-008 — Servicio contenerizado como unidad de usuario

- **Decisión:** Quadlet (`~/.config/containers/systemd/web.container`) con
  `Restart=on-failure`, `RestartSec=5` y `loginctl enable-linger`.
- **Motivo:** el servicio debe existir por declaración, no por comando manual;
  `linger` hace que la instancia de systemd del usuario arranque sin sesión.
- **Alternativa descartada:** `podman generate systemd` (en desuso desde Podman
  4.4) y contenedor rootful con unidad de sistema (más privilegios de los
  necesarios).
- **Verificación:** tras `reboot` el contenedor se recrea con otro ID; tras
  `podman kill` vuelve en ~5 s; tras `systemctl --user stop` permanece detenido.
