# Sistema de Postes Inteligentes com ESP32

## Objetivo Geral

O sistema de postes inteligentes visa criar uma solução IoT (Internet of Things) que utiliza microcontroladores (ESP32) instalados em postes para monitoramento, análise de imagem e coleta de dados ambientais. O sistema tem como principais funcionalidades a captura de imagens, o envio dessas imagens via MQTT para análise por meio de inteligência artificial (processamento realizado em uma instância na Google Cloud), a leitura de dados ambientais por meio de um sensor BME280, e a capacidade de ajustar a intensidade luminosa dos postes.

### Componentes Principais

1. Módulo Mestre:

    * Responsável por coletar dados ambientais (BME280), capturar imagens e enviar esses dados via MQTT para análise por IA.
    * Envia imagens para processamento em uma instância na Google Cloud para detecção de pessoas.
    * Desempenha o papel do módulo atenuador, controlando a intensidade luminosa dos postes associados (em desenvolvimento).
    * Cada módulo mestre está associado a cada conjunto de 3 postes.
    * Abaixo está o 3D de como deve ficar o módulo mestre, a ideia inicial é que essas duas placas fiquem empilhadas.

    <img src = "Imagens/modulo_mestre(completo).png">

2. Módulo Atenuador (ESP32 com Dimmer):

    * O módulo atenuador é composto apenas por um dimmer e uma ESP32.
    * Responsável por ajustar a intensidade luminosa dos postes que não possuem o módulo mestre.
    * Recebe informações de controle de intensidade luminosa dos módulos mestres e ajusta a luminosidade de acordo.
    * Abaixo está o 3D de como deve ficar o módulo.

    <img src = "Imagens/modulo_atenuador.png">

4. Análise de Imagem com IA (Google Cloud):

    * Processa as imagens capturadas pelos módulos mestres utilizando inteligência artificial.
    * Foco na detecção de pessoas nas imagens.

### Fluxo de Funcionamento

1. Captura de Imagens e Dados Ambientais:

    * O módulo mestre (ESP32CAM) captura imagens periodicamente.
    * Os dados ambientais (temperatura, pressão, altitude, umidade) são lidos pelo sensor BME280.

2. Envio para o MQTT Broker:

    * As imagens e dados ambientais são enviados para o MQTT Broker.
    * O Broker MQTT gerencia a comunicação entre os módulos e o sistema em nuvem.

3. Análise de Imagem por IA (Posterior):

    * As imagens enviadas para o servidor MQTT serão processadas posteriormente por um sistema de inteligência artificial.
    * O foco é na detecção de pessoas nas imagens capturadas.

4. Controle de Intensidade Luminosa:

    * O módulo mestre também tem a funcionalidade de atuar como um módulo atenuador, controlando a intensidade luminosa dos postes.
    * De acordo com as informações recebiadas pela análise dos dados o módulo mestre e os módulos atenuadores alteram a intensidade dos seus respectivos postes.
    * Aqui em baixo está uma representação de como deve funcionar o sistema. O poste 'P1' estará equipado com o módulo mestre com a câmera apontada em direção aos outros 3 postes (que estão equipados com o módulo atenuador). Ao detectar alguma pessoa nesse raio todos as luzes dos postes terão a intensidade luminosa aumentada.

    <img src = "Imagens/simulação1.png">
