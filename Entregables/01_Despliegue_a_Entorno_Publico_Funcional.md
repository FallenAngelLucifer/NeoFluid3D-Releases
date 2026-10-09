# Entregable 1: Despliegue a Entorno Público Funcional

Proyecto: NeoFluid3D — Motor de Simulación Hidrodinámica Computacional y Reconstrucción Volumétrica  
Versión de Entrega: v0.2.0-alpha (Versión de Acceso Controlado)  
Plataforma: Sistemas de 64 bits (Linux y Windows)  

---

## 1. Declaración de Homologación de Criterios

La rúbrica general de desarrollo solicita la publicación de la solución en una URL pública remota accesible o mediante un compilado instalable funcional conectado a una base de datos persistida fuera de localhost.

### 1.1 Adaptación del Entregable a la Naturaleza del Proyecto
El software NeoFluid3D es un motor de simulación de fluidos tridimensionales de alto rendimiento que ejecuta cálculos matemáticos masivamente paralelos en la tarjeta gráfica del equipo. Por sus requerimientos de cálculo y memoria, no es técnicamente viable desarrollarlo como una página web ordinaria ni como una aplicación para teléfonos celulares, ya que estos entornos carecen de la potencia térmica y el ancho de banda necesarios para procesar simulaciones de fluidos a gran escala.

Por esta razón, la entrega se homologa mediante un paquete ejecutable autónomo para computadoras de escritorio. Este paquete incluye el programa compilado, los módulos de cálculo para la tarjeta de video y las configuraciones de prueba, permitiendo que cualquier persona pueda ejecutarlo sin necesidad de instalar entornos de desarrollo adicionales.

Respecto a la persistencia en base de datos, en la simulación de fluidos no se almacenan registros tradicionales de usuarios o contraseñas, sino el estado físico de millones de partículas en movimiento (posiciones, presiones y velocidades). El sistema persiste esta información fuera del programa mediante formatos estándar de la industria científica (archivos VTK y ParaView), los cuales quedan listos para su almacenamiento en repositorios remotos y servicios en la nube.

Adicionalmente, debido a que el simulador se encuentra en una etapa temprana de ajuste y refinamiento físico, se distribuye bajo una versión de acceso controlado (versión alfa). Esto previene que usuarios generales intenten ejecutarlo en equipos incompatibles y protege el trabajo técnico en desarrollo.

---

## 2. Artefacto Distribuible y Contenido del Paquete

El paquete comprimido generado contiene todos los elementos indispensables para ejecutar la simulación y las pruebas de verificación de manera independiente. En la Tabla 1 se describe el propósito de cada uno de los componentes incluidos en la carpeta de distribución.

| Componente del Paquete | Contenido | Función en la Entrega |
|---|---|---|
| NeoFluid3D | Programa interactivo principal | Muestra la ventana tridimensional con la simulación de fluidos en tiempo real. |
| NeoFluidValidation | Programa de pruebas formales | Ejecuta de forma automática los experimentos canónicos de física y genera el reporte. |
| Shaders | Archivos de cómputo para la GPU | Contiene las instrucciones que resuelven las ecuaciones de fluidos directamente en la tarjeta gráfica. |
| Config | Archivos de configuración | Permite ajustar propiedades físicas como la densidad del agua y la viscosidad del líquido. |
| Models | Modelos geométricos tridimensionales | Mallas poligonales como recipientes y copas donde el líquido colisiona. |
| Reports | Informe de validación en HTML | Documento visual que resume el resultado y precisión de las pruebas realizadas. |
| Scripts de lanzamiento | Archivos ejecutables de inicio | Facilitan iniciar la simulación o las pruebas con un solo clic en la máquina destino. |

*Nota.* Componentes y archivos que conforman el paquete de entrega autónomo de NeoFluid3D.

---

## 3. Persistencia de Datos Fuera del Entorno Local

Para asegurar que los resultados de las simulaciones no se pierdan al cerrar el programa, NeoFluid3D implementa un sistema de exportación desacoplado que escribe los datos en formatos abiertos de ingeniería. En la Tabla 2 se presentan los tipos de datos generados y su destino.

| Nivel de Información | Formato de Archivo | Propósito y Destino de los Datos |
|---|---|---|
| Partículas del fluido | Archivos VTK PolyData (.vtp) | Guarda las posiciones, presiones y velocidades de las partículas para su apertura en software especializado. |
| Serie temporal completa | Colecciones ParaView (.pvd) | Permite reproducir toda la animación del agua como un video interactivo en herramientas científicas. |
| Superficie del agua | Mallas poligonales (.obj) | Extrae la forma visual del fluido como una superficie 3D compatible con programas de modelado. |
| Auditoría de precisión | Informe de validación (.html) | Documento interactivo con curvas analíticas que evidencia el margen de error del simulador. |
| Respaldo remoto | Repositorio y nube | Almacenamiento del paquete distribuible comprimido y los archivos generados en almacenamiento en la nube. |

*Nota.* Estructura de almacenamiento y persistencia de resultados generados por el simulador.

---

## 4. Instrucciones Sencillas para Comprobar el Despliegue

Para facilitar la revisión por parte del evaluador, el proceso de despliegue se ha preparado de modo que no requiera configuraciones complejas en el equipo de destino:

1. Descargar el archivo comprimido del release (`NeoFluid3D-v0.2.0-alpha-linux-x64.tar.gz`) desde el enlace de entrega.
2. Descomprimir el archivo en una carpeta local de la computadora.
3. Ejecutar el archivo lanzador interactivo (`./run_interactive.sh`) para observar el simulador en funcionamiento, o el archivo de pruebas (`./run_validation.sh`) para verificar los cálculos de física.
4. El programa se ejecutará de forma limpia sin solicitar privilegios administrativos ni modificar archivos del sistema operativo.
