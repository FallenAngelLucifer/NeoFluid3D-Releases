## NeoFluid3D v0.2.0-alpha — Academic Research Preview (Closed Evaluation)

> **Aviso de Estado del Software (Research Prototype):**  
> Esta publicación corresponde a un compilado autónomo pre-release de evaluación académica y verificación técnica. El solver hidrodinámico (DFSPH) se encuentra en fase activa de investigación y calibración matemática. Se publica como versión de acceso controlado con el fin de auditar su rigor físico y estabilidad numérica.

---

### Componentes Incluidos en el Paquete Autónomo
* **NeoFluid3D:** Ejecutable interactivo tridimensional para visualización física en tiempo real a 60 FPS (Vulkan 1.3).
* **NeoFluidValidation:** Módulo de pruebas formales desatendidas que verifica los 5 experimentos canónicos de fluidos (100% aprobados).
* **Shaders SPIR-V Precompilados:** Módulos de cómputo en VRAM de fuerzas SPH, advección, densidad y Marching Cubes (cero dependencias de SDK en la máquina destino).
* **Modelos Geométricos y Configuraciones:** Escenarios canónicos de prueba (.obj y campos de distancia .nfsdf).

---

### Requisitos Mínimos del Sistema
* **GPU:** Compatible con Vulkan 1.3 y operaciones de subgrupos (*Subgroup Operations*), mínimo 2 GB de VRAM dedicada.
* **CPU:** x86_64 multinúcleo (4 núcleos mínimo, 8 recomendados).
* **RAM:** 8.0 GB libres (16.0 GB recomendados).
* **SO:** Linux de 64 bits (Ubuntu 22.04+, Debian 12, Arch) o Windows 10/11 de 64 bits.

---

### Instrucciones de Ejecución
1. Descargue y descomprima el archivo adjunto `NeoFluid3D-v0.2.0-alpha-linux-x64.tar.gz`.
2. Ejecute `./run_interactive.sh` para iniciar el simulador interactivo.
3. Ejecute `./run_validation.sh` para reproducir la suite de validación científica y generar el informe visual en `reports/validation.html`.
