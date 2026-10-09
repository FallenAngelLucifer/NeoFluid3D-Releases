# NeoFluid3D — Portal Oficial de Distribución (Releases)

Bienvenido al repositorio oficial de distribución técnica de **NeoFluid3D**, un motor de simulación hidrodinámica computacional (SPH) y reconstrucción volumétrica tridimensional en tiempo real, desarrollado sobre **Vulkan 1.3** y **C++20**.

Este repositorio público tiene como propósito exclusivo albergar los **paquetes ejecutables autónomos precompilados (*Releases*)**, garantizando un canal de acceso público, transparente y auditable para usuarios y evaluadores.

---

## Aviso de Estado del Software (*Academic Research Preview*)

> **Declaración de Etapa Temprana:**  
> La versión actual (`v0.2.0-alpha`) corresponde a un prototipo de investigación académica en fase activa de desarrollo y calibración matemática del solver de divergencia libre (*Divergence-Free SPH*, DFSPH). Los paquetes distribuidos en este portal están preparados con dependencias autocontenidas y están orientados a la evaluación técnica de sus capacidades hidrodinámicas y verificación contra soluciones analíticas exactas.

---

## Descarga del Paquete Ejecutable Autónomo

El paquete precompilado no requiere la instalación de compiladores ni del SDK de Vulkan en la máquina destino:

* **Versión Actual:** `v0.2.0-alpha`
* **Artefacto:** `NeoFluid3D-v0.2.0-alpha-linux-x64.tar.gz` (145 MB)
* **Descarga Oficial:** Disponible en la sección de [**GitHub Releases**](https://github.com/FallenAngelLucifer/NeoFluid3D-Releases/releases/tag/v0.2.0-alpha)

### Instrucciones de Ejecución Rápida
Una vez descargado el archivo comprimido:

```bash
# 1. Descomprimir el paquete
tar -xzvf NeoFluid3D-v0.2.0-alpha-linux-x64.tar.gz
cd NeoFluid3D-v0.2.0-alpha

# 2. Iniciar la simulación interactiva 3D
./run_interactive.sh

# 3. O ejecutar la suite de validación física formal (genera reports/validation.html)
./run_validation.sh
```

---

## Requisitos Mínimos del Sistema

* **Procesador (CPU):** x86_64 multinúcleo (4 núcleos lógicos mínimo, 8 recomendados).
* **Memoria RAM:** 8.0 GB libres (16.0 GB recomendados).
* **Tarjeta Gráfica (GPU):** Compatible con Vulkan 1.3 y operaciones de subgrupos (*Subgroup Operations*), con al menos 2 GB de VRAM dedicada.
* **Controladores:** Drivers oficiales vigentes del fabricante de video (NVIDIA, AMD o Intel).
* **Sistema Operativo:** Linux x64 (Kernel 5.15+) o Windows 10/11 de 64 bits.
