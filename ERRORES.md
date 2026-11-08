# Errores

Formato: síntoma, causa raíz, solución, cómo evitarlo.

## E-001 — `apt-get update` falla desde la instalación

- **Estado:** abierto.
- **Síntoma:** tareas `Update package database` en rojo, con
  `Error: command 'apt-get update' failed`, repetidas desde el 7 de octubre.
- **Impacto:** el host no recibe actualizaciones ni parches de seguridad; no se
  pueden instalar paquetes nuevos, incluido `git`.
- **Causa raíz:** pendiente de confirmar. Hipótesis: repositorio empresarial
  activo sin suscripción (401), repositorio de versión equivocada (404), o
  resolución de nombres/reloj.
- **Solución:** pendiente.
- **Cómo evitarlo:** pendiente.

