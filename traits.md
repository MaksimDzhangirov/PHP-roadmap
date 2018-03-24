# [Трейты](http://php.net/manual/ru/language.oop5.traits.php)

Трейт - это механизм обеспечения повторного использования кода в языках с поддержкой только одиночного наследования, таких как PHP. Трейт предназначен для уменьшения некоторых ограничений одиночного наследования, позволяя разработчику повторно использовать наборы методов свободно, в нескольких независимых классах и реализованных с использованием разных архитектур построения классов. Любое свойство (или метод), определенное в трейте, становится частью того класса, в который этот трейт включен. При этом трейт изменяет структуру этого класса, но не меняет его тип. 

Пример использования трейта

```php 
<?php
trait ezcReflectionReturnInfo {
    function getReturnType() { /*1*/ }
    function getReturnDescription() { /*2*/ }
}

class ezcReflectionMethod extends ReflectionMethod {
    use ezcReflectionReturnInfo;
    /* ... */
}

class ezcReflectionFunction extends ReflectionFunction {
    use ezcReflectionReturnInfo;
    /* ... */
}
?>
```
## Особенности использования трейтов

### Использование нескольких трейтов

В класс можно включить несколько трейтов. Для этого их нужно перечислить через запятую после ключевого слова use.

```php
<?php
trait Hello {
    public function sayHello() {
        echo 'Hello ';
    }
}

trait World {
    public function sayWorld() {
        echo 'World';
    }
}

class MyHelloWorld {
    use Hello, World;
    public function sayExclamationMark() {
        echo '!';
    }
}

$o = new MyHelloWorld();
$o->sayHello();
$o->sayWorld();
$o->sayExclamationMark();
?>
```

### Совместное использование трейтов и интерфейсов

Как было сказано выше, трейты не позволяют изменить тип класса, в который были включены. Поэтому, если трейт используется сразу в нескольких классах, у вас не будет общего типа, который можно было бы указать в уточнениях для сигнатур методов. К счастью, трейты можно успешно использовать вместе с интерфейсами. Мы можем определить интерфейс с методами, которые затем реализуем в трейте, а затем указать, что в нужном нам классе реализуются методы этого интерфейса.

### Устранение конфликтов имен с помощью ключевого слова `insteadof`. Псевдонимы для переопределенных методов трейта

Если два трейта вставляют метод с одним и тем же именем, это приводит к фатальной ошибке в случае, если конфликт явно не разрешен.

Для разрешения конфликтов именования между трейтами, используемыми в одном и том же классе, необходимо использовать оператор `insteadof` для того, чтобы точно выбрать один из конфликтующих методов.

Так как предыдущий оператор позволяет только исключать методы, оператор `as` может быть использован для включения одного из конфликтующих методов под другим именем. Оператор `as` не переименовывает метод и не влияет на какой-либо другой метод.

```php
<?php
trait A {
    public function smallTalk() {
        echo 'a';
    }
    public function bigTalk() {
        echo 'A';
    }
}

trait B {
    public function smallTalk() {
        echo 'b';
    }
    public function bigTalk() {
        echo 'B';
    }
}

class Talker {
    use A, B {
        B::smallTalk insteadof A;
        A::bigTalk insteadof B;
    }
}

class Aliased_Talker {
    use A, B {
        B::smallTalk insteadof A;
        A::bigTalk insteadof B;
        B::bigTalk as talk;
    }
}
?>
```

### Использование статических методов в трейте

На статические переменные можно ссылаться внутри методов трейта, но нельзя определить статические переменные в самом трейте. Тем не менее, трейт может описывать статические методы для демонстрации класса.

```php
<?php
trait Counter {
    public function inc() {
        static $c = 0;
        $c = $c + 1;
        echo "$c\n";
    }
}

class C1 {
    use Counter;
}

class C2 {
    use Counter;
}

$o = new C1(); $o->inc(); // echo 1
$p = new C2(); $p->inc(); // echo 1
?>
```

### Определение абстрактных методов в трейтах

В трейтах можно объявлять абстрактные методы точно так же, как и в обычных классах. При использовании такого трейта в классе в нем должны быть реализованы все объявленные в трейте абстрактные методы.

```php
<?php
trait Hello {
    public function sayHelloWorld() {
        echo 'Hello'.$this->getWorld();
    }
    abstract public function getWorld();
}

class MyHelloWorld {
    private $world;
    use Hello;
    public function getWorld() {
        return $this->world;
    }
    public function setWorld($val) {
        $this->world = $val;
    }
}
?>
```

### Изменение прав доступа к методам трейта

Используя синтаксис оператора `as` можно также настроить видимость метода в использующем трейт классе.

```php
<?php
trait HelloWorld {
    public function sayHello() {
        echo 'Hello World!';
    }
}

// Изменение видимости класса sayHello
class MyClass1 {
    use HelloWorld { sayHello as protected; }
}

// Создание псевдонима метода с измененной видимостью
// видимость sayHello не изменилась
class MyClass2 {
    use HelloWorld { sayHello as private myPrivateHello; }
}
?>
```

### Трейты, состоящие из трейтов

Аналогично тому, как классы могут использовать трейты, также и трейты могут использовать другие трейты.

```php
<?php
trait Hello {
    public function sayHello() {
        echo 'Hello ';
    }
}

trait World {
    public function sayWorld() {
        echo 'World!';
    }
}

trait HelloWorld {
    use Hello, World;
}

class MyHelloWorld {
    use HelloWorld;
}

$o = new MyHelloWorld();
$o->sayHello();
$o->sayWorld();
?>
```

### Свойства

Трейты могут также определять свойства.

```php
<?php
trait PropertiesTrait {
    public $x = 1;
}

class PropertiesExample {
    use PropertiesTrait;
}

$example = new PropertiesExample;
$example->x;
?>
```
