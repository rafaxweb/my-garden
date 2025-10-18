# JARD-002 - Configuración de linters y formateadores

*(Calidad de código y consistencia.)*

## Story
Como desarrollador, 
quiero estándares de código para mantener coherencia.

## Criterios de aceptación
- AC1: ESLint, Prettier y Stylelint configurados.
- AC2: Commits fallan si hay errores de lint.

## Escenarios
- Dado que el repositorio está inicializado
  Cuando se realiza un commit con errores de lint
  Entonces el commit falla y se muestra el error correspondiente

- Dado que el equipo desarrolla nuevas funcionalidades
  Cuando se ejecuta el pipeline de CI
  Entonces se verifica que ESLint, Prettier y Stylelint están configurados y no hay errores