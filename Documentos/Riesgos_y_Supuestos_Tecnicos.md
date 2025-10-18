# Riesgos y Supuestos Técnicos

Fecha: 16/10/2025
Proyecto: Mi Huerto Digital

## Objetivo

Documento complementario que recoge los principales riesgos técnicos identificados durante el kickoff y los supuestos técnicos que definen las condiciones de diseño del MVP. Este documento es una referencia para decisiones de arquitectura, planificación de sprints y estimación de mitigaciones.

---

## 1. Supuestos técnicos clave

1. Infraestructura y tecnologías
   - El frontend se desarrollará con Angular 18 y se desplegará como PWA.
   - El backend se implementará con .NET 9 (API REST) y PostgreSQL para el catálogo de plantas.
   - El repositorio será monorepo (Nx o similar) para facilitar la modularización.

2. Persistencia y datos
   - Todos los datos del usuario (diseños, posiciones, metadatos) serán almacenados localmente usando IndexedDB.
   - El catálogo de plantas se descargará desde el backend en el primer arranque y se cacheará localmente con un campo `catalog_version`.

3. Offline-first
   - La aplicación debe funcionar completamente sin conexión después de la carga inicial.
   - Todas las operaciones UI deben ser validas en modo offline y rehidratables en memoria/IndexedDB.

4. Seguridad y despliegue
   - El entorno de producción utilizará HTTPS y las imágenes/recursos estáticos estarán servidos desde CDN seguras.
   - No se implementa autenticación en MVP (datos locales). La arquitectura debe permitir añadirla posteriormente.

5. Testing y QA
   - Se adoptan Jest (frontend), Cypress (e2e) y NUnit (backend) para pruebas automatizadas.
   - CI/CD será gestionado con GitHub Actions y contendrá pasos de lint, tests y build.

---

## 2. Matriz de riesgos técnicos

Formato: ID | Riesgo | Probabilidad | Impacto | Severidad | Medida de mitigación / Contingencia

- RISK-001 | Pérdida de datos locales (IndexedDB corruption) | Media | Alto | Alto
  - Mitigación: Implementar versionado de esquema en IndexedDB (migrations) y backups periódicos en local (export JSON) como fallback. Añadir pruebas de integridad al cargar datos.

- RISK-002 | Problemas de rendimiento en canvas con muchos elementos | Alta | Medio | Alto
  - Mitigación: Optimizar renderizado usando canvas virtualizado o reducir re-renderizaciones; throttling/debouncing de eventos de arrastre; límites razonables por diseño MVP; pruebas de carga local.

- RISK-003 | Catálogo desactualizado o fallos en la carga inicial desde backend | Media | Medio | Medio
  - Mitigación: Implementar retry con backoff, fallback a un catálogo embarcado en la app y mostrar estado al usuario. Versionado de catálogo y checksum.

- RISK-004 | Incompatibilidades entre navegadores (IndexedDB/Service Worker) | Media | Medio | Medio
  - Mitigación: Definir lista de navegadores soportados; usar wrappers probados (`ngx-indexed-db`); añadir tests en navegadores objetivo.

- RISK-005 | Complejidad en la futura sincronización con backend | Baja | Alto | Medio
  - Mitigación: Diseñar interfaces `IDataRepository` desde inicio; almacenar operaciones (oplog) para replay; documentar conflictos esperados y estrategia de merge.

- RISK-006 | Fallos en pipeline CI/CD (deploy o builds rotos) | Media | Medio | Medio
  - Mitigación: Pipelines modulares, tests rápidos en PRs, caché de dependencias y alertas en fallos. Política de merge solo si pipeline pasa.

- RISK-007 | Vulnerabilidades en assets externos (CDN o imágenes) | Baja | Medio | Bajo
  - Mitigación: Firmar/sumarizar assets, servir desde CDN controlado o embebido en release si necesario.

- RISK-008 | Errores críticos en el backend que bloquean la descarga del catálogo | Baja | Alto | Medio
  - Mitigación: Health checks en backend, endpoint estático con versión, fallback a catálogo embarcado.

---

## 3. Evaluación de severidad y prioridades

- Prioridad inmediata: RISK-001, RISK-002, RISK-003. Estos afectan directamente la experiencia del usuario y la estabilidad del MVP.
- Media prioridad: RISK-004, RISK-006, RISK-008. Requieren pruebas y pipelines para reducir la superficie.
- Baja prioridad: RISK-005, RISK-007. Importantes para fases posteriores o mitigaciones menores.

---

## 4. Plan de mitigación y tareas recomendadas (rápidas)

1. Implementar migraciones y esquema versionado para IndexedDB (Tarea: Persistencia - Sprint 1).
2. Prototipar y perfilar el canvas con escenarios de 100-500 elementos (Tarea: Rendimiento - Sprint 1/2).
3. Incluir un catálogo embarcado mínimo en la app para fallback (Tarea: Backend - Sprint 0/1).
4. Añadir tests cross-browser en la matriz de CI (Tarea: QA - Sprint 0).
5. Definir la interfaz `IDataRepository` y un `SyncRepository` stub (Tarea: Arquitectura - Sprint 0).

---

## 5. Supuestos de pruebas y aceptación

- Los tests E2E cubrirán un flujo crítico: inicio, carga catálogo, crear huerto, arrastrar planta, ver ficha.
- Las pruebas unitarias cubrirán servicios críticos: persistencia, catálogo y renderización de componentes clave.

---

## 6. Monitoreo y métricas a capturar

- Tiempo de carga inicial (cold start) en ms.
- Tiempo de respuesta del canvas bajo carga (FPS o ms por frame).
- Número de elementos guardados por diseño promedio.
- Errores de sincronización/descarga del catálogo.

---

## 7. Notas finales

Este documento es deliberadamente conciso para integrarse en la carpeta `Documentos` como complemento de la documentación principal generada en el kickoff. Se recomienda revisarlo al final del Sprint 1 y actualizar según hallazgos de pruebas de rendimiento y feedback de QA.
