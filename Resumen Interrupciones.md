# Módulo de Interrupciones NVIC

## Uso de Interrupciones en Microcontroladores ARM Cortex-M4

### Introducción

Las interrupciones permiten a los microcontroladores atender eventos imprevistos, tanto de hardware como de software, interrumpiendo la ejecución del programa principal para realizar tareas de mayor prioridad. Estas interrupciones pueden ser controladas por un sistema de habilitación o deshabilitación y se clasifican en enmascarables (**IRQ**) o no enmascarables (**NMI**).

### Modos de Operación del Procesador

- **Thread Mode:** El procesador ejecuta el código principal del programa, pero puede ser interrumpido por eventos externos.
- **Handler Mode:** Se ejecuta en respuesta a una interrupción o excepción, y deshabilita otras interrupciones para manejar el evento crítico.

### Estados de Excepción

1. **Inactivo:** Sin excepciones presentes.
2. **Pendiente:** La excepción está detectada, pero no manejada.
3. **Activo:** El procesador está manejando una excepción.
4. **Activo y Pendiente:** Se están manejando múltiples excepciones del mismo tipo.

### Tratamiento de una Interrupción

El microcontrolador puede manejar múltiples interrupciones con diferentes niveles de prioridad. Durante la ejecución de una interrupción de baja prioridad, una de alta prioridad puede interrumpirla. Este proceso se denomina interrupciones anidadas.

### Context Saving

Cuando ocurre una interrupción, el microcontrolador guarda el contexto del programa (registros, estado de la pila, dirección de retorno) antes de cambiar al **Handler Mode** y ejecutar la rutina de interrupción. Una vez finalizado, restaura el estado anterior para continuar con la ejecución normal.

## Módulo NVIC

El **Nested Vectored Interrupt Controller (NVIC)** es responsable de gestionar las interrupciones en microcontroladores ARM Cortex-M4, permitiendo la configuración de prioridades, habilitación/deshabilitación de interrupciones y manejo del vector de interrupción.

### Mapa de Interrupciones

El mapa de interrupciones es una lista de direcciones en memoria que apuntan a los manejadores de interrupciones específicos. Ejemplos de interrupciones son el **Non-maskable Interrupt (NMI)** y el **Hard Fault**, que se activan en eventos críticos.

### Interrupt Request (IRQ)

Cada tipo de interrupción en el NVIC tiene un número de IRQ único, lo que permite al controlador de interrupciones direccionar el flujo de ejecución hacia el manejador correspondiente.

## Registros de Gestión de Interrupciones

El NVIC contiene varios registros para habilitar/deshabilitar interrupciones y gestionar su estado:
- **NVIC_ISER** (Interrupt SET ENABLE)
- **NVIC_ICER** (Interrupt CLEAR ENABLE)
- **NVIC_ISPR** (Interrupt SET PENDING)
- **NVIC_ICPR** (Interrupt CLEAR PENDING)
- **NVIC_IABR** (Interrupt Active BIT)
- **NVIC_IPR** (Interrupt Priority)

## Niveles de Prioridad de Interrupciones

Las interrupciones en los microcontroladores ARM Cortex-M4 se clasifican en niveles de prioridad, donde un valor más bajo indica mayor prioridad. Por ejemplo, la prioridad 0 es la más alta y la 15 es la más baja.

## Configuración de una Interrupción

Para configurar una interrupción en un microcontrolador, se sigue este proceso:
1. Localizar el número de IRQ.
2. Determinar el registro ISER correspondiente mediante la división entera del número de IRQ por 32.
3. Determinar la posición del bit de la interrupción.
4. Calcular la posición de los bits de prioridad mediante una división de IRQ por 4.

## Funciones en C para Configuración

Se utilizan funciones en C para gestionar las interrupciones, tales como `NVIC_EnableIRQ()`, `NVIC_DisableIRQ()`, `NVIC_SetPendingIRQ()`, `NVIC_ClearPendingIRQ()`, y `NVIC_SetPriority()`.

## Ejemplo de Rutina de Interrupción

Se proporciona un ejemplo de código en C para configurar y manejar una interrupción con el temporizador **SysTick** que genera interrupciones cada 1 ms:

```c
void SysTick_Handler(void) {
    // Manejar la interrupción del temporizador SysTick
}

int main(void) {
    SysTick_Config(SystemCoreClock / 1000);
    NVIC_SetPriority(SysTick_IRQn, 15);
    NVIC_EnableIRQ(SysTick_IRQn);

    while (1) {
        // Bucle principal
    }

    return 0;
}
