# STM32F103_SineWave_ADC_DMA_Ex01
Generating of a sinusoidal signal using PWM as a DAC, in parallel with ADC conversions.

Neste tutorial será demonstrado um experimento no qual, ao mesmo tempo, um senoidal senoidal com 128 amostras é gerado e
conversões ADC são realizadas.
Ao final de um ciclo completo do sinal senoidal, teremos 128 leituras analógicas realizads pelo ADC. Cada leitura será referente
à um ponto do sinal senoidal gerado.
Esse algoritmo é a base de funcionamente de um Amplificar Lock-in Digital, onde é necessário que dois sinais senoidais estejam 
sincronizados, com uma diferença de fase constante. 

A Figura abaixo mostra como o programa foi idealizado:
![Diagrama SineWave_ADC_DMA](https://user-images.githubusercontent.com/114233216/192414594-c673f5cd-c4e6-4b83-bc29-12fc4f3902d7.png)

O Timer 2 é usado para gerar o sinal PWM de saída . Esse sinal terá o formato senoidal após passar por um filtro passa baixa para eliminar as altas
frequências do sinal PWM.
O Timer 4 é usado para determinar o momentos em que uma conversão ADC deve ser realizada e o momento no qual o registrador TIM2_CCR1 deve ser atualizado
com o próximo valor de uma tabela de senos previamente escrita na memória do microcontrolador.



1.Configuração do Clock
![SW_Clock](https://user-images.githubusercontent.com/114233216/192416752-a24df7ed-e5b9-4773-ad54-9679b7981f32.png)

2. Configuração do Timer 2
![SW_TIM2a](https://user-images.githubusercontent.com/114233216/192416791-08fa633e-7c1d-4138-b6c5-81073e4b31f1.png)
![SW_TIM2b](https://user-images.githubusercontent.com/114233216/192416794-c484835b-c461-4dde-8023-06be90a20718.png)

3.Configuração do Timer 4
![SW_TIM4a](https://user-images.githubusercontent.com/114233216/192416850-e5ebdeee-0a5e-4d5c-944b-b0b883b24a91.png)
![SW_TIM4b](https://user-images.githubusercontent.com/114233216/192416858-ada7beb4-589e-4709-b113-b75d82d7c6fd.png)
![SW_TIM4_DMA](https://user-images.githubusercontent.com/114233216/192416862-ddff8015-92dc-440d-9d2f-93b46b032e37.png)


4.Configuração do ADC
![SW_ADC](https://user-images.githubusercontent.com/114233216/192416896-55dddb5b-76ae-4242-8632-79d14c532328.png)
![SW_ADC_DMA](https://user-images.githubusercontent.com/114233216/192416900-239a6ed9-68fd-4da3-8bd5-2377b08cd410.png)


5.Configuração do DMA
![SW_DMA](https://user-images.githubusercontent.com/114233216/192416921-675de895-3441-4ef7-a474-e8431a41dc73.png)


6.Partes importantes do Código
![SW_Code_2](https://user-images.githubusercontent.com/114233216/192416969-1acb6ceb-aa73-4ee2-9acf-c5abd665b51f.png)

![SW_Code_1](https://user-images.githubusercontent.com/114233216/192416991-bbc1c01c-ac25-49ac-9e51-6c381f731132.png)

![SW_Code_3](https://user-images.githubusercontent.com/114233216/192417023-0644f548-38c6-4880-b765-3aaf0c782b38.png)

7. Resultado Obtido  

![1](https://user-images.githubusercontent.com/114233216/192417066-89201318-688a-4b32-a6cd-ed855dcfa38c.png)

![2](https://user-images.githubusercontent.com/114233216/192417077-3d9cfe51-2226-4f5f-bc9c-256125373a6b.png)

O sinal em azul será o sinal senoidal de referência que fornecerá a oscilação para o laser DFB. Esse sinal tem uma frequência de 732 Hz e possui 128 amostras discretas por período.

O sinal amarelo é apenas um sinal de debug obtido na oirta PB7. Tanto a borda superior como a borda inferior indicam o início do preenchimento do buffer. Nesse experimento foi configurado um buffer com 128 posições. Isso significa que o buffer armazena exatamente um período completo do sinal de referência.

Vendo essa imagem é possível perceber uma defasagem entre o início do preenchimento do buffer e o início de um ciclo da senóide. É preciso analisar isso melhor.
Nas próximas etapas

