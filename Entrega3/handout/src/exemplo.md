# Algoritimo de WaterShed

## Contexto

O algoritmo de WaterShed introduzido no inicio dos anos 90 por F. Meyer possui uma aplicação significativa na área de processamento de imagem, em específico na parte de segmentação de imagem.

##

![brain](brain.jpg)

## O algoritmo

O algoritmo recebe como entrada uma imagem em _greyscale_, ou seja, em tons de cinza. Ele interpreta essa imagem como um mapa topográfico em que os píxeis vizinhos de mesmo tom são como curvas de nível.

![gif1](gif1.png)

Os níveis de menor valor são preenchidos como uma "piscina".

![gif2](gif2.png)

Quando as "piscinas" se encontram é delimitada uma barreira na imagem.

![gif3](gif3.png)

## Exercício 1

Queremos separar todas as moedas dessa imagem. O watershed pode causar algum problema nessa segmentação em que os objetos são maiores?

![input](input.jpg)

###

Sim, o que pode acontecer é a super segmentação da imagem. Uma vez que a entrada consiste de diferentes valores de pixel, formando várias "piscinas", a imagem de saída é em _greyscale_ com muitas barreiras o que acaba dificultando a análise.

img supersegmentadaaaaaaaaaa

## Exercício 2

Como é possível solucionar esse problema?

###

Em uma implementação do algoritmo a utilização de marcadores iniciais pode fazer a diferença e diminuir os pontos pelos quais o algoritmo deve iterar, ou seja, diminuindo o número de "piscinas" iniciais, evitando a supersegmentação. Mas então como funciona essa implementação.

É possível adicionar marcadores com uma segunda imagem de entrada com as mesmas dimensões da imagem a ser segmentada contendo pontos/marcadores onde são localizados os centros das áreas conectadas. Esses pontos geralmente correspondem aos mínimos locais da imagem de entrada.

![marker](marker.png)

![output](output.jpg)

Implementação:
