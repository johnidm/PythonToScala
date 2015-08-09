Funções
---------

Aviso: na seguinte seção eu uso "funções" par se refereir a funções em Scala, definidas com  `=>`, e métodos em Scala, definido com `def`.

Métodos e funções em Scala são muito familiares para programadores Python, exceto pelo fato de você ter que especificar o tipo do parãmetro que está sendo passado na função ou método:

##### Python
```python
def concat_num_str(x, y):
    if not isinstance(x, str):
        x = str(x)
    return x + y
>>> concat_num_str(1, "string")
'1string'
```

Primeiro, observe que o Scala ira simplismente retornar o resultado do bloco no método, a menos que o retorno é explicito:

##### Scala:
```scala
def concat_num_str(x:Int, y:String) = x.toString + y
scala> concat_num_str(1, "string")
res146: String = 1string

// O que acontce ser tentarmos passar um tipo incorreto?
scala> concat_num_str("string", num)
<console>:19: error: type mismatch;
 found   : String("string")
 required: Int
              concat_num_str("string", num)
                             ^
<console>:19: error: not found: value num
              concat_num_str("string", num)
```

Se usar multiplas expressões, use o bloco entre colchetes:

##### Scala:
```scala
import scala.collection.mutable.Map
val str_arr = Array("apple", "orange", "grape")

def len_to_map(arr:Array[String]) = {
    var lenmap:Map[String, Int] = Map()
    for (a <- arr) lenmap += (a -> a.length)
    lenmap
}

scala> len_to_map(str_arr)
res149: scala.collection.mutable.Map[String,Int] = Map(orange -> 6, apple -> 5, grape -> 5)
```

Em Scala, você pode especificar o tipo de retorno, e fazer funções recursivas:

##### Scala:
```scala
def factorial(n: Int): Int = if (n <= 0) 1 else n * factorial(n - 1)
scala> factorial(5)
res152: Int = 120

// Isso é interessante para especificar o tipo de retorno como um bom hábito
scala> def spec_type(x: Int, y:Double): Int = x + y.toInt
spec_type: (x: Int, y: Double)Int

scala> spec_type(1, 3.4)
res33: Int = 4
```

Padrões e argumentos nomeados são muito familiares para desenvovledores Python:

##### Python
```python
def make_arr(x, y, fruit="apple", drink="water"):
    return [x, y, fruit, drink]
>>> make_arr("orange", "banana")
['orange', 'banana', 'apple', 'water']
>>> make_arr("orange", "banana", "melon")
['orange', 'banana', 'melon', 'water']
>>> make_arr("orange", "banana", drink="coffee")
['orange', 'banana', 'apple', 'coffee']
```

##### Scala
```scala
def make_arr(x:String, y:String, fruit:String = "apple", drink:String = "water") = Array(x, y, fruit, drink)

scala> make_arr("orange", "banana")
res154: Array[String] = Array(orange, banana, apple, water)

scala> make_arr("orange", "banana", "melon")
res155: Array[String] = Array(orange, banana, melon, water)

scala> make_arr("orange", "banana", drink="coffee")
res156: Array[String] = Array(orange, banana, apple, coffee)

// As with Python, non-named parameters need to be supplied before named ones
scala> make_arr("orange", drink="coffee", "banana")
<console>:19: error: not enough arguments for method make_arr: (x: String, y: String, fruit: String, drink: String)Array[String].
Unspecified value parameter y.
              make_arr("orange", drink="coffee", "banana")
```

Scala suporta argumentos variavéis de maneira similar ao *args do Python, mas um pouco menos flexivél, Scala apenas sabe que isso é uma sequencia de arqumentos que podem ser interados.

##### Python:
```python
def sum_args(*args):
    return sum(args)

>>> sum_args(1, 2, 3, 4, 5)
15
```

##### Scala:
```scala
def sum_args(args:Int*) = args.sum
scala> sum_args(1, 2, 3, 4, 5)
res159: Int = 15
```

Tal como ocorre em Python, você não pode passar uma lista, isso precisa ser descontruido primeiro:

##### Python:
```
>>> sum_args([1, 2, 3])
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 2, in sum_args
TypeError: unsupported operand type(s) for +: 'int' and 'list'

>>> sum_args(*[1, 2, 3])
6
```

##### Scala:
```scala
scala> sum_args(Array(1, 2, 3))
<console>:17: error: type mismatch;
 found   : Array[Int]
 required: Int
              sum_args(Array(1, 2, 3))

scala> sum_args(Array(1, 2, 3): _*)
res161: Int = 6
```

Observe que Scala tem um tipo especial de função conhecida como "Procedure" que não retorna valor, nesse caso o sinal `=` é omitido.

##### Scala:
```scala
def proc_func(x:String, y:String) {print(x + y)}
proc_func("x", "y")
```

Scala suporta funções anônimas da mesma forma que funções `lamda` em Python:

##### Python:
```python
>>> concat_fruit = lambda x, y: x + y
>>> concat_fruit('apple', 'orange')
'appleorange'
```

##### Scala:
```scala
scala> val concat_fruit = (x: String, y: String) => x + y
concat_fruit: (String, String) => String = <function2>

scala> concat_fruit("apple", "orange")
res4: String = appleorange
```

Funções de primeira-classe em Scala, como em Python, podem passar uma função para outra função de de ordem-superior:

##### Python:
```python
def apply_to_args(func, arg1, arg2):
    return func(arg1, arg2)
>>> apply_to_args(concat_fruit, 'apple', 'orange')
'appleorange'
```

##### Scala:
```scala
scala> def applyToArgs(func: (String, String) => String, arg1: String, arg2: String): String = func(arg1, arg2)
applyToArgs: (func: (String, String) => String, arg1: String, arg2: String)String

scala> applyToArgs(concat_fruit, "apple", "banana")
res9: String = applebanana

// Você pode aplicar funções anonimas também 
scala> def applySingleArgFunc(func: (Int) => Int, arg1: Int): Int = func(arg1)
applySingleArgFunc: (func: Int => Int, arg1: Int)Int

scala> applySingleArgFunc((x: Int) => x + 5, 1)
res11: Int = 6
```

Scala faz facilmente currying. Esse é um padrão que você não se usa muito em Python, mas isso é facil de implementar: 

##### Python:
```python
def concat_curry(fruit):
  def perf_concat(veg):
      return fruit + veg
  return perf_concat

>>> curried = concat_curry('apple')
>>> curried('spinach')
'applespinach'
>>> curried('carrot')
'applecarrot'
```

##### Scala:
```scala
scala> def concat_curried(fruit: String)(veg: String): String = fruit + veg
concat_curried: (fruit: String)(veg: String)String

scala> val curried = concat_curried("apple") _
curried: String => String = <function1>

scala> curried("spinach")
res14: String = applespinach

scala> curried("carrot")
res15: String = applecarrot
```

