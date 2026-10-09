# Entregable 3: Documentación del Proceso de Despliegue

Proyecto: NeoFluid3D — Motor de Simulación Hidrodinámica Computacional y Reconstrucción Volumétrica  
Configuración: Compilación optimizada para computadoras de 64 bits  

---

## 1. Propósito y Enfoque del Despliegue

La rúbrica de desarrollo define este entregable como la redacción detallada de los pasos, comandos y configuraciones utilizados para desplegar la solución mientras el proceso se encuentra fresco.

En este proyecto, documentar el despliegue significa explicar claramente qué características debe tener una computadora para poder ejecutar el simulador y qué pasos se siguieron para transformar el código fuente en un paquete de instalación listo para ser utilizado por cualquier persona sin requerir herramientas de programación.

---

## 2. Requisitos de la Computadora para Ejecutar el Simulador

Para que la simulación en tiempo real funcione con fluidez y precisión, la computadora del usuario o evaluador debe cumplir con ciertas características de hardware y software, las cuales se detallan en la Tabla 1 y en la Tabla 2.

| Parte de la Computadora | Requisito Mínimo | Recomendación Óptima |
|---|---|---|
| Procesador (CPU) | Procesador de 64 bits con al menos 4 núcleos lógicos. | Procesador moderno de 8 núcleos para mayor rapidez al cargar archivos. |
| Memoria RAM | Al menos 8 GB de memoria RAM libre. | 16 GB de RAM para simulaciones grandes de cientos de miles de partículas. |
| Tarjeta Gráfica (GPU) | Tarjeta gráfica compatible con Vulkan 1.3 con al menos 2 GB de memoria dedicada. | Tarjeta gráfica de gama media o superior (NVIDIA, AMD o Intel) con 4 GB o más. |
| Espacio en Disco | 1 GB de espacio disponible en disco. | Unidad de estado sólido (SSD) para agilizar el guardado de datos. |

*Nota.* Requisitos de hardware recomendados para la ejecución fluida del simulador.

| Programa o Sistema | Versión Utilizada | Propósito en el Proyecto |
|---|---|---|
| Sistema Operativo | Linux de 64 bits o Windows 10/11 de 64 bits. | Sistemas operativos donde el simulador ha sido probado y verificado. |
| Compilador de C++ | GCC 11 o superior, Clang o Visual Studio 2022. | Traduce el código de programación a lenguaje de máquina de alto rendimiento. |
| Sistema CMake | Versión 3.20 o superior. | Automatiza y organiza los pasos de compilación en todas las plataformas. |
| Controladores de Video | Drivers oficiales vigentes del fabricante de la tarjeta gráfica. | Proporciona la compatibilidad necesaria con la biblioteca gráfica Vulkan 1.3. |

*Nota.* Entorno de software y herramientas empleadas para la construcción del sistema.

---

## 3. Pasos Seguidos para Construir el Paquete de Entrega

El proceso de preparación del software se estructuró en tres etapas sencillas y reproducibles:

### 3.1 Preparación de las Instrucciones de Video (Shaders)
El programa delega los cálculos físicos más pesados a la tarjeta gráfica. Para que la computadora entienda estas instrucciones sin demoras al abrir el programa, los archivos de cálculo se compilan de antemano a un formato optimizado. Este paso se realiza ejecutando el archivo de preparación:

`./compile_shaders.sh`

### 3.2 Compilación del Código Fuente
A continuación, el código fuente del simulador se compila en modo de alto rendimiento (modo Release). Esto activa las optimizaciones matemáticas del procesador para que el agua se mueva de forma fluida a 60 cuadros por segundo:

`cmake -B build -DCMAKE_BUILD_TYPE=Release`  
`cmake --build build --config Release`

### 3.3 Empaquetado Automático
Finalmente, para evitar que el evaluador tenga que compilar nada o instalar programas extra, un script reúne el ejecutable, los modelos 3D y las configuraciones en un único paquete comprimido:

`./scripts/package_release.sh`

Este comando genera el archivo final `NeoFluid3D-v0.2.0-alpha-linux-x64.tar.gz`.

---

## 4. Guía para el Evaluador: Cómo Ejecutar el Simulador en un Equipo Limpio

Cualquier persona que reciba el paquete comprimido puede ponerlo en marcha en tres pasos elementales:

1. Descomprimir el archivo descargado en cualquier carpeta de su preferencia.
2. Abrir la carpeta resultante `NeoFluid3D-v0.2.0-alpha`.
3. Hacer doble clic en el archivo `run_interactive.sh` para abrir la ventana 3D del simulador, o en `run_validation.sh` para correr las pruebas automáticas.

El programa comenzará a funcionar inmediatamente sin requerir permisos de administrador ni modificar la configuración del sistema operativo.
