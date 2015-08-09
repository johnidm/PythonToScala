Strings
-------
Python e Scala compartilham uma sintaxe semelhante com relação a operações com String, existem poucas diferenças.

##### Python
```python
>>> foo = "bar"
>>> foo[1]
'a'
>>> len(foo)
3
>>> foo + str(1)
'bar1'
>>> foo.split("a")
['b', 'r']
>>> "foo   ".strip()
'foo'
>>> "String here: {}, Int here: {}".format("foo", 1)
'String here: foo, Int here: 1'
>>> foo.upper()
'BAR'
```

##### Scala
```scala
scala> val foo = "bar"
foo: String = bar

scala> foo(1)
res19: Char = a

scala> foo.length
res2: Int = 3

scala> foo + 1.toString
res3: String = bar1

scala> foo.split("a")
res10: Array[String] = Array(b, r)

scala> "fooo   ".trim
res11: String = fooo

scala> "String here: %s, Int here: %d".format("foo", 1)
res13: String = String here: foo, Int here: 1

// Scala carece de alguns operadores, mas torna isso mais fácil com mapas de strings
// Observe o uso do _ que indica a passagem de que cada variavel no mapa.

scala> foo.map(_.toUpper)
res18: String = BAR
```

Scala 2.10 apresenta uma sintaxe muito elegante de interpolaão de strings, que é familiar a desenvovledores Coffee Script.

##### Scala
```scala
scala> val fruit = "apple"
fruit: String = apple

scala> val apple_count = 5
apple_count: Int = 5

scala> val veg = "broccoli"
veg: String = broccoli

scala> val broc_count = 10
broc_count: Int = 10

scala> s"I have $apple_count $fruit and $broc_count $veg. In total I have ${apple_count + broc_count}."
res15: String = I have 5 apple and 10 broccoli. In total I have 15.
```

Ambas as linguagens permitem a você facilmente interar sobre caracteres individuais de uma string.

##### Python
```python
for c in foo:
    print(c)
b
a
r
```

##### Scala
```scala
scala> for (c <- foo) println(c)
b
a
r
```

Multiplas linhas de string em Scala são muito failiares para programadores Python.

##### Python
```python
>>> """
... This is
... a multiline string
... """
'\nThis is\na multiline string\n'
```

##### Scala
```scala
scala> """
     | This is
     | a multiline string
     | """
res8: String =
"
This is
a multiline string
"
```
