# Algoritimo de WaterShed

## Contexto

O algoritmo de watershed propõe uma abordagem morfológica para o problema de segmentação de imagens, interpretando-as como superfícies sendo que cada pixel corresponde à uma posição. Dessa forma, recebendo uma entrada grayscale cada valor de cinza que estiver presente na imagem pode ser considerado uma altura, como se fosse um label (pode ser com uma cor). Esse algoritimo é considerado uma transformada que aplica métodos em pixeis de uma imagem para encontrar diferentes regiões. Além disso, ele trata a imagem como um mapa topográfico classifica as regiões com diferentes cores.

## Segmentação

A segmentação nada mais é que uma maneira de identificar as diferentes regiões de uma imagem e delimitar o contorno delas. A segmentação de 
imagens é utilizada para localizar objetos e/ou formas. O resultado da segmentação é um conjunto de regiões separadas por contornos.


## Exercício 1

Vamos praticar nossa metodologia para aplicar a segmentação de imagem.

Temos embaixo uma imagem com algumas moedas.

Entrem no [link](https://sketchpad.pro/CF31EF06D26063205C2:74bf2b1s#p5,0,0,r0,s1) e "segmentem" a imagem, lembrem-se dos contornos.

Agora apliquem a mesma metologia para segmentar uma imagem de um cerébro neste [link](https://sketchpad.pro/CF31EF06D26063205C2:74bf2b1s#p5,0,0,r0,s1).

### 

## Exercício 2

Há alguma diferença na quantidade de segmentos ao aplicar a metodologia para as duas imagens?

### 

Sim, a segunda imagem possui muito mais regiões. Depois da segmentação de uma imagem que tem diferentes regiões ou regiões grandes com tons diferentes podemos obter como resultado imagens supersegmentadas. Podemos verificar que a imagem com as moedas é uma imagem que pode acabar ficando supersegmentada, prejudicando a ánalise.

![input](input.jpg)

![image_super_segmentada](output_superSeg.png)

Quando observamos a imagem supersegmentada do cerébro podemos verificar que ouve um aproveitamento maior, pois os cerébros têm mais 
regiões que um punho de moedas, não é mesmo?

![brain](brain.jpg)

Dessa forma, existem imagens que a aplicação da metologia do algoritmo acabam ficando super segmentadas. Dessas algumas acabam ficando boas para ánalise, como a imagem supersegmentada do cérebro, outras, como é o caso das moedas, ficam difíceis de serem analisadas quando supersegmentadas.

## O algoritmo

O algoritmo recebe como entrada uma imagem em _greyscale_, ou seja, em tons de cinza. Ele interpreta essa imagem como um mapa topográfico em que os píxeis vizinhos de mesmo tom são como curvas de nível.

Os níveis de menor valor são preenchidos como uma "piscina".

Quando as "piscinas" se encontram é delimitada uma barreira na imagem. Essa barreira se extende ao longo de vários pixeís vizinhos fazendo o contorno de "territórios" em que a cor é diferente da cor adjacente.

![gif](watershed.gif)

## Como codar

O algoritimo é dividido em três passos fundamentais:

1. Todos os pixeis de valores mínimos de uma imagem grayscale, as "piscinas", são marcados uma _key_ única e inserdos em uma fila de prioridade. A interface dos pixeis pode ser representada dessa forma:

        interface Pixel {
            value: number //cor do pixel
            key: string | null //chave que representa a qual "piscina" o pixel pertence. É inicializada como null
        }

2. Logo após, é retirado um elemento desta fila e, para todos seus pixeis adjacentes com _key_ == _null_ é colocada a _key_ do elemento que foi retirado. Esses pixeis adjacentes são adicionados na fila e o processo se repete, como uma busca em largura. 

3. Quando um pixel com a _key_ x tem um pixel adjecente com _key_ y, a chave value do pixel com _key_ y é trocada para representar uma barreira.

## Complexidade

Para o algoritmo identificar onde as "piscinas" se encontraram é realizada uma iteração por todos os píxeis da imagem, ou seja, uma busca em largura. Dessa forma o watershed tem característica linear e possui complexidade O(n).

## A supersegmentação

No exemplo das moedas, o algoritimo de watershed acabou poluindo a análise, gerando várias regiões indesejadas. Isso ocorreu, visto que 
a entrada consiste de diferentes valores de pixel, formando várias "piscinas" e, consequentemente, várias regiões.

## Exercício 3

Como é possível solucionar esse problema?

###

Em uma implementação do algoritmo a utilização de marcadores iniciais pode fazer a diferença e diminuir os pontos pelos quais o algoritmo deve iterar, ou seja, diminuindo o número de "piscinas" iniciais, evitando a supersegmentação.

É possível adicionar marcadores com uma segunda imagem de entrada com as mesmas dimensões da imagem a ser segmentada contendo pontos/marcadores onde são localizados os centros das áreas conectadas. Esses pontos geralmente correspondem aos mínimos locais da imagem de entrada.

![marker](marker.png)

## Implementação

Agora vamos abrir o jupyter notebook que está na raiz deste [repositório](https://github.com/pedr0luiz/desprog-projeto).