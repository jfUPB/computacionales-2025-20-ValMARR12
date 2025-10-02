# Bitácora de aprendizaje de la unidad 6

## Actividad 01

### ¿Cómo puedes interactuar con la aplicación? Menciona específicamente las teclas y qué efecto parecen tener sobre las partículas.

La interacción se realiza mediante las siguientes teclas, que cambian el comportamiento de todas las partículas de forma global, a	son atraídas hacia el cursor, r son repelidas por el cursor, s hace que las particulas dejen de moverse, n vuelven a su movimiento inicial de velocidad constante

### ¿Observas los diferentes tipos de “partículas”? ¿Se comportan todas igual inicialmente?

si, se observan tres tipos de partículas, distinguibles por color y tamaño. No se comportan igual inicialmente, las tipo star de color rojo y tamaño pequeño y velocidad baja y constante, las tipo Shooting_Star de color verde y tamaño medio y velocidad tres veces más rápida que las otras y por ultimo las Planet de color azul tamaño grande y velocidad baja y constante

### Toma algunas capturas de pantalla de la aplicación en diferentes momentos (estado inicial, después de presionar ‘a’, ‘r’, ‘s’, ‘n’) y añádelas a tu bitácora.

estado incial:
<img width="1919" height="1003" alt="image" src="https://github.com/user-attachments/assets/137ec725-88ae-4b48-857f-fe8e934de2c9" />

preciono a:
<img width="1914" height="1034" alt="image" src="https://github.com/user-attachments/assets/67a2c0fe-a77e-4bb7-8fa1-f9ad359411c8" />

preciono r:
<img width="1912" height="1033" alt="image" src="https://github.com/user-attachments/assets/3e8b7b20-0d1a-4d22-8d5c-770e9252a595" />

preciono s:
<img width="1916" height="1033" alt="image" src="https://github.com/user-attachments/assets/3c9a002c-72ee-498f-927e-b8d316fb8643" />

preciono n:
<img width="1915" height="1031" alt="image" src="https://github.com/user-attachments/assets/8bac93d8-5a61-4404-87a3-471d21e9a1a7" />

### ¿Qué crees que está pasando “detrás de cámaras” cuando presionas las teclas? Formula una hipótesis inicial sobre cómo la aplicación cambia el comportamiento de las partículas.

al presionar una tecla:

la clase ofApp actúa como un Sujeto y emite una notificación

todas las partículas, actuando como observadores, reciben esta notificación.

cada partícula reacciona a la notificación y reemplaza su objeto de comportamiento interno (patrón State) por uno nuevo, por ejemplo, al presionar 'a', la partícula cambia su objeto de estado de NormalState a AttractState.

en el siguiente ciclo de update, la partícula delega la lógica de movimiento al nuevo objeto de estado, cambiando su comportamiento instantáneamente.

## Actividad 02

### Explica con tus propias palabras el propósito del patrón Observer. ¿Qué problema resuelve?

el patron observer establece una relación de dependencia uno-a-muchos donde un objeto notifica automáticamente a una lista de objeto cuando su estado cambia. El propósito es desacoplar al sujeto de sus observadores. Resuelve el problema de que el sujeto tenga que conocer y llamar métodos específicos en clases concretas. El sujeto solo interactúa con la interfaz genérica observer, haciendo el código más flexible y fácil de extender.

### Dibuja un diagrama que muestre la relación entre Subject, Observer, ofApp y Particle en el caso de estudio, indicando quién es el Sujeto y quiénes los Observadores.

### Construye un diagrama de secuencia que muestre cómo funciona el patrón Observer al presionar una tecla.

### ¿Qué ventajas crees que ofrece usar el patrón Observer en esta aplicación en comparación con, por ejemplo, que ofApp::update recorriera todas las partículas y les dijera directamente que cambien su comportamiento basado en una variable global? Piensa en términos de acoplamiento y extensibilidad.

Ofrece ventajas en acoplamiento y extensibilidad:

Desacoplamiento: ofApp no necesita saber cómo la partícula cambia su comportamiento (si usa setState o si tiene un color interno). Simplemente dice: "Ha ocurrido un evento 'attract'". Esto aísla a ofApp de los detalles internos de Particle.

Extensibilidad: Si se añade un nuevo objeto que deba reaccionar a las teclas (ej. un contador de FPS), solo necesita implementar Observer y registrarse en ofApp. No se necesita modificar el código de ofApp::keyPressed(), cumpliendo el Principio Abierto/Cerrado.

## Actividad 03

### Explica con tus propias palabras el propósito del patrón Factory Method (o Simple Factory, en este caso). ¿Qué problema principal aborda en la creación de objetos?

el patron Factory centraliza y encapsula la lógica de creación de objetos. Aborda el problema del acoplamiento entre el código cliente y las clases concretas con sus reglas de inicialización. El cliente solo solicita un objeto por su tipo y la Factory se encarga de llamar a new Particle() y aplicar todas sus propiedades (size, color, velocity).

### ¿Qué ventajas aporta el uso de ParticleFactory en ofApp::setup en comparación con instanciar y configurar las partículas directamente allí? Piensa en términos de organización del código (SRP - Single Responsibility Principle), legibilidad y facilidad para añadir nuevos tipos de partículas en el futuro.

SRP (Single Responsibility Principle): La Factory es la única responsable de conocer cómo construir cada tipo de partícula. ofApp::setup solo es responsable de orquestar la aplicación.

Legibilidad: ofApp::setup es más limpio, llamando a createParticle en lugar de tener múltiples líneas de configuración por cada tipo.

Extensibilidad: Para añadir un nuevo tipo de partícula, solo se modifica ParticleFactory::createParticle (se añade un else if). La lógica existente de ofApp se mantiene sin cambios, reduciendo el riesgo de errores.

### Imagina que quieres añadir un nuevo tipo de partícula llamada "black_hole" que tiene tamaño grande, color negro y velocidad muy lenta. Describe los pasos que necesitarías seguir para implementar esto utilizando la ParticleFactory existente. ¿Tendrías que modificar ofApp::setup? ¿Por qué sí o por qué no?

Modificar ParticleFactory::createParticle: Añadir un nuevo else if para la clave "black_hole" con las configuraciones deseadas (size grande, color negro, velocity lenta).

¿Modificar ofApp::setup? Sí, solo para llamar a la Factory. Se añadiría un bucle for llamando a ParticleFactory::createParticle("black_hole"). No se modificaría la lógica de creación, solo la lógica de solicitud de objetos.

### El método createParticle en el ejemplo es estático. ¿Qué implicaciones (ventajas/desventajas) tiene esto comparado con tener una instancia de ParticleFactory y un método de instancia createParticle()?.

El uso de un método estático (Simple Factory) es:

Ventaja: Es muy simple y rápido de usar (ParticleFactory::createParticle) sin necesidad de instanciar la clase Factory.

Desventaja: Pierde Polimorfismo. No se puede aplicar el patrón Factory Method completo (subclases de Factory que crean objetos). Es más difícil de probar unitariamente. En este caso simple, la ventaja de la sencillez prevalece.

## Actividad 04

### Explica con tus propias palabras el propósito del patrón State. ¿Cuándo es útil aplicarlo?

Permite que un objeto cambie su comportamiento cuando su estado interno cambia, haciendo que el objeto parezca cambiar de clase. El patrón encapsula cada comportamiento en una clase separada. Es útil cuando:

El comportamiento de un objeto depende de una variable de estado.

Hay muchos bloques if/else/switch en la clase principal que seleccionan el comportamiento. El patrón reemplaza estas condiciones con delegación a objetos.

### Dibuja un diagrama de estados simple para la clase Particle. Muestra los diferentes estados (Normal, Attract, Repel, Stop) como nodos y las transiciones entre ellos como flechas etiquetadas con el evento que las causa (p. ej., la tecla presionada: ‘n’, ‘a’, ‘r’, ‘s’).

### Describe las ventajas de usar el patrón State en Particle en lugar de tener un miembro std::string estadoActual y usar un gran if/else if/else o switch dentro de Particle::update() para cambiar el comportamiento. Piensa en cohesión, extensibilidad (añadir nuevos estados) y el Principio Abierto/Cerrado (Open/Closed Principle).

Cohesión
Alta: La lógica de cada movimiento está aislada en su propia clase de estado (ej. AttractState).
Baja: Toda la lógica de movimiento está mezclada en un único método (Particle::update).

Extensibilidad 	
Respeta OCP: Para añadir un nuevo comportamiento (FastState), solo se crea una nueva clase de estado. No se modifica Particle::update().	
Viola OCP: Hay que modificar el switch dentro de Particle::update() cada vez que se añade un estado, introduciendo riesgo.

## ¿Qué responsabilidad tienen los métodos onEnter y onExit en el patrón State? Proporciona un ejemplo de por qué podrían ser útiles (incluso si no se usan mucho en todos los estados de este caso de estudio). Por ejemplo, ¿Qué podrías hacer en onEnter para AttractState o en onExit para StopState?

Estos métodos gestionan las acciones de configuración y limpieza que solo deben ejecutarse una vez al cambiar de estado, no en cada fotograma (update).

onEnter: Inicializa valores, ajusta propiedades para el nuevo estado.

Ejemplo para AttractState: Podrías cambiar el color de la partícula a amarillo en onEnter para indicar visualmente el estado.

onExit: Limpia o asegura condiciones al salir del estado.

Ejemplo para StopState: Podrías asegurar que la velocidad de la partícula quede exactamente a cero en onExit para evitar cualquier movimiento residual antes de pasar al siguiente estado.

## Actividad 05

### El código fuente completo de tu proyecto openFrameworks.

ofApp.h

```
#pragma once

#include "ofMain.h"
#include <string>
#include <vector>

class Observer {
public:
    virtual ~Observer() = default;
    virtual void onNotify(const std::string & event) = 0;
};

class Subject {
public:
    void addObserver(Observer * observer);
    void removeObserver(Observer * observer);

protected:
    void notify(const std::string & event);

private:
    std::vector<Observer *> observers;
};

class Particle;

class State {
public:
    virtual ~State() = default;
    virtual void update(Particle * particle) = 0;
    virtual void onEnter(Particle * particle) { }
    virtual void onExit(Particle * particle) { }
};

class Particle : public Observer {
public:
    Particle();
    ~Particle() override;

    Particle(const Particle &) = delete;
    Particle & operator=(const Particle &) = delete;

    void update();
    void draw();
    void onNotify(const std::string & event) override;

    void setState(State * newState);

    ofVec2f position;
    ofVec2f velocity;
    float size;
    ofColor color;

private:
    void keepInsideWindow();
    State * state;
};

class NormalState : public State {
public:
    void update(Particle * particle) override;
    void onEnter(Particle * particle) override;
};

class AttractState : public State {
public:
    void update(Particle * particle) override;
};

class RepelState : public State {
public:
    void update(Particle * particle) override;
};

class StopState : public State {
public:
    void update(Particle * particle) override;
};

class FastState : public State {
public:
    void update(Particle * particle) override;
    void onEnter(Particle * particle) override;
};

class ParticleFactory {
public:
    static Particle * createParticle(const std::string & type);
};

class ofApp : public ofBaseApp, public Subject {
public:
    ~ofApp() override;
    void setup() override;
    void update() override;
    void draw() override;
    void keyPressed(int key) override;

private:
    std::vector<Particle *> particles;
};
```
ofApp.cpp

```
#include "ofApp.h"
#include <algorithm>

void Subject::addObserver(Observer * observer) {
    if (!observer) return;
    if (std::find(observers.begin(), observers.end(), observer) == observers.end()) {
        observers.push_back(observer);
    }
}
void Subject::removeObserver(Observer * observer) {
    if (!observer) return;
    observers.erase(std::remove(observers.begin(), observers.end(), observer), observers.end());
}
void Subject::notify(const std::string & event) {
    for (Observer * observer : observers) {
        observer->onNotify(event);
    }
}

Particle::Particle() : state(nullptr) {
    position = ofVec2f(ofRandomWidth(), ofRandomHeight());
    velocity = ofVec2f(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));
    size = ofRandom(2.0f, 5.0f);
    color = ofColor(255);
    state = new NormalState();
    state->onEnter(this);
}
Particle::~Particle() {
    if (state) {
        state->onExit(this);
        delete state;
        state = nullptr;
    }
}
void Particle::setState(State * newState) {
    if (state) {
        state->onExit(this);
        delete state;
    }
    state = newState;
    if (state) {
        state->onEnter(this);
    }
}
void Particle::update() {
    if (state) {
        state->update(this);
    }
    keepInsideWindow();
}
void Particle::draw() {
    ofPushStyle();
    ofSetColor(color);
    ofDrawCircle(position, size);
    ofPopStyle();
}
void Particle::onNotify(const std::string & event) {
    if (event == "attract") {
        setState(new AttractState());
    } else if (event == "repel") {
        setState(new RepelState());
    } else if (event == "stop") {
        setState(new StopState());
    } else if (event == "normal") {
        setState(new NormalState());
    } else if (event == "fast") {
        setState(new FastState());
    }
}
void Particle::keepInsideWindow() {
    const float W = static_cast<float>(ofGetWidth());
    const float H = static_cast<float>(ofGetHeight());
    if (position.x < 0.0f) {
        position.x = 0.0f;
        velocity.x *= -1.0f;
    } else if (position.x > W) {
        position.x = W;
        velocity.x *= -1.0f;
    }
    if (position.y < 0.0f) {
        position.y = 0.0f;
        velocity.y *= -1.0f;
    } else if (position.y > H) {
        position.y = H;
        velocity.y *= -1.0f;
    }
}

void NormalState::onEnter(Particle * particle) {
    particle->velocity.set(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));
}
void NormalState::update(Particle * particle) {
    particle->position += particle->velocity;
}

static void steer(Particle * particle, const ofVec2f & toward, float accel, float vmax, float posScale) {
    ofVec2f dir = toward - particle->position;
    float len = dir.length();
    if (len > 1e-6f) {
        dir /= len;
        particle->velocity += dir * accel;
    }
    particle->velocity.limit(vmax);
    particle->position += particle->velocity * posScale;
}

void AttractState::update(Particle * particle) {
    ofVec2f mouse(ofGetMouseX(), ofGetMouseY());
    steer(particle, mouse, /*accel*/ 0.05f, /*vmax*/ 3.0f, /*posScale*/ 0.2f);
}
void RepelState::update(Particle * particle) {
    ofVec2f mouse(ofGetMouseX(), ofGetMouseY());
    ofVec2f away = particle->position - mouse;
    float len = away.length();
    if (len > 1e-6f) {
        away /= len;
        particle->velocity += away * 0.05f;
    }
    particle->velocity.limit(3.0f);
    particle->position += particle->velocity * 0.2f;
}
void StopState::update(Particle * particle) {
    particle->velocity *= 0.80f;
    if (particle->velocity.lengthSquared() < 1e-4f) {
        particle->velocity.set(0.0f, 0.0f);
    }
    particle->position += particle->velocity;
}

void FastState::onEnter(Particle * particle) {
    if (particle->velocity.lengthSquared() < 1e-4f) {
        particle->velocity.set(ofRandom(-5.0f, 5.0f), ofRandom(-5.0f, 5.0f));
    }
    particle->velocity *= 5.0f; 
}
void FastState::update(Particle * particle) {
    particle->position += particle->velocity;
}

Particle * ParticleFactory::createParticle(const std::string & type) {
    Particle * particle = new Particle();

    if (type == "star") {
        particle->size = ofRandom(2.0f, 4.0f);
        particle->color = ofColor(255, 0, 0);
    } else if (type == "shooting_star") {
        particle->size = ofRandom(3.0f, 6.0f);
        particle->color = ofColor(0, 255, 0);
        particle->velocity *= 3.0f;
    } else if (type == "planet") {
        particle->size = ofRandom(5.0f, 8.0f);
        particle->color = ofColor(0, 0, 255);
    } else if (type == "comet") {
        particle->size = ofRandom(1.5f, 2.5f);
        particle->color = ofColor(0, 255, 255);
        particle->velocity *= 8.0f;
        particle->setState(new FastState());
    }
    return particle;
}

ofApp::~ofApp() {
    for (Particle * p : particles) {
        removeObserver(p);
        delete p;
    }
    particles.clear();
}

void ofApp::setup() {
    ofBackground(0);
    particles.reserve(100 + 5 + 10 + 20); 

    for (int i = 0; i < 100; ++i) {
        Particle * p = ParticleFactory::createParticle("star");
        particles.push_back(p);
        addObserver(p);
    }
    for (int i = 0; i < 5; ++i) {
        Particle * p = ParticleFactory::createParticle("shooting_star");
        particles.push_back(p);
        addObserver(p);
    }
    for (int i = 0; i < 10; ++i) {
        Particle * p = ParticleFactory::createParticle("planet");
        particles.push_back(p);
        addObserver(p);
    }
    for (int i = 0; i < 20; ++i) {
        Particle * p = ParticleFactory::createParticle("comet");
        particles.push_back(p);
        addObserver(p);
    }
}

void ofApp::update() {
    for (Particle * p : particles) {
        p->update();
    }
}

void ofApp::draw() {
    for (Particle * p : particles) {
        p->draw();
    }
}

void ofApp::keyPressed(int key) {
    switch (key) {
    case 's':
        notify("stop");
        break;
    case 'a':
        notify("attract");
        break;
    case 'r':
        notify("repel");
        break;
    case 'n':
        notify("normal");
        break;
    case 'f':
        notify("fast");
        break;
    default:
        break;
    }
}
```

### Explica cómo usaste el patrón Factory para esta nueva partícula.

Utilicé el ParticleFactory modificando el método estático createParticle. Añadí un nuevo bloque else if para manejar la clave "comet".

Responsabilidad de la Factory: La Factory se encarga de crear la partícula y aplicar su configuración única: color cian (ofColor(0, 255, 255)), tamaño pequeño, alta velocidad inicial y, crucialmente, establecer su estado inicial a new FastState().

Ventaja: ofApp::setup solo necesita llamar a ParticleFactory::createParticle("comet"). Esto mantiene la lógica de creación fuera de la clase principal, respetando el Principio de Responsabilidad Única (SRP).

### Describe cómo implementaste el patrón Observer para esta nueva partícula.

El patrón Observer se utilizó para permitir que el ofApp comunique el cambio de estado a todas las Particle cuando el usuario pulsa la nueva tecla.

ofApp: Se añadió el caso 'f' en ofApp::keyPressed para emitir la notificación global: notif

Particle: Se modificó el método Particle::onNotify (el manejador del Observer) para reaccionar a la cadena "fast"

### Explica cómo aplicaste el patrón State a esta nueva partícula.

Se aplicó el patrón State creando la clase FastState que hereda de la clase base State. Esto encapsula el nuevo comportamiento de movimiento.

Comportamiento Encapsulado: El método FastState::update define el movimiento rápido: particle->position += particle->velocity. Este estado ignora las fuerzas de atracción/repulsión que se aplican en otros estados, haciendo que el movimiento sea inalterable.

Transición de Entrada (onEnter): El método FastState::onEnter se utiliza para inicializar una velocidad muy alta (velocity *= 5.0f) cuando la partícula entra en este estado. Esto garantiza una aceleración brusca desde cualquier estado anterior (incluso desde StopState).

Delegación: Particle::update() delega su lógica de movimiento a FastState::update() cuando está activo, siguiendo el principio del patrón State.

# Evaluacion

### 1. Profundidad de la Indagación: 4.0
Las preguntas se responden con síntesis conceptual clara, especialmente en la Actividad 04 (State) y 05 (aplicación). Se explican las interdependencias entre patrones.

### 2. Calidad de la Experimentación: 3.9	
Se realizo la experimentacion en a base (Act. 01) y la implementación y modificación (Act. 05) de forma efectiva y correcta, sin embargo, no logre agregar los diagramas.

### 3. Análisis y Reflexión: 3.5 
La reflexión es superficial en cuanto a la evidencia visual. Se conecta la evidencia a la explicación teórica, y se describen correctamente las ventajas de desacoplamiento (Act. 02 y 03) y extensibilidad (Act. 04). La falta de los diagramas de secuencia y estados resta peso a la profundidad del análisis estructural.

### 4. Apropiación y Articulación de Conceptos: 4.5
con este trabajo he tenido una comprensión clara y correcta de cada patrón. Los conceptos se explican con terminología adecuada (acoplamiento, SRP, OCP, polimorfismo, delegación). Se articula un sistema interdependiente al aplicar los tres patrones juntos en la Actividad 05.

## Nota Calculada: 4.0
