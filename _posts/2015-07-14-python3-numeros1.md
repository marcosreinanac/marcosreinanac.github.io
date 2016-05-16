---
layout: post
title:  "Python 3 - Números: o básico"
---


## Tipos de dados numéricos

Existem três tipos de dados para números na versão atual do Python. Seja introduzido a eles e a como lidar com os mesmos abaixo.

### O tipo "int"

Tipo de dados para números inteiros (engloba o antigo tipo *long*).

{% highlight python %}
>>> 1  # bem chato, mesmo... A perfeição é chata.
1
{% endhighlight %}


### O tipo "float"

Tipo para os reais. 

{% highlight python %}
>>> 6.2831853072  # isto é um float; um número racional. Na verdade, se você
6.2831853072      # sabe que número é esse, sabe que ele não é racional. Se
                  # não sabe, tenha sua mente explodida lendo sobre o "Tau"!
{% endhighlight %}

*Float* vem do inglês *floating point* - números "de ponto flutuante" - assim chamados por usarem notação matemática similar à científica, mas em base 2, o que facilita cálculos envolvendo números fracionários nas máquinas digitais. Existe um problema com os *floating point numbers*. Leia sobre ele [aqui]({* post_url problemas-com-floating-numbers *}). ~~me lembre de fazer esse post!~~


### O tipo "complex"

Tipo numérico para os complexos.

{% highlight python %}
>>> 2 + 3j  # forma padrão "a + bi | a, b ∈ R"; j = i = sqrt(-1)
(2+3j)

>>> (2+3j)  # também dá pra mandar desse jeito diferentoso que ele retorna
(2+3j)

>>> 5j      # E assim, no caso de a parte real ser 0.
5j

>>> 
{% endhighlight %}


## Ordem de abrangência numérica

Uma operação entre números sempre tem como resultado um outro número de tipo igual ou mais geral. O tipo será igual ao tipo mais abrangente entre os operandos, a menos que estejamos falando de uma divisão entre inteiros quaisquer, o que geraria um "float", ou da raiz de um negativo, que retornaria um "complex".
A ordem de abrangência numérica (em ordem crescente) é a seguinte:

* int
* float
* complex

Para provar isso no Python, vou utilizar a função type(), que retorna o tipo (seja número, lista, string, ou classe que for) da informação posta entre os parêntesis (argumento).

{% highlight python3 %}
>>> type(1 + 1)
<class 'int'>

>>> type(2 - 1)
<class 'int'>

>>> type(4 * 2)
<class 'int'>

>>> type(4 / 2)
<class 'float'>

>>> type(2 ** 2)
<class 'int'>

>>> type(4 ** (1/2))
<class 'float'>

>>> type(3 // 2)
<class 'int'>

>>> type(2j - 3)
<class 'complex'>

>>> type(3 * 2j)
<class 'complex'>

type(2.28/2.28)
<class 'float'>

>>> type(2j / 2j)
<class 'complex'>
{% endhighlight %}


## Transformando tipos numéricos em outros

Pode-se transformar um float num inteiro, cortando seus decimais, pela função *int(umFloatQualquer)*. Pode-se ainda transformar um inteiro num float pela função *float(umIntQualquer)*. pode-se passar qualquer um destes para complex, o tipo numérico mais abrangente, por meio da função *complex(umNúmeroQualquer)*, mas a recíproca não é verdadeira. Na realidade, a função *complex* toma dois argumentos: o primeiro e o segundo serão, respectivamente, as partes real e imaginária do complexo a ser retornado; se o segundo argumento é omitido, ele é tomado por 0.  Caso um número seja transformado em seu próprio tipo, nenhum erro será acionado. Nada acontecerá, além do retorno do argumento dado. 

Aqui:

{% highlight python %}
>>> int(3.0)  # float
3             # int

>>> float(3)  # int
3.0           # float

>>> complex(3)  #int
(3+0j)          #complex

>>> complex(3.1, 4.56)  #float
(3.1+4.56j)             # complex

>>> int(1j)  # vai dar erro; a parte complexa não é simplesmente cortada

>>> float(1j)  # igualmente

>>> int(1)  # int
1           # int

>>> float(1.0)  # float
1.0             # float
{% endhighlight %}


## Operadores numéricos básicos

Os operadores básicos do Python são:

Operador | Função
 :--- | :---
a + b | adição
a - b | subtração
a * b | multiplicação
a / b | divisão
a ** b | exponenciação
a // b | divisão inteira
a % b | resto da divisão inteira
divmod(a, b) | retorna (a // b, x % y)
abs(a) | módulo de *a*; é o mesmo operador usado para complexos (módulo)
round(a[, n]) | arredonda número para *n* casas decimais; se *n* for omitido, será 0


Obs.: a norma PEP-8 recomenda a utilização de espaços entre os operadores e os operandos para uma maior legibilidade.

Exemplos e explicações:

{% highlight python %}
>>> 1 + 1  # soma
2

>>> 1 - 2  # subtração
-1

>>> 3 * 3  # multiplicação
9

>>> 3 / 4  # divisão
0.75

>>> 2 ** 2  # exponenciação
4

>>> 2 ** (1/2)      # raiz --> exponenciação de fração:
1.4142135623730951  # raiz de xº grau de um número n = n ** (1/x)

>>> 5 // 2  # divizão inteira --> aquela divisão moleque, aquela divisão raiz,
2           # aquela divisão da alfabetização. A que sobra resto e você para aí.

>>> 5 % 2   # o resto de uma divisão inteira
1           # 5/2 = 2; 5 = 2 * 2 (+ 1 de resto)

>>> divmod(5,2)
(2, 1)
>>> div, resto = divmod(5,2)
>>> print(div)
2
>>> print(resto)
1

>>> abs(-2)        # módulo...   
2
>>> abs(-31.5)     # módulo...
31.5
>>> abs(-5+6j)      # módulo... Sim, é vetorial!
7.810249675906654

>>> 3+5j.conjugate()  # conjugado de 3+5j (3-5j)   
(3-5j)

>>> round(3.45, 1)
3.5
>>> round(3.45)
3
{% endhighlight %}