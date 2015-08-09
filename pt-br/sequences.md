Sequencias
---------

Scala tem um número muito grande de estruturas sequencias para escolher. Isso inclui List (linked-lists), Arrays (arrays imutavéis), Vetores (arrays mutaveis com tamanho fixo), e ArrayBuffers (arrays mutavies com tamanho variável).

Naturalmente você deve escolher a estrutura de dados que melhor se adapta ao seu problema. Nos vamos ver brevemente Vetores, Arrays e ArrayBuffers. Esse último se assemelha a listas em Python.

Vetor é a melhor sequencia imutavel em Scala. Abaixo você podem ver uma sequencia de operações que pode se feita em Scala, incluido um pouco de programação funcional.

##### Scala:
```scala
scala> val vector = Vector(1, 2, 3)
vector: scala.collection.immutable.Vector[Int] = Vector(1, 2, 3)

scala> vector.map(_ + 2)
res30: scala.collection.immutable.Vector[Int] = Vector(3, 4, 5)

scala> vector.count(_ == 2)
res31: Int = 1

scala> Vector(1, 2, 3, 4, 5).drop(3)
res33: scala.collection.immutable.Vector[Int] = Vector(4, 5)

scala> vector.exists(_ == 4)
res35: Boolean = false

scala> vector.take(2)
res8: scala.collection.immutable.Vector[Int] = Vector(1, 2)

scala> Vector(1, 20, 3, 25).reduce(_ + _)
res4: Int = 49

scala> Vector(3, 4, 4, 5, 3).distinct
res5: scala.collection.immutable.Vector[Int] = Vector(3, 4, 5)

scala> Vector(1, 20, 3, 25).partition(_ > 10)
res2: (scala.collection.immutable.Vector[Int], scala.collection.immutable.Vector[Int]) = (Vector(20, 25),Vector(1, 3))

scala> Vector("foo", "bar", "baz", "foo", "bar").groupBy(_ == "foo")
res0: scala.collection.immutable.Map[Boolean,scala.collection.immutable.Vector[String]] = Map(false -> Vector(bar, baz, bar), true -> Vector(foo, foo))

scala> Vector(1, 20, 3, 25).groupBy(_ > 10)
res1: scala.collection.immutable.Map[Boolean,scala.collection.immutable.Vector[Int]] = Map(false -> Vector(1, 3), true -> Vector(20, 25))

scala> vector.filter(_ != 2)
res9: scala.collection.immutable.Vector[Int] = Vector(1, 3)

scala> vector.max
res11: Int = 3

scala> Vector(3, 2, 1).sorted
res17: scala.collection.immutable.Vector[Int] = Vector(1, 2, 3)

scala> Vector("fo", "fooooo", "foo", "fooo").sortWith(_.length > _.length)
res17: scala.collection.immutable.Vector[String] = Vector(fooooo, fooo, foo, fo)

scala> vector.sum
res15: Int = 6

scala> Vector(Vector(1, 2, 3), Vector(4, 5, 6)).flatten
res28: scala.collection.immutable.Vector[Int] = Vector(1, 2, 3, 4, 5, 6)

// Outra maneira de fazer a operação anterio
scala> Vector.concat(Vector(1, 2, 3), Vector(4, 5, 6))
res16: scala.collection.immutable.Vector[Int] = Vector(1, 2, 3, 4, 5, 6)

scala> Vector(1, 2, 3).intersect(Vector(3, 4, 5))
res7: scala.collection.immutable.Vector[Int] = Vector(3)

scala> Vector(1, 2, 3).diff(Vector(3, 4, 5))
res8: scala.collection.immutable.Vector[Int] = Vector(1, 2)
```

O Array tem um tamanho fixo, assim é possível fazer a inicialização dos valores.

##### Python:
```python
# These are contrived - you will rarely see the need for this in Python outside of NumPy
# Esse são inventados - você raramente vai ver uma necessidade disso em Python fora do NumPy
ten_zeroes = [0]*10
ten_none = [None]*10
```

##### Scala
```scala
scala> val init_int = new Array[Int](10)
init_int: Array[Int] = Array(0, 0, 0, 0, 0, 0, 0, 0, 0, 0)

scala> val init_str = new Array[String](10)
init_str: Array[String] = Array(null, null, null, null, null, null, null, null, null, null)

scala> Array.tabulate(3)(a => a + 5)
res20: Array[Int] = Array(5, 6, 7)

scala> Array.tabulate(3)(a => a * 5)
res21: Array[Int] = Array(0, 5, 10)

scala> Array.fill(3)(10)
res22: Array[Int] = Array(10, 10, 10)
```

ArrayBuffer é uma sequencia mutavel, e funcional de forma semelhante as listas em Python.

##### Python:
```python
int_list = []
int_list.append(1)
int_list.extend([2, 3, 4])
int_list.extend((5, 6, 7))
>>> int_list
[1, 2, 3, 4, 5, 6, 7]
>>> int_list.count(1)
>> # Closest thing to Scala trimEnd
>>> int_list = int_list[0:-5]
>>> int_list
[1, 2]
>>> int_list.insert(1, 5)
>>> int_list
[1, 5, 2]
>>> int_list.pop(1)
5
>>> int_list
[1, 2]
>>> int_list.reverse()
>>> int_list
[2, 1]
>>> int_list.sort()
>>> int_list
[1, 2]
>>> max(int_list)
2
>>> min(int_list)
1
>>> int_list = []
```


##### Scala:
```scala
import scala.collection.mutable.ArrayBuffer

val int_arr = ArrayBuffer[Int]()
int_arr += 1
int_arr += (2, 3, 4)
int_arr ++= Array(5, 6, 7)

res182: int_arr.type = ArrayBuffer(1, 2, 3, 4, 5, 6, 7)

scala> int_arr.count(_ == 1)
res187: Int = 1

scala> int_arr.trimEnd(5)

scala> int_arr
res192: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 2)

scala> int_arr.insert(1, 5)

scala> int_arr
res195: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 5, 2)

scala> int_arr.remove(1)
res196: Int = 5

scala> int_arr
res197: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 2)

// Scala will also let you be more flexible with multiple insert/remove
scala> int_arr.insert(1, 5, 6)

scala> int_arr
res199: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 5, 6, 2)

scala> int_arr.remove(1, 2)

scala> int_arr
res201: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 2)

scala> int_arr.reverse
res205: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(2, 1)

scala> int_arr.max
res210: Int = 2

scala> int_arr.min
res211: Int = 1

scala> int_arr.reverse.sorted
res215: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 2)

scala> int_arr.clear

scala> int_arr
res29: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer()
```

Embora já conversamos sobre estruturas de loops, em Scala existe o operador `until` que funciona como o range em Python.

##### Python:
```python
foo = [f for f in range(0, 10, 1)]
>>> foo
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
foo = [f for f in range(0, 10, 2)]
>>> foo
[0, 2, 4, 6, 8]
```

##### Scala:
```scala
scala> val foo = for (x <- 0 until 10) yield x
foo: scala.collection.immutable.IndexedSeq[Int] = Vector(0, 1, 2, 3, 4, 5, 6, 7, 8, 9)

scala> val foo = for (x <- 0 until (10, 2)) yield x
foo: scala.collection.immutable.IndexedSeq[Int] = Vector(0, 2, 4, 6, 8)

// Scala also has a "to" operator that creates an inclusive range
scala> 0 to (10, 2)
res22: scala.collection.immutable.Range.Inclusive = Range(0, 2, 4, 6, 8, 10)

scala> 0 until (10, 2)
res23: scala.collection.immutable.Range = Range(0, 2, 4, 6, 8)
```

Veja uma breve revisão da sintaxe de *comprehension*.

##### Python:
```python
foo = [x + "qux" for x in ["foo", "bar", "baz"] if x != "foo"]
>>> foo
['barqux', 'bazqux']
```

##### Scala:
```scala
scala> val foo = for (x <- Vector("foo", "bar", "baz") if x != "foo") yield x + "qux"
foo: scala.collection.immutable.Vector[String] = Vector(barqux, bazqux)

// Observe que a comprehension retorna o tipo que é elimentado 
scala> val foo = for (x <- ArrayBuffer("foo", "bar", "baz") if x != "foo") yield x + "qux"
foo: scala.collection.mutable.ArrayBuffer[String] = ArrayBuffer(barqux, bazqux)

// Observe que podemos usar operações funcionais nas sequencias 
scala> Vector("foo", "bar", "baz").filter(_ != "foo").map(_ + "qux")
res25: scala.collection.immutable.Vector[String] = Vector(barqux, bazqux)

```

Uma rapida observação é que Scala suporta arrays multidimensionais, enquanto que em Python a melhor forma de usar e com a biblioteca NumPy.

##### Scala:
```scala
scala> val multdim = Array.ofDim[Int](3, 4)
multdim: Array[Array[Int]] = Array(Array(0, 0, 0, 0), Array(0, 0, 0, 0), Array(0, 0, 0, 0))

scala> multdim(0)(2) = 15

scala> multdim
res217: Array[Array[Int]] = Array(Array(0, 0, 15, 0), Array(0, 0, 0, 0), Array(0, 0, 0, 0))
```
