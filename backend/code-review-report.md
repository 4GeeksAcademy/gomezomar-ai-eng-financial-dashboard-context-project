# Code Review Report

## Resumen Ejecutivo
El proyecto presenta una base sólida para un dashboard financiero de alcance académico o de prototipado: la separación Frontend/Backend es clara, existen contratos tipados, el backend expone endpoints útiles para análisis y ya hay pruebas automáticas relevantes. Sin embargo, el sistema todavía conserva decisiones propias de una fase temprana que serían riesgosas en un entorno productivo: datos simulados en memoria, configuración insegura por defecto, duplicación de lógica analítica entre capas y cobertura de pruebas aún incompleta en escenarios negativos y operativos.

## Hallazgos por Categoría

### Arquitectura

#### Buenas prácticas implementadas
- Separación clara de responsabilidades entre interfaz y API. El frontend consume datos y renderiza visualizaciones, mientras que el backend centraliza los endpoints y el procesamiento de movimientos financieros.
- El backend encapsula lógica de dominio en funciones puras y reutilizables como generación, filtrado, agregación, comparación y detección de alertas, lo que mejora mantenibilidad y testabilidad.
- La presencia de endpoints analíticos especializados como summary, top categories, comparison y alerts muestra una orientación correcta hacia una API con capacidades de reporting más allá del CRUD.

#### Malas prácticas o riesgos potenciales
- La fuente de datos sigue siendo completamente mock y en memoria. Esto limita trazabilidad, persistencia, concurrencia real y validación contra escenarios productivos.
- Existe duplicación de comportamiento en los endpoints segmentados B2B y B2C, que repiten la misma estructura de filtrado y ordenamiento en lugar de reutilizar una abstracción común.
- Parte de la lógica analítica relevante se calcula en el frontend a partir del endpoint base, aun cuando el backend ya ofrece endpoints agregados. Esto aumenta riesgo de divergencia funcional entre capas.

### Naming y Consistencia

#### Buenas prácticas implementadas
- Los nombres de modelos y tipos principales son semánticamente correctos y comunican bien la intención del dominio, por ejemplo FinancialMovement, MetricsSummaryItem, MetricsComparison y MetricsAlert.
- El uso de alias de importación en frontend mejora legibilidad y reduce fragilidad de rutas relativas largas.

#### Malas prácticas o riesgos potenciales
- Hay mezcla de idioma en el producto: el código y labels principales están en inglés, mientras algunos mensajes de error al usuario están en español. Esto dificulta consistencia de UX, documentación y colaboración.
- Se observan decisiones de nomenclatura con ambigüedad de contexto, por ejemplo outcome frente a expense. Aunque es consistente internamente, puede generar fricción si el dominio del negocio usa otro vocabulario financiero.

### Testing

#### Buenas prácticas implementadas
- El backend cuenta con pruebas automatizadas para rutas relevantes, filtros, facetas, resúmenes, comparación y alertas, lo que cubre el comportamiento principal de la API.
- La generación determinística con seed fija favorece repetibilidad en pruebas y evita flaky tests por aleatoriedad no controlada.
- El frontend incluye pruebas unitarias para utilidades puras de cálculo y formateo, lo que protege el núcleo analítico de la UI.

#### Malas prácticas o riesgos potenciales
- Falta cobertura de escenarios negativos y de borde: fechas inválidas, rangos invertidos, respuestas vacías, errores de red, inputs fuera de catálogo y validaciones semánticas del negocio.
- No hay pruebas de integración frontend-backend ni validación end-to-end del flujo principal del dashboard.
- El frontend no parece tener pruebas sobre componentes críticos de visualización, estados de loading y manejo de errores.

### Seguridad

#### Buenas prácticas implementadas
- El uso de tipado estricto con Pydantic, Literal y restricciones de Query reduce parte del riesgo de entradas inválidas y endurece el contrato de la API.
- El límite parametrizado en endpoints como top categories evita solicitudes excesivas triviales sobre ese recurso.

#### Malas prácticas o riesgos potenciales
- La configuración CORS actual permite cualquier origen con credenciales habilitadas. Esa combinación es riesgosa y no debería usarse fuera de desarrollo controlado.
- El contenedor backend expone debugpy y ejecuta uvicorn con reload por defecto, lo que amplía superficie de ataque y promueve una configuración de desarrollo como si fuera operativa.
- No existe autenticación, autorización, rate limiting ni separación por entornos para la configuración sensible.

### DX y Operación

#### Buenas prácticas implementadas
- Docker Compose simplifica el levantamiento del entorno local y reduce fricción de onboarding.
- El proxy de Vite hacia el backend evita configuración manual innecesaria durante desarrollo y hace más simple el consumo relativo de la API.
- El frontend contempla estados básicos de loading y error, lo que mejora la experiencia de desarrollo y depuración inicial.

#### Malas prácticas o riesgos potenciales
- La gestión de errores en frontend pierde contexto operativo: el catch reemplaza cualquier causa por un mensaje genérico, dificultando diagnóstico.
- No hay una capa explícita de servicios o cliente API en frontend; el fetch está acoplado al componente raíz, lo que complica escalabilidad y pruebas.
- No se evidencia una estrategia de configuración por entorno para diferenciar desarrollo, testing y producción de forma robusta.

### Documentación

#### Buenas prácticas implementadas
- El README explica propósito, forma de ejecución local y puertos principales, lo que es suficiente para arrancar el proyecto rápidamente.

#### Malas prácticas o riesgos potenciales
- Falta documentación técnica de decisiones arquitectónicas, modelo de datos, estrategia de testing, convenciones de naming y políticas de seguridad.
- No se documenta claramente qué endpoints ya están disponibles pero aún no están integrados en la UI, lo que puede ocultar capacidad existente del backend.

## Consolidado de Buenas Prácticas Identificadas
- Separación clara entre frontend y backend.
- Lógica de dominio extraída en funciones reutilizables y testeables.
- Contratos tipados con Pydantic, TypeScript y Literals.
- Validaciones básicas en parámetros de API con Query.
- Pruebas automatizadas en backend y utilidades frontend.
- Datos determinísticos para pruebas reproducibles.
- Entorno local consistente con Docker Compose y proxy de Vite.

## Consolidado de Riesgos y Malas Prácticas
- Dependencia de datos mock sin persistencia real.
- Configuración CORS permisiva con credenciales.
- Exposición de debugpy y reload como configuración por defecto del contenedor.
- Duplicación de endpoints B2B y B2C.
- Duplicación de lógica analítica entre backend y frontend.
- Cobertura de pruebas insuficiente en escenarios negativos, integración y UI.
- Manejo de errores frontend con poca observabilidad.
- Ausencia de autenticación y controles operativos básicos.
- Inconsistencias de idioma y terminología.
- Documentación técnica insuficiente para evolución del sistema.

## Reglas y Lineamientos Propuestos

### 1. Arquitectura
- Toda lógica de negocio reusable debe vivir en servicios o funciones puras del backend; el frontend debe limitarse a presentación, composición y adaptación de datos.
- No se deben crear endpoints segmentados por variante de negocio si el mismo resultado puede obtenerse con filtros parametrizados.
- Los datos mock solo pueden existir detrás de una interfaz de repositorio o proveedor; nunca deben quedar acoplados a los handlers finales.

### 2. Seguridad
- CORS debe configurarse por entorno y con allow_origins explícitos; no se permite allow_origins universal junto con credenciales fuera de desarrollo local.
- Herramientas de depuración como debugpy y flags como reload deben quedar deshabilitadas por defecto fuera del perfil de desarrollo.
- Todo endpoint no público debe contemplar autenticación, autorización y límites de consumo.

### 3. Testing
- Cada endpoint nuevo debe incorporar pruebas de camino feliz, validación de inputs, escenarios vacíos y errores esperados.
- Toda funcionalidad crítica visible en UI debe tener al menos pruebas de render, loading, error y comportamiento con datos vacíos.
- Debe existir al menos un flujo de integración o end-to-end que valide la experiencia principal del dashboard.

### 4. Naming y Consistencia
- El idioma del producto debe definirse una sola vez para código visible al usuario, labels, mensajes y documentación funcional.
- Los términos del dominio financiero deben alinearse con un glosario compartido; si se usa outcome, debe documentarse y mantenerse consistente en todo el sistema.

### 5. DX y Operación
- El acceso a la API en frontend debe pasar por una capa de cliente o servicios desacoplada de los componentes.
- Los errores deben registrar causa técnica y presentar mensajes de usuario diferenciados según el tipo de fallo.
- La configuración por entorno debe centralizarse y documentarse para desarrollo, test y producción.

### 6. Documentación
- Cada capacidad relevante del backend debe reflejarse en documentación funcional o técnica, especialmente si aún no está integrada en frontend.
- Las decisiones arquitectónicas no triviales deben registrarse en documentos breves de decisión o en una sección técnica del repositorio.

## Prioridades Recomendadas
1. Reemplazar la configuración insegura por defaults separados para desarrollo y producción.
2. Introducir una capa de persistencia o, como mínimo, una abstracción de repositorio para desacoplar los datos mock.
3. Consolidar la lógica analítica en backend y consumir endpoints agregados desde frontend.
4. Ampliar la cobertura de pruebas hacia integración, errores y componentes UI.
5. Formalizar convenciones de nomenclatura, idioma y configuración operativa.
