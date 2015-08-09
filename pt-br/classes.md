Classes
-------

Criar classe em Scala é mais simples que o Java, mas ainda com a mesma meandros adicionados que voce não irá normalemente ver quando contrio classe em Python. Eu recomendo altamente ler um pouco como classes em Scala trabalham, como eleas são relacionadas ao Java e quais os detalhes que vale a penas conhecer.

Entretanto eu vou mostrar algumas classes simples que sçao comparadas entre as duas, e  deixar isso para ler com futuramente:

##### Python
```python
class Automobile(object):

    def __init__(self, wheels=4, engine=1, lights=2):
        self.wheels = wheels
        self.engine = engine
        self.lights = lights

    def total_parts(self):
        return self.wheels + self.engine + self.lights

    def remove_wheels(self, count):
        if (self.wheels - count) < 0:
            raise ValueError('Automobile cannot have fewer than 0 wheels!')
        else:
            self.wheels = self.wheels - count
            print('The automobile now has {} wheels!').format(self.wheels)


>>> car = Automobile()
>>> car.wheels
3
>>> car.total_parts()
7
>>> car.wheels = 6
>>> car.total_parts()
9
>>> car.remove_wheels(7)
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-30-24207883207a> in <module>()
----> 1 car.remove_wheels(7)

<ipython-input-27-41c5871dc8ce> in remove_wheels(self, count)
     11     def remove_wheels(self, count):
     12         if (self.wheels - count) < 0:
---> 13             raise ValueError('Automobile cannot have fewer than 0 wheels!')
     14         else:
     15             self.wheels = self.wheels - count

ValueError: Automobile cannot have fewer than 0 wheels!

>>> car.remove_wheels(2)
The automobile now has 4 wheels!
```

Em Scala , use var para criar todos os atributos mutaveis. Internamente, Scala criar getters e setters para cada:

##### Scala
```scala
class Automobile(var wheels:Int = 4, var engine:Int = 1, var lights:Int = 2 ){

    def total_parts() = {
        // No "self" needed, and implicit return
        wheels + engine + lights
    }

    // Purely side-effecting function, no "=" needed
    def remove_wheels(count:Int) {
        if (wheels - count < 0) {
            throw new IllegalArgumentException("Automobile cannot have fewer than 0 wheels!")
        } else {
            wheels = wheels - count
            println(s"Auto now has $wheels wheels!")
        }
    }
}

scala> val car = new Automobile()
car: Automobile = Automobile@77424e9

scala> car.wheels
res64: Int = 4

scala> car.total_parts()
res65: Int = 7

scala> car.wheels = 6
car.wheels: Int = 6

scala> car.total_parts()
res66: Int = 9

scala> car.remove_wheels(7)
java.lang.IllegalArgumentException: Automobile cannot have fewer than 0 wheels!
  at Automobile.remove_wheels(<console>:19)
  ... 32 elided

scala> car.remove_wheels(2)
Auto now has 4 wheels!
```

Em Scala, se você definir um contrutor com um campo `val` (imutavél), voce tem disponivel um getter mas não um setter. Isso semelhante a você definir suas proprias propriedade getter/setter em classe Python (para um grande resumo dePripriedade e descritores Python confira [Python Descriptors Demystified](http://nbviewer.ipython.org/gist/ChrisBeaumont/5758381/descriptor_writeup.ipynb)):

##### Python
```python
class Automobile(object):

    def __init__(self, wheels=4):
        # The underscore is convention, but not enforced
        self._wheels = wheels

    @property
    def wheels(self):
        return self._wheels

    @wheels.setter
    def wheels(self, count):
        raise ValueError('This value is immutable!')

>>> car = Automobile()
>>> car.wheels
4
>>> car.wheels = 5
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-26-f07fada773fb> in <module>()
----> 1 car.wheels = 5

<ipython-input-23-87368b68789b> in wheels(self, count)
     11     @wheels.setter
     12     def wheels(self, count):
---> 13         raise ValueError('This value is immutable!')

ValueError: This value is immutable!
```

##### Scala
```scala
class Automobile(val wheels:Int = 4){}

scala> val car = new Automobile()
car: Automobile = Automobile@64284ba3

scala> car.wheels
res67: Int = 4

scala> car.wheels = 5
<console>:12: error: reassignment to val
       car.wheels = 5
                  ^
```

Como em Java, Scala também permite você definir campos como `private`, que impede getter/setter de ser gerados e  somente permite acesso ao compo dentro da classe. Esse comportamento pode ser replicado em Python, mas você não ira frequentementever esse padrão ser usado em programaas Python - isso é entendido que os atributos de classe principal com underscore são privados e não devem ser devem usados:

##### Python
```python
class Automobile(object):

    def __init__(self, wheels=4):
        # The underscore is convention, but not enforced
        self._wheels = wheels

    @property
    def wheels(self):
        raise ValueError('You cannot access this value!')

    @wheels.setter
    def wheels(self, count):
        raise ValueError('You cannot access this value!')

>>> car.wheels
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-41-d267b674bbda> in <module>()
----> 1 car.wheels

<ipython-input-39-73ff0f17068d> in wheels(self)
      7     @property
      8     def wheels(self):
----> 9         raise ValueError('You cannot access this value!')
     10
     11     @wheels.setter

ValueError: You cannot access this value!

>>> car.wheels = 5
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-42-f07fada773fb> in <module>()
----> 1 car.wheels = 5

<ipython-input-39-73ff0f17068d> in wheels(self, count)
     11     @wheels.setter
     12     def wheels(self, count):
---> 13         raise ValueError('You cannot access this value!')

ValueError: You cannot access this value!
```

##### Scala
```scala
class Automobile(private val wheels:Int = 4){}

scala> car.wheels
<console>:11: error: value wheels in class Automobile cannot be accessed in Automobile
              car.wheels
                  ^

scala> car.wheels = 5
<console>:13: error: value wheels in class Automobile cannot be accessed in Automobile
val $ires4 = car.wheels
```

Métodos staticos em Scala são manipulados atrapes de "companion objects" das classes, que são nomeados com a mesma classe. Objetos são uma entrada de strudo da linguagem Scala - Eu estou mostrando como eles se relacionamd com `staticmethod`em Python, mas eu recomendo que voce faça o mesmo com os objetos usados em Scala. Tambem demostrado nesse exemplo é como os cmapos do objetos podem ser usados para espelhar atributos em nível de classe no Python:


##### Python
```python
class Automobile(object):

    wheels = 4
    lights = 2

    def __init__(self, name):
        self.name = name

    @staticmethod
    def print_uninst_str():
        print("No 'self' passed to this method, and no instantiation."
              " It's static!")

>>> Automobile.print_uninst_str()
No 'self' passed to this method, and no instantiation. It's static!
>>> Automobile.wheels
4
>>> Automobile.wheels = 5
>>> Automobile.wheels
5
```

##### Scala
```scala
class Automobile(var name:String){}

object Automobile {
    var wheels = 4
    var lights = 2
    def print_uninst_str() = "No 'self' passed to this method, and no instantiation. It's static!"
}

scala> Automobile.print_uninst_str
res3: String = No 'self' passed to this method, and no instantiation. It's static!

scala> Automobile.wheels
res4: Int = 4

scala> Automobile.wheels = 5
Automobile.wheels: Int = 5

scala> Automobile.wheels
res5: Int = 5
```

A seguinte seção mostra como pode ser feito herança em Scala e Python. Eu recomentod leri mais sobreambas as linguagens em relação *abstract base classes* e  *traits* (Scala) e  Method Resolution Order (Python). Pora hora, veremos o básico.

Scala suporta herança única via classe base abstrata, que são nomeadas explicitamente como tal. Python pode tratar qualquer classe como abstrata:

##### Python
```python
class Automobile(object):

    wheels = 4
    lights = 2
    doors = 2

    def __init__(self, color, make):
        self.color = color
        self.make = make

    def towing_capacity(self):
        pass

    def top_speed(self):
        pass

    def print_make_color(self):
        print(" ".join([self.color, self.make]))

class Car(Automobile):

    doors = 4

    def __init__(self, color, model):
        super(Car, self).__init__(color, model)

    def towing_capacity(self):
        return 0

    def top_speed(self):
        return 150


>>> mycar = Car("red", "Toyota")
>>> mycar.doors
4
>>> mycar.towing_capacity()
0
>>> mycar.top_speed()
150
>>> mycar.print_make_color()
Red Toyota
```

##### Scala
```scala
abstract class Automobile(val color:String, val make:String) {
    val wheels:Int = 4
    val lights:Int = 2
    val doors:Int = 4

    def towing_capacity: Int
    def top_speed: Int
    def print_make_color():String = return s"$color $make"
}

class Car(color:String, make:String) extends Automobile(color, make) {

    override val doors = 4 // Override needed if immutable "val"

    def towing_capacity() = 0
    def top_speed() = 150
}

scala> val mycar = new Car("Red", "Toyota")
mycar: Car = Car@351cdd99

scala> mycar.print_make_color()
res2: String = Red Toyota

scala> mycar.doors
res3: Int = 4

scala> mycar.top_speed
res4: Int = 150

// Abstract classes only support single inheritance!
scala> abstract class SportPackage {}
defined class SportPackage

scala> class Car(color:String, make:String) extends Automobile(color, make) with SportPackage(){}
<console>:9: error: class SportPackage needs to be a trait to be mixed in
       class Car(color:String, make:String) extends Automobile(color, make) with SportPackage(){}
```

Geralmente, você deve apenas usar abstract base classes em Scala se você precusa de interoperabildiade em Java ou precisar passar parametros em contrutores na classe base. Caso contrário, você precisar usar oque Scala chama de "Traits", que agem como mixins e permitem herança multipla em Scala.

##### Python
```python

class Engine(object):

    started = False

    def start(self):
        self.started = True

    def shutdown(self):
        self.started = False

class Transmission(object):

    fluid_level = 0

    def add_fluid(self, amount):
        self.fluid_level = self.fluid_level + amount

# Using Automobile class from earlier
class Car(Automobile, Engine, Transmission):

    doors = 4

    def __init__(self, color, model):
        super(Car, self).__init__(color, model)

    def towing_capacity(self):
        return 0

    def top_speed(self):
        return 150

>>> mycar = Car("Red", "Toyota")

>>> mycar.start()

>>> mycar.started
True

>>> mycar.fluid_level
0

>>> mycar.add_fluid(50)

>>> mycar.fluid_level
50
```

##### Scala
```scala
trait Engine {
    var started:Boolean = false
    // These don't return anything, so no "=" needed
    def start() {started = true}
    def shutdown() {started = false}
}

trait Transmission {
    var fluid_level:Int = 0
    def add_fluid(amount:Int) {fluid_level = fluid_level + amount}
}

class Car(color:String, make:String) extends Automobile(color, make)
  with Engine
  with Transmission {

    override val doors = 4 // Override needed if immutable "val"

    def towing_capacity() = 0
    def top_speed() = 150
}

scala> val mycar = new Car("Red", "Toyota")
mycar: Car = Car@38134991

scala> mycar.start()

scala> mycar.started
res2: Boolean = true

scala> mycar.add_fluid(50)

scala> mycar.fluid_level
res4: Int = 50
```
