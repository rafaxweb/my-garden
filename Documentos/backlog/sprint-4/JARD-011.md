# JARD-011 - Optimización offline

*(Garantizar funcionamiento sin conexión.)*

## Story
Como usuario, 
quiero que la app funcione sin conexión desde el primer arranque.

## Criterios de aceptación
- AC1: App usable offline.
- AC2: Sin errores de sincronización inexistente.

## Escenarios
- Dado que el usuario instala la app
  Cuando la usa sin conexión
  Entonces todas las funcionalidades principales están disponibles y no hay errores de sincronización

- Dado que el usuario está offline
  Cuando realiza cualquier operación
  Entonces no ve mensajes de error por falta de conexión