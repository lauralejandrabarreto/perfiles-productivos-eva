# Perfiles productivos municipales en Colombia: k-medias vs k-medoides

Agrupamiento no supervisado de los **1.102 municipios de Colombia** según su perfil productivo agrícola, usando datos oficiales de las **Evaluaciones Agropecuarias Municipales (EVA) 2025** de la UPRA. Se comparan dos métodos: **k-medias** y **k-medoides (PAM)**.

## Datos

- **Fuente:** UPRA, *Evaluaciones Agropecuarias Municipales – EVA. 2019-2025. Base Agrícola*.
- **Portal:** [datos.gov.co (uejq-wxrr)](https://www.datos.gov.co/en/Agricultura-y-Desarrollo-Rural/Evaluaciones-Agropecuarias-Municipales-EVA-2019-20/uejq-wxrr/about_data)
- **Alcance:** 166.732 registros; se trabaja solo con 2025 (1.102 municipios).

El CSV **no se incluye en el repositorio** por su tamaño. Para reproducir el análisis hay que descargarlo del enlace anterior.

## Metodología

1. Construcción de una matriz municipal con 8 variables a partir del área sembrada: logaritmo del área total, número de cultivos, proporción de área permanente y proporción de área en cereales, frutales, tropicales tradicionales, raíces y tubérculos, y hortalizas.
2. Estandarización de las variables.
3. Elección de k con el criterio del codo y el coeficiente de silueta (k = 2 a 10).
4. k-medias (50 inicializaciones) y PAM con distancia de Manhattan, ambos con k = 4.
5. Comparación con silueta media, índice de Rand ajustado y análisis de sensibilidad a valores atípicos.

## Resultados principales

| Perfil | Municipios | Rasgo dominante |
|---|---|---|
| Tropical tradicional | 415 | 65 % del área en café, caña y cacao |
| Frutícola permanente | 252 | 54 % del área en frutales (plátano, aguacate, banano) |
| Andino de pequeña escala | 222 | 45 % en raíces y tubérculos; los municipios más pequeños |
| Cerealero de ciclo corto | 213 | 53 % en cereales (arroz, maíz); los municipios más grandes |

- Ambos métodos coinciden en el **85,0 %** de los municipios (índice de Rand ajustado = **0,667**).
- La estructura de los grupos es débil (silueta media de 0,255 con k-medias y 0,247 con k-medoides): los perfiles son tendencias dominantes dentro de un continuo, no categorías cerradas.
- La partición es robusta a los valores atípicos (índice de Rand ajustado = 0,966 al excluirlos).

![Grupos de k-medias y k-medoides en los dos primeros componentes principales](figuras/fig5_pca.png)

## Cómo reproducirlo

1. Descargar el CSV desde datos.gov.co.
2. Ponerlo en la misma carpeta que `eva_kmedias_kmedoides_corregido.Rmd`. El código lo encuentra solo, sin importar el nombre exacto.
3. Instalar los paquetes:
   ```r
   install.packages(c("readr", "dplyr", "tidyr", "ggplot2", "cluster",
                      "factoextra", "kableExtra", "reshape2", "gridExtra"))
   ```
4. Abrir el `.Rmd` en RStudio y presionar **Knit**.

## Contenido del repositorio

| Archivo | Descripción |
|---|---|
| `eva_kmedias_kmedoides_corregido.Rmd` | Código completo del análisis en R Markdown |
| `eva_kmedias_kmedoides_corregido.html` | Resultado compilado |
| `reporte/` | Reporte final en PDF |
| `figuras/` | Figuras usadas en este README |

## Autores

- Esteban Pinzón
- Alejandra Barreto

Proyecto del curso *Modelos de Machine Learning*, Ingeniería de Sistemas, Fundación Universitaria Konrad Lorenz, Bogotá, 2026.
