# JARD-006 - Carga del catálogo desde backend

*(Obtención del catálogo de plantas.)*

## Story
Como usuario, 
quiero disponer de un catálogo de plantas precargado con información básica.

## Criterios de aceptación
- AC1: La app descarga el catálogo la primera vez.
- AC2: Se guarda localmente para uso offline.

## Escenarios
- Dado que el usuario abre la app por primera vez
  Cuando se inicia la carga
  Entonces la app descarga el catálogo de plantas y lo almacena localmente

- Dado que el usuario está offline tras la primera carga
  Cuando accede al catálogo
  Entonces puede consultar la información sin conexión