# Evidencias para la unidad 4

## Código

Código para ofApp.h:

``` cpp

#pragma once
#include "ofMain.h"

struct Node {
    float x, y;
    float radius;
    ofColor color;
    float opacity;
    Node* next;

    Node(float _x, float _y, float _radius, ofColor _color, float _opacity)
        : x(_x), y(_y), radius(_radius), color(_color), opacity(_opacity), next(nullptr) {
    }
};

class BrushQueue {
public:
    Node* front;
    Node* rear;
    int size;
    int maxSize;

    BrushQueue(int _maxSize);
    ~BrushQueue();

    void enqueue(float x, float y, float radius, ofColor color, float opacity);
    void dequeue();
    void clear();
    bool isEmpty();
};


BrushQueue::BrushQueue(int _maxSize) : front(nullptr), rear(nullptr), size(0), maxSize(_maxSize) {}

BrushQueue::~BrushQueue() {
    clear();
}

void BrushQueue::enqueue(float x, float y, float radius, ofColor color, float opacity) {
}

void BrushQueue::dequeue() {
}

void BrushQueue::clear() {
}

bool BrushQueue::isEmpty() {
 
}


class ofApp : public ofBaseApp {
public:
    BrushQueue strokes;
    float backgroundHue = 0;

    ofApp() : strokes(50) {} 

    void setup();
    void update();
    void draw();
    void keyPressed(int key);
};
```

Código para ofApp.cpp:

``` cpp

#include "ofApp.h"

void ofApp::setup() {
    ofBackground(0);
}

void ofApp::update() {
    backgroundHue += 0.2;
    if (backgroundHue > 255) backgroundHue = 0;

    if (ofGetMousePressed()) {
        ofColor randomColor(ofRandom(255), ofRandom(255), ofRandom(255));
        float opacity = 255.0;
        strokes.enqueue(ofGetMouseX(), ofGetMouseY(), 10.0, randomColor, opacity);
    }
}

void ofApp::draw() {
    ofColor color1, color2;
    color1.setHsb(backgroundHue, 150, 240);
    color2.setHsb(fmod(backgroundHue + 128, 255), 150, 240);
    ofBackgroundGradient(color1, color2, OF_GRADIENT_LINEAR);

    Node* current = strokes.front;
    int count = 0;
    while (current != nullptr) {
        float opacity = ofMap(count, 0, strokes.size, 0, 255);
        ofSetColor(current->color, opacity);
        ofDrawCircle(current->x, current->y, current->radius);
        current = current->next;
        count++;
    }
}

void ofApp::keyPressed(int key) {
    if (key == 'c') {
        strokes.clear();
    }
    if (key == 'a') {
        if (strokes.maxSize == 50) {
            strokes.maxSize = 100;
        } else {
            strokes.maxSize = 50;
            while (strokes.size > strokes.maxSize) {
                strokes.dequeue();
            }
        }
    } else if (key == 's') {
        ofSaveScreen("screenshot.png");
    }
}
```

Código para main.cpp:
``` cpp

#include "ofMain.h"
#include "ofApp.h"

int main( ){

	ofGLWindowSettings settings;
	settings.setSize(1024, 768);
	settings.windowMode = OF_WINDOW;

	auto window = ofCreateWindow(settings);

	ofRunApp(window, std::make_shared<ofApp>());
	ofRunMainLoop();

}

```

## Demostración:


[Aquí está el video demostrativo de mi aplicación](https://youtu.be/pjkhxT1TZ0s)

