Variáveis
---------

Esse vai ser um resumo rápido, não deve ser novidade a forma com o Scala manipula valores (imutáveis) e variáveis (mutáveis):

##### Python:
```python
>>> foo = "Apples"
>>> baz = foo + " and Oranges."
>>> baz
'Apples and Oranges.'
>>> baz = "Only Grapes."
```

##### Scala:
```scala
scala> val foo = "Apples"
foo: String = Apples

scala> val baz = foo + " and Oranges."
baz: String = Apples and Oranges.

scala> baz
res60: String = Apples and Oranges.

// Em escala, *vals* são imutáveis
scala> baz = "Only Grapes."
<console>:13: error: reassignment to val
       baz = "Only Grapes."

// Criando uma variável 
scala> var baz = "Apples and Oranges."
baz: String = Apples and Oranges.

scala> baz = "Only Grapes."
baz: String = Only Grapes.

scala> var one = 1
one: Int = 1

scala> one += 1

scala> one
res21: Int = 2
```

Scala também permite variáveis fortemente tipadas, ao invés de deixar o compilador interpretar o seu tipo.

##### Scala

```scala
scala> val foo: String = "Apples"
foo: String = Apples
```

Python e Scala permitem atribuição múltipla de valores. Contudo, você deve ser cuidadoso com Python ao passar por referência! Você geralmente vai querer desempacotar atribuições múltiplas.

##### Scala:
```scala
scala> val foo, bar = Array(1, 2, 3)
foo: Array[Int] = Array(1, 2, 3)
bar: Array[Int] = Array(1, 2, 3)

// *foo* and *bar* não fazem referência a mesma posição de memória.
scala> bar(0) = 4

scala> bar
res70: Array[Int] = Array(4, 2, 3)

scala> foo
res71: Array[Int] = Array(1, 2, 3)
```

O mesmo pode ser feito com Python desempacotando:

```python
>>> foo, bar = [1, 2, 3], [1, 2, 3]

# Eles estão fazendo referência a mesma posição na memória?
>>> foo is bar
False

O que acontece quando você muda *bar*?
>>> bar[0] = 4
>>> bar
[4, 2, 3]
>>> foo
[1, 2, 3]

# Você *pode* atribuir tanto a *foo* com a  *bar* o mesmo valor, mas eles fazem referência a mesma posição de memória!
>>> foo = bar = [1, 2, 3]
>>> foo is bar
True
>>> bar[0] = 4
>>> bar
[4, 2, 3]
>>> foo
[4, 2, 3]
```

Scala e Python compartilham a maior parte dos operadores aritméticos. Nos bastidores, ambos usam métodos para implementar os operadores - Scala usa o símbolo atual do operador, em vez de um caractere alfanumérico

##### Python
```python
>>> foo = 1

# O que está acontecendo nos bastidores?
>>> foo.__add__(4)
5
```

##### Scala
```scala
scala> val foo = 1
foo: Int = 1

scala> foo + 1
res72: Int = 2

// O que está acontecendo nos bastidores:
scala> foo.+(1)
res73: Int = 2
```
