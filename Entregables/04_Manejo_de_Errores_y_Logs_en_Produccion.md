# Entregable 4: Manejo de Errores y Logs en Producción

Proyecto: NeoFluid3D — Motor de Simulación Hidrodinámica Computacional y Reconstrucción Volumétrica  
Subsistema Evaluado: Sistema de Tolerancia a Fallos y Registro de Diagnóstico  

---

## 1. El Manejo de Errores en Aplicaciones Gráficas frente a Servicios Web

La rúbrica de desarrollo solicita comprobar que las peticiones erróneas o rutas inexistentes devuelvan respuestas controladas y no provoquen la caída del proceso, quedando el fallo registrado en la consola o panel de control del sistema.

En una página web, si el usuario busca una página que no existe, el servidor devuelve un mensaje de error 404 y continúa funcionando con normalidad. En una aplicación gráfica que interactúa directamente con la tarjeta de video, un error mal manejado (como que falte un archivo de simulación o que la tarjeta gráfica se quede sin memoria) puede congelar la pantalla de la computadora o hacer que el programa se cierre de forma repentina sin dejar explicación.

Para evitar esto, NeoFluid3D incorpora un sistema de protección y diagnóstico que detecta las anomalías a tiempo, evita cierres abruptos y registra detalladamente lo sucedido en un archivo de registro (log). En la Tabla 1 se explican los principales escenarios de fallo previstos y cómo responde el programa.

| Tipo de Situación o Fallo | Causa Posible | Cómo lo Detecta el Programa | Respuesta Controlada del Sistema |
|---|---|---|---|
| Tarjeta gráfica incompatible | La computadora no cuenta con los controladores necesarios de Vulkan. | Al iniciar, el programa consulta la versión de video disponible en el equipo. | Muestra un aviso explicativo en la terminal y se cierra de forma segura sin congelar la pantalla. |
| Memoria de video insuficiente | Se intentan simular demasiadas partículas para la memoria disponible. | El gestor de memoria monitorea el espacio libre antes de cada asignación. | Rechaza la creación de partículas adicionales y avisa al usuario en lugar de colapsar el sistema. |
| Archivo de cálculo ausente | Falta un archivo en la carpeta del programa o fue borrado por error. | Se comprueba la existencia física y la integridad de cada archivo antes de abrirlo. | Avisa exactamente qué archivo falta y detiene la carga con un código de salida controlado. |
| Parámetros físicos imposibles | El usuario configura números extremos que harían explotar el líquido. | El motor revisa que las velocidades y presiones no den valores infinitos o indefinidos. | Pausa temporalmente el avance del agua, guarda el último estado seguro y emite una advertencia. |

*Nota.* Mecanismos de protección del simulador ante posibles situaciones de error o incompatibilidad.

---

## 2. El Sistema de Diagnóstico y Registro de Logs

Para ofrecer una evidencia clara y accesible del estado de la computadora (el equivalente al panel de control de un servicio web), el proyecto incluye un programa de diagnóstico integral (`scripts/system_verification.py`).

Este programa realiza una auditoría completa de la computadora en menos de un segundo y guarda los resultados en un archivo ordenado llamado `system_verification_report.json`. En la Tabla 2 se presenta el resumen de los puntos comprobados por esta auditoría.

| Aspecto Auditado de la Computadora | Qué se Comprobó Exactamente | Resultado Obtenido | Estado |
|---|---|---|:---:|
| Procesador y Sistema Operativo | Que la computadora sea de 64 bits y cuente con suficientes núcleos de trabajo. | Sistema de 64 bits con 12 hilos de procesamiento detectados. | Aprobado |
| Memoria RAM Disponible | Que haya suficiente memoria para los buffers del líquido sin ralentizar el equipo. | Más de 14 GB de memoria física con más de 7 GB disponibles. | Aprobado |
| Soporte de Tarjeta Gráfica | Que el sistema cuente con la biblioteca de video Vulkan 1.3 o superior. | Controlador Vulkan 1.4 detectado y cargado correctamente. | Aprobado |
| Integridad de Archivos de Cálculo | Que todos los archivos de video cuenten con su formato y firma binaria correcta. | Dieciocho módulos de cálculo verificados sin alteraciones. | Aprobado |
| Modelos Tridimensionales | Que las mallas de recipientes y objetos no tengan polígonos rotos. | Objetos de prueba verificados con dimensiones coherentes. | Aprobado |
| Comunicación Interna de Telemetría | Que los canales locales de medición puedan enviar y recibir datos en milisegundos. | Comunicación local verificada en menos de un milisegundo. | Aprobado |

*Nota.* Resultados de la auditoría de diagnóstico del sistema ejecutada en el entorno de producción.

---

## 3. Comprobación Práctica para el Evaluador

El evaluador puede comprobar en cualquier momento el funcionamiento del sistema de diagnóstico ejecutando una única orden en la terminal:

`python3 scripts/system_verification.py`

En la pantalla aparecerá un listado claro de cada componente revisado con su correspondiente indicador verde de aprobación, y se actualizará automáticamente el informe `system_verification_report.json` en la carpeta raíz del proyecto, sirviendo como evidencia de que el software funciona de forma confiable y sin errores ocultos.
