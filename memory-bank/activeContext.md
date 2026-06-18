# Active Context

## Estado actual del desarrollo
Snapshot tecnico del repositorio al momento actual, basado en codigo y configuracion presentes.

## Features implementadas y funcionales
- Backend FastAPI operativo con endpoint de salud y ocho endpoints de metricas/analitica.
- Modelado tipado de dominio financiero con validacion de parametros en query strings.
- Generacion de datos mock deterministica para pruebas y ejecucion local repetible.
- Dashboard frontend con:
  - Encabezado de vista ejecutiva
  - KPIs de ingreso, egreso, utilidad y margen
  - Grafica de ingresos vs egresos
  - Grafica de margen porcentual
  - Estados de loading y error en la vista principal
- Integracion local frontend-backend via proxy /api de Vite.
- Suite de pruebas backend para rutas principales y filtros.
- Suite de pruebas frontend para utilidades financieras.
- Reglas de repositorio creadas en .agents/rules.

## Gaps conocidos observables
- Persistencia de datos no implementada: no hay capa de base de datos.
- Configuracion de CORS altamente permisiva con allow_origins=* y credenciales activas.
- Configuracion de backend orientada a desarrollo en Docker (debugpy expuesto y --reload).
- El frontend consume de forma directa solo /api/metrics; endpoints analiticos adicionales no estan integrados en UI.
- No se observan pruebas de componentes frontend ni pruebas end-to-end de flujo completo.
- El manejo de errores en frontend es generico y no expone detalle tecnico por tipo de fallo.

## Siguientes prioridades logicas
1. Introducir una capa de datos desacoplada para preparar migracion de mock a persistencia real.
2. Incorporar en frontend los endpoints analiticos ya disponibles facets, summary, top, comparison y alerts.
3. Endurecer configuracion por entorno seguridad/runtime CORS, debugpy y modo de arranque.
4. Crear una capa de cliente API en frontend para centralizar fetch, mapping de errores y reutilizacion.
5. Aumentar cobertura con pruebas de componentes UI y al menos un flujo de integracion o E2E.
6. Mantener sincronizado README y documentacion tecnica con la capacidad backend efectiva.

## Evidencia del repositorio
- API y logica de dominio: backend/app/routes.py
- Configuracion de app y CORS: backend/app/main.py
- Dashboard y consumo API actual: frontend/src/App.tsx
- Calculos frontend: frontend/src/lib/financial-utils.ts
- Pruebas backend: backend/tests/test_routes.py
- Pruebas frontend presentes: frontend/src/lib/financial-utils.test.ts
- Infra local: docker-compose.yml, backend/Dockerfile, frontend/Dockerfile
- Reglas actuales del repositorio: .agents/rules/RULES.md
