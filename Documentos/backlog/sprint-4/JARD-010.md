# JARD-010 - Testing e2e

*(Pruebas end-to-end del flujo completo.)*

## Story
Como QA, 
quiero ejecutar pruebas completas de usuario final.

## Criterios de aceptación
- AC1: Flujo "crear huerto → añadir planta → ver ficha" pasa todas las pruebas.

## Escenarios
- Dado que el QA ejecuta el flujo completo
  Cuando crea un huerto, añade una planta y consulta la ficha
  Entonces todas las pruebas pasan en el pipeline e2e

- Dado que se ejecutan las pruebas en el pipeline
  Cuando algún paso falla
  Entonces se genera un reporte detallado del error