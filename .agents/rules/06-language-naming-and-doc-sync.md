# Regla: Consistencia de idioma, nomenclatura y documentacion

## Nombre claro
Lenguaje uniforme y documentacion sincronizada con la capacidad real

## Alcance
- Aplica a frontend/src/**, backend/app/**, README*, .agents/rules/** y documentos tecnicos
- Aplica a labels, mensajes de error, nombres funcionales y descripcion de endpoints

## Regla
- El lenguaje visible al usuario debe mantenerse consistente dentro de una misma experiencia; no mezclar ingles y espanol sin una decision explicita de producto.
- Los terminos del dominio financiero deben seguir un glosario estable. Si se usa outcome como termino oficial, debe sostenerse en API, UI y documentacion.
- Todo endpoint o capacidad backend nueva debe reflejarse en la documentacion si modifica el alcance funcional del dashboard.
- Si una capacidad existe en backend pero aun no esta integrada en frontend, debe quedar documentada como disponible pero no expuesta en UI.

## Razon / Justificacion
El repositorio mezcla idiomas en mensajes y no documenta claramente toda la capacidad analitica ya disponible. Eso genera friccion de mantenimiento y oculta funcionalidades aprovechables.

## Criterios verificables
- Un mismo flujo de UI no alterna idiomas sin una razon definida.
- Los nombres funcionales en codigo y documentacion no cambian entre income, revenue, outcome o expense de forma arbitraria.
- README o documentacion tecnica reflejan los endpoints y capacidades reales del backend cuando estas cambian.
