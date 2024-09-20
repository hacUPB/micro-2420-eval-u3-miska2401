[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/tn5SB-Yw)
# Unidad 3
## Documentación del Proyecto
 
Nombre del estudiante:  
ID: 

---

# Actividad 1: Lenguaje C para sistemas embebidos

## **Ejercicio 1**:

### 1. ¿Cuáles son los lenguajes en los que se puede programar sistemas embebidos? Haz un listado.

- C
- C++
- Python (MicroPython)
- Assembly
- Ada
- Rust
- Lua
- Java (usado en ciertos dispositivos embebidos)
- JavaScript (Node.js para algunos sistemas IoT)
- Embedded C++
  
### 2. ¿Qué ventajas y desventajas tienen dichos lenguajes comparados con C?

| Lenguaje     | Ventajas                                                                 | Desventajas                                                         |
|--------------|--------------------------------------------------------------------------|----------------------------------------------------------------------|
| **C**        | Eficiente, bajo nivel, acceso directo a hardware                         | Más complejo para proyectos grandes                                  |
| **C++**      | Orientado a objetos, librerías estándar más amplias                      | Mayor consumo de memoria y recursos                                  |
| **Python**   | Fácil de aprender, interpretado, rápido desarrollo                       | No tan eficiente para sistemas con recursos muy limitados            |
| **Assembly** | Máximo control sobre el hardware, muy eficiente                          | Difícil de mantener, poco portable                                   |
| **Rust**     | Seguridad en memoria, eficiente                                          | No tan maduro en sistemas embebidos, curva de aprendizaje pronunciada|
| **Java**     | Multiplataforma, manejo automático de memoria                            | Alto consumo de recursos para sistemas embebidos                     |

### 3. ¿Existe un ranking de lenguajes para sistemas embebidos?

Sí, existen varios rankings que evalúan los lenguajes de programación para sistemas embebidos. Un ejemplo es el índice TIOBE, que clasifica los lenguajes en función de su popularidad en diversas aplicaciones, incluyendo sistemas embebidos.

Puedes consultar un ranking actualizado en: [**TIOBE Index**](https://www.tiobe.com/tiobe-index/).

Mis percepciones del ranking:
- C y C++ continúan siendo dominantes en sistemas embebidos debido a su cercanía al hardware y su eficiencia.
- Python ha ganado popularidad, especialmente en aplicaciones de prototipado rápido e IoT.

---

## **Ejercicio 2**:

### 1. Macro para aplicar una máscara a un registro del microcontrolador

```c
#define APPLY_MASK(reg, mask) ((reg) |= (mask))
```

Ejemplo de uso: 

```c
// Aplicar una máscara al registro GPIO_PDDR para configurar múltiples pines como salida
APPLY_MASK(GPIO_PDDR, 0x0F);  // Configurar los primeros 4 bits como salidas
```

### 2. Macro para verificar si un periférico está habilitado

```c
#define IS_PERIPHERAL_ENABLED(peripheral_reg, peripheral_bit) ((peripheral_reg) & (1 << (peripheral_bit)))
```

Ejemplo de uso: 

```c
if (IS_PERIPHERAL_ENABLED(PCC_PORTD, 30)) {
    printf("El periférico está habilitado
");
}
```

### 3. Macro para alternar un bit en un registro

```c
#define TOGGLE_BIT(reg, bit) ((reg) ^= (1 << (bit)))
```

Ejemplo de uso:

```c
// Alternar el estado del pin 5 del puerto D
TOGGLE_BIT(GPIO_PDOR, 5);
```

---

## **Ejercicio 3**:

### Errores en el código proporcionado

#### 1. Declaración incorrecta de un entero

```c
int entero = 10.5;  // Esto da un error porque 10.5 es un valor flotante
```

**Solución**:

```c
float entero = 10.5;  // Cambiar la variable a tipo float si queremos un valor decimal
```

#### 2. División entre enteros

```c
float decimal = 3 / 2;  // Esto da como resultado 1 en lugar de 1.5 porque ambos son enteros
```

**Solución**:

```c
float decimal = 3.0 / 2.0;  // Asegurarse de que los números sean flotantes
```

#### 3. Imprimir un float con formato incorrecto

```c
printf("El valor del decimal es: %d
", decimal_1);  // %d es para enteros, no para float
```

**Solución**:

```c
printf("El valor del decimal es: %f
", decimal_1);  // Cambiar a %f para floats
```

#### 4. Asignar un carácter a una cadena

```c
char letra = "A";  // Esto da error porque "A" es una cadena, no un carácter
```

**Solución**:

```c
char letra = 'A';  // Usar comillas simples para caracteres
```

#### 5. Desbordamiento de array

```c
char nombre[5];  
strcpy(nombre, "Henry");  // "Henry" tiene 5 caracteres + 1 para el terminador null
```

**Solución**:

```c
char nombre[6];  // Reservar espacio para el terminador null
```

---

## **Ejercicio 4**:

### Errores identificados y soluciones

#### 1. Bucle infinito en el primer `for`

```c
for (i = 1; i < 10; i--) {  // El bucle nunca termina porque i se decrementa en lugar de incrementarse
```

**Solución**:

```c
for (i = 1; i < 10; i++) {  // Cambiar a incremento
```

#### 2. Acceso fuera del rango del array

```c
for (i = 0; i <= 5; i++) {  // El índice 5 está fuera del rango del array de tamaño 5
```

**Solución**:

```c
for (i = 0; i < 5; i++) {  // Cambiar a < en lugar de <=
```

#### 3. Bucle infinito en `while`

```c
while (num != 0) {
    num = num + 1;  // El valor de num nunca será 0
```

**Solución**:

```c
while (num > 0) { 
    num = num - 1;  // Decrementar num para salir del bucle
```

#### 4. Otro bucle infinito

```c
while (contador < 5) {
    // No se incrementa contador, por lo que el bucle nunca termina
```

**Solución**:

```c
while (contador < 5) {
    printf("Valor de contador: %d
", contador);
    contador++;  // Incrementar contador en cada iteración
```

---

## **Ejercicio 5**:

### Implementación de la función factorial

```c
#include <stdio.h>

int factorial(int n) {
    if (n == 0) {
        return 1;  // Caso base
    } else {
        return n * factorial(n - 1);  // Llamada recursiva
    }
}

int main() {
    int num = 5;
    printf("El factorial de %d es: %d
", num, factorial(num));
    return 0;
}
```

# Ejemplo del SDK
# Ejercicio 1: Análisis de las funciones `GPIO_PinInit()` y `PORT_SetPinMux()`

## `GPIO_PinInit()`
La función `GPIO_PinInit()` se utiliza para inicializar los pines GPIO en el microcontrolador. En este caso, configura un pin específico como entrada o salida digital y asigna un valor inicial de salida si el pin se establece como salida. A continuación, se muestra un desglose de su funcionamiento:

- **Parámetros de entrada**:
  - `base`: Apunta a la base de registros del puerto GPIO.
  - `pin`: Número de pin que se va a inicializar.
  - `config`: Apunta a la estructura que contiene la configuración del pin, como la dirección (entrada o salida) y el valor inicial si es una salida.

- **Proceso**:
  1. Dependiendo de la dirección especificada en `config->pinDirection`, el pin se configura como entrada o salida.
  2. Si es salida, se inicializa el pin con el valor especificado en `config->outputLogic`.

Esta función es útil para definir el comportamiento de los pines GPIO según las necesidades del programa, como encender o apagar un LED o leer el estado de un botón.

## `PORT_SetPinMux()`
La función `PORT_SetPinMux()` configura la funcionalidad de multiplexado de un pin. En los microcontroladores modernos, los pines pueden tener múltiples funciones, como GPIO, funciones especiales o periféricos. Esta función selecciona cuál de esas funciones se asigna al pin.

- **Parámetros de entrada**:
  - `base`: Apunta a la base de registros del puerto de pines (por ejemplo, PORTA, PORTE).
  - `pin`: Número de pin que se va a configurar.
  - `mux`: Selecciona la función que se asignará al pin.

- **Proceso**:
  1. Cambia el valor en el registro de control del pin (PCR) para seleccionar la función adecuada.
  2. Asegura que el pin se configure para la funcionalidad correcta (GPIO, función alternativa, etc.).

En este ejemplo, se utiliza para configurar el pin como GPIO, permitiendo que el LED se controle como una salida digital simple.

# Ejercicio 2

En este ejercicio, vamos a examinar las máscaras utilizadas en la configuración del puerto A en el ejemplo y descubrir qué configuración se realizó.

## Máscaras Utilizadas

Las máscaras que se utilizan para la configuración del puerto A en el ejemplo son las siguientes:

1. **PORT_PCR_PS_MASK**: Esta máscara se utiliza para seleccionar si el pin correspondiente utiliza una resistencia pull-up o pull-down. En este caso, está relacionada con el campo `PS` del registro PCR (Pin Control Register) del puerto A.

   - **PORT_PCR_PS(kPORT_PullDown)**: Selecciona una resistencia pull-down interna en el pin configurado.

2. **PORT_PCR_PE_MASK**: Esta máscara habilita o deshabilita las resistencias internas (pull-up o pull-down) en el pin configurado.

   - **PORT_PCR_PE(kPORT_PullDisable)**: Deshabilita la resistencia pull-up o pull-down interna en el pin configurado.

3. **PORT_PCR_ISF_MASK**: Esta máscara es utilizada para limpiar el flag de estado de interrupción del pin correspondiente.

   - **(~PORT_PCR_ISF_MASK)**: Limpia cualquier interrupción pendiente en el pin configurado.

# Ejercicio 3
Se propone cambiar el puerto de salida del LED (se sustituye el pin 9 del puerto E por el pin 9 del puerto B). Para tal propósito, se realiza el siguiente cambio en el archivo pin_mux.h:

``` C
/*! @name PORTB9 (number 23), USER_LED_2
  @{ */
#define BOARD_INITPINS_LED_RED_GPIO GPIOB /*!<@brief GPIO device name: GPIOB */
#define BOARD_INITPINS_LED_RED_PORT PORTB /*!<@brief PORT device name: PORTB */
#define BOARD_INITPINS_LED_RED_PIN 9U     /*!<@brief PORTB pin index: 9 */
                                          /* @} */
```
Adicionalmente, se implementa un ciclo for tal que el tiempo de encendido y apagado disminuya progresivamente. Se comienza con un tiempo de 2 s, y en cada conmutación de la salida se disminuye en 200 ms. Al llegar a un tiempo de 0 s, se repite el procedimiento. A continuación se muestra la sección de código modificada (pertenece a main):

``` C
for(int i = 2000; i >= 0; i -= 200){
    SysTick_DelayTicks(i);
    GPIO_PortToggle(BOARD_LED_GPIO, 1u << BOARD_LED_GPIO_PIN);
	}
```
