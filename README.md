# homelab

[English version](README.en.md)

Laboratorio de infraestructura personal para practicar operación de sistemas
Linux, virtualización y automatización. Todo corre en una red privada, sin
exposición a internet y sin datos reales.

## Estado

En construcción — fase 0 (host en estado conocido).

## Hardware

| Componente | Valor |
|---|---|
| Host | HP, Intel i5 9ª gen |
| RAM | _pendiente: `free -h`_ |
| Disco | _pendiente: `df -h`_ |
| Hipervisor | Proxmox VE 9.2.2 |
| Red | LAN privada, `192.168.1.0/24` |

## Arquitectura

_pendiente: diagrama y tabla de VMs_

## Alcance de v0.1

- Host Proxmox con repositorios correctos y actualizado.
- Plantilla AlmaLinux 9 reutilizable con cloud-init.
- Dos VMs: `lab-control` y `lab-app`, con IP fija.
- Un servicio contenerizado en `lab-app`, verificado desde `lab-control`.
- Un fallo provocado, diagnosticado y documentado.

## Cómo se levanta

_pendiente: se escribe cuando exista la primera VM._

## Seguridad

- El laboratorio **no** está expuesto a internet.
- Sin credenciales, llaves ni IPs públicas en este repositorio.
- Acceso administrativo por SSH con llave, no por contraseña.

## Documentos

- [PROGRESO_LAB.md](PROGRESO_LAB.md) — estado actual y próximo paso.
- [DECISIONES.md](DECISIONES.md) — qué se eligió y por qué.
- [ERRORES.md](ERRORES.md) — fallos, causa raíz, cómo evitarlos.
