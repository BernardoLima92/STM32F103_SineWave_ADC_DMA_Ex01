# STM32F103_SineWave_ADC_DMA_Ex01
Generating of a sinusoidal signal using PWM as a DAC, in parallel with ADC conversions.

Neste tutorial será demonstrado um experimento no qual, ao mesmo tempo, um senoidal senoidal com 128 amostras é gerado e
conversões ADC são realizadas.
Ao final de um ciclo completo do sinal senoidal, teremos 128 leituras analógicas realizads pelo ADC. Cada leitura será referente
à um ponto do sinal senoidal gerado.
Esse algoritmo é a base de funcionamente de um Amplificar Lock-in Digital, onde é necessário que dois sinais senoidais estejam 
sincronizados, com uma diferença de fase constante. 
