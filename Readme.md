_____________________________________________________________________________________________________________________________________________________________________
**AUTORES:** Acssa Sousa e Fábio Itturriet

**DATA:** 07/04/2022

**OBJETIVO:** Este projeto visa configurar a plataforma STM32 a fim de capturar e transmitir uma senoide, a partir de um gerador de funções, para um servidor web através do módulo ESP8266.

**IDE:** STM32CUBEIDE V.1.8.0

________________________________________________________________________________________________________________________________________________________________________
## Diagrama do experimento:
<img width="509" alt="image" src="https://user-images.githubusercontent.com/101206099/196711829-c977f13e-3def-4f6d-9f1b-e80a8c690661.png">


## Descrição do experimento:
O projeto consite em gerar dados analógicos, através do gerador de função, que vão ser convertidos em sinais digitais, pelo conversor ADC e envia-los a um servidor web com o ESP8266. Como primeiro passo é necessário checar as portas demonstradas no diagrama do experimento.

-Aquisição de dados com o gerador de funções:

O Conversor ADC converte sinais analógicos em digitais. Sinais analógicos são sinais contínuos que variam com o tempo, proveniente de muitos sensores, para a capitação e representação desses números o MCU pega amostras e converte em valores discretos e descontínuos (binário), no caso da STM32F411RE o conversor AD é de 12 Bits, tem precisão de 4096, ou seja, a conversão ocupa valores ente 0 a 4095.

como demonstrado nas imagens a seguir o gerador de funções vai estar conectado ao pino PA0 que fará a converção AD.  

<img width="494" alt="image" src="https://user-images.githubusercontent.com/101206099/162277705-7041bf8a-e7f9-4dce-a03b-e771b4e05b7f.png">

-Acionamento da aquisição de dados:

Para que os dados sejam coletados será necessário o acionamento do botão, que ao clicar irá possibilitar a conversão dos dados e clicando novamente interrompe aquisição. Abaixo temos o diagrama que define a porta de comunicação do botão.

<img width="578" alt="image" src="https://user-images.githubusercontent.com/101206099/162285063-9daaf75e-4ac1-41ab-9312-3e1085748f6e.png">

-Comunicação para transmição de dados pelo módulo Esp-01:

//posteriormente*

________________________________________________________________________________________________________________________________________________________________________


## Começando um novo projeto:

Criando um novo projeto na área de trabalho do CUBE IDE:

1. Vá até a guia Arquivo > Novo > Projeto STM32

<img width="770" alt="image" src="https://user-images.githubusercontent.com/101206099/162268568-6a5fbd51-5a2c-4eef-9b4d-61510b893fa8.png">

2. Ao abrir a janela "Target selection" e selecione na aba "board selector" a plataforma de desenvolvimento a ser utilizada, para este caso NUCLEO-F411RE. 

<img width="960" alt="image" src="https://user-images.githubusercontent.com/101206099/162270921-1167cfc5-8806-4a85-99f1-6a3f9db821e5.png">

3. Dê um nome ao seu projeto e prossiga com o "Finish".

<img width="376" alt="image" src="https://user-images.githubusercontent.com/101206099/162271925-38ad9a78-8248-49fd-86d5-cdd3789f8ffe.png">

________________________________________________________________________________________________________________________________________________________________________

## Configuração da plataforma:

Após criado um novo projeto altere o pino PA0 para ADC1_IN0, e mantenha as outras configurações padrão:

<img width="853" alt="image" src="https://user-images.githubusercontent.com/101206099/167686916-b26c407b-e533-43f6-b496-06c0654715a6.png">

Se quisermos fazer várias leituras de ADC para preencher um buffer sem intervenção da CPU, precisaremos confiar no DMA. Uma das maneiras mais fáceis de ver o DMA em ação é usá-lo em conjunto com o UART. Então, vamos criar um buffer bastante grande preenchido com texto arbitrário, e vamos dizer ao DMA para enviar esses dados, um byte por vez, para o periférico UART. O UART enviará os dados para o nosso programa de terminal serial.

O controlador de acesso direto a memória (DMA) é uma ferramenta muito útil para liberar capacidade de processamento da CPU. Para se transferir dados, por exemplo, do ADC para a memória, a CPU executa linhas de códigos o que tira ciclo do processador de coisas úteis, com o DMA isso se torna dispensável, ou seja a CPU fica fora de jogo, e agora essa transferência fica responsável pelo DMA. 

A partir do projeto anterior nas configurações da MCU vá em system core, DMA e na aba DMA2 adicione um novo DMA com a requisição do ADC1. Selecione o modo circular, ou seja, o DMA acessará o vetor Buffer no inicio quando o buffer estiver cheio. 

<img width="856" alt="image" src="https://user-images.githubusercontent.com/101206099/167689352-cfe69a33-b47a-458b-b4de-f2f7fc798be9.png">

Volte para Analógico > ADC1 . Nas configurações, altere DMA Continuous Requests para Enabled . As demais configurações podem ser deixadas como padrão.

<img width="793" alt="image" src="https://user-images.githubusercontent.com/101206099/167690986-6efc3b25-31f5-4791-ac0f-9de0a32634ae.png">

Salve e gere código. Abra main.c . Altere o código para o seguinte:






