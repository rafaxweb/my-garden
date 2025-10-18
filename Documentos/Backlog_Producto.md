# Backlog del proyecto **JARD**

**Proyecto:** Mi Huerto Digital  
**Código del proyecto:** JARD  
**Fecha:** 16/10/2025

Este documento contiene el backlog del proyecto, estructurado por tickets individuales siguiendo el formato solicitado por el Product Owner.

---

# Sprint 0 – Infraestructura técnica

## JARD-001 - Configuración del monorepo

*(Infraestructura del proyecto, configuración inicial del repositorio y herramientas.)*

### Story
Como desarrollador, 
quiero tener un entorno configurado con Angular, .NET y Nx, 
para mantener una estructura limpia y modular.

### Criterios de aceptación
- AC1: Proyecto Angular 18 y .NET 9 inicializados.
- AC2: CI/CD activo en GitHub Actions.

### Escenarios
*(Los escenarios pertinentes)*

---

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
*(Los escenarios pertinentes)*

---

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
*(Los escenarios pertinentes)*

---

## Sprint 1 – Lienzo de diseño del huerto

# JARD-004 - Lienzo editable

*(Interfaz de diseño visual.)*

## Story
Como usuario, 
quiero un espacio visual donde añadir elementos (macetas, áreas) 
para diseñar mi huerto.

## Criterios de aceptación
- AC1: Puedo añadir y mover elementos con drag & drop.
- AC2: Los cambios se guardan localmente.

## Escenarios
- Dado que el usuario accede al lienzo
	Cuando añade una maceta o área
	Entonces el elemento aparece en el lienzo y puede moverse con drag & drop
- Dado que el usuario realiza cambios en el diseño
	Cuando guarda o sale de la app
	Entonces los cambios se guardan localmente
*(Los escenarios pertinentes)*

---

# JARD-005 - Persistencia local

*(Almacenamiento de datos del usuario.)*

## Story
Como usuario, 
quiero que mis diseños se guarden automáticamente.

## Criterios de aceptación
- AC1: Datos guardados en IndexedDB.
- AC2: Persisten tras cerrar la app.

## Escenarios
- Dado que el usuario diseña su huerto
	Cuando realiza cambios
	Entonces los datos se guardan automáticamente en IndexedDB
- Dado que el usuario cierra y vuelve a abrir la app
	Cuando accede al lienzo
	Entonces recupera su diseño anterior
*(Los escenarios pertinentes)*

---

## Sprint 2 – Catálogo de plantas

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
*(Los escenarios pertinentes)*

---

# JARD-007 - Visualización del catálogo

*(Navegación y filtrado del catálogo.)*

## Story
Como usuario, 
quiero navegar por el catálogo de plantas.

## Criterios de aceptación
- AC1: Lista de plantas con imágenes e información básica.
- AC2: Filtrado por tipo de planta.

## Escenarios
- Dado que el usuario accede al catálogo
	Cuando navega por la lista
	Entonces ve imágenes e información básica de cada planta
- Dado que el usuario utiliza el filtro
	Cuando selecciona un tipo de planta
	Entonces la lista se actualiza mostrando solo las plantas del tipo seleccionado
*(Los escenarios pertinentes)*

---

## Sprint 3 – Interacción y detalles

# JARD-008 - Arrastrar planta al huerto

*(Interacción drag & drop desde catálogo al lienzo.)*

## Story
Como usuario, 
quiero arrastrar una planta desde el catálogo hasta el huerto.

## Criterios de aceptación
- AC1: Drag & drop fluido.
- AC2: Posición guardada localmente.

## Escenarios
- Dado que el usuario ve el catálogo y el lienzo
	Cuando arrastra una planta al huerto
	Entonces la planta aparece en la posición seleccionada y se guarda localmente
*(Los escenarios pertinentes)*

---

# JARD-009 - Ver información de planta

*(Mostrar ficha de cuidados.)*

## Story
Como usuario, 
quiero abrir una ficha con los cuidados de una planta.

## Criterios de aceptación
- AC1: Al hacer clic en la planta se abre su ficha.
- AC2: La información se muestra correctamente offline.

## Escenarios
- Dado que el usuario ve una planta en el huerto o catálogo
	Cuando hace clic en la planta
	Entonces se abre la ficha con los cuidados y la información está disponible offline
*(Los escenarios pertinentes)*

---

## Sprint 4 – Refinamiento y QA

# JARD-010 - Testing e2e

*(Pruebas end‑to‑end del flujo completo.)*

## Story
Como QA, 
quiero ejecutar pruebas completas de usuario final.

## Criterios de aceptación
- AC1: Flujo “crear huerto → añadir planta → ver ficha” pasa todas las pruebas.

## Escenarios
- Dado que el QA ejecuta el flujo completo
	Cuando crea un huerto, añade una planta y consulta la ficha
	Entonces todas las pruebas pasan en el pipeline e2e
*(Los escenarios pertinentes)*

---

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
*(Los escenarios pertinentes)*

---

# JARD-012 - Preparar estructura para sincronización futura

*(Preparación de arquitectura para futura sincronización.)*

## Story
Como desarrollador, 
quiero interfaces listas para añadir sincronización en la siguiente fase.

## Criterios de aceptación
- AC1: SyncRepository implementado como stub.
- AC2: Arquitectura preparada sin romper compatibilidad.

## Escenarios
- Dado que el equipo prepara la arquitectura
	Cuando se implementa el stub de SyncRepository
	Entonces la app está lista para añadir sincronización en el futuro sin romper compatibilidad
*(Los escenarios pertinentes)*

