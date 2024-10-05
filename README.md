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

# Proyecto PWM
# Entregable 1: Diagrama de Estados
![Diagrama sin título drawio](https://github.com/user-attachments/assets/eb17d8ac-1b08-4c88-8b77-5b3b89a75767)

# Entregable 2: Código Fuente
```c
/*
 * Todos los derechos reservados.
 *
 * SPDX-License-Identifier: BSD-3-Clause
 */

#include "fsl_debug_console.h"
#include "board.h"
#include "fsl_ftm.h"
#include "pin_mux.h"
#include "clock_config.h"
#include "fsl_gpio.h"

/*******************************************************************************
 * Definiciones
 ******************************************************************************/
/* Dirección base y canal del FlexTimer utilizados */
#define BOARD_FTM_BASEADDR FTM3
#define BOARD_FTM_CHANNEL  kFTM_Chnl_4

/* Número de interrupción y manejador de interrupción para el FTM utilizado */
#define FTM_INTERRUPT_NUMBER FTM3_IRQn
#define FTM_LED_HANDLER      FTM3_IRQHandler

/* Interrupción a habilitar y bandera a leer */
#define FTM_CHANNEL_INTERRUPT_ENABLE kFTM_Chnl4InterruptEnable
#define FTM_CHANNEL_FLAG             kFTM_Chnl4Flag

/* Obtener fuente de reloj para el controlador FTM */
#define FTM_SOURCE_CLOCK CLOCK_GetFreq(kCLOCK_CoreSysClk)

/* Definiciones para el teclado matricial */
#define NUM_ROWS 4U
#define NUM_COLS 4U

/* Macro para verificar si una tecla es numérica */
#define is_number_key(key) ((key) >= '0' && (key) <= '9')

/*******************************************************************************
 * Prototipos
 ******************************************************************************/
void delay(void);
void activate_pwm(void);
void deactivate_pwm(void);
void update_duty_cycle(uint8_t update_value);
void state_idle_function(void);
void state_pwm_function(void);
void state_duty_cycle_entry_function(void);
void state_machine_init(void);
char scan_keypad(void);

/*******************************************************************************
 * Variables
 ******************************************************************************/
/* Variables globales y volátiles */
volatile bool ftmIsrFlag          = false;
volatile uint8_t updatedDutycycle = 10U;

/* Configuraciones para FTM */
ftm_config_t ftmInfo;
ftm_chnl_pwm_signal_param_t ftmParam;
ftm_pwm_level_select_t pwmLevel = kFTM_LowTrue;

/* Definición de estados para la máquina de estados */
typedef enum {
    STATE_IDLE = 0,
    STATE_PWM_ACTIVE,
    STATE_DUTY_CYCLE_ENTRY
} State;

State current_state;

/* Tabla de funciones de estado */
static void (*state_table[])(void) = {
    state_idle_function,
    state_pwm_function,
    state_duty_cycle_entry_function
};

/* Variables para la entrada del ciclo de trabajo */
char duty_cycle_input[3] = {0}; /* Almacena hasta dos dígitos y terminador nulo */
uint8_t input_index;
volatile uint8_t duty_cycle_value = 0;

/* Variables para el teclado matricial */
char key;
const char key_map[NUM_ROWS][NUM_COLS] = {
    {'1', '2', '3', 'A'},
    {'4', '5', '6', 'B'},
    {'7', '8', '9', 'C'},
    {'*', '0', '#', 'D'}
};

const uint8_t row_pins[NUM_ROWS] = {12U, 13U, 14U, 15U}; /* Pines de las filas */
const uint8_t col_pins[NUM_COLS] = {11U, 12U, 13U, 14U}; /* Pines de las columnas */

/*******************************************************************************
 * Código
 ******************************************************************************/

/*!
 * @brief Función principal
 */
int main(void)
{
    /* Inicialización de pines, reloj y consola de depuración */
    BOARD_InitPins();
    BOARD_BootClockRUN();
    BOARD_InitDebugConsole();

    /* Inicialización de la máquina de estados */
    state_machine_init();

    /* Bucle principal */
    while (1) {
        /* Escaneo del teclado matricial */
        key = scan_keypad();
        /* Ejecución de la función correspondiente al estado actual */
        state_table[current_state]();
    }

    return 0;
}

/*!
 * @brief Activar PWM con el ciclo de trabajo actual
 */
void activate_pwm(void) {
    /* Configurar parámetros de FTM con frecuencia de 24 kHz */
    ftmParam.chnlNumber            = BOARD_FTM_CHANNEL;
    ftmParam.level                 = pwmLevel;
    ftmParam.dutyCyclePercent      = duty_cycle_value;
    ftmParam.firstEdgeDelayPercent = 0U;
    ftmParam.enableDeadtime        = false;

    /* Obtener configuración por defecto de FTM */
    FTM_GetDefaultConfig(&ftmInfo);
    /* Inicializar módulo FTM */
    FTM_Init(BOARD_FTM_BASEADDR, &ftmInfo);

    /* Configurar PWM de FTM */
    FTM_SetupPwm(BOARD_FTM_BASEADDR, &ftmParam, 1U, kFTM_CenterAlignedPwm, 24000U, FTM_SOURCE_CLOCK);

    /* Iniciar temporizador FTM */
    FTM_StartTimer(BOARD_FTM_BASEADDR, kFTM_SystemClock);
}

/*!
 * @brief Desactivar PWM
 */
void deactivate_pwm(void) {
    /* Actualizar selección de nivel de borde del canal para desactivar la salida */
    FTM_UpdateChnlEdgeLevelSelect(BOARD_FTM_BASEADDR, BOARD_FTM_CHANNEL, 0U);
}

/*!
 * @brief Actualizar el ciclo de trabajo del PWM
 *
 * @param update_value Nuevo valor de ciclo de trabajo (0-100)
 */
void update_duty_cycle(uint8_t update_value) {
    /* Deshabilitar salida del canal antes de actualizar el ciclo de trabajo */
    FTM_UpdateChnlEdgeLevelSelect(BOARD_FTM_BASEADDR, BOARD_FTM_CHANNEL, 0U);

    /* Actualizar ciclo de trabajo del PWM */
    FTM_UpdatePwmDutycycle(BOARD_FTM_BASEADDR, BOARD_FTM_CHANNEL, kFTM_CenterAlignedPwm, update_value);

    /* Disparar software para actualizar registros */
    FTM_SetSoftwareTrigger(BOARD_FTM_BASEADDR, true);

    /* Iniciar salida del canal con ciclo de trabajo actualizado */
    FTM_UpdateChnlEdgeLevelSelect(BOARD_FTM_BASEADDR, BOARD_FTM_CHANNEL, pwmLevel);

    /* Pequeña demora para ver el ciclo de trabajo actualizado */
    delay();
}

/*!
 * @brief Función de demora
 */
void delay(void)
{
    volatile uint32_t i = 0U;
    for (i = 0U; i < 8000U; ++i)
    {
        __asm("NOP"); /* No operación para demora */
    }
}

/*!
 * @brief Inicializar la máquina de estados
 */
void state_machine_init(void) {
    current_state = STATE_IDLE;
    input_index = 0;
}

/*!
 * @brief Función del estado IDLE
 */
void state_idle_function(void) {
    if (key == 'A') {
        activate_pwm();
        current_state = STATE_PWM_ACTIVE;
    }
    else {
        /* Reiniciar entrada de ciclo de trabajo en cualquier otra tecla */
        memset(duty_cycle_input, 0, sizeof(duty_cycle_input));
    }
}

/*!
 * @brief Función del estado PWM ACTIVE
 */
void state_pwm_function(void) {
    if (key == 'B') {
        deactivate_pwm();
        duty_cycle_value = 0;
        current_state = STATE_IDLE;
    } else if (is_number_key(key)) {
        /* Iniciar entrada de ciclo de trabajo */
        duty_cycle_input[0] = key;
        input_index = 1;
        current_state = STATE_DUTY_CYCLE_ENTRY;
    }
}

/*!
 * @brief Función del estado DUTY CYCLE ENTRY
 */
void state_duty_cycle_entry_function(void) {
    if (is_number_key(key) && input_index < 2) {
        /* Almacenar dígito ingresado */
        duty_cycle_input[input_index++] = key;
    } else if (key == 'D') {
        /* Convertir entrada a entero y actualizar ciclo de trabajo */
        duty_cycle_input[input_index] = '\0';
        duty_cycle_value = atoi(duty_cycle_input);
        if (duty_cycle_value >= 0 && duty_cycle_value <= 100) {
            update_duty_cycle(duty_cycle_value);
        }
        /* Reiniciar entrada */
        input_index = 0;
        memset(duty_cycle_input, 0, sizeof(duty_cycle_input));
        current_state = STATE_PWM_ACTIVE;
    } else if (key == 'C') {
        /* Cancelar entrada y regresar al estado PWM ACTIVE */
        input_index = 0;
        memset(duty_cycle_input, 0, sizeof(duty_cycle_input));
        current_state = STATE_PWM_ACTIVE;
    }
}

/*!
 * @brief Escaneo del teclado matricial
 *
 * @return Carácter de la tecla presionada, 'Z' si ninguna tecla es presionada
 */
char scan_keypad(void) {
    for (uint8_t row = 0; row < NUM_ROWS; row++)
    {
        /* Establecer todas las filas en alto */
        for (uint8_t i = 0; i < NUM_ROWS; i++)
        {
            GPIO_PinWrite(GPIOB, row_pins[i], 1U);
        }

        /* Establecer la fila actual en bajo */
        GPIO_PinWrite(GPIOB, row_pins[row], 0U);

        /* Pequeña demora para estabilización de señal */
        SDK_DelayAtLeastUs(5U, CLOCK_GetFreq(kCLOCK_CoreSysClk));

        /* Leer columnas */
        for (uint8_t col = 0; col < NUM_COLS; col++)
        {
            if (!GPIO_PinRead(GPIOA, col_pins[col]))
            {
                /* Tecla presionada */
                /* Demora para anti-rebote */
                SDK_DelayAtLeastUs(20U, CLOCK_GetFreq(kCLOCK_CoreSysClk));

                /* Verificar que la tecla sigue presionada */
                if (!GPIO_PinRead(GPIOA, col_pins[col]))
                {
                    /* Esperar hasta que la tecla sea liberada */
                    while (!GPIO_PinRead(GPIOA, col_pins[col]))
                    {
                        /* Pequeña demora para evitar bloqueo de CPU */
                        SDK_DelayAtLeastUs(5U, CLOCK_GetFreq(kCLOCK_CoreSysClk));
                    }

                    /* Retornar valor de la tecla */
                    return key_map[row][col];
                }
            }
        }
    }

    /* Ninguna tecla presionada */
    return 'Z';
}
```

# Entregable 3: Explicación del Código
## Descripción General

El programa controla la intensidad de un LED mediante la variación del ciclo de trabajo de una señal PWM. El usuario puede interactuar con el sistema utilizando un teclado matricial para:

- **Estado IDLE (Reposo)**: El sistema espera a que el usuario presione la tecla 'A' para activar el PWM.
- **Estado PWM ACTIVE (PWM Activo)**: El PWM está activo, y el usuario puede ingresar un nuevo ciclo de trabajo o desactivar el PWM presionando 'B'.
- **Estado DUTY CYCLE ENTRY (Entrada de Ciclo de Trabajo)**: El usuario ingresa un valor numérico (0-99) seguido de 'D' para actualizar el ciclo de trabajo, o 'C' para cancelar.

## Implementación de la Máquina de Estados

La máquina de estados se implementa utilizando:

- **Enum State**: Define los posibles estados del sistema (`STATE_IDLE`, `STATE_PWM_ACTIVE`, `STATE_DUTY_CYCLE_ENTRY`).
- **Variable `current_state`**: Almacena el estado actual de la máquina de estados.
- **Tabla de funciones `state_table`**: Arreglo de punteros a funciones que corresponden a cada estado.

En el bucle principal, el programa:

1. Escanea el teclado matricial y almacena la tecla presionada en `key`.
2. Llama a la función correspondiente al estado actual desde `state_table[current_state]()`.
3. Las funciones de estado manejan las transiciones y acciones basadas en la entrada.

## Lectura del Teclado Matricial

La función `scan_keypad()` realiza el escaneo del teclado:

- Configura todas las filas en alto.
- Para cada fila:
  - Establece la fila actual en bajo.
  - Lee cada columna para detectar si una tecla está presionada.
  - Implementa una demora para el anti-rebote.
  - Verifica si la tecla sigue presionada y espera hasta que sea liberada.
- Retorna el carácter correspondiente desde `key_map`.

## Control del PWM

Las funciones relacionadas con el control del PWM son:

- **`activate_pwm()`**: Configura y activa el PWM con el ciclo de trabajo actual (`duty_cycle_value`).
- **`deactivate_pwm()`**: Desactiva el PWM.
- **`update_duty_cycle(uint8_t update_value)`**: Actualiza el ciclo de trabajo del PWM al nuevo valor proporcionado.

Estas funciones utilizan las APIs del FlexTimer Module (FTM) para configurar y controlar la señal PWM.

## Descripción de las Funciones Principales

- **`main()`**: Inicializa el sistema y entra en un bucle infinito donde se escanea el teclado y se ejecuta la función del estado actual.
- **`state_machine_init()`**: Inicializa la máquina de estados estableciendo el estado inicial y reseteando índices.
- **`state_idle_function()`**: Maneja el estado IDLE; activa el PWM si se presiona 'A'.
- **`state_pwm_function()`**: Maneja el estado PWM ACTIVE; desactiva el PWM si se presiona 'B' o inicia la entrada de ciclo de trabajo si se presiona una tecla numérica.
- **`state_duty_cycle_entry_function()`**: Maneja la entrada del ciclo de trabajo; permite ingresar hasta dos dígitos y actualiza el ciclo de trabajo al presionar 'D'.

## Manejo de Entradas del Usuario

- **Entrada Numérica**: Se verifica con la macro `is_number_key(key)`. Los dígitos ingresados se almacenan en `duty_cycle_input`.
- **Confirmación y Cancelación**:
  - **Confirmar ('D')**: Convierte la entrada a entero y actualiza el ciclo de trabajo.
  - **Cancelar ('C')**: Reinicia la entrada y regresa al estado anterior.

## Demoras y Anti-rebote

Se utilizan funciones de demora como `delay()` y `SDK_DelayAtLeastUs()` para:

- Estabilizar señales durante el escaneo del teclado.
- Implementar anti-rebote al leer las teclas.
- Proporcionar demoras necesarias al actualizar el PWM.

## Configuración del Hardware

- **Pines del Teclado Matricial**:
  - **Filas (`row_pins`)**: Pines configurados como salidas para seleccionar la fila.
  - **Columnas (`col_pins`)**: Pines configurados como entradas para leer el estado de las columnas.

- **PWM**:
  - **FTM (FlexTimer Module)**: Utilizado para generar la señal PWM.
  - **Canal y Nivel**: Configurados mediante `ftmParam`.
