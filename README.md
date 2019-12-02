# Ejemplo interrupciones de la UART

En este ejemplo se muestra la forma de detectar el evento RX de la UART

```c
#include "sapi.h"

void onRx( void *noUsado )
{
   char c = uartRxRead( UART_USB );
   printf( "Recibimos <<%c>> por UART\r\n", c );
}

int main(void)
{
   boardConfig();
   uartConfig( UART_USB, 115200 );
   uartRxInterruptCallbackSet( UART_USB, onRx );
   uartRxInterruptSet( UART_USB, true );
   while(TRUE) {
      sleepUntilNextInterrupt();
   }
   return 0;
}
```
