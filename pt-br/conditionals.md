Expressões Condicionais
-----------------------

Em Scala são representados por `if/else/else-if`, isso é muito familiar para quem escreve no estilo da linguagem C.

##### Python
```python
>>> x = 0
# Inline: expressão_se_verdadeiro if condição else expressão_se_falso
>>> foo = 1 if x > 0 else -1
>>> foo
-1
# Expressões quebradas em múltiplas linhas
if x == 1:
    foo = 5
elif x == 0:
    foo = 6
>>> foo
6
>>>
if isinstance('foo', str):
    print('Foo is string')
else:
    print('Foo is not string')

Foo is string
```

##### Scala
```scala
scala> val x = 0
x: Int = 0

// Inline: Expressão atribuída a variável
scala> val foo = if (x > 0) 1 else -1
foo: Int = -1

scala> var baz = 1
baz: Int = 1

// Modo paste 
scala> :paste

// Entering paste mode (ctrl-D to finish)
// Kernighan & Ritchie preferem o suporte ao estilo de expressões em várias linhas
if (x == 0) {
  baz = 5
}

// Exiting paste mode, now interpreting.

scala> baz
res90: Int = 5

// Mas para expressões simples, tente mantê-las em uma linha
scala> if (x == 0) baz = 6

scala> baz
res94: Int = 6

scala>

if (foo.isInstanceOf[String]) {
    print("Foo is a string!")
} else if (foo.isInstanceOf[Int]) {
    print("Foo is an int!")
} else {
    print("I dont know what foo is...")
}

Foo is a string!
```

*Loops* devem ser familiares, veja:

##### Python
```python
n = 0
nlist = []
while n < 5:
    nlist.append(n)
    n += 1
>>> nlist
[0, 1, 2, 3, 4]
```

A seguir podemos tratar como uma *comprehension*, que é uma abordagem mais funcional:

##### Scala
```scala
var n: Int = 0

// ArrayBuffer é um array mutável que age como lista em Python.  
scala> import scala.collection.mutable.ArrayBuffer
import scala.collection.mutable.ArrayBuffer

scala> var nlist = ArrayBuffer[Int]()
nlist: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer()

scala>

while (n < 5) {
    nlist += n
    n += 1
}

scala> nlist
res115: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(0, 1, 2, 3, 4)
}
```

Para *loops* e *comprehension*, o último é provável que seja desperdiçado por programadores Python e Java. Scala suporta uma sintaxe `for (variable <- expression)`. Vamos ver primeiro em Python:

##### Python
```python
foo = "Apple"
n = 0
for a in foo:
    n += 1
>>> n
5
```

##### Scala
```scala
scala> val foo = "Apple"

scala> var n = 0

scala>
for (x <- foo) {
    n += 1
}

scala> n
res140: n: Int = 5

// Isso poderá ser melhor expressado em uma linha.
scala> n = 0

scala> for (x <- foo) n += 1

scala> n
res141: n: Int = 5
```

*Comprehension* em Python são partes muito importantes de escrita idiomática do Python; Scala suporta o mesmo com a sintaxe `yeld`:


##### Python
```python
>>> [f + 1 for f in [1, 2, 3, 4, 5]]
[2, 3, 4, 5, 6]
```

##### Scala
```scala
scala> for (f <- Array(1, 2, 3, 4, 5)) yield f + 1
res59: Array[Int] = Array(2, 3, 4, 5, 6)
```

Python tem uma função muito útil chamada `zip` que permite iterar sobre *iterables* ao mesmo tempo. Scala permite a você ter múltiplos "generators" em uma expressão, que pode ser replicada para um comportamento `zip`.

##### Python
```python
foo, bar = [1, 2, 3], ['a', 'b', 'c']
foobars = {}
for f, b in zip(foo, bar):
    foobars[b] = f
>>> foobars
{'a': 1, 'c': 3, 'b': 2}

# E mais Pythonic usando *comprehension*
>>> {b: f for f, b in zip(foo, bar)}
{'a': 1, 'c': 3, 'b': 2}
```

##### Scala
```scala
val foo = Array(1, 2, 3)
val bar = Array("a", "b", "c")

import scala.collection.mutable.Map

// Vamos especificar o tipo, desde que os conhecemos 
var foobars= Map[String, Int]()

for (f <- foo; b <- bar) foobars += (b -> f)
scala> foobars
res5: scala.collection.mutable.Map[String,Int] = Map(b -> 3, a -> 3, c -> 3)

// Isso é realmente poderoso - nós não estamos limitados a dois iterables
val baz = Array("apple", "orange", "banana")
val mapped = Map[String, (Int, String)]()
for (f <- foo; b <- bar; z <- baz) mapped += (z -> (f, b))
scala> mapped
res7: scala.collection.mutable.Map[String,(Int, String)] = Map(banana -> (3,c), orange -> (3,c), apple -> (3,c))

// É interessante notar que Scala também tem um método `zip` explicito
val arr1 = Array(1, 2, 3)
val arr2 = Array(4, 5, 6)

scala> arr1.zip(arr2)
res240: Array[(Int, Int)] = Array((1,4), (2,5), (3,6))
```

O `enumerate` do Python é um recurso muito interessante, é semelhante ao `zipWithIndex` do Scala:

##### Python
```python
>>> [(x, y) for x, y in enumerate(["foo", "bar", "baz"])]
[(0, 'foo'), (1, 'bar'), (2, 'baz')]
```

##### Scala
```scala
scala> for ((y, x) <- Array("foo", "bar", "baz").zipWithIndex) yield (x, y)
res27: Array[(Int, String)] = Array((0,foo), (1,bar), (2,baz))

// Observe que simplesmente chamando zipWithIndex o retornado é algo parecido, mas com valores em ordem inversa.
scala> Array("foo", "bar", "baz").zipWithIndex
res31: Array[(String, Int)] = Array((foo,0), (bar,1), (baz,2))
```

Scala permite expressões "guard", que é o mesmo que expressões de controle de fluxo em Python:

##### Python
```python
foo = [1,2,3,4,5]
bar = [x for x in foo if x != 3]
>>> bar
[1, 2, 4, 5]
```

##### Scala
```scala
val foo = Array(1, 2, 3, 4, 5)
var bar = ArrayBuffer[Int]()
for (f <- foo if f != 3) bar += f
scala> bar
res136: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 2, 4, 5)

// Você pode empilhar guards
scala> for (x <- (1 to 5).toArray if x != 2 if x != 3) yield x
res44: Array[Int] = Array(1, 4, 5)
```

Observe que em muitos casos, isso pode ser muito sucinto, para usar `map` versus `for-comprehension`:

##### Scala
```scala
scala> for (c <- Array(1, 2, 3)) yield c + 2
res56: Array[Int] = Array(3, 4, 5)

scala> Array(1, 2, 3).map(_ + 2)
res57: Array[Int] = Array(3, 4, 5)
```
