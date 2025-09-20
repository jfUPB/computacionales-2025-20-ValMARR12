# Bitácora de aprendizaje de la unidad 5

## 1.  **Diagnóstico inicial**
Aquí están mis respuestas basadas en la experiencia con C#.

### Encapsulamiento 

Para mí, el **encapsulamiento** es como meter los datos de un objeto y los métodos que trabajan con esos datos en una caja fuerte. La caja tiene una interfaz (botones, una pantalla) que te permite interactuar con lo que hay dentro, pero no puedes abrirla para manipular directamente el contenido. . El objetivo es proteger los datos internos de ser modificados de forma incorrecta o inesperada desde fuera.

Una situación en la que vi su importancia fue en un proyecto de gestión de usuarios. La clase `User` tenía un campo `password` que era `private`. El único método para cambiar la contraseña era `ChangePassword(string newPassword)`, que validaba si la nueva contraseña cumplía ciertos criterios de seguridad (longitud mínima, caracteres especiales, etc.). Si el campo no hubiera sido `private`, cualquier parte del código podría haber cambiado la contraseña directamente, sin pasar por las validaciones, lo que habría creado una vulnerabilidad de seguridad. El encapsulamiento nos obligó a usar el método de forma correcta, garantizando la integridad de los datos.

### Herencia 

La **herencia** es una forma de crear una nueva clase basándose en una clase ya existente. La clase nueva, llamada clase derivada, "hereda" las propiedades y métodos de la clase original, llamada clase base. Es como si un niño heredara el ADN de sus padres; obtiene sus características y puede desarrollar otras nuevas propias.

Un programador decide usar la herencia para **reutilizar código** y establecer una **relación "es-un"** (is-a). En lugar de escribir el mismo código una y otra vez para clases similares, puedes definir una clase base con las funcionalidades comunes y luego crear clases derivadas que añadan o modifiquen comportamientos específicos.

**Ejemplo simple:**
Considera una clase base `Vehiculo` con propiedades como `Velocidad` y un método `Acelerar()`. Luego, puedes tener clases derivadas como `Coche` y `Moto` que heredan de `Vehiculo`. El `Coche` podría añadir un método `TocarClaxon()`, mientras que la `Moto` podría tener un método `HacerCaballito()`. De esta manera, no tienes que reescribir `Velocidad` y `Acelerar()` en ambas clases, lo que ahorra tiempo y hace que el código sea más organizado.

### Polimorfismo 

El **polimorfismo** es la capacidad de que un objeto de una clase derivada se comporte como su clase base. La palabra viene del griego y significa "muchas formas".

Decir que un código es "polimórfico" significa que puedes escribir código que interactúe con objetos de diferentes clases de manera uniforme, a través de una sola interfaz o clase base. . En lugar de tratar a cada objeto de forma diferente, puedes tratarlos como si fueran del mismo tipo base, y el programa sabe automáticamente qué método específico de cada objeto debe llamar en tiempo de ejecución.

Por ejemplo, si tienes una lista de `Vehiculo` que contiene objetos `Coche` y `Moto`, puedes recorrer la lista y llamar a `vehiculo.Acelerar()` en cada uno. Aunque todos son tratados como `Vehiculo`, el programa llamará al método `Acelerar()` de la clase `Coche` para los coches y al método de la clase `Moto` para las motos. Esto hace que el código sea mucho más limpio, flexible y fácil de extender, ya que no necesitas un `if/else` gigante para manejar cada tipo de objeto.
### Encapsulamiento
una línea de código que muestra encapsulamiento es public double Radio { get; private set; } dentro de la clase Circulo

el campo nombre es private para ocultar los detalles de implementación y proteger el estado interno de la clase. Al mismo tiempo, la propiedad Nombre es public para proporcionar un acceso controlado y seguro a ese campo desde fuera.

### Herencia
la herencia se evidencia en la clase Circulo a través de la sintaxis : Figura, lo que indica que Circulo hereda de la clase base Figura. Esto significa que Circulo adquiere las propiedades y métodos de Figura.

un objeto de tipo Circulo, además de su propio dato Radio, almacena también el nombre que hereda de la clase Figura.

### Polimorfismo

cuando se llama a fig.Dibujar() dentro del bucle foreach, el programa determina qué versión del método Dibujar debe ejecutar en tiempo de ejecución. Esto se conoce como enlace dinámico. Una posible hipótesis sobre cómo funciona "por debajo" es que cada objeto (como Circulo o Rectangulo) guarda una referencia a la tabla de métodos virtuales de su clase. Esta tabla actúa como un índice que mapea nombres de métodos a las implementaciones concretas. Cuando se llama a fig.Dibujar(), el programa usa el tipo real del objeto (sea Circulo o Rectangulo) para buscar en su tabla de métodos virtuales la dirección de memoria correcta de la función Dibujar específica para ese objeto, y luego la ejecuta.

### Hipótesis sobre la implementación

#### Memoria y herencia

al crear un objeto Rectangulo que hereda de Figura, me imagino que los datos se organizan en la memoria de manera contigua para formar una sola unidad. La memoria del objeto podría comenzar con los campos de la clase base (nombre), seguidos inmediatamente por los campos de la clase derivada (Base y Altura). Así, en un bloque de memoria, tendrías una estructura similar a: [nombre], [Base], [Altura]. De esta forma, un solo puntero al inicio del bloque de memoria es suficiente para acceder a todos los datos del objeto, tanto los heredados como los propios.

el mecanismo del polimorfismo
Para la llamada fig.Dibujar(), mi hipótesis es que el compilador no sabe cuál Dibujar llamar en tiempo de compilación. En su lugar, el objeto fig podría tener un pequeño puntero a una tabla de funciones (vtable o "tabla de métodos virtuales"), que es específica para la clase a la que el objeto pertenece (Circulo o Rectangulo). Cuando el programa se ejecuta y se encuentra con fig.Dibujar(), sigue ese puntero, busca la entrada Dibujar en la tabla de funciones y llama a la función cuya dirección está almacenada allí. De esta manera, aunque fig sea de tipo Figura estáticamente, en tiempo de ejecución se utiliza la información del tipo real del objeto para encontrar y ejecutar la implementación correcta del método.

la barrera del encapsulamiento
el compilador logra que no puedas acceder a un miembro private durante la fase de compilación. Esta protección se implementa revisando el código antes de que se convierta en un ejecutable. Cuando intentas acceder a nombre desde fuera de la clase Figura (por ejemplo, en la clase Programa), el compilador detecta que nombre tiene el modificador de acceso private y emite un error de compilación. Es una barrera que se impone en el momento de escribir y compilar el código, no durante la ejecución, lo que evita que el programa se cree si las reglas de acceso no se cumplen.

## 2.  **La pregunta inicial**

### Analiza el código de la aplicación y trata de explicar en tus propias palabras qué está haciendo

lo que esta haciendo el codigo es que cada vez le des click a la pantalla en en el recuadro se genera una pelota que despues de cierta trayectoria este estalle en particulas como un fuego artificial

<img width="1918" height="1030" alt="image" src="https://github.com/user-attachments/assets/b070a1fd-e0bf-42a2-86af-845abe250184" />

### Hipótesis y Observación de la Memoria

antes de ejecutar el código, espero que el objeto RisingParticle se almacene de forma contigua en la memoria. La jerarquía de herencia (Particle -> RisingParticle) implica que el objeto RisingParticle contendrá los miembros de su clase base, además de sus propios miembros.

### Observación en el Depurador

al capturar un objeto RisingParticle con el depurador, la ventana de 'Auto' o 'Locals' muestra de forma clara todos los miembros del objeto, incluyendo los datos heredados. La ventana de 'Memory 1' me permite ver la representación cruda de esos datos.

###  Captura y Análisis de CircularExplosion

para facilitar la captura, se podría agregar un breakpoint en el método update de la clase ofApp, justo después de crear el objeto CircularExplosion. Esto me permitiría examinar el objeto recién creado.

observación en la Memoria: La jerarquía de clases para CircularExplosion es: Particle -> ExplosionParticle -> CircularExplosion. Esto significa que un objeto CircularExplosion debe contener los miembros de ambas clases base, además de los suyos propios.

al examinar la memoria, se observa: un puntero a la vtable de CircularExplosion.

los miembros de la clase base ExplosionParticle: position, velocity, color, age, lifetime, y size.

no hay campos adicionales en la clase CircularExplosion porque utiliza el constructor para inicializar los valores de la clase base.

información del depurador: el depurador muestra claramente todos estos campos. La ventana de 'Memory 1' revela que, al igual que con RisingParticle, el primer dato del objeto es el puntero a la vtable, seguido por los datos miembros de la clase base ExplosionParticle.

conclusion: Se refuerza la idea de que la herencia se implementa a través de la composición de datos en memoria. La memoria de un objeto de una clase derivada es la suma de la memoria de sus clases base más la memoria de sus propios miembros.

```
#include <iostream>

class MyClass {
private:
    int secret1;
    float secret2;
    char secret3;

public:
    MyClass(int s1, float s2, char s3) : secret1(s1), secret2(s2), secret3(s3) {}

    void printMembers() const {
        std::cout << "secret1: " << secret1 << "\n";
        std::cout << "secret2: " << secret2 << "\n";
        std::cout << "secret3: " << secret3 << "\n";
    }
};


int main() {
    MyClass obj(42, 3.14f, 'A');
    // Esta línea causará un error de compilación
    std::cout << obj.secret1 << std::endl;

    obj.printMembers();  // Método público para mostrar los valores
    return 0;
}
```
Al compilar el primer programa, obtendrás un error de compilación. La línea que causa el problema es std::cout << obj.secret1 << std::endl;. El compilador detiene el proceso porque el miembro secret1 es privado (private). Esto significa que solo puede ser accedido desde dentro de la clase MyClass, y la función main no forma parte de esa clase. Este error es una demostración directa del encapsulamiento en acción, impidiendo el acceso no autorizado a los datos internos de la clase.

```
#include <iostream>

class MyClass {
private:
    int secret1;
    float secret2;
    char secret3;

public:
    MyClass(int s1, float s2, char s3) : secret1(s1), secret2(s2), secret3(s3) {}

    void printMembers() const {
        std::cout << "secret1: " << secret1 << "\n";
        std::cout << "secret2: " << secret2 << "\n";
        std::cout << "secret3: " << secret3 << "\n";
    }
};

int main() {
    MyClass obj(42, 3.14f, 'A');

    // Usando reinterpret_cast para violar el encapsulamiento
    int* ptrInt = reinterpret_cast<int*>(&obj);
    float* ptrFloat = reinterpret_cast<float*>(ptrInt + 1);
    char* ptrChar = reinterpret_cast<char*>(ptrFloat + 1);

    // Accediendo y mostrando los valores privados
    std::cout << "Accediendo directamente a los miembros privados:\n";
    std::cout << "secret1: " << *ptrInt << "\n";       // Accede a secret1
    std::cout << "secret2: " << *ptrFloat << "\n";     // Accede a secret2
    std::cout << "secret3: " << *ptrChar << "\n";      // Accede a secret3

    return 0;
}
```

al compilar y ejecutar el segundo programa, este se ejecutara exitosamente y mostrara los valores de los miembros privados. esto es posible porque el codigo utiliza reinterpret_cast para manipular directamente los punteros de memoria, eludiendo las reglas de acceso del compilador.

conclusion del experimento
la principal conclusion es que el encapsulamiento es una proteccion a nivel de compilacion, no a nivel de ejecucion. el compilador de c++ es el que hace cumplir las reglas de acceso (private, public, protected). sin embargo, estas reglas no son una barrera fisica en la memoria. si un programador es lo suficientemente habil (o imprudente) y utiliza herramientas como reinterpret_cast, puede sortear la proteccion del lenguaje. esto subraya que el encapsulamiento es una buena practica de diseño para prevenir errores y mantener la integridad del codigo, pero no es una medida de seguridad absoluta contra un programador que intencionalmente quiere acceder a los datos.

¿que es el encapsulamiento y por que es importante?
en mis propias palabras, el encapsulamiento es la practica de agrupar los datos (atributos) y los metodos (funciones) que operan sobre esos datos en una unica unidad, la clase. su proposito principal es proteger los datos internos del acceso externo y del manejo indebido. es como la capsula de una pastilla, que contiene el ingrediente activo (los datos) y la libera de forma controlada (a traves de los metodos publicos) para evitar efectos secundarios no deseados.

es importante por las siguientes razones:

seguridad: previene la corrupcion de datos al impedir la manipulacion directa de los miembros privados de una clase. por ejemplo, en una clase que gestiona las calificaciones de un estudiante, el encapsulamiento asegura que una nota no pueda ser un valor negativo.

abstraccion: oculta la complejidad interna. los usuarios de una clase solo necesitan saber que metodos publicos existen para interactuar con ella, sin tener que preocuparse por como se implementan los datos o la logica interna.

mantenibilidad y flexibilidad: permite cambiar la implementacion interna de una clase (por ejemplo, el tipo de dato de un miembro) sin afectar a otras partes del codigo que la utilizan, siempre y cuando la interfaz publica permanezca igual. esto hace que el codigo sea mas robusto y facil de evolucionar.

###  captura de nuevo la memoria que ocupa el objeto CircularExplosion compara la jerarquía de clases con los campos en memoria del objeto. ¿Qué puedes observar? ¿Qué información te proporciona el depurador? ¿Qué puedes concluir?

Al capturar la memoria de un objeto CircularExplosion con el depurador, se puede observar una correspondencia directa entre la jerarquía de herencia y el diseño del objeto en memoria.

Jerarquía de clases: Particle -> ExplosionParticle -> CircularExplosion

Observación en la memoria:

El objeto CircularExplosion tiene un puntero a la tabla de funciones virtuales (vtable) de su clase, que es el primer elemento en memoria.

Justo después del vptr, se encuentran los campos heredados de la clase ExplosionParticle: position, velocity, color, age, lifetime y size.

La clase CircularExplosion en sí misma no tiene campos de datos adicionales, pero su constructor inicializa los campos de su clase base.

Información del depurador:
El depurador muestra esta estructura de forma clara. La ventana de "Autos" o "Locals" te permite expandir el objeto y ver tanto sus campos como los heredados de la clase base ExplosionParticle. La ventana de "Memory" confirma que los datos se almacenan de forma contigua, con los campos de la clase base ExplosionParticle inmediatamente después del vptr y antes de cualquier campo propio de CircularExplosion.

Conclusión:
La herencia en C++ se implementa a través de la composición de subobjetos. Cuando creas una instancia de una clase derivada, el compilador crea un objeto que es la combinación de los campos de todas sus clases base y sus propios campos, en un solo bloque de memoria contiguo. El puntero this siempre apunta al inicio de este bloque, permitiendo acceder a todos los miembros de la jerarquía

### ¿Cómo se implementa la herencia en C++?

La herencia se implementa en C++ de la siguiente manera:

Subobjetos de clase base: Cada objeto de una clase derivada contiene un subobjeto de su clase base. La memoria para el subobjeto de la clase base se asigna antes que la memoria para los miembros de la clase derivada. Esto garantiza que la herencia se traduzca en una estructura de datos jerárquica y coherente en la memoria.

Puntero this: Cuando llamas a un método de la clase base desde un objeto de la clase derivada, el compilador ajusta automáticamente el puntero this para que apunte al subobjeto de la clase base, permitiendo un acceso transparente a sus miembros.

vtable (Tablas de Funciones Virtuales): Si la herencia es polimórfica (es decir, si hay funciones virtuales), cada objeto tiene un puntero a una vtable de su tipo real, lo que habilita el enlace dinámico y garantiza que el método correcto se llame en tiempo de ejecución.

### C++ permite hacer algo que C# no: herencia múltiple. Realiza un experimento que te permita ver cómo se objeto en memoria cuya clase base tiene herencia múltiple.

A diferencia de C#, C++ permite la herencia múltiple, donde una clase puede heredar de varias clases base. Esto tiene un impacto interesante en la memoria del objeto.

Experimento:
Para ver esto, puedes crear una clase que herede de dos o más clases base. Por ejemplo:

```
class Base1 {
public:
    int b1;
};

class Base2 {
public:
    float b2;
};

class Derived : public Base1, public Base2 {
public:
    char d;
};

// En tu función main
Derived obj;
obj.b1 = 10;
obj.b2 = 20.5f;
obj.d = 'C';
```
Observación en el depurador:
Al inspeccionar un objeto de tipo Derived en la memoria, observarás que la memoria no es solo un bloque, sino que contiene los subobjetos de ambas clases base en un orden específico. La vtable es algo más compleja si las clases base también tienen métodos virtuales. Los campos de la primera clase base (b1) se almacenan primero, seguidos por los campos de la segunda clase base (b2), y finalmente los campos de la clase derivada (d).

Conclusión:
El compilador organiza los subobjetos de las clases base en la memoria en el orden en que fueron declaradas en la herencia. Este mecanismo, aunque poderoso, puede llevar a complejidades como el "diamante de la muerte" si no se maneja con cuidado, ya que puede resultar en ambigüedades cuando se accede a miembros de una clase base común. La herencia múltiple es una característica de C++ que muestra cómo el lenguaje resuelve la necesidad de combinar funcionalidades de múltiples fuentes en un solo objeto.

### ¿Qué relación existe entre los métodos virtuales y el polimorfismo?
La relación es fundamental y directa:

Los métodos virtuales son el habilitador clave del polimorfismo dinámico.

Sin métodos virtuales: Si un método no es virtual, la llamada a ese método se resuelve en tiempo de compilación (enlace estático) basándose en el tipo del puntero o referencia. Esto significa que si tienes un Animal* miAnimal = new Perro(); y hacerSonido() no es virtual, miAnimal->hacerSonido() siempre llamaría a Animal::hacerSonido() (si existiera una implementación en Animal), ignorando la implementación de Perro.

Con métodos virtuales: Al declarar un método como virtual en la clase base, le estás diciendo al compilador que la llamada a ese método debe resolverse en tiempo de ejecución (enlace dinámico) basándose en el tipo real del objeto, no en el tipo del puntero o referencia. Es precisamente la existencia de estos métodos virtuales lo que obliga al compilador a crear y utilizar el mecanismo de la vtable para cada clase involucrada.

En resumen, los métodos virtuales son la condición necesaria para que el compilador implemente el polimorfismo dinámico a través de la vtable, permitiendo que el mismo código (miAnimal->hacerSonido()) tenga un comportamiento diferente según el objeto subyacente (Perro o Gato).

## 3.

Modificaciones en ofApp.h.

```
#pragma once
#include "ofMain.h"
#include <vector>

// ... (todas tus clases Particle, RisingParticle, etc.) ...

// Agrega las nuevas clases aquí

class GravityParticle : public ExplosionParticle {
    // ... (el código de la clase) ...
};

class FadingParticle : public ExplosionParticle {
    // ... (el código de la clase) ...
};

class VortexExplosion : public ExplosionParticle {
    // ... (el código de la clase) ...
};

class ofApp : public ofBaseApp {
// ...
};
```
Modificaciones en ofApp.cpp

```
void ofApp::update() {
    float dt = ofGetLastFrameTime();
    
    // ... (tu lógica de actualización existente) ...

    for (int i = particles.size() - 1; i >= 0; i--) {
        if (particles[i]->shouldExplode()) {
            int explosionType = (int)ofRandom(4);
            int numParticles = (int)ofRandom(20, 30);
            for (int j = 0; j < numParticles; j++) {
                if (explosionType == 0) {
                    particles.push_back(new CircularExplosion(particles[i]->getPosition(), particles[i]->getColor()));
                } else if (explosionType == 1) {
                    particles.push_back(new RandomExplosion(particles[i]->getPosition(), particles[i]->getColor()));
                } else if (explosionType == 2) {
                    particles.push_back(new StarExplosion(particles[i]->getPosition(), particles[i]->getColor()));
                } else {
                    particles.push_back(new VortexExplosion(particles[i]->getPosition(), particles[i]->getColor()));
                }
            }
            delete particles[i];
            particles.erase(particles.begin() + i);
        }
        // ... (el resto de tu lógica para eliminar partículas muertas) ...
    }
}

void ofApp::createRisingParticle() {
    // ... (tu lógica existente) ...

    int particleType = (int)ofRandom(3);
    if (particleType == 0) {
        particles.push_back(new RisingParticle(pos, vel, col, lifetime));
    } else if (particleType == 1) {
        particles.push_back(new GravityParticle(pos, col));
    } else {
        particles.push_back(new FadingParticle(pos, col));
    }
}
```

####  Nuevos tipos de `Particle`

1.  **Clase `GravityParticle`**: Esta partícula se lanzará en una dirección aleatoria y será afectada por una fuerza de gravedad. Con el tiempo, su velocidad vertical se invertirá, haciendo que su trayectoria sea un arco descendente.
    * **¿Cómo?** Se creará una nueva clase `GravityParticle` que hereda de `ExplosionParticle`. En su método `update`, se añadirá una fuerza de gravedad que incremente continuamente la componente `y` de la velocidad.
    * **¿Por qué?** Esto diversifica el comportamiento de las partículas iniciales, ofreciendo un efecto de "fuegos artificiales errantes" que se elevan y luego caen, lo que enriquece la simulación.

2.  **Clase `FadingParticle`**: Esta partícula no se verá afectada por la gravedad. Se moverá en línea recta y su opacidad (`alpha`) disminuirá gradualmente con el tiempo hasta desaparecer por completo.
    * **¿Cómo?** Se creará la clase `FadingParticle` que hereda de `ExplosionParticle`. En su constructor, se establecerá una velocidad constante y un tiempo de vida. En el método `update`, se mapeará la opacidad en función de la edad de la partícula.
    * **¿Por qué?** Permite crear efectos visuales más sutiles y de corta duración, como estelas o chispas de una explosión, que complementan los efectos más dramáticos.

#### b) Nuevo modo de explosión

1.  **Clase `VortexExplosion`**: Las partículas de esta explosión no se dispersarán de forma lineal, sino que orbitarán alrededor de un punto central mientras se desvanecen.
    * **¿Cómo?** Se creará la clase `VortexExplosion` que hereda de `ExplosionParticle`. En su constructor, se calculará una velocidad que combine un vector de dirección radial con un componente tangencial. En el método `update`, se ajustará continuamente el vector de velocidad para simular un efecto de torbellino.
    * **¿Por qué?** Introduce una dinámica de movimiento compleja que no se consigue con las explosiones existentes (circular, aleatoria, estrella). Esto añade una nueva capa de complejidad y realismo a la simulación.


### 2. Conceptos de POO en el Código

Los conceptos de encapsulamiento, herencia y polimorfismo son la base de estas extensiones.

* **Encapsulamiento**: Los miembros de las nuevas clases (`position`, `velocity`, `color`, etc.) se mantendrán como `protected` o `private`. Por ejemplo, la lógica de actualización del `VortexExplosion` está encapsulada dentro de su método `update`, y solo se expone a través de la interfaz pública de la clase. Esto protege la lógica de simulación y evita que se manipule directamente.
* **Herencia**: Las nuevas clases `GravityParticle`, `FadingParticle` y `VortexExplosion` heredarán de la clase base `ExplosionParticle` (que a su vez hereda de `Particle`). Esta herencia nos permite **reutilizar código** y propiedades comunes (posición, color, tiempo de vida) sin tener que redefinirlas en cada clase.
* **Polimorfismo**: Esta es la clave. La lista `std::vector<Particle*> particles` puede contener instancias de `RisingParticle`, `CircularExplosion`, `VortexExplosion`, o cualquier otra partícula que creemos. Cuando el bucle de actualización llama a `particles[i]->update()` o `particles[i]->draw()`, el polimorfismo garantiza que se ejecute la versión **correcta** del método para cada tipo de partícula. .


### 3. Verificación y Evidencia

Para verificar que las extensiones funcionan correctamente, se utilizará un enfoque paso a paso, con el uso del depurador para capturar evidencia.

1.  **Verificación de `GravityParticle`**: Se agregará un *breakpoint* en el método `update` de la nueva clase. Al ejecutar el programa, se inspeccionará la variable `velocity` en cada fotograma. Se espera que la componente `y` de la velocidad (`velocity.y`) aumente con el tiempo, lo que visualmente hará que la partícula se desacelere en su ascenso y luego comience a caer.
    * **Captura de depurador**: Se mostrará una captura de la ventana de variables con la velocidad de la partícula en dos fotogramas distintos, evidenciando el cambio.

2.  **Verificación del polimorfismo**: Esta es la prueba más importante.
    * **Escenario**: Se ejecutará el programa en modo depuración. En el método `ofApp::update()`, se colocará un *breakpoint* en la línea `particles[i]->update(dt)`.
    * **Análisis**: Al detener la ejecución, se inspeccionará la variable `particles[i]`. En la ventana del depurador, se verá el **tipo real** del objeto (por ejemplo, `CircularExplosion*` o `VortexExplosion*`), a pesar de que el puntero es de tipo `Particle*`. Lo más importante, al expandir el objeto, se observará que el puntero a la tabla de funciones virtuales (`_vptr`) apunta a la `vtable` correcta para el tipo de objeto.
    * **Captura de depurador**: Se capturará la pantalla mostrando la ventana de "Locals" o "Autos" con el `_vptr` expandido, evidenciando que el puntero de la función `update` o `draw` apunta a la implementación específica de `VortexExplosion`. Esta es la prueba concreta de que el polimorfismo está funcionando como se espera. .

## 4.  **Consolidación, autoevaluación y cierre:**

lo que puedo concluir de este trabajo es que es una buena practica de repaso de conceptos de c#, pero al mismo se aprende mas del funcionamiento interno de los objetos y otros conceptos, aunque n pude finalizar al cien este trabajo siento que hice gran parte del trabajo de analisis por lo que desde mi perspectiva tomando en cuenta mi aprendisaje y tiempo de trabajo dira que mi **nota: 4.5**
