# Bitácora de aprendizaje de la unidad 5

## 1.  **Diagnóstico inicial**

### Encapsulamiento
Una línea de código que muestra encapsulamiento es public double Radio { get; private set; } dentro de la clase Circulo

El campo nombre es private para ocultar los detalles de implementación y proteger el estado interno de la clase. Al mismo tiempo, la propiedad Nombre es public para proporcionar un acceso controlado y seguro a ese campo desde fuera.

### Herencia
La herencia se evidencia en la clase Circulo a través de la sintaxis : Figura, lo que indica que Circulo hereda de la clase base Figura. Esto significa que Circulo adquiere las propiedades y métodos de Figura.

Un objeto de tipo Circulo, además de su propio dato Radio, almacena también el nombre que hereda de la clase Figura.

### Polimorfismo

Cuando se llama a fig.Dibujar() dentro del bucle foreach, el programa determina qué versión del método Dibujar debe ejecutar en tiempo de ejecución. Esto se conoce como enlace dinámico. Una posible hipótesis sobre cómo funciona "por debajo" es que cada objeto (como Circulo o Rectangulo) guarda una referencia a la tabla de métodos virtuales de su clase. Esta tabla actúa como un índice que mapea nombres de métodos a las implementaciones concretas. Cuando se llama a fig.Dibujar(), el programa usa el tipo real del objeto (sea Circulo o Rectangulo) para buscar en su tabla de métodos virtuales la dirección de memoria correcta de la función Dibujar específica para ese objeto, y luego la ejecuta.

### Hipótesis sobre la implementación

#### Memoria y herencia

Al crear un objeto Rectangulo que hereda de Figura, me imagino que los datos se organizan en la memoria de manera contigua para formar una sola unidad. La memoria del objeto podría comenzar con los campos de la clase base (nombre), seguidos inmediatamente por los campos de la clase derivada (Base y Altura). Así, en un bloque de memoria, tendrías una estructura similar a: [nombre], [Base], [Altura]. De esta forma, un solo puntero al inicio del bloque de memoria es suficiente para acceder a todos los datos del objeto, tanto los heredados como los propios.

El mecanismo del polimorfismo
Para la llamada fig.Dibujar(), mi hipótesis es que el compilador no sabe cuál Dibujar llamar en tiempo de compilación. En su lugar, el objeto fig podría tener un pequeño puntero a una tabla de funciones (vtable o "tabla de métodos virtuales"), que es específica para la clase a la que el objeto pertenece (Circulo o Rectangulo). Cuando el programa se ejecuta y se encuentra con fig.Dibujar(), sigue ese puntero, busca la entrada Dibujar en la tabla de funciones y llama a la función cuya dirección está almacenada allí. De esta manera, aunque fig sea de tipo Figura estáticamente, en tiempo de ejecución se utiliza la información del tipo real del objeto para encontrar y ejecutar la implementación correcta del método.

La barrera del encapsulamiento
El compilador logra que no puedas acceder a un miembro private durante la fase de compilación. Esta protección se implementa revisando el código antes de que se convierta en un ejecutable. Cuando intentas acceder a nombre desde fuera de la clase Figura (por ejemplo, en la clase Programa), el compilador detecta que nombre tiene el modificador de acceso private y emite un error de compilación. Es una barrera que se impone en el momento de escribir y compilar el código, no durante la ejecución, lo que evita que el programa se cree si las reglas de acceso no se cumplen.

## 2.  **La pregunta inicial**

## 3.  **Registro de exploración:** 
> Aquí documentas cada ciclo de pregunta -> hipótesis -> experimento -> hallazgo -> reflexión.
> Debe ser rico en evidencia visual (código, capturas del depurador con anotaciones, diagramas).

## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación
