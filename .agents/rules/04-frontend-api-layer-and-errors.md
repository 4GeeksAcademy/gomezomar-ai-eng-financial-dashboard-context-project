# Regla: Consumo de API y manejo de errores en frontend

## Nombre claro
Cliente API desacoplado de componentes

## Alcance
- Aplica a frontend/src/**/*.ts y frontend/src/**/*.tsx
- Aplica a fetch, transformaciones de respuesta, manejo de errores y estados de carga
- Aplica especialmente a App.tsx y futuros componentes de dashboard

## Regla
- Ningun componente de presentacion debe contener llamadas fetch directas si la misma API puede reutilizarse en otro punto de la UI.
- El acceso a backend debe centralizarse en una capa de cliente o servicios.
- Los errores deben conservar contexto tecnico para diagnostico y mapearse a mensajes de usuario consistentes.
- La UI debe distinguir entre loading, error, vacio y datos disponibles en funcionalidades visibles.

## Razon / Justificacion
Hoy el fetch al endpoint principal vive en el componente raiz y el catch reemplaza toda causa por un mensaje generico. Eso dificulta pruebas, reutilizacion y diagnostico cuando crezca el dashboard.

## Criterios verificables
- Los componentes renderizan datos recibidos por props o hooks, no construyen URLs de negocio ad hoc.
- La transformacion de errores conserva status o causa original en una capa reutilizable.
- Una nueva vista de dashboard no repite logica de carga o errores ya existente.
