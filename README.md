Autor: [Kaique Dognani](https://github.com/kaiqued)
# Tutorial Joystick e aplicação com o  Motor De Passo

# Objetivo
  Primeiros passos com o Joystick e motores de passo utilizando a NUCLEO F103RB como microcontrolador.
  
# Materiais
* NUCLEO F103RB
* Joystick
* Compilador [Mbed](https://ide.mbed.com/)

# [MBED Hand Book](https://os.mbed.com/handbook/Homepage)
  Aqui você poderá consultar informações adcionais sobre algumas das funções do MBED, como BusOut, AnalogIn...
  
# Primeiros passos
  A placa Nucleo F103RB tem a capacidade de ler um valor de tensão aplicado sobre alguns pinos, para isto utilizaremos a classe AnalogIn.
  
  É importante sempre lembrar que em geral ***os pinos da placa Nucleo são tolerantes apenas a 3.3V***, logo só poderemos fazer a leitura de valores entre 0V e 3.3V.
  
  Neste tutorial vamos fazer as primeiras medidas analógicas e entender um pouco melhor a construção de um código no MBED.

# Como fazer uma leitura da porta analógica?
  Primeiro devemos inicializar o pino que vamos fazer a leitura, neste caso estou utilizando o pino A1 e o nomeei de VRX, pois este é o nome que está descrito no joystick.
  
  Vamos inicializar também a porta serial, pois assim podemos tanto debuggar o código como imprimir o valor que estamos lendo na porta analógica.
  
  Com o pino inicializado, se fizermos "*float Valor = VRX;*" veremos que na variável "Valor" receberemos um float entre 0 e 1, logo, para evitar o trabalho de utilizar float, eu prefiro pegar este valor e multiplicar por 100. Logo, teremos um valor entre 0 e 100, assim podendo trabalhar com inteiros apenas.
  
  O arquivo ***main.cpp*** deve ficar parecido com este:
  
```c++
#include "mbed.h"

Serial pc(USBTX, USBRX);
AnalogIn VRX(A1);

// Variável que guarda o valor de VRX*100
float Valor;

int main()
{
    // Inicializa a Serial com Baudrate de 115200 b/s
    pc.baud(115200);
    
    // Loop Principal
    while (true) 
    {   
        // Leitura da porta analógica
        Valor = VRX * 100;
        
        // Imprime no monitor serial
        pc.printf("%f", Valor);
        
        wait(0.5);
    }
}
```
