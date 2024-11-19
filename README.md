# Repositorio de Simulación de SOFC con OpenFuelCell2

Bienvenido al repositorio para la **[Simulación de una Celda de Combustible de Óxido Sólido (SOFC)](https://youtu.be/z8SVKpRC4zo)** utilizando **OpenFuelCell2**, una extensión de OpenFOAM diseñada específicamente para modelar dispositivos electroquímicos. Este proyecto permite estudiar el impacto de condiciones operativas, como la temperatura, sobre el rendimiento de una SOFC tubular.


La reacción química de la SOFC a simular es la siguiente:

- Anode side:
<img src="https://latex.codecogs.com/svg.latex?\Large&space;\textrm{H}_{2}+\textrm{O}^{2-}\to\textrm{H}_2\textrm{O}+\textrm{2e}^{-}" title="\Large \textrm{H}_{2}+\textrm{O}^{2-}\to\textrm{H_2O}+\textrm{2e}^{-}" />
- Cathode side:
<img src="https://latex.codecogs.com/svg.latex?\Large&space;\textrm{0.5O}_{2}+\text{2e}^{-}\to\textrm{O}_{2-}" title="\Large \textrm{0.5O}_{2}+\textrm{2H}^{+}+\textrm{2e}^{-}\to\textrm{H}_{2}\textrm{O}" />
- Overall Reaction:
<img src="https://latex.codecogs.com/svg.latex?\Large&space;\textrm{H}_{2}+\textrm{0.5O}_{2}\to\textrm{H}_{2}\textrm{O}" title="\Large \textrm{H}_{2}+\textrm{0.5O}_{2}\to\textrm{H}_{2}\textrm{O}" />

En la siguiente figura, se observan los componentes del SOFC, El color azul es el cátodo, el color verde es el ánodo y el blanco es el electrolito. El conducto superior es el conducto en donde fluye el aire y el inferior es donde pasa el combustible, el hidrogeno.

![Estructura SOFC](./images/estructura-SOFC.png)

## Objetivo del Proyecto

El propósito de este proyecto es evaluar el desempeño de una **Celda de Combustible de Óxido Sólido (SOFC)** utilizando el software **OpenFuelCell2**. Este análisis se centra en el impacto de parámetros operativos, como la temperatura, sobre las variables clave del sistema, incluyendo el voltaje, la densidad de corriente y la distribución de temperatura.


## Justificación Científica

La temperatura es un parámetro crítico en el funcionamiento de las SOFC, ya que afecta directamente la eficiencia electroquímica, las pérdidas térmicas y la degradación de los materiales. Investigaciones recientes (Zeng et al., 2020; Bessler et al., 2010) han demostrado que operar a temperaturas demasiado altas puede causar tensiones térmicas y acelerar la degradación, mientras que temperaturas más bajas pueden reducir la conductividad iónica y el rendimiento electroquímico.

## Como usar Openfuelcell2

El código se compila con las librerías de OpenFOAM, ya sean versiones [ORG](https://openfoam.org/) o [COM](https://www.openfoam.com/). La rama por defecto es compatible con la versión COM, mientras que las otras ramas también se proporcionan para diferentes entornos OpenFOAM. Los entornos disponibles incluyen: OpenFOAM-v2012, OpenFOAM-v2106, OpenFOAM-v2306, OpenFOAM-v6, OpenFOAM-v8. Nota: la rama principal sólo es compatible con OpenFOAM-v2306, mientras que las demás están en preparación.

```bash
# Download the source code
# Setup the corresponding openfoam environment
# Switch to the corresponding branch

# Change dictionary to the repository
cd openFuelCell2/src

# Compile the source code with
./Allwmake

# Or compile in parallel
./Allwmake -j n
```

También puede borrar las bibliotecas y los archivos ejecutables con

```bash

cd openFuelCell2/src

./Allclean

```

## Estructura de los archivos presentes en el repositorio:

- **0.orig/**  
  Contiene los archivos de condiciones iniciales y de frontera, incluyendo:
  - `T`: Distribución de temperatura para cada región (ánodo, cátodo y electrolito).
  - Otros archivos que definen la configuración inicial del sistema como la presión, phi, etc.

- **constant/**  
  Archivos con las propiedades del material, parámetros de reacción y definiciones termofísicas:
  - `thermophysicalProperties`: Propiedades térmicas y de transporte.
  - `combustionProperties`: Detalles de las tasas de reacción y mecanismos químicos.
  - `regionProperties`: señala el fluido, solido y electric de la celda.

- **system/**  
  Archivos de control para configurar la simulación:
  - `controlDict`: Define el tiempo de simulación, configuraciones del solucionador y tipo de simulación (transitoria o estacionaria).

- **scripts/**  
  Scripts en Python o Bash para automatizar modificaciones de parámetros y ejecutar simulaciones. Esta parte no se toca!

- **results/**  
  Archivos de salida y datos post-procesados de las simulaciones. Incluye gráficos de voltaje, densidad de corriente y distribución de temperatura.

## Cómo Usar Este Repositorio

1. **Instalar OpenFuelCell2**  
   Asegúrate de tener OpenFOAM y OpenFuelCell2 instalados en tu sistema. Sigue la [guía de instalación de OpenFuelCell2](https://github.com/openFuelCell2/openFuelCell2) para más detalles.

2. **Modificar Parámetros**  
   Ajusta la temperatura u otros parámetros en el archivo `0.orig/T` para simular diferentes condiciones operativas. Ejemplo:
   ```plaintext
   internalField   uniform 973; 

 En este proyecto, evaluamos el desempeño de una SOFC bajo temperaturas de 773 K, 873 K, 973 K y 1073 K. 
 
 
## Resultados Clave

- **Temperatura óptima (773 K):** Equilibrio entre eficiencia electroquímica y estabilidad térmica, minimizando pérdidas y degradación.
- **Temperaturas altas (1073 K):** Aumento de la cinética de reacción pero intensificación de las tensiones térmicas y gradientes de temperatura.
- **Distribución de voltaje y corriente:** Las regiones iniciales de la celda contribuyen más al voltaje máximo, mientras que las finales están limitadas por la disponibilidad de combustible.

**Se recomienda ver el informe del repositorio que tiene más información**.

## Fuentes
- Zeng, K., et al. (2020). Thermal management in SOFC systems. Journal of Power Sources.
- Bessler, W. G., et al. (2010). Performance and durability of SOFCs under variable conditions. Solid State Ionics.
- Kishimoto, M., et al. (2016). Ammonia decomposition for DA-SOFCs. International Journal of Hydrogen Energy.

## Contribuyentes
- Catalina Arcila Restrepo
- Pontificia Universidad Católica de Chile
- Correo: catalina.arcila@uc.cl
