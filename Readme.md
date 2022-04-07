_____________________________________________________________________________________________________________________________________________________________________
**AUTORES:** Acssa Sousa e Fábio Itturriet

**DATA:** 07/04/2022

**OBJETIVO:** Este projeto visa configurar a plataforma STM32 a fim de capturar e transmitir uma senoide, a partir de um gerador de funções, para um servidor web através do módulo ESP8266.

**IDE:** STM32CUBEIDE V.1.8.0

________________________________________________________________________________________________________________________________________________________________________
## Diagrama do experimento:
<img width="707" alt="image" src="https://user-images.githubusercontent.com/101206099/162263943-0e3f3ed7-bb28-4048-803d-cbc18c18c92c.png">


## Descrição do experimento:
O projeto consite em gerar dados analógicos, através do gerador de função, que vão ser convertidos em sinais digitais, pelo conversor ADC e envia-los a um servidor web com o ESP8266. Como primeiro passo é necessário checar as portas demonstradas no diagrama do experimento.

-Aquisição de dados com o gerador de funções:

como demonstrado nas imagens a seguir o gerador de funções vai estar conectado ao pino PA0 que fará a converção AD.  

<img width="494" alt="image" src="https://user-images.githubusercontent.com/101206099/162277705-7041bf8a-e7f9-4dce-a03b-e771b4e05b7f.png">

-Acionamento da aquisição de dados:

Para que os dados sejam coletados será necessário o acionamento do botão, que ao clicar irá possibilitar a conversão dos dados e clicando novamente interrompe aquisição. Abaixo temos o diagrama que define a porta de comunicação do botão.

<img width="578" alt="image" src="https://user-images.githubusercontent.com/101206099/162285063-9daaf75e-4ac1-41ab-9312-3e1085748f6e.png">


## Começando um novo projeto:

Criando um novo projeto na área de trabalho do CUBE IDE:

1. Vá até a guia Arquivo > Novo > Projeto STM32

<img width="770" alt="image" src="https://user-images.githubusercontent.com/101206099/162268568-6a5fbd51-5a2c-4eef-9b4d-61510b893fa8.png">

2. Ao abrir a janela "Target selection" e selecione na aba "board selector" a plataforma de desenvolvimento a ser utilizada, para este caso NUCLEO-F411RE. 

<img width="960" alt="image" src="https://user-images.githubusercontent.com/101206099/162270921-1167cfc5-8806-4a85-99f1-6a3f9db821e5.png">

3. Dê um nome ao seu projeto e prossiga com o "Finish".

<img width="376" alt="image" src="https://user-images.githubusercontent.com/101206099/162271925-38ad9a78-8248-49fd-86d5-cdd3789f8ffe.png">




