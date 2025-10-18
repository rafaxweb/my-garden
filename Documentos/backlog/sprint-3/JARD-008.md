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

- Dado que el usuario mueve una planta existente
  Cuando la arrastra a una nueva posición
  Entonces la planta se reubica y la posición se actualiza en el almacenamiento local