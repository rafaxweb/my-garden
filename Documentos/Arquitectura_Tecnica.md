# Arquitectura Técnica
Fecha: 16/10/2025
Proyecto: Mi Huerto Digital
## 1. Introducción

Este documento resume las decisiones de arquitectura para el MVP de "Mi Huerto Digital". Contiene el modelo de capas, componentes principales, decisiones tecnológicas, patrones adoptados, y consideraciones de despliegue y escalabilidad.
## 2. Visión general de la arquitectura

Arquitectura de referencia: Clean Architecture con separación clara entre UI, aplicación, dominio e infraestructura. El sistema está compuesto por:
- Frontend: Angular 18 como PWA (Progressive Web App), orientado a un diseño offline-first.
- Backend: API REST mínima escrita en .NET 9 con PostgreSQL para el catálogo de plantas.
- Persistencia local: IndexedDB (vía `ngx-indexed-db`) para todo dato de usuario.
La comunicación entre frontend y backend es asincrónica y sólo necesaria para la descarga inicial del catálogo de plantas.

## 3. Componentes y capas
### 3.1 Frontend (Angular 18)

- UI Layer (Components)
	- Canvas Editor: editor drag & drop para diseñar huertos (Angular CDK DragDrop)
	- Plant Catalog Viewer: lista y tarjetas de plantas
	- Plant Info Card: modal o drawer con ficha de cuidados
	- Toolbar / Menú: acciones globales, export, settings
- Application Layer
	- NgRx Store: estado global rehidratable desde IndexedDB
	- Services: PlantService, GardenService, PersistenceService
	- Command Handlers: para acciones complejas (undo/redo opcional)

- Data Layer
	- Repositories: PlantRepository, GardenLayoutRepository (implementación local)
	- IndexedDB Adapter: wrapper para migraciones y versionado

### 3.2 Backend (.NET 9)
- API Layer
	- Controllers: PlantCatalogController (/api/plants/catalog)

- Application Layer
	- Queries/Handlers: GetPlantCatalogQuery

- Domain
	- Entities: Plant (id, name, light, water, season, imageUrl, tags)
- Infrastructure
	- EF Core layer + PostgreSQL
	- DTO mapping (AutoMapper o manual)
## 4. Flujos críticos

1. Carga inicial del catálogo
	- Frontend solicita `/api/plants/catalog`.
	- Backend devuelve JSON con `catalog_version`.
	- Frontend guarda en IndexedDB y marca versión.
2. Guardado de diseño
	- Usuario arrastra elementos en canvas.
	- NgRx persiste estado en memoria y PersistenceService escribe en IndexedDB (debounced).
3. Modo offline
	- Service Worker y cache de recursos estáticos.
	- Todas las operaciones UI aplican sobre la copia local.
## 5. Decisiones de diseño relevantes

- Offline-first: priorizar que la app funcione sin conexión tras la carga inicial.
- Persistencia local mediante IndexedDB para evitar dependencia temprana del backend.
- Uso de NgRx para simplificar la rehidratación y time-travel debugging.
- Diseñar interfaces `IDataRepository` para facilitar futura sincronización con servidor.
## 6. Integridad de datos y migraciones

- Esquema versionado de IndexedDB con migraciones incrementales.
- Validaciones al cargar datos y estrategias de recuperación (rollback, import/export JSON).
## 7. Seguridad

- En producción usar HTTPS y CSP estricto.
- Validar y sanitizar cualquier URL o input desde el catálogo.
## 8. Escalabilidad y roadmap técnico

- MVP: backend mínimo, cache en cliente.
- Post-MVP: añadir sincronización bidireccional, autenticación, y multi-device.
## 9. Endpoints (propuesta mínima)

- GET /api/plants/catalog -> Devuelve catálogo de plantas y versión
- GET /api/plants/{id} -> Detalle extendido (opcional)
## 10. Observabilidad y métricas

- Métricas iniciales: tiempo de carga, FPS del canvas, errores de IndexedDB.
- Logging backend mínimo y health endpoints.
## 11. Notas finales

Revisar este documento al cierre del Sprint 1 y actualizar según hallazgos de performance y QA.
