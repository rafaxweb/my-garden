# JARD-001 - Configuración del monorepo

*(Infraestructura del proyecto, configuración inicial del repositorio y herramientas.)*

## Story
Como desarrollador, 
quiero tener un entorno configurado con Angular, .NET y Nx, 
para mantener una estructura limpia y modular.

## Criterios de aceptación
- AC1: Proyecto Angular 18 y .NET 9 inicializados.
- AC2: CI/CD activo en GitHub Actions.

## Escenarios
- Dado que el equipo inicia el proyecto
  Cuando se configura el monorepo con Nx
  Entonces se crean las estructuras para frontend y backend

- Dado que el monorepo está configurado
  Cuando se realiza un push a main
  Entonces el pipeline de CI/CD se ejecuta automáticamente