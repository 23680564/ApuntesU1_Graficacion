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

<img width="246" height="70" alt="image" src="https://github.com/user-attachments/assets/4e6a6321-58c1-4d38-8a9a-09e3fe3e3925" />


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

   # Flor_de_Vida

## Creación de el proyecto FLor de Vida

### Descargar Python y Blender
- Abrir el programa Blender, ir a "archivo" darle en "Generico"

  
  <img width="487" height="154" alt="image" src="https://github.com/user-attachments/assets/232a2b59-4687-4ffe-b29a-02a0a3862962" />

- Una vez se haya creado el archivo, ir a el apartado de Scripts y dar click en el apartado de "Nuevo" y poder generar el proyecto

  <img width="728" height="78" alt="image" src="https://github.com/user-attachments/assets/60ab7000-4603-4919-a66b-dc02035356c7" />

  

### Importación de librerías

`
import bpy
import math
`

` bpy`

Es la biblioteca de Blender que permite:

- Crear objetos

- Modificar escenas

- Controlar materiales, luces, cámaras, etc.

` math`

Se usa para:

- Funciones trigonométricas (cos, sin)

- Convertir grados a radianes (radians())


### Limpiar la escena
`
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()
`
¿Qué hace?

- Selecciona todos los objetos existentes.

- Los elimina.

 Esto asegura que el script empiece desde una escena vacía.

 ## Parámetros principales
 `
radio = 50
angulo_actual = 0
paso_angular = 10
`

`radio`

- Es el radio de cada círculo.

- También determina la distancia desde el centro para posicionarlos.

` angulo_actual`

- Guarda el ángulo actual en grados.

- Empieza en 0°.

`paso_angular`

- Indica cuántos grados avanza cada círculo.

- Aquí está en 10°, así que habrá:

`360 / 10 = 36 círculos alrededor`

## Círculo central
`
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(0, 0, 0), vertices=64)
`

**¿Qué hace?**

Crea un círculo:

Radio: 50

Ubicación: centro (0,0,0)

64 vértices → se ve suave

Este es el círculo base en el centro.

## Círculo 1 (Manual)
`
x1 = radio * math.cos(math.radians(angulo_actual))
y1 = radio * math.sin(math.radians(angulo_actual))
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x1, y1, 0), vertices=64)
`

**¿Qué está pasando aquí?**

Se usan las fórmulas del círculo:
`
x = r cos(θ)
y = r sin(θ)
`

Como `angulo_actual = 0`:
`
cos(0°) = 1
sin(0°) = 0
`

Entonces:
`
x = 50
y = 0
`

Se crea un círculo en (50, 0, 0).

## Círculo 2 (Manual)
`
angulo_actual += paso_angular
`

Ahora el ángulo pasa a:
`
0 + 10 = 10°
`

Luego:
`
x2 = radio * math.cos(math.radians(angulo_actual))
y2 = radio * math.sin(math.radians(angulo_actual))
`

Se calcula su nueva posición usando trigonometría.

Después se crea el círculo en esa nueva posición.

## Círculos restantes con WHILE
`
angulo_actual += paso_angular
while angulo_actual < 360:
`

Aquí comienza el ciclo automático.

El while repite:

- Calcula posición con cos y sin

- Crea el círculo

- Aumenta el ángulo 10 grados

- Se detiene cuando llega a 360°

  ## Codigo completo

 ```
import bpy
import math

# Limpiar escena
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

# Parámetros de la figura
radio = 3
angulo_actual = 0
paso_angular = 60  # Cada 60 grados para obtener 6 círculos alrededor

# 1. Círculo Central
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(0, 0, 0), vertices=64)

# --- INICIO DEL PATRÓN REPETITIVO ---
# Círculo 1 (Manual)
x1 = radio * math.cos(math.radians(angulo_actual))
y1 = radio * math.sin(math.radians(angulo_actual))
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x1, y1, 0), vertices=64)

# Círculo 2 (Manual)
angulo_actual += paso_angular
x2 = radio * math.cos(math.radians(angulo_actual))
y2 = radio * math.sin(math.radians(angulo_actual))
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x2, y2, 0), vertices=64)

# Completar círculos restantes con ciclo WHILE
angulo_actual += paso_angular
while angulo_actual < 360:
    x = radio * math.cos(math.radians(angulo_actual))
    y = radio * math.sin(math.radians(angulo_actual))
    bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x, y, 0), vertices=64)
    angulo_actual += paso_angular
 ```

## Para poder ejecutarlo
- Ir a el icono de **RUN** y darle click

  <img width="29" height="26" alt="image" src="https://github.com/user-attachments/assets/ff007ffa-75ba-49e6-825b-fd827aa0684e" />

  - Despues se mostrara en pantalla la figura que se realizo mediante el codiggo, en este caso lo es la "Flor de Vida"

    <img width="394" height="457" alt="image" src="https://github.com/user-attachments/assets/73abb3bc-6259-4957-a374-45fb56752c1e" />

    - Y asi es como se finaliza el proyecto
   
      **NOTA: Si no llegase a correr o ejecutarse, revisa la identacion**

      ---

## 1.6 Procesamiento de Mapas de Bits
El procesamiento digital de imágenes consiste en aplicar funciones matemáticas a la matriz de píxeles:

- **Histogramas**: Representación gráfica de la distribución de tonalidades. Permite realizar Ecualización para mejorar el contraste.

- **Filtros de Convolución**: Se pasa una pequeña matriz (kernel) sobre la imagen:

- **Desenfoque (Blur)**: Promedia los píxeles vecinos.

- **Detección de Bordes (Sobel): Resalta los cambios bruscos de intensidad.

- **Umbralización (Thresholding)**: Convierte una imagen a blanco y negro puro basándose en un límite de brillo, fundamental para el reconocimiento de formas.
