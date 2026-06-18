# Product Context

## Proposito del producto
Este repositorio implementa un dashboard de metricas financieras con frontend en React + TypeScript y backend en FastAPI. El objetivo es visualizar indicadores clave de ingresos, egresos, utilidad y margen mediante una UI con tarjetas KPI y graficas.

## Problema que resuelve
Permite concentrar en una sola vista ejecutiva informacion financiera agregada para facilitar seguimiento y analisis de desempeno. La API expone datos de movimientos y vistas analiticas ya preparadas por periodo, categoria y tipo de negocio.

## Funcionamiento a nivel macro
1. El backend expone endpoints HTTP para salud, listado de movimientos y analitica financiera.
2. El frontend consume la API (actualmente el endpoint base de metricas) y calcula/representa KPIs y series mensuales.
3. En desarrollo local, Vite enruta solicitudes /api hacia el servicio backend via proxy.
4. Docker Compose levanta ambos servicios con puertos dedicados para frontend y backend.

## Limites actuales observables
- La fuente de datos es mock y deterministica en memoria seed=42, sin persistencia de base de datos.
- El dashboard frontend actual muestra una parte de la capacidad analitica ya disponible en backend.

## Evidencia del repositorio
- README general: README.md
- Endpoints y modelos de API: backend/app/routes.py
- App FastAPI y CORS: backend/app/main.py
- Consumo frontend y visualizacion: frontend/src/App.tsx
- Utilidades de KPI y agregacion mensual: frontend/src/lib/financial-utils.ts
- Proxy de desarrollo: frontend/vite.config.ts
- Orquestacion local: docker-compose.yml
