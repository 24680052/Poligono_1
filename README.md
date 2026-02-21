#Generador de poligono 2D en Blender

##Explicacion 

Este proyecto consiste en el desarrollo de un poligono 2D usando **Python** dentro de BLender mediante la API bpy.
El script genera una malla personalizada calculando los vertices mediante trigonometria y conectandolos a traves de aristas para formar una figura cerrada. 

---

#Objetivo del proyecto

- Comprender el uso de la API bpy en Blender.
- Aplicar conversion de coordenadas polares a cartesianas.
- Generar mallas manualmente mediante Python.
- Automatiar la creacion de geometria dentro de Blender.

---

#Explicacion tecnica del codigo

##Importacion de modulos 

Python

import bpy
import math 

·bpy: permite interactuar con BLender a nivel interno 
·math: se utiliza para realizar calculos matematicos como seno, coseno y pi

#Creacion de la malla y objeto 

`malla = bpy.data.meshes.new(nombre)
objeto = bpy.data.objects.new(nombre, malla)
bpy.context.collection.objects.link(objeto)`

Aquí se:

· Crea una nueva estructura de malla. 
· Se crea un objeto que usa esa malla.
· Se vincula el objeto a la colección activa de la escena.

#Calculo de vertices

`for i in range(lados):
    angulo = 2 * math.pi * i / lados
    x = radio * math.cos(angulo)
    y = radio * math.sin(angulo)
    vertices.append((x, y, 0))1. Abrir Blender
`

Se realiza:

· División del círculo completo (2π radianes) entre el número de lados.
· Conversión de coordenadas polares a cartesianas.
· Se fija Z = 0 para mantener la figura en el plano 2D.

#Creación de aristas

`
for i in range(lados):
    aristas.append((i, (i + 1) % lados))
`
Cada vértice se conecta con el siguiente.
El operador módulo (%) permite que el último vértice se conecte nuevamente con el primero, cerrando la figura.

#Carga de datos en la malla

`malla.from_pydata(vertices, aristas, [])
malla.update()
`
Se cargan:
Lista de vértices
Lista de aristas
Lista de caras (vacía en este caso)

#Limpieza de la escena

`bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()
`
Se eliminan todos los objetos antes de crear el nuevo polígono para evitar superposición.

#Llamada final

`crear_poligono_2d("Poligono2D", lados=6, radio=5)
`
Se genera un hexágono con radio 5 unidades.

---

## Cómo ejecutar el script.

1. Abrir Blender.
2. Ir a la pestaña **Scripting**.

<img width="1023" height="51" alt="image" src="https://github.com/user-attachments/assets/6adb7ec3-621f-496a-943a-d510599e4c0f" />

4. Abrir el archivo `poligono.py`.
5. Presionar **Run Script** o Alt + P.`

---

#Parametros configurales
En la ultima linea del codigo se puede modificar
python

crear_poligono_2d("oligno", lados=6, radio=5)

·lados -> Numero de lados del poligono. 
·radio -> Tamaño del poligono.

---

#Codigo completo 

<img width="596" height="607" alt="image" src="https://github.com/user-attachments/assets/e7e28087-dd02-4f12-8dfd-6d54548d26d7" />

```
import bpy
import math

def crear_poligono_2d(nombre, lados, radio):
malla = bpy.data.meshes.new(nombre)
objeto = bpy.data.objects.new(nombre, malla)

bpy.context.collection.objects.link(objeto)  
  
vertices = []  
aristas = []  
  
for i in range(lados):  
    angulo = 2 * math.pi * i / lados  
    x = radio * math.cos(angulo)  
    y = radio *math.sin(angulo)  
    vertices.append((x, y, 0)) # Z = 0 para mantenerlo en 2D  
      
for i in range (lados):  
        aristas.append((i, (i + 1) % lados))  
          
malla.from_pydata(vertices, aristas, [])  
malla.update()

bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

crear_poligono_2d("Poligono2D", lados=6, radio=5)
```
---


##Resultado 

<img width="506" height="621" alt="image" src="https://github.com/user-attachments/assets/c593e366-b7ec-49e2-8999-96307840e8e0" />

El ejemplo actual genera un **hexagono** de radio 5 unidades.
