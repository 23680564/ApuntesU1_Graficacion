# APUNTES UNIDAD 1 - GRAFICACION

## 1.1 Historia y Evolución de la Graficación por Computadora

La evolución de los gráficos no es solo una historia de mejores imágenes, sino de cómo los humanos interactúan con las máquinas:

- **La Era de los Osciloscopios (1950-1960)**: Las primeras imágenes eran puntos y líneas en pantallas de radar. El sistema Whirlwind de la Marina de EE. UU. fue pionero en mostrar datos visuales en tiempo real.

- **El Hito de Sketchpad (1963)**: Ivan Sutherland creó Sketchpad, el primer programa que permitía a los usuarios dibujar objetos geométricos de forma interactiva. Introdujo conceptos que usamos hoy, como las restricciones geométricas y la jerarquía de objetos.

- **La Revolución de los Algoritmos (1970-1980)**: Investigadores como Henri Gouraud y Bui Tuong Phong desarrollaron métodos de sombreado que permitieron que los objetos 3D dejaran de verse planos y comenzaran a mostrar superficies curvas y brillos realistas.

- **El Renderizado Moderno (1990-Presente)**: Con la llegada de las GPUs (Unidades de Procesamiento Gráfico), pasamos del renderizado por software al hardware. Actualmente, el Ray Tracing (trazado de rayos) permite simular el comportamiento físico de la luz en tiempo real.

  ## 1.2 Áreas de Aplicación
La graficación por computadora ha permeado casi todas las industrias modernas:

- **Medicina y Bioinformática**: Reconstrucción 3D a partir de tomografías computarizadas (CT) y resonancias magnéticas, permitiendo cirugías asistidas por computadora y visualización de estructuras moleculares complejas.

- **Simulación y Entrenamiento**: Simuladores de vuelo y conducción que utilizan gráficos fotorrealistas para entrenar a pilotos y conductores en entornos de riesgo controlado.

- **Cartografía y GIS**: Sistemas de Información Geográfica que procesan datos de satélite para generar mapas interactivos y modelos de elevación del terreno.

- **Manufactura e Industria (CAD/CAM)**: El Diseño Asistido por Computadora permite probar la resistencia de piezas mecánicas antes de fabricarlas mediante simulaciones visuales de estrés.

  ---

## 1.3 Aspectos Matemáticos de la Graficación
Los gráficos son, en esencia, matemáticas aplicadas al espacio visual: 

**Geometría Analítica**: Uso de ecuaciones para definir formas (líneas, círculos, elipses).

**Transformaciones Lineales**: Las matrices de $3 \times 3$ y $4 \times 4$ son el estándar para mover objetos. Para rotar un punto $(x, y)$ un ángulo $\theta$ respecto al origen, usamos:

$$\begin{bmatrix} x' \\ y' \end{bmatrix} = \begin{bmatrix} \cos \theta & -\sin \theta \\ 
\sin \theta & \cos \theta \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix}$$

- **Coordenadas Homogéneas**: Permiten tratar traslaciones, rotaciones y escalados como una sola operación matricial, facilitando el procesamiento en tarjetas de video.

  ---

## 1.4 Modelos del Color
El color es la interpretación de la luz, y en computación se modela para diferentes fines:

- **RGB** (Red, Green, Blue): Basado en la Síntesis Aditiva. Se utiliza en pantallas donde la suma de los tres colores al 100% genera blanco.

- **CMY / CMYK (Cyan, Magenta, Yellow, Black)**: Basado en la Síntesis Sustractiva. Se usa en impresión; al mezclar pigmentos, estos "restan" luz al papel, y la suma de todos genera negro (o un café muy oscuro, por eso se añade el canal K para el negro puro).

- **HSV (Hue, Saturation, Value)**: Diseñado para ser intuitivo para los artistas. El Tono (Hue) es el color en el espectro (0°-360°), la Saturación es la pureza del color, y el Valor es el brillo.

- **HSL (Hue, Saturation, Lightness)**: Similar al HSV, pero la Luminosidad (Lightness) escala de negro a blanco pasando por el color puro en el centro.

  <img width="356" height="343" alt="image" src="https://github.com/user-attachments/assets/586024ca-903e-4aba-b9a1-0faa4aea02be" />

  ---

  ## 1.5 Representación y Trazo de Líneas y Polígonos
El desafío es representar formas continuas en un mundo de píxeles discretos:

- **Rasterización**: El proceso de convertir vectores en píxeles.

- **Algoritmo de DDA (Digital Differential Analyzer)**: Un algoritmo simple de trazado de líneas basado en el incremento de coordenadas, pero lento por el uso de punto flotante.

- **Algoritmo de Bresenham**: Esencial en la historia de la computación porque utiliza solo aritmética de enteros, lo que lo hace extremadamente rápido para el hardware.

   ### 1.5.1 Formatos de Imagen
  
- **Vectores** (SVG, AI, EPS): No dependen de la resolución. Ideales para logotipos y tipografía.

- **Raster** (JPG, PNG, GIF, WEBP):

    - **PNG**: Formato sin pérdida con canal alfa (transparencia).

    - **JPG:** Utiliza la Transformada Discreta del Coseno para comprimir, perdiendo detalle pero ahorrando espacio.

    - **BMP**: Formato sin compresión, cada píxel se guarda tal cual.

  ## 1.6 Procesamiento de Mapas de Bits
El procesamiento digital de imágenes consiste en aplicar funciones matemáticas a la matriz de píxeles:

- **Histogramas**: Representación gráfica de la distribución de tonalidades. Permite realizar Ecualización para mejorar el contraste.

- **Filtros de Convolución**: Se pasa una pequeña matriz (kernel) sobre la imagen:

- **Desenfoque (Blur)**: Promedia los píxeles vecinos.

- **Detección de Bordes (Sobel): Resalta los cambios bruscos de intensidad.

- **Umbralización (Thresholding)**: Convierte una imagen a blanco y negro puro basándose en un límite de brillo, fundamental para el reconocimiento de formas.
