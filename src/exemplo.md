Bucket Sort
======

Para compreendermos o algoritmo Bucket Sort, vamos primeiro pensar em um exemplo análogo. Imagine um baralho desorganizado.

Ele deve ter 52 cartas divididas em 4 naipes: copas, espadas, ouros e paus (se você não souber o que é cada naipe, veja aqui). Agora imagine que pediram para que você o ordenasse.

!!! OBSERVAÇÃO
Imagine que o critério utilizado é priorizar a ordem dos **números** acima dos naipes. Dessa forma seria muito complicado, pois é confuso a questão da ordenação dos naipes, já que eles não possuem uma ordem muito definida.
!!!

??? Checkpoint

Tendo em vista os pontos levantados, qual estratégia voce utilizaria para ordenar um baralho? 

::: Gabarito

Uma metodologia comum seria, primeiramente, agrupar cartas olhando apenas para seu naipe. De acordo com o seu símbolo, as cartas vão ser inseridas em grupos de cartas com o mesmo naipe.

Então, para cada um dos conjuntos de um mesmo naipe, poderíamos ordenar as cartas em ordem crescente, sem se preocupar com os naipes, pois seriam todos do mesmo. 

Por fim, quando todos os conjuntos de cartas do mesmo naipe estiverem em ordem crescente, podemos juntá-los conforme conforme solicitado. 

![](baralho.png)

:::

???

A ideia do algoritmo
---------
De forma semelhante ao exemplo acima, o Bucket Sort é um algoritmo de ordenação que se baseia na ideia de buckets, isso é, ele agrupa os elementos 
por um intervalo numérico, e dentro desse intervalo, ele ordena os algarismos. 

Ele é um algoritmo relativamente simples, mas existem algumas etapas que exigem um pouco mais de reflexão por não serem tão triviais:

??? Atividade 1

Vamos começar a entender melhor o Bucket Sort entendendo como calcular os **intervalos** dos buckets:

Supondo que serão criados 3 buckets, dado o vetor $v = [8,2,7,3,5,4,6,9]$, como fazer para calcular os intervalos para alocar corretamente cada um dos valores?

!!! DICA
O que aconteceria se fossem outros valores no vetor, ou se fossem criados mais buckets? Mudaria os intervalos? 
!!!

::: Gabarito

Vamos começar encontrando o intervalo total do vetor, isso é, encontrar o **maior** e **menor** valor e calcular a diferença de ambos. Em seguida, dividiremos pelo número de buckets para dividir igualmente os intervalos. Por último, vamos arredondar para cima esse valor.

:::



???


Construindo o código
---------
Tendo em vista como o Bucket Sort opera, vamos agora compreender o modo como ele é implementado. Como esse algoritmo se apropria bastante da utilização de vetores, faremos a implementação em Python, para facilitar a compreensão do código.

Primeiramente, veja o pseudocódigo a seguir e pense se faz sentido de acordo com a explicação anterior do funcionamento do Bucket Sort. 

``` py
bucketSort(arr, n_buckets)

    Encontrar o elemento máximo e mínimo da array.

    Calcular o intervalo para cada bucket.

    Criar n Buckets vazios (ou listas) com o intervalo calculado.
    
    Insira os elementos em seus respectivos buckets.

    Ordenar cada bucket individualmente utilizando um algoritmo de ordenação.

    Juntar todos os buckets ordenados em um único vetor.
```


Vamos por partes! Para conseguirmos dividir o nosso vetor em buckets, precisamos saber quais são os seus limites, concorda? E é justamente essa a primeira operação realizada pelo pseudocódigo.

??? Atividade

Veja o trecho em questão e tente implementá-lo em **Python**.

``` py
bucketSort(arr, n_buckets)
    Encontrar o elemento máximo e mínimo da array.
    
```

::: Gabarito

``` py
def bucketSort(arr, n_buckets):
    max_ele = max(arr)
    min_ele = min(arr)
```
:::

???

Após descobrirmos o máximo e mínimo da array, podemos segmentar esse intervalo nos referidos buckets. Lembre-se que o número de buckets será passado como argumento da função.

??? Atividade

Tendo isso em vista, como você calcularia o tamanho do intervalo dos buckets considerando o pseudocódigo abaixo? Tente implementar em **Python** e adicione ao código do item anterior.

``` py
    Calcular o intervalo para cada bucket.	
```

::: Gabarito

``` py
def bucketSort(arr, n_buckets):
    max_ele = max(arr)
    min_ele = min(arr)

    rnge = ceil((max_ele - min_ele) / n_buckets)
```
Perceberam que colocamos a função *ceil*? Ela serve para arredondarmos o valor para cima quando o resultado não é um inteiro.

:::

Pronto, agora temos o tamanho do intervalo de cada bucket, mas os buckets em si ainda não foram criados. Esta será a próxima etapa do código.

??? Atividade

Levando isso em consideração, tente implementar em **Python** e adicione ao código do item anterior a lógica abaixo:

**Dica:** Lembre-se novamente que o número de buckets é passado como argumento da função *bucketSort*.

``` py
    Criar n Buckets vazios (ou listas) com o intervalo calculado.
	
```

::: Gabarito

``` py
def bucketSort(arr, n_buckets):
    max_ele = max(arr)
    min_ele = min(arr)

    rnge = ceil((max_ele - min_ele) / n_buckets)
    temp = []

    for i in range(n_buckets):
        temp.append([])
```
:::

???

Agora que temos os buckets criados e os seus respectivos intervalos, precisamos separar os elementos dentro de cada um deles. Pense que para isso precisamos realizar duas operações:

    1) Ver em qual dos buckets cada elemento está localizado. 
    
    2) Colocá-lo em seu devido bucket.

??? Atividade

Com base nessas duas operações, tente implementar em **Python** e adicione ao código do item anterior a lógica abaixo:

``` py
    Insira os elementos em seus respectivos buckets.
```

::: Gabarito

``` py
def bucketSort(arr, n_buckets):
    max_ele = max(arr)
    min_ele = min(arr)

    rnge = ceil((max_ele - min_ele) / n_buckets)
    temp = []

    for i in range(n_buckets):
        temp.append([])

    for i in range(len(arr)):
        #Verifica em qual dos buckets o elemento está localizado e guarda na variável diff:
        diff = floor((arr[i] - min_ele) / rnge)
        
        #Se o bucket estiver na lista temp, adicionamos o elemento em seu respectivo bucket:
        if(diff == len(temp)):
            temp.append([arr[i]])

        #Caso o bucket não esteja na lista temp, criamos um novo bucket e colocamos o elemento:
        else:
            temp[diff].append(arr[i])

```


:::

???

A próxima etapa, depois de organizar os elementos nos respectivos buckets, é ordená-los dentro de cada bucket com um algoritmo de ordenação.

??? Atividade
Considerando o que você aprendeu sobre os algoritmos de ordenação dados em aula, qual seria o mais eficiente para esse caso?

**Dica:** pense no tamanho do vetor!

::: Gabarito

Como a função do bucket sort seja dividido em vários vetores pequenos, faz sentido buscar um algoritmo de ordenção que possua melhor complexidade para vetores menores.Se considerarmos o tempo na prática,o melhor algoritmo de ordenação para ser usado seria o **Insertion Sort**.
:::
???

??? Atividade

Sabendo da resposta do item anterior, tente implementar em **Python** e adicione ao código do item anterior a lógica abaixo:

``` py
	Ordenar cada bucket individualmente utilizando um algoritmo de ordenação.
```

::: Gabarito

``` py
def bucketSort(arr, n_buckets):
    max_ele = max(arr)
    min_ele = min(arr)

    rnge = ceil((max_ele - min_ele) / n_buckets)
    temp = []

    for i in range(n_buckets):
        temp.append([])

    for i in range(len(arr)):
        diff = floor((arr[i] - min_ele) / rnge)
        
        if(diff == len(temp)):
            temp.append([arr[i]])
 
        else:
            temp[diff].append(arr[i])

    for i in range(len(temp)):
        if len(temp[i]) != 0:
            insertion_sort(temp[i],len(temp[i]))
```
:::

???

Para finalizar, precisamos juntar todos os buckets em um único vetor.

??? Atividade

Tente implementar em **Python** e adicione ao código do item anterior a lógica abaixo:

``` py
	Juntar todos os buckets ordenados em um único vetor.
```

::: Gabarito

``` py
def bucketSort(arr, n_buckets):
    max_ele = max(arr)
    min_ele = min(arr)

    rnge = ceil((max_ele - min_ele) / n_buckets)
    temp = []

    for i in range(n_buckets):
        temp.append([])

    for i in range(len(arr)):
        diff = floor((arr[i] - min_ele) / rnge)
        
        if(diff == len(temp)):
            temp.append([arr[i]])
 
        else:
            temp[diff].append(arr[i])

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


::: Gabarito

O pior caso de ordenação seria justamente quando todos os elementos acabam no mesmo bucket, tornando inútil a divisão do vetor neles. 

:::

???

??? Atividade

Vamos supor que estamos utilizando o Insertion Sort para ordenar os buckets. Sabendo que a complexidade dele é $O(n^2)$, qual vai ser a complexidade no pior caso do Bucket Sort?


::: Gabarito

No **pior caso**, se todos os elementos caírem no mesmo bucket, a **complexidade** será **igual à** própria **complexidade do algoritmo de ordenação**, portanto será $O(n^2)$.

:::

???


??? Atividade

E qual você imagina que seria o melhor caso de ordenação por Bucket Sort?

::: Gabarito

O melhor caso de ordenação ocorre justamente quando os elementos do vetor são distribuídos homogeneamente entre os buckets.

:::

???

??? Atividade

Supondo novamente que estamos utilizando o Insertion Sort $(O(n^2))$ para ordenar os buckets, qual vai ser a complexidade no melhor caso do Bucket Sort? 

**OBS:.** Considere que existem **k** buckets e **n** inteiros no vetor original. Dessa forma em cada bucket terá $\frac{n}{k}$ algarismos.

::: Gabarito
O **melhor caso**, é um pouco mais trabalhoso de analisar a complexidade. Como foi mencionado, em cada bucket terá $\frac{n}{k}$ algarismos, então a complexidade será $O((n/k)^2)$, isto é, $O(n^2/k^2)$.
Como isso será feito para os $k$ buckets, a complexidade total dessa fase será igual a $O((n^2/k^2)·k)$, isto é, **$O(n^2/k)$**.

:::

???



??? Atividade

Considerando essa complexidade, em que tipos de vetor você acredita que o Bucket Sort operaria de forma mais rápida?

::: Gabarito

O Bucket Sort melhor performa, em termos de tempo, em vetores grandes, quanto maior o valor de $k$.

:::

???

Isso significa que, se o seu $k$ não foi muito pequeno, você consegue fazer com que a complexidade fique melhor do que $O(n^2)$. Em particular, se $k$ for proporcional a $n$, a complexidade se tornará linear.

Desse modo, muitas vezes, o Bucket Sort é utilizado como algoritmo de ordenação externo, especialmente se você precisa ordenar um **vetor que é tão grande que não cabe na sua memória**.

