# Progreso del laboratorio

## Proyecto actual

`homelab` — alcance definido en el README, 2 semanas.

## Fase

4 — servicio contenerizado en `lab-app` y firewall activo.

## Hecho

- [x] Host con Proxmox VE 9.2.26, kernel 7.0.14-28-pve, 0 unidades fallidas.
- [x] Repositorios enterprise desactivados; canal `pve-no-subscription` activo (E-001).
- [x] Repositorio clonado en el host; push por deploy key.
- [x] Imagen AlmaLinux 9.8 GenericCloud verificada por hash (D-005).
- [x] Plantilla 9000 `tpl-alma9` con cloud-init, disco scsi0 y consola serie (E-002).
- [x] VM 100 `lab-control` con IP fija 192.168.1.50, SSH por llave, SELinux enforcing.
- [x] VM 101 `lab-app` con nginx en 8080, verificado desde `lab-control`.
- [x] `firewalld` activo en `lab-app`; sólo 8080/tcp abierto (E-003).

## Pendiente

- [ ] Declarar firewall en la plantilla vía vendor-data (D-007).
- [ ] Persistencia del contenedor: unidad de systemd + `loginctl enable-linger`.
- [ ] Ejercicio de rotura y recuperación documentado.
- [ ] Diagrama de arquitectura.
- [ ] `baseline.txt` del host.

## Próximo paso

Corregir la plantilla para que todo clon nazca con firewall, y verificar clonando
una VM temporal.
