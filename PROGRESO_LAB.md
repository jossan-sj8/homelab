# Progreso del laboratorio

## Proyecto actual

`homelab` — alcance definido en el README, 2 semanas.

## Fase

2 — plantilla AlmaLinux 9 creada; `lab-control` operativa.

## Hecho

- [x] Host con Proxmox VE 9.2.26, kernel 7.0.14-28-pve, 0 unidades fallidas.
- [x] Repositorios enterprise desactivados; canal `pve-no-subscription` activo (E-001).
- [x] Repositorio clonado en el host; push por deploy key.
- [x] Imagen AlmaLinux 9.8 GenericCloud verificada por hash (D-005).
- [x] Plantilla 9000 `tpl-alma9` con cloud-init, disco scsi0 y consola serie.
- [x] VM 100 `lab-control` con IP fija 192.168.1.50, SSH por llave, SELinux enforcing.

## Pendiente

- [ ] VM 101 `lab-app` (3 GB, 192.168.1.51) y servicio contenerizado.
- [ ] Ejercicio de rotura y recuperación documentado en ERRORES.md.
- [ ] Diagrama de arquitectura.

## Próximo paso

Crear `lab-app` desde la plantilla, desplegar un servicio y verificarlo desde
`lab-control`.
