# Regla: Seguridad minima y modos de ejecucion

## Nombre claro
Configuracion segura por entorno

## Alcance
- Aplica a backend/app/main.py
- Aplica a backend/Dockerfile, docker-compose.yml y configuracion de entorno
- Aplica a cualquier endpoint nuevo expuesto fuera del entorno local

## Regla
- CORS debe declararse por entorno y con origins explicitos; no se permite allow_origins universal junto con credenciales en configuraciones no locales.
- Debugpy, reload automatico y otras facilidades de desarrollo deben activarse solo en modo desarrollo.
- Toda capacidad no publica debe definir desde el inicio su estrategia de autenticacion, autorizacion y limitacion de consumo, aunque se implemente en una fase posterior documentada.

## Razon / Justificacion
La configuracion actual del backend esta orientada a desarrollo y seria riesgosa si se promoviera sin cambios a un entorno compartido o productivo.

## Criterios verificables
- Existe una separacion visible entre configuracion de desarrollo y configuracion no local.
- El contenedor o comando de produccion no expone debugpy ni ejecuta reload.
- Ningun cambio de API introduce nuevos accesos sin documentar su nivel de proteccion.
