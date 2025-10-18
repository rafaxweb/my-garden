# JARD-003 - Setup de pruebas automáticas

*(Configuración de pipeline de pruebas.)*

## Story
Como QA, 
quiero un pipeline básico con Jest, Cypress y NUnit.

## Criterios de aceptación
- AC1: Tests ejecutables desde pipeline.
- AC2: Reporte automático en GitHub Actions.

## Escenarios
- Dado que el pipeline está configurado
  Cuando se realiza un push a la rama principal
  Entonces se ejecutan los tests de Jest, Cypress y NUnit automáticamente

- Dado que hay fallos en los tests
  Cuando se genera el reporte en GitHub Actions
  Entonces el equipo recibe notificación y el build falla