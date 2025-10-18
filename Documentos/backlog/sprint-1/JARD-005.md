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