# Controle de Pedidos de Mamadeiras via MQTT

Este projeto utiliza um **ESP32** para controlar pedidos de mamadeiras em um ambiente hospitalar. Ele se comunica com um cliente MQTT para enviar perguntas sobre a quantidade de mamadeiras e receber respostas. O ESP32 exibe as informações no LCD e envia as respostas para um tópico MQTT.

## Funcionalidades

- O **ESP32** envia uma pergunta sobre o número de mamadeiras via **MQTT**.
- O **cliente MQTT** (como **MyMQTT**) envia a resposta para o **ESP32**.
- O **ESP32** exibe a resposta no **LCD**.
- O sistema pode ser **cancelado** pressionando a tecla 'X' no **Monitor Serial**.

## Requisitos

- **Hardware**:
  - **ESP32**
  - **LCD 16x2 com I2C**
  - **Conexão Wi-Fi** para o ESP32 (ou utilizar um ponto de acesso local)

- **Software**:
  - **Arduino IDE** com suporte para **ESP32**.
  - **Bibliotecas**:
    - `WiFi.h`
    - `PubSubClient.h` (para comunicação MQTT)
    - `LiquidCrystal_I2C.h` (para controlar o LCD)

## Como Configurar

1. **Instalar as bibliotecas necessárias**:
   - No **Arduino IDE**, vá em **Sketch** > **Incluir Biblioteca** > **Gerenciar Bibliotecas...**
   - Procure por **WiFi**, **PubSubClient** e **LiquidCrystal_I2C** e instale-os.

2. **Conectar o LCD**:
   - **SDA**: GPIO 21 (ESP32)
   - **SCL**: GPIO 22 (ESP32)
   - **VCC**: 5V ou 3.3V (dependendo do modelo do LCD)
   - **GND**: GND

3. **Configuração do Wi-Fi**:
   - No código, substitua `"Wokwi-GUEST"` e `""` pelos detalhes da sua rede Wi-Fi.

4. **Subir o código para o ESP32**:
   - Selecione a placa **ESP32** no Arduino IDE.
   - Conecte o ESP32 via USB e **faça o upload do código**.

5. **Configuração do MQTT**:
   - O código já usa o broker MQTT público `test.mosquitto.org`. Se preferir, você pode configurar um broker local ou privado.
   
6. **Usando o MyMQTT**:
   - **Subscreva** ao tópico `pedido/mamadeira` para receber a pergunta enviada pelo ESP32.
   - **Envie a resposta** para o tópico `pedido/resposta` (por exemplo: "5" para 5 mamadeiras).

## Fluxo do Projeto

1. O **ESP32** envia a pergunta "Qual a quantidade de mamadeira?" para o tópico **`pedido/mamadeira`** via **MQTT**.
2. O **cliente MQTT** (como **MyMQTT**) envia a resposta para o tópico **`pedido/resposta`**.
3. O **ESP32** recebe a resposta e a exibe no **LCD**.
4. Caso o usuário pressione a tecla **'X'** no **Monitor Serial**, o pedido será cancelado e uma mensagem de cancelamento será enviada via MQTT.

## Diagrama de Arquitetura

O diagrama abaixo ilustra a arquitetura do sistema, mostrando a comunicação entre o **ESP32**, o **cliente MQTT** e o **broker MQTT**.

## Licença

Este projeto é licenciado sob a [MIT License](https://opensource.org/licenses/MIT).
