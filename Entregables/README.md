# Paquete de Entregables de Desarrollo — NeoFluid3D

Este directorio contiene la documentación formal de los **4 entregables de desarrollo**, adaptados rigurosamente desde el modelo genérico de aplicaciones web hacia los estándares de ingeniería de software de alto rendimiento (HPC), simulación hidrodinámica computacional (SPH) y gráficos en tiempo real sobre Vulkan 1.3 y C++20.

---

## Índice de Entregables

| # | Documento (Word APA 7 / Markdown) | Criterio de la Rúbrica Adaptado | Evidencia Principal |
|:---:|---|---|---|
| **1** | [**01. Despliegue a Entorno Público**](file:///home/lucifer/proyectos/NeoFluid3D/Entregables/01_Despliegue_a_Entorno_Publico_Funcional.docx) ([.md](file:///home/lucifer/proyectos/NeoFluid3D/Entregables/01_Despliegue_a_Entorno_Publico_Funcional.md)) | Publicación de solución / Build instalable / Persistencia fuera de localhost | Artefacto distribuible autónomo (`.tar.gz`), shaders SPIR-V precompilados y persistencia en formatos industriales (.vtp, .pvd, .obj). |
| **2** | [**02. Validación Funcional**](file:///home/lucifer/proyectos/NeoFluid3D/Entregables/02_Validacion_Funcional_en_Entorno_Real.docx) ([.md](file:///home/lucifer/proyectos/NeoFluid3D/Entregables/02_Validacion_Funcional_en_Entorno_Real.md)) | Flujo principal de valor de inicio a fin registrado en persistencia | Validación física canónica de 5/5 experimentos de mecánica de fluidos (Dam Break, Euler Column, Poiseuille) y reporte interactivo `reports/validation.html`. |
| **3** | [**03. Documentación de Despliegue**](file:///home/lucifer/proyectos/NeoFluid3D/Entregables/03_Documentacion_del_Proceso_de_Despliegue.docx) ([.md](file:///home/lucifer/proyectos/NeoFluid3D/Entregables/03_Documentacion_del_Proceso_de_Despliegue.md)) | Pasos, comandos y configuración usados para desplegar | Runbook de ingeniería: pipeline de compilación SPIR-V, CMake Release, matriz de compatibilidad de GPU Vulkan 1.3 e instalación de cero impacto. |
| **4** | [**04. Manejo de Errores y Logs**](file:///home/lucifer/proyectos/NeoFluid3D/Entregables/04_Manejo_de_Errores_y_Logs_en_Produccion.docx) ([.md](file:///home/lucifer/proyectos/NeoFluid3D/Entregables/04_Manejo_de_Errores_y_Logs_en_Produccion.md)) | Peticiones erróneas/rutas inexistentes con respuesta controlada y logs | Resiliencia de hardware (Vulkan VMA), verificación binaria de shaders (magic number 0x07230203), guardias CFL y auditoría `system_verification_report.json`. |

---

## Resumen Ejecutivo de Homologación

* **Protección de Etapa Temprana:** Se distribuye bajo versión controlada `v0.2.0-alpha (Academic Research Preview)`. Se evitan URLs web abiertas o dependencias inestables de terceros, garantizando que los evaluadores interactúen con casos canónicos científicamente verificados.
* **Flujo de Valor Real:** La "transacción" del sistema corresponde a la simulación numérica hidrodinámica con doble bucle de presión (DFSPH) y conservación estricta de densidad, exportando datasets volumétricos compatibles con Kitware ParaView.
* **Cero Caídas Catastróficas:** El motor implementa guardias contra fallos de GPU, ausencia de shaders o divergencia física (NaNs/Infs), garantizando terminaciones limpias y diagnósticos legibles.
