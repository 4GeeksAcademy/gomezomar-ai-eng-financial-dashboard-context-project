# Regla: Cobertura minima de pruebas

## Nombre claro
Pruebas obligatorias por tipo de cambio

## Alcance
- Aplica a backend/tests/*.py
- Aplica a frontend/src/**/*.test.ts y futuras pruebas de componentes
- Aplica a cambios en endpoints, utilidades financieras y UI critica del dashboard

## Regla
- Cada endpoint nuevo o modificado debe cubrir al menos: camino feliz, validacion de parametros, caso vacio y caso de error esperado.
- Toda utilidad financiera debe tener pruebas deterministicas para calculos y orden cronologico.
- Toda vista critica de frontend debe tener pruebas de loading, error, vacio y render con datos.
- Cuando un cambio conecte frontend y backend en una funcionalidad visible, debe existir al menos una prueba de integracion o end-to-end para ese flujo.

## Razon / Justificacion
El proyecto ya tiene una buena base de pruebas en backend y utilidades frontend, pero todavia faltan escenarios negativos, componentes UI e integracion entre capas.

## Criterios verificables
- No se acepta un endpoint nuevo sin pruebas de validacion de input.
- No se acepta un componente critico sin validar estados de loading y error.
- Los datos aleatorios usados en pruebas deben fijarse con seed o fixtures deterministicas.
