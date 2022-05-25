Bucket Sort
======

Para compreendermos o algoritmo Bucket Sort, vamos primeiro pensar em um exemplo análogo. Imagine um baralho desorganizado.

Ele deve ter 52 cartas divididas em 4 naipes: copas, espadas, ouros e paus (se você não souber o que é cada naipe, veja aqui). Agora imagine que pediram para que você o ordenasse, sendo que as cartas ficariam em ordem crescente e dividas por naipe na seguinte sequência: espadas, ouros, copas e paus.

Se você fosse passar carta por carta, buscando o menor algarismo, os naipes ficariam embaralhados. Se você buscasse o menor naipe, os algarismos ficariam embaralhados. 

??? Checkpoint

Tendo em vista esse problema dos baralhos, de que outra forma você poderia realizar a ordenação do jogo de cartas? 

::: Gabarito

Uma metodologia comum seria, primeiramente, agrupar cartas semelhantes. Para isso, sem uma ordem numérica, incialmente, poderíamos percorrer o baralho carta a carta e olhar apenas para seu naipe. De acordo com seu o valor lido, as cartas vão ser inseridas em grupos de cartas com o mesmo naipe, ou "buckets".

Então, para cada um dos "buckets", poderíamos ordenar as cartas em ordem crescente, sem se preocupar com os naipes. 

Por fim, quando todos os buckets estiverem em ordem crescente, podemos juntá-los conforme conforme solicitado, na ordem espadas, ouros, copas e paus e o baralho estará ordenado. 

![](baralho.png)

:::

???





Construindo o código
---------
Tendo em vista como o Bucket Sort opera, vamos agora compreender o modo como ele é implementado. Como esse algoritmo se apropria bastante da utilização de vetores, faremos a implementação em Python, para facilitar a compreensão do código. 

Primeiramente, veja o pseudocódigo a seguir e pense se faz sentido de acordo com a explicação anterior do funcionamento do Bucket Sort. Além disso, considerer que será utilizado o Insertion Sort para ordenar cada bucket individualmente.

``` py
bucketSort(arr[], n)
    Encontrar o elemento máximo e mínimo da array.
    Calcular o intervalo para cada bucket.
	Criar n Buckets vazios (ou listas) com o intervalo calculado.
	Insira os elementos em seus respectivos buckets.
	Ordenar cada bucket individualmente utilizando Insertion Sort.
	Juntar todos os buckets ordenados em um único vetor.
```

!!! Aviso
Só continue o handout se você entendeu o pseudocódigo!
!!!

??? Atividade

Vamos começar pelo primeiro loop do pseudocódigo. Tente implementar em Python a seguinte lógica:

``` py
bucketSort(arr[], n)
    Encontrar o elemento máximo e mínimo da array.
    
```

::: Gabarito

``` py
def bucketSort(arr, noOfBuckets):
    max_ele = max(arr)
    min_ele = min(arr)
```
:::

???

??? Atividade

Agora vamos para o segundo loop. Tente implementar em Python e adicione ao código do item anterior a lógica abaixo:

``` py
    Calcular o intervalo para cada bucket.	
```

::: Gabarito

``` py
def bucketSort(arr, noOfBuckets):
    max_ele = max(arr)
    min_ele = min(arr)
 
    rnge = (max_ele - min_ele) / noOfBuckets
```
:::

???
??? Atividade

Agora vamos para o segundo loop. Tente implementar em Python e adicione ao código do item anterior a lógica abaixo:

``` py
    Criar n Buckets vazios (ou listas) com o intervalo calculado.
	
```

::: Gabarito

``` py
def bucketSort(arr, noOfBuckets):
    max_ele = max(arr)
    min_ele = min(arr)
 
    rnge = (max_ele - min_ele) / noOfBuckets
 
    temp = []
 
    for i in range(noOfBuckets):
        temp.append([])
```
:::

???
??? Atividade

Agora vamos para o segundo loop. Tente implementar em Python e adicione ao código do item anterior a lógica abaixo:

``` py
    Insira os elementos em seus respectivos buckets.
```

::: Gabarito

``` py
def bucketSort(arr, noOfBuckets):
    max_ele = max(arr)
    min_ele = min(arr)
 
    rnge = (max_ele - min_ele) / noOfBuckets
 
    temp = []
 
    for i in range(noOfBuckets):
        temp.append([])

    for i in range(len(arr)):
        diff = (arr[i] - min_ele) / rnge -
              int((arr[i] - min_ele) / rnge)
 
        if(diff == 0 and arr[i] != min_ele):
            temp[int((arr[i] - min_ele) / rnge) - 1].append(arr[i])
 
        else:
            temp[int((arr[i] - min_ele) / rnge)].append(arr[i])
```
:::

???

??? Atividade

Agora vamos para o segundo loop. Tente implementar em Python e adicione ao código do item anterior a lógica abaixo:

``` py
	Ordenar cada bucket individualmente utilizando Insertion Sort.
```

::: Gabarito

``` py
def bucketSort(arr, noOfBuckets):
    max_ele = max(arr)
    min_ele = min(arr)
 
    rnge = (max_ele - min_ele) / noOfBuckets
 
    temp = []
 
    for i in range(noOfBuckets):
        temp.append([])
 
    for i in range(len(arr)):
        diff = (arr[i] - min_ele) / rnge -
              int((arr[i] - min_ele) / rnge)
 
        if(diff == 0 and arr[i] != min_ele):
            temp[int((arr[i] - min_ele) / rnge) - 1].append(arr[i])
 
        else:
            temp[int((arr[i] - min_ele) / rnge)].append(arr[i])
 
    for i in range(len(temp)):
        if len(temp[i]) != 0:
            temp[i].sort()
```
:::

???

??? Atividade

Agora vamos para o segundo loop. Tente implementar em Python e adicione ao código do item anterior a lógica abaixo:

``` py
	Juntar todos os buckets ordenados em um único vetor.
```

::: Gabarito

``` py
def bucketSort(arr, noOfBuckets):
    max_ele = max(arr)
    min_ele = min(arr)

    rnge = (max_ele - min_ele) / noOfBuckets
 
    temp = []

    for i in range(noOfBuckets):
        temp.append([])
 

    for i in range(len(arr)):
        diff = (arr[i] - min_ele) / rnge -
              int((arr[i] - min_ele) / rnge)
 

        if(diff == 0 and arr[i] != min_ele):
            temp[int((arr[i] - min_ele) / rnge) - 1].append(arr[i])
 
        else:
            temp[int((arr[i] - min_ele) / rnge)].append(arr[i])
 

    for i in range(len(temp)):
        if len(temp[i]) != 0:
            temp[i].sort()
 

    k = 0
    for lst in temp:
        if lst:
            for i in lst:
                arr[k] = i
                k = k+1
```
:::

???









De modo análogo, o **bucket sort**, ou bin sort, é um algoritmo de ordenação que funciona dividindo um vetor em um **número finito de recipientes**. Cada recipiente é então ordenado individualmente, seja usando um algoritmo de ordenação diferente, ou usando o algoritmo bucket sort recursivamente. Abaixo está um exemplo do Bucket Sort sendo aplicado.

:Slide

É muito comum o algoritmo utilizado nos recipientes do Bucket Sort ser o **Insertion Sort**. 

??? Checkpoint

Para compreendermos melhor o funcionamento do Bucket Sort, vamos separar o vetor $[ 12, 30, 8, 22, 5, 7, 15, 27, 20, 9, 16 ]$ em seus respectivos recipientes (assim como foi feito no exemplo acima). 

*Pense nos intervalos para dividir os números igualmente entre os buckets*


::: Gabarito

![](ex1.png)

:::

???







Complexidade e casos de uso
---------

Em se tratando de complexidade, você deve ter imaginado que o modo como os algarismos são distribuídos dentro do vetor ordenado pelo Bucket Sort influencia o tempo de ordenação.

??? Atividade

Considerando a implementação do Bucket Sort acima, qual você imagina que seria o pior caso de ordenação por Bucket Sort?

::: Dica

Imagine a ordenação do seguinte vetor nos buckets do exemplo anterior:

[1 2 3 4 5 6 7 8 9]

:::

::: Gabarito

O pior caso de ordenação seria justamente o do vetor [1 2 3 4 5 6 7 8 9] nos buckets do exemplo, já que todos os elementos vão cair no mesmo bucket, tornando inútil a divisão do vetor em buckets.

:::

???

Desse modo, pode-se considerar que, no **pior caso**, se todos os elementos caírem no mesmo bucket, a **complexidade** será **igual à** própria **complexidade do algoritmo de ordenação**.

??? Atividade

E qual você imagina que seria o melhor caso de ordenação por Bucket Sort?

::: Gabarito

O melhor caso de ordenação ocorre quando os elementos do vetor são distribuídos homogeneamente entre os buckets. 

:::

???

Agora considerando o **melhor caso**, é um pouco mais complicado de analisar a complexidade. A fim de exemplo, vamos imaginar que o algoritmo de ordenação é o **Insertion Sort**, que é adequado para o Bucket Sort, pois ele é bom para vetores pequenos e espera-se que os buckets contenham vetores pequenos.

Considerando que a complexidade do Insertion Sort no pior caso é $O(n^2)$ e que, se 
a distribuição é boa e você tem $k$ buckets, o tamanho de cada bucket é $n/k$ e a complexidade será igual a $O((n/k)^2)$, isto é, $O(n^2/k^2)$.
Como isso será feito para os $k$ buckets, a complexidade total dessa fase será igual a $O((n^2/k^2)·k)$, isto é, **$O(n^2/k)$**.


??? Atividade

Considerando essa complexidade, em que tipos de vetor você acredita que o Bucket Sort operaria de forma mais rápida?

::: Gabarito

O Bucket Sort melhor performa, em termos de tempo, em vetores grandes, quanto maior o valor de $k$.

:::

???

Isso significa que, se o seu $k$ não foi muito pequeno, você consegue fazer com que a complexidade fique melhor do que $O(n^2)$. Em particular, se $k$ for proporcional a $n^2$, a complexidade se tornará linear.

Desse modo, muitas vezes, o Bucket Sort é utilizado como algoritmo de ordenação externo, especialmente se você precisa ordenar um **vetor que é tão grande que não cabe na sua memória**.