# Regla: Limites de logica de dominio en backend

## Nombre claro
Logica de dominio centralizada en backend

## Alcance
- Aplica a backend/app/*.py
- Aplica a nuevos endpoints de metricas y transformaciones financieras
- Aplica a cualquier cambio que agregue calculos reutilizables para KPI, resumenes, comparaciones, alertas o segmentacion

## Regla
- Toda regla de negocio reutilizable debe implementarse en funciones puras o servicios del backend.
- Los handlers HTTP solo pueden validar parametros, orquestar dependencias y devolver respuestas.
- No se deben crear endpoints duplicados si el mismo comportamiento puede expresarse con filtros o parametros.
- Si una capacidad ya existe en backend como agregacion o comparacion, el frontend no debe reimplementar la misma logica salvo adaptacion de formato para UI.

## Razon / Justificacion
Esta regla evita la divergencia entre lo que calcula la API y lo que calcula la interfaz. En este repositorio ya existe logica analitica en backend y tambien calculos de KPI en frontend; si ambas capas evolucionan por separado, el dashboard puede mostrar resultados inconsistentes.

## Criterios verificables
- Un nuevo calculo financiero no aparece duplicado en backend y frontend con distinta implementacion.
- Los endpoints B2B o B2C nuevos se modelan como filtros antes que como rutas separadas.
- Los archivos de rutas no concentran bloques largos de transformacion de datos que puedan extraerse a funciones reutilizables.
