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

  # Generar un poligono 2D

## Explicacion para crear el poligono

Este ejercicio consiste en la creacion un poligono 2D usando **Python** en Blender mediante la API bpy
El codigo genera una malla personalizada calculando los vertices mediante trigonometria y conectandolos a traves de aristas para formar una figura cerrada.

---

# Objetivo de la creacion del proyecto

- Comprender y analizar el uso de la API bpy de Blender.
- Generar mallas manualmente mediante el uso de python.
- Automatizar la creacion de la geometria dentro de Blender.
- Aplicar la conversion de coordenadas polares  a cartesianas.

---

# Explicacion del codigo

# Importacion de librerias de Python

`import bpy
import math`

- bpy: Nos permite interactuar con Blender a nivel interno
- math: Esta se utiliza para realizar calculos automaticos como seno, coseno y pi

# Creacion de malla y el objeto

`malla = bpy.data.meshes.new(nombre)
objeto = bpy.data.objects.new(nombre, malla)
bpy.context.collection.objects.link(objeto)`

Aqui se:

- Se crea una nueva estructura de malla
- Crea un objeto de usa la malla
- Vinculamos el objeto a la coleccion activa de la escena

  # Calculo de vertices

  `for i in range(lados):
        angulo = 2 * math.pi * i / lados
        x = radio *  math.cos(angulo)
        y = radio * math.sin(angulo)
        vertices.append((x, y, 0)) #Z = 0 para mantenerlo en 2D
  `

  Se realiza:

  - Division del circulo completo en (2pi radianes) entre el numero de lados.
  - Conversion de coordenadas polares a cartesianas
  - Se fija Z = 0 para mantener la figura en el plano 2D.

  # Creacion de aristas

  `for i in range(lados):
            aristas.append((i, (i + 1) % lados))`
  
  Cada vertice se conecta con el siguiente.
  El operador modulo (%) permite que el ultimo vertice se conecte nuevamente con el primero, cerrando la figura

  # Carga de datos en la malla
  `malla.from_pydata(vertices, aristas, [])
    malla.update()`

  Aqui se cargan:
  Lista de vertices
  Lista de aristas
  Lista de caras (vacia en este caso)

  # Limpieza de escena

  `bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()`

Se eliminan todos los objetos antes de crear el nuevo poligono para evitar superposicion

# Llamada final

`crear_poligono_2d("Poligono2D", lados=6, radio=5)
`

## Como ejecuta el codigo

1. Abrir Blender.
2. Ir a la pestaña **Scripts**

   <img width="1056" height="28" alt="image" src="https://github.com/user-attachments/assets/f90ca054-a144-4938-b5d1-87c6d368459d" />
3. Generar un nuevo scripts
4. Generar codigo
5. Darle en el icono de **Run**
   <img width="35" height="30" alt="image" src="https://github.com/user-attachments/assets/954d90a7-6ba0-4a0d-926b-18b5840ce8f9" />
6. Esperar que se ejecute el codigo

   ---

   # Parametros configurales
   En la ultima linea del codigo se puede modificar python

   crear_poligono_2d("Poligono2D", lados=6, radio=5)

   - Lados -> l numero de lados del poligono
   - radio -> El tamaño del poligono
  
     ---

     # Codigo completo
     <img width="512" height="546" alt="image" src="https://github.com/user-attachments/assets/91176203-e303-4413-9d6e-3d201a11158a" />
```import bpy
import math

def crear_poligono_2d(nombre, lados, radio):
    #Crear una nueva malla y un nuevo objeto
    malla = bpy.data.meshes.new(nombre)
    objeto = bpy.data.objects.new(nombre, malla)
    
    #Vincular el objeto a la escena actual
    bpy.context.collection.objects.link(objeto)
    
    vertices = []
    aristas = []
    
    #Calculo de vertices usando coordernadas palares cartesianas
    for i in range(lados):
        angulo = 2 * math.pi * i / lados
        x = radio *  math.cos(angulo)
        y = radio * math.sin(angulo)
        vertices.append((x, y, 0)) #Z = 0 para mantenerlo en 2D
        
     # Definir las conexiones (aristas) entre los vertices
    for i in range(lados):
            aristas.append((i, (i + 1) % lados))
            
    # Cargar los datos en la malla
    malla.from_pydata(vertices, aristas, [])
    malla.update()
            
# Limpiar la escena antes de empezar
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()
            
# Llamada a la funciom : UN hexagono de radio de 5
crear_poligono_2d("Poligono2D", lados=6, radio=5)
```
---

## Resultado

   <img width="398" height="499" alt="image" src="https://github.com/user-attachments/assets/caa3fdb4-1779-4955-9917-b518f8b73987" />

   ---

## 1.6 Procesamiento de Mapas de Bits
El procesamiento digital de imágenes consiste en aplicar funciones matemáticas a la matriz de píxeles:

- **Histogramas**: Representación gráfica de la distribución de tonalidades. Permite realizar Ecualización para mejorar el contraste.

- **Filtros de Convolución**: Se pasa una pequeña matriz (kernel) sobre la imagen:

- **Desenfoque (Blur)**: Promedia los píxeles vecinos.

- **Detección de Bordes (Sobel): Resalta los cambios bruscos de intensidad.

- **Umbralización (Thresholding)**: Convierte una imagen a blanco y negro puro basándose en un límite de brillo, fundamental para el reconocimiento de formas.
