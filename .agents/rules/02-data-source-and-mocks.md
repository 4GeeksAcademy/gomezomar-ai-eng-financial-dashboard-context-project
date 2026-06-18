# Regla: Aislamiento de datos mock y fuente de datos

## Nombre claro
Datos mock encapsulados detras de proveedor o repositorio

## Alcance
- Aplica a backend/app/*.py
- Aplica a cualquier futura integracion con base de datos, archivos CSV o servicios externos
- Aplica a tests que dependan de movimientos financieros

## Regla
- Los datos mock no deben quedar acoplados directamente a los endpoints finales.
- Toda fuente de datos debe exponerse a traves de una interfaz simple de proveedor o repositorio.
- El cambio de mock a persistencia real no debe requerir reescribir la logica de negocio.
- Las pruebas deben poder fijar una fuente deterministica sin modificar handlers HTTP.

## Razon / Justificacion
Hoy el backend genera movimientos en memoria con una seed fija. Eso sirve para prototipado y testing, pero bloquea la evolucion hacia persistencia real y mezcla infraestructura con dominio.

## Criterios verificables
- Un endpoint nuevo no llama directamente a un generador mock si ese acceso puede inyectarse desde una capa de datos.
- La logica de filtrado y agregacion funciona igual recibiendo listas mock o datos de una fuente real.
- La migracion a base de datos queda contenida en una capa de acceso a datos.
