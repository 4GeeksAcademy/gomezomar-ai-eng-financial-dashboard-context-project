# Reglas del Repositorio

Este directorio contiene reglas accionables y medibles derivadas del estado real del proyecto. Cada archivo define una expectativa concreta para desarrollo diario en frontend, backend, pruebas, seguridad y documentación.

## Indice

- [01-backend-domain-boundaries.md](01-backend-domain-boundaries.md): centraliza la logica de negocio en backend y evita duplicacion entre API y UI.
- [02-data-source-and-mocks.md](02-data-source-and-mocks.md): obliga a encapsular datos mock detras de una capa de proveedor o repositorio.
- [03-api-security-and-runtime-modes.md](03-api-security-and-runtime-modes.md): separa configuracion local de configuracion segura para entornos compartidos o productivos.
- [04-frontend-api-layer-and-errors.md](04-frontend-api-layer-and-errors.md): desacopla el acceso a API de los componentes y mejora el manejo de errores.
- [05-testing-requirements.md](05-testing-requirements.md): define la cobertura minima exigible por tipo de cambio.
- [06-language-naming-and-doc-sync.md](06-language-naming-and-doc-sync.md): mantiene consistencia de idioma, nomenclatura y documentación funcional.

## Criterio de uso

- Antes de modificar backend, revisar reglas 01, 02 y 03.
- Antes de modificar frontend, revisar reglas 04, 05 y 06.
- Antes de introducir una nueva capacidad funcional, revisar todas las reglas que afecten arquitectura, pruebas y documentación.
