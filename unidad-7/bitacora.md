# Bitácora de aprendizaje de la unidad 7

## Actividad 01

### 3. ¿que preguntas te surgen al ver el codigo? anota al menos tres preguntas.

¿como funciona la libreria glad al cargar funciones de la gpu? ¿que diferencia hay entre gluseprogram y glbindvertexarray? ¿por que opengl usa un rango de coordenadas de -1.0 a 1.0?)

## Actividad 02

### Resumen

por lo que puedo ver para dibujar un triangulo en opengl se requiere un contexto opengl gestionado por glfw para crear la ventana. se deben cargar las funciones modernas con glad, se debe configurar y subir los datos de vertices a la gpu, para el shader se necesita un programa compilado y linkeado (shader program) que contenga al menos un vertex shader y un fragment shader, el rol de glfw es crera la ventana y el contexto opengl, permitiendo programar graficos sin codigo especifico del sistema operativo, el rol de los drivers es implementar las funciones modernas de opengl, el glad consulta a los drivers para obtener y cargar dinamicamente estas funciones en el programa, los glfwswapbuffers() intercambian el buffer trasero con el buffer delantero, esto es esencial para la tecnica de double buffering.

## Actividad 03

### ¿Qué pasa si? glViewport(0, bufferHeight/2, bufferWidth/2, bufferHeight/2); Cambia los valores de bufferWidth y bufferHeight: divide por 2, por 4, multiplica por 2, por 4, etc. ¿Qué pasa? ¿Qué observas? ¿Qué crees que está pasando?

el dibujo se limita a la esquina inferior izquierda de la ventana. lo que esta pasando es que el viewport define el área del framebuffer que se usa, comprimiendo las coordenadas ndc [-1, 1] en esa área reducida

### Entonces hagamos “digestión”: en tu bitácora, escribe un resumen de lo que has aprendido hasta ahora y piensa en un experimento del tipo ¿Qué pasaría si?



### ¿Qué pasa si cambias el primer parámetro de glDrawArrays a GL_LINES?
opengl dibujaria el contorno del triangulo usando tres lineas

### Qué pasa si lo cambias a GL_POINTS?
opengl dibujaria tres puntos individuales en las posiciones de los vertices

### ¿Qué pasa si cambias el tercer parámetro a 2? 
no se dibuja la primitiva (gl_triangles necesita 3), o se omite

### ¿Qué pasa si lo cambias a 4?
opengl intenta leer datos de un cuarto vertice, resultando en la lectura de datos fuera del arreglo (comportamiento indefinido)






