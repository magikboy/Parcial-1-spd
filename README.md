##Documentación de la parte práctica del primer parcial para la materia Sistemas de procesamiento de datos - UTN Tecnicatura Superior en Programación.
##Sistema de Procesamiento de Datos (SPD)

## Modelo de montacarga funcional

![Semáforos para no videntes](https://github.com/magikboy/Parcial-1/blob/1a975207471b0b0f8a8c081eb3d869e3463c76a1/tinkercad1.png)

##Consigna Montacargas:
Se nos pide armar un modelo de montacarga funcional como maqueta para un hospital. El
objetivo es que implementes un sistema que pueda recibir ordenes de subir, bajar o pausar
desde diferentes pisos y muestre el estado actual del montacargas en el display 7 segmentos

## Función principal

``` C++
#define BOTON_SUBIR 2
#define BOTON_BAJAR 3
#define BOTON_PAUSAR 4
#define led_Verde 5
#define led_Rojo 6
#define A 7
#define B 8
#define C 9
#define D 10
#define E 11
#define F 12
#define G 13
const int TIEMPO_ESPERA_BOTON = 10; // Tiempo de espera entre lecturas de botones en milisegundos.
const int TIEMPO_POR_PISO = 1000; // Tiempo que tarda el montacargas en llegar a cada piso en milisegundos.
const int TIEMPO_ESPERA_MOVIMIENTO = 1000; // Tiempo de espera después de que se mueve el montacargas en milisegundos.

boolean botonSubir = false;
boolean botonBajar = false;
boolean botonPausa = false;
boolean enMovimiento = false;

int contador = 0; //INICIALIZO EL CONTADOR EN 0
String mensaje = ""; //PARA PODER ESCRIBIR EN EL MONITOR

const int LED_ROJO_PIN = 5;
const int LED_VERDE_PIN = 6;
const char* mensajesPisos[] = {
  "Llego al piso 0.",
  "Llego al piso 1.",
  "Llego al piso 2.",
  "Llego al piso 3.",
  "Llego al piso 4.",
  "Llego al piso 5.",
  "Llego al piso 6.",
  "Llego al piso 7.",
  "Llego al piso 8.",
  "Llego al piso 9."
};

void mostrarPiso(int piso) {
switch(piso) {
  case 0:
  	cero(1);
  	break;
  case 1:
  	uno(1);
  	break;
  case 2:
    dos(1);
    break;
  case 3:
    tres(1);
    break;
  case 4:
    cuatro(1);
    break;
  case 5:
    cinco(1);
    break;
  case 6:
    seis(1);
    break;
  case 7:
    siete(1);
    break;
  case 8:
    ocho(1);
    break;
  case 9:
    nueve(1);
    break;
}
mensaje = mensajesPisos[piso];
}

void cambiarPiso(String direccion) {
  if (direccion == "subir" && contador < 9) {
    contador++;
  }
  else if (direccion == "bajar" && contador > 0) {
    contador--;
  }
}

int moverPiso(String subirBajar, int tiempoDelay)
{
  digitalWrite(led_Rojo, 0);
  cambiarPiso(subirBajar);
  mostrarPiso(contador);
  digitalWrite(led_Verde, 1);
  delay(tiempoDelay);
  digitalWrite(led_Verde , 0);
  displayOff();
  Serial.println(mensaje);
  return contador;
}

// FUNCIONES
void displayOff() // Apago display al salir del switch
{
  digitalWrite(A, LOW);
  digitalWrite(B, LOW);
  digitalWrite(C, LOW);
  digitalWrite(D, LOW);
  digitalWrite(E, LOW);
  digitalWrite(F, LOW);
  digitalWrite(G, LOW);
}

void cero(int on)
{
  digitalWrite(A, HIGH);
  digitalWrite(B, HIGH);
  digitalWrite(C, HIGH);
  digitalWrite(D, HIGH);
  digitalWrite(E, HIGH);
  digitalWrite(F, HIGH);
  digitalWrite(G, LOW);
}

void uno(int on)
{
  digitalWrite(A, LOW);
  digitalWrite(B, HIGH);
  digitalWrite(C, HIGH);
  digitalWrite(D, LOW);
  digitalWrite(E, LOW);
  digitalWrite(F, LOW);
  digitalWrite(G, LOW);
}

void dos(int on)
{
  digitalWrite(A, HIGH);
  digitalWrite(B, HIGH);
  digitalWrite(C, LOW);
  digitalWrite(D, HIGH);
  digitalWrite(E, HIGH);
  digitalWrite(F, LOW);
  digitalWrite(G, HIGH);
}

void tres(int on)
{
  digitalWrite(A, HIGH);
  digitalWrite(B, HIGH);
  digitalWrite(C, HIGH);
  digitalWrite(D, HIGH);
  digitalWrite(E, LOW);
  digitalWrite(F, LOW);
  digitalWrite(G, HIGH);
}

void cuatro(int on)
{
  digitalWrite(A, LOW);
  digitalWrite(B, HIGH);
  digitalWrite(C, HIGH);
  digitalWrite(D, LOW);
  digitalWrite(E, LOW);
  digitalWrite(F, HIGH);
  digitalWrite(G, HIGH);
}

void cinco(int on)
{
  digitalWrite(A, HIGH);
  digitalWrite(B, LOW);
  digitalWrite(C, HIGH);
  digitalWrite(D, HIGH);
  digitalWrite(E, LOW);
  digitalWrite(F, HIGH);
  digitalWrite(G, HIGH);
}

void seis(int on)
{
  digitalWrite(A, HIGH);
  digitalWrite(B, LOW);
  digitalWrite(C, HIGH);
  digitalWrite(D, HIGH);
  digitalWrite(E, HIGH);
  digitalWrite(F, HIGH);
  digitalWrite(G, HIGH);
}

void siete(int on)
{
  digitalWrite(A, HIGH);
  digitalWrite(B, HIGH);
  digitalWrite(C, HIGH);
  digitalWrite(D, LOW);
  digitalWrite(E, LOW);
  digitalWrite(F, LOW);
  digitalWrite(G, LOW);
}

void ocho(int on)
{
  digitalWrite(A, HIGH);
  digitalWrite(B, HIGH);
  digitalWrite(C, HIGH);
  digitalWrite(D, HIGH);
  digitalWrite(E, HIGH);
  digitalWrite(F, HIGH);
  digitalWrite(G, HIGH);
}

void nueve(int on)
{
  digitalWrite(A, HIGH);
  digitalWrite(B, HIGH);
  digitalWrite(C, HIGH);
  digitalWrite(D, HIGH);
  digitalWrite(E, LOW);
  digitalWrite(F, HIGH);
  digitalWrite(G, HIGH);
}

void todos(int on)
{
  digitalWrite(A, HIGH);
  digitalWrite(B, HIGH);
  digitalWrite(C, HIGH);
  digitalWrite(D, HIGH);
  digitalWrite(E, HIGH);
  digitalWrite(F, HIGH);
  digitalWrite(G, HIGH);
}

void actualizarDisplay(int piso) {
  switch (piso) {
    case 1:
      digitalWrite(A, HIGH);
      digitalWrite(B, HIGH);
      digitalWrite(C, HIGH);
      digitalWrite(D, HIGH);
      digitalWrite(E, HIGH);
      digitalWrite(F, HIGH);
      digitalWrite(G, LOW);
      break;
    case 2:
      digitalWrite(A, LOW);
      digitalWrite(B, HIGH);
      digitalWrite(C, HIGH);
      digitalWrite(D, LOW);
      digitalWrite(E, LOW);
      digitalWrite(F, LOW);
      digitalWrite(G, LOW);
      break;
    case 3:
      digitalWrite(A, HIGH);
      digitalWrite(B, HIGH);
      digitalWrite(C, HIGH);
      digitalWrite(D, HIGH);
      digitalWrite(E, LOW);
      digitalWrite(F, LOW);
      digitalWrite(G, HIGH);
      break;
    case 4:
      digitalWrite(A, LOW);
      digitalWrite(B, HIGH);
      digitalWrite(C, HIGH);
      digitalWrite(D, LOW);
      digitalWrite(E, LOW);
      digitalWrite(F, HIGH);
      digitalWrite(G, HIGH);
      break;
    case 5:
      digitalWrite(A, HIGH);
      digitalWrite(B, LOW);
      digitalWrite(C, HIGH);
      digitalWrite(D, HIGH);
      digitalWrite(E, LOW);
      digitalWrite(F, HIGH);
      digitalWrite(G, HIGH);
      break;
    case 6:
      digitalWrite(A, HIGH);
      digitalWrite(B, LOW);
      digitalWrite(C, HIGH);
      digitalWrite(D, HIGH);
      digitalWrite(E, HIGH);
      digitalWrite(F, HIGH);
      digitalWrite(G, HIGH);
      break;
    case 7:
      digitalWrite(A, HIGH);
      digitalWrite(B, HIGH);
      digitalWrite(C, HIGH);
      digitalWrite(D, LOW);
      digitalWrite(E, LOW);
      digitalWrite(F, LOW);
      digitalWrite(G, LOW);
      break;
    case 8:
      digitalWrite(A, HIGH);
      digitalWrite(B, HIGH);
      digitalWrite(C, HIGH);
      digitalWrite(D, HIGH);
      digitalWrite(E, HIGH);
      digitalWrite(F, HIGH);
      digitalWrite(G, HIGH);
      break;
    case 9:
      digitalWrite(A, HIGH);
      digitalWrite(B, HIGH);
      digitalWrite(C, HIGH);
      digitalWrite(D, HIGH);
      digitalWrite(E, LOW);
      digitalWrite(F, HIGH);
      digitalWrite(G, HIGH);
      break;
  }
}
// FIN FUNCIONES

void setup() {
pinMode(BOTON_SUBIR, INPUT_PULLUP);
pinMode(BOTON_BAJAR, INPUT_PULLUP);
pinMode(BOTON_PAUSAR, INPUT_PULLUP);
pinMode(led_Rojo, OUTPUT);
pinMode(led_Verde, OUTPUT);
pinMode(A, OUTPUT);
pinMode(B, OUTPUT);
pinMode(C, OUTPUT);
pinMode(D, OUTPUT);
pinMode(E, OUTPUT);
pinMode(F, OUTPUT);
pinMode(G, OUTPUT);
Serial.begin(9600);
mostrarPiso(contador);
}

void loop() {
// Leer el estado de los botones
botonSubir = digitalRead(BOTON_SUBIR);
botonBajar = digitalRead(BOTON_BAJAR);
botonPausa = digitalRead(BOTON_PAUSAR);

// Si se presiona el botón de subir, mover hacia arriba
if (botonSubir == LOW) {
moverPiso("subir", TIEMPO_POR_PISO);
}

// Si se presiona el botón de bajar, mover hacia abajo
if (botonBajar == LOW) {
moverPiso("bajar", TIEMPO_POR_PISO);
}

// Si se presiona el botón de pausa, detener el movimiento
if (botonPausa == LOW) {
  mensaje = "El montacargas se detuvo";
  Serial.println(mensaje);
  digitalWrite(led_Verde, 0);
  digitalWrite(led_Rojo, 1);
  delay(TIEMPO_ESPERA_MOVIMIENTO);
  mostrarPiso(contador);
}
}


```

### Explicacion

Enciende y apaga el buzzer junto al led correspondiente durante el tiempo indicado.

Recibe como parametros:
##void prender_led
+ **luz** (el led/pin), de tipo entenro, que va a encender junto a la buzzer.
+ **hz** es el segundo parametro que recibe la funcion **tone** dentro de `SonarBuzzer` que es la frecuencia del tono en Hz.
+ **int leds[]** = {led_rojo, led_naranja, led_azul, led_verde}; son los leds a prender
+ **int numeros[]** = {3, 2, 1, 0}; los casos del display 7 segmentos que tiene que prender
+ **int p = digitalRead(pulsador)** el pulsador que al apretarlo baja la bandera y empieza el bulce

---
## <img src="tinkercad.png" alt="Tinkercad" height="32px"> Link al proyecto

- [Proyecto](https://www.tinkercad.com/things/cn31fUhwE2b)

### Parcial:

[Consignas](https://github.com/magikboy/Parcial-1/blob/02b8c8bd45b8f18107d74b41cb75eaca4d41e1a5/Primer%20Parcial%20SPD%20Parte%20Practica.pdf)
