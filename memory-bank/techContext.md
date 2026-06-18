# Tech Context

## Frontend
- Framework principal: React 19 con TypeScript.
- Build y servidor de desarrollo: Vite 8.
- Estilos: Tailwind CSS v4 con plugin de Vite.
- Visualizacion: Recharts para graficas de linea y series temporales.
- UI auxiliar: lucide-react para iconos, class-variance-authority, clsx y tailwind-merge para composicion de estilos.
- Testing frontend: Vitest con cobertura V8.
- Linting frontend: ESLint 9 + typescript-eslint + plugins de React hooks/refresh.

## Backend
- Lenguaje: Python 3.13.
- Framework servidor: FastAPI.
- Servidor ASGI: uvicorn standard.
- Validacion y contratos: Pydantic BaseModel + tipos Literal para campos de dominio.
- Endpoints implementados:
  - /health
  - /api/metrics
  - /api/metrics/facets
  - /api/metrics/summary
  - /api/metrics/categories/top
  - /api/metrics/comparison
  - /api/metrics/alerts
  - /api/metrics/b2b
  - /api/metrics/b2c
- Base de datos: no hay base de datos configurada en el repositorio actual.

## Infraestructura / Tooling
- Orquestacion local: Docker Compose con servicios frontend y backend.
- Contenedor frontend: Node 24 Alpine, comando npm run dev con host 0.0.0.0.
- Contenedor backend: Python 3.13 slim, ejecucion con debugpy + uvicorn --reload.
- Puertos:
  - Frontend: 5173
  - Backend API: 8000
  - Debug backend: 5678
- Proxy de integracion local: Vite redirige /api a http://backend:8000.

## Dependencias clave

### frontend/package.json
- react, react-dom
- recharts
- tailwindcss, @tailwindcss/vite, postcss, autoprefixer
- vite, @vitejs/plugin-react
- typescript
- eslint, @eslint/js, typescript-eslint
- vitest, @vitest/coverage-v8
- lucide-react, class-variance-authority, clsx, tailwind-merge

### backend/requirements.txt
- fastapi
- uvicorn[standard]
- debugpy
- pytest
- pytest-cov
- httpx

## Evidencia del repositorio
- Dependencias frontend: frontend/package.json
- Dependencias backend: backend/requirements.txt
- Configuracion Vite y proxy: frontend/vite.config.ts
- Contenedores: frontend/Dockerfile, backend/Dockerfile
- Orquestacion: docker-compose.yml
- API y modelos: backend/app/main.py, backend/app/routes.py
