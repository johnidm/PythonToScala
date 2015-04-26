Tuplas
------

Em Scala, tuplas pode ser tipos mistos, como em Python. Tuplas são também uma boa maneira para desenpacotar vals/vars em Scala, bem como o resultado de muitas operações `zip`: 

##### Python:
```python
>>> foo = (1, 2.5, "three")
>>> a, b, c = foo
>>> a
1
>>> b
2.5
>>> c
'three'
>>> bar = (4, 5.5, "six")
>>> foobar = ((x, y) for x, y in zip(foo, bar))
>>> foobar
<generator object <genexpr> at 0x10ac21f50>
>>> foobar = tuple(((x, y) for x, y in zip(foo, bar)))
>>> foobar
((1, 4), (2.5, 5.5), ('three', 'six'))
```

##### Scala:
```scala
scala> val foo = (1, 2.5, "three")
foo: (Int, Double, String) = (1,2.5,three)

// Podem ser acessados por posição
scala> foo._1
res17: Int = 1

scala> foo._2
res18: Double = 2.5

// Desempacotando

scala> val (a, b, c) = foo
a: Int = 1
b: Double = 2.5
c: String = three

scala> val bar = (4, 5.5, "six")
bar: (Int, Double, String) = (4,5.5,six)

// Nós vemos a função zip anteriormente - ela produz uma tupla
scala> val pairs = Array(1, 2, 3).zip(Array("four", "five", "six"))
pairs: Array[(Int, String)] = Array((1,four), (2,five), (3,six))

scala> for ((k, v) <- pairs) yield k.toString + v
res243: Array[String] = Array(1four, 2five, 3six)
```
