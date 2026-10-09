# Entregable 2: Validación Funcional en Entorno Real

Proyecto: NeoFluid3D — Motor de Simulación Hidrodinámica Computacional y Reconstrucción Volumétrica  
Módulo Evaluado: Módulo de Pruebas Físicas (NeoFluidValidation)  
Resultado Global: Cinco de cinco casos de prueba aprobados (100% de éxito)  

---

## 1. El Flujo Principal de Valor en un Simulador de Fluidos

La rúbrica de evaluación solicita verificar el funcionamiento del flujo principal de valor del sistema de inicio a fin (como ocurriría con el registro de un usuario y el procesamiento de una transacción en un sistema web).

### 1.1 Definición del Flujo de Valor en NeoFluid3D
En un software de física computacional, la transacción o aporte de valor principal consiste en calcular correctamente cómo se comporta un fluido en el tiempo y comprobar que las leyes de la física se cumplan sin errores numéricos. Este proceso se compone de cuatro pasos secuenciales descritos en la Tabla 1.

| Paso del Flujo | Operación que Realiza el Sistema | Objetivo de la Validación |
|---|---|---|
| 1. Configuración de Escenario | Carga de las propiedades del fluido (como la densidad del agua de 1000 kg/m³ y la viscosidad) y los límites de los recipientes. | Asegurar que los datos iniciales sean válidos y que el agua comience en una posición estable. |
| 2. Cálculo Físico en la GPU | Resolución del movimiento y choque de miles de partículas de agua en la tarjeta de video mediante el algoritmo DFSPH. | Garantizar que el agua no se comprima artificialmente y mantenga su volumen natural constante. |
| 3. Control de Calidad | Verificación continua de que las partículas no atraviesen las paredes y que las presiones no se vuelvan inestables. | Comprobar que los errores matemáticos se mantengan por debajo de los límites tolerables. |
| 4. Guardado y Reporte | Exportación de los resultados de la simulación a disco y generación automática del informe visual interactivo. | Dejar registro permanente de los datos calculados para su inspección por parte del usuario o evaluador. |

*Nota.* Etapas que componen el flujo de valor completo del simulador NeoFluid3D.

---

## 2. Experimentos Clásicos de Validación y Resultados Obtenidos

Para demostrar que el simulador funciona correctamente en una computadora real, el sistema fue evaluado contra cinco experimentos clásicos de la mecánica de fluidos reconocidos internacionalmente en la literatura científica. Los resultados de estas pruebas se resumen en la Tabla 2.

| Experimento Canónico | Fenómeno Físico Comprobado | Margen de Tolerancia | Error Obtenido | Resultado |
|---|---|---|---|:---:|
| Columna de Agua en Reposo | Comprueba que la presión del agua aumente linealmente con la profundidad debido a la gravedad. | Error menor a 2.0% | 0.49% | Aprobado |
| Rotura de Presa (Dam Break) | Mide la velocidad con la que una columna de agua colapsa y se desplaza hacia adelante. | Error menor a 5.0% | 2.07% | Aprobado |
| Gota de Agua en Relajación | Verifica que la tensión superficial cohesione el líquido hasta formar una esfera perfecta. | Error menor a 5.0% | 0.15% | Aprobado |
| Flujo en Canal Laminar | Mide la fricción del líquido contra las paredes para formar una curva parabólica de velocidad. | Error menor a 3.0% | 0.95% | Aprobado |
| Colisión contra Obstáculos | Comprueba que las partículas reboten contra los objetos sólidos sin atravesarlos ni perder energía. | Error menor a 5.0% | 0.00% | Aprobado |

*Nota.* Comparación entre los cálculos de NeoFluid3D y los resultados teóricos exactos de la literatura de fluidos.

Al ejecutar las pruebas en la computadora de producción, los cinco casos fueron aprobados satisfactoriamente en fracciones de segundo, demostrando la estabilidad del cálculo.

---

## 3. Informe Visual de Resultados (validation.html)

Como comprobante de la ejecución, el simulador genera de forma automática un informe visual en formato HTML (`reports/validation.html`). Al abrir este archivo en cualquier navegador de internet, se pueden apreciar:

1. Curvas gráficas que comparan los puntos calculados por el simulador directamente sobre las líneas teóricas de los experimentos reales.
2. Tablas detalladas con el tiempo de cálculo en microsegundos y el porcentaje de error exacto de cada prueba.
3. El archivo funciona de manera 100% independiente y no requiere conexión a internet para mostrar sus gráficos.

---

## 4. Instrucción para Comprobar la Validación

El evaluador puede reproducir todas las pruebas físicas y regenerar el informe visual en cualquier momento mediante un único comando en la terminal:

`./build/NeoFluidValidation/NeoFluidValidation --report reports/validation.html`

Una vez concluida la prueba, el informe se puede abrir en el navegador habitual haciendo doble clic en el archivo generado dentro de la carpeta `reports/`.
