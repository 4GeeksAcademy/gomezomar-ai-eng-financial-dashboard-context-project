# Resumen Ejecutivo y Técnico del Proyecto

## 1. Objetivo Principal
Este proyecto implementa un dashboard de métricas financieras para visualizar el desempeño del negocio (ingresos, egresos, utilidad y margen), con foco en análisis rápido para la toma de decisiones. Resuelve la necesidad de centralizar indicadores ejecutivos en una interfaz clara respaldada por una API.

## 2. Stack Tecnológico
- Frontend: React 19, TypeScript, Vite, Tailwind CSS v4, Recharts, Lucide React
- Backend: Python 3.13, FastAPI, Pydantic, Uvicorn
- Testing: Pytest (backend), Vitest (frontend)
- Infraestructura local: Docker y Docker Compose
- Base de datos: no hay persistencia implementada actualmente; se usan datos simulados en memoria

## 3. Arquitectura y Componentes Clave
- Arquitectura general: aplicación web de dos capas en monorepo (Frontend + Backend API)
- Frontend:
  - Dashboard con tarjetas KPI (ingresos, egresos, utilidad, margen)
  - Gráficas de evolución mensual (ingresos vs egresos, margen porcentual)
  - Cálculo de métricas en cliente a partir de los movimientos obtenidos por API
- Backend:
  - API REST con endpoints de métricas financieras
  - Generación de datos mock determinísticos (seed fija) para resultados reproducibles
  - Funciones de filtrado, agregación temporal, top categorías, comparación de periodos y alertas
- Integración:
  - Proxy de Vite para enrutar /api al backend en desarrollo local
  - Orquestación de servicios con Docker Compose

## 4. Estado Actual
Funcionalidades ya implementadas y operativas:
- API con endpoints para salud, métricas base, facetas, resumen por periodo, top categorías, comparación, alertas y segmentación B2B/B2C
- Dashboard frontend funcional con carga de datos, KPIs y dos gráficas principales
- Manejo básico de estados de carga y error en UI
- Pruebas automatizadas en backend y utilidades del frontend
- Entorno local reproducible con Docker

Observación:
- El frontend actual consume principalmente el endpoint base de métricas, mientras que el backend ya expone endpoints analíticos adicionales que aún no se explotan completamente en la UI.

## 5. Próximos Pasos / Pendientes
- Integrar en el frontend los endpoints analíticos avanzados (summary, facets, top categories, comparison, alerts)
- Incorporar persistencia real (base de datos) y separar claramente datos mock de datos productivos
- Estandarizar una capa de servicios en frontend para consumo API, manejo de errores y reintentos
- Ampliar cobertura con pruebas de integración end-to-end (frontend-backend)
- Definir lineamientos de despliegue y operación: variables de entorno, observabilidad y pipeline CI/CD
