# [Абстрактные классы](http://php.net/manual/ru/language.oop5.abstract.php)

Классы, определенные как абстрактные, не могут быть созданы, и любой класс, который содержит по крайней мере один абстрактный метод, должен быть определен как абстрактный. Абстрактный метод не может иметь реализацию в абстрактном классе. Он объявляется, как обычный метод, но объявление заканчивается точкой с
запятой, а не телом метода.

```php
<?php

abstract class AbstractClass
{
   /* Данный метод должен быть определён в дочернем классе */
    abstract protected function getValue();
    abstract protected function prefixValue($prefix);

   /* Общий метод */
    public function printOut() {
        print $this->getValue() . "\n";
    }
}

?>
```
