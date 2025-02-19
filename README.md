# Projeto de Controle de LEDs e Joystick com Display OLED

Este projeto foi desenvolvido para controlar LEDs RGB e um LED verde usando um joystick, além de exibir informações no display OLED SSD1306. Ele utiliza a placa Raspberry Pi Pico e se comunica com o display via I2C e com o joystick via ADC. A funcionalidade inclui o controle dos LEDs com base na posição do joystick e o controle do display OLED para exibir um quadrado em movimento.

## Tabela de Conteúdos
1. [Descrição do Projeto](#descrição-do-projeto)
2. [Hardware Requerido](#hardware-requerido)
3. [Funcionamento do Código](#funcionamento-do-código)
4. [Configuração do Sistema](#configuração-do-sistema)
5. [Funções](#funções)
6. [Compilação e Execução](#compilação-e-execução)
7. [Licença](#licença)

## Descrição do Projeto
Este projeto implementa a leitura de um joystick (com botões e controle analógico), controla LEDs RGB e um LED verde, além de exibir um quadrado no display OLED com base nos dados do joystick. O código é projetado para ser executado em uma Raspberry Pi Pico, utilizando suas funcionalidades de PWM para controle de brilho dos LEDs e I2C para o display OLED.

## Hardware Requerido
- **Raspberry Pi Pico**
- **Joystick** com 2 eixos (X e Y) e um botão
- **Display OLED SSD1306 (com interface I2C)**
- **3 LEDs RGB** (vermelho, verde e azul)
- **Fios de conexão**

## Funcionamento do Código
O código realiza a seguinte sequência de ações:
1. **Leitura dos eixos do joystick**: O movimento do joystick nos eixos X e Y é lido via ADC e mapeado para a posição do quadrado no display OLED.
2. **Controle de LEDs**: O brilho dos LEDs RGB é ajustado conforme o movimento do joystick. Além disso, um LED verde é controlado por um botão físico e os LEDs RGB podem ser alternados com outro botão.
3. **Exibição no Display OLED**: A posição do quadrado é atualizada no display OLED com base nos valores de X e Y do joystick. A cor do fundo e a borda do display são alternadas conforme o estado do LED verde.

## Configuração do Sistema
### Pinos e Interfaces
- **I2C**: Pinos 14 (SDA) e 15 (SCL) para comunicação com o display OLED
- **Joystick**: Eixos X e Y conectados aos pinos 26 e 27, respectivamente, e o botão do joystick no pino 22
- **Botões**: Botões A no pino 5 e botão do joystick no pino 22
- **LEDs**: LEDs RGB conectados aos pinos 12 (vermelho), 11 (verde) e 13 (azul)

### Biblioteca SSD1306
Este código utiliza a biblioteca `ssd1306` para gerenciar o display OLED, que precisa estar configurada para a interface I2C.

## Funções
### `configurar_pwm(uint pino, uint *slice, uint16_t brilho)`
Configura o controle PWM de um LED para ajustar o brilho. Recebe o pino do LED, o slice PWM e o valor de brilho.

### `configurar_led_rgb()`
Configura os LEDs RGB (vermelho e azul) utilizando a função PWM, e o LED verde como saída digital.

### `configurar_display()`
Configura o display OLED SSD1306 para iniciar a comunicação via I2C e exibe um retângulo no display.

### `alternar_led_rgb(bool *estado)`
Alterna o estado dos LEDs RGB (liga/desliga).

### `alternar_led_verde(bool *estado)`
Alterna o estado do LED verde (liga/desliga).

### `imprimir_estado_leds()`
Imprime no terminal o estado atual dos LEDs RGB e do LED verde, apenas quando houver mudança.

### `imprimir_posicao_joystick()`
Imprime no terminal a posição do joystick, apenas quando houver mudança na posição.

### `tratar_interrupcao_botao(uint pino, uint32_t eventos)`
Função de interrupção para tratar os botões. Ela alterna os LEDs e o display OLED.

### `configurar_hardware()`
Configura os pinos e a leitura do joystick, além de definir as interrupções para os botões.

### `atualizar_display()`
Atualiza a exibição no display OLED com base na posição do joystick.

### `ler_joystick(uint16_t *eixo_x, uint16_t *eixo_y)`
Lê os valores dos eixos X e Y do joystick via ADC.

## Compilação e Execução
1. **Instalar o SDK do Raspberry Pi Pico**:
   - Baixe e configure o SDK do Raspberry Pi Pico em sua máquina. Siga as instruções no [site oficial](https://www.raspberrypi.org/documentation/pico/getting-started/).
   
2. **Compilar o Código**:
   - Para compilar o código, utilize a ferramenta `CMake` junto com o SDK do Raspberry Pi Pico.
   - O comando para compilar o projeto pode ser algo como:
     ```bash
     mkdir build
     cd build
     cmake ..
     make
     ```

3. **Carregar no Raspberry Pi Pico**:
   - Conecte o Raspberry Pi Pico ao computador enquanto mantém pressionado o botão BOOTSEL.
   - Copie o arquivo compilado para o dispositivo (geralmente um arquivo `.uf2`).

4. **Executar o Código**:
   - Após copiar o arquivo para o Raspberry Pi Pico, ele será executado automaticamente.

## Licença
Este projeto está licenciado sob a licença MIT - veja o arquivo [LICENSE](LICENSE) para mais detalhes.

---

Este README oferece uma visão geral do projeto e como configurá-lo e executá-lo em sua Raspberry Pi Pico. Certifique-se de conectar corretamente os pinos e usar o código de acordo com a configuração do hardware.
