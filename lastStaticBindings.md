# [Позднее статическое связывание](http://php.net/manual/ru/language.oop5.late-static-bindings.php)

Позднее статическое связывание может быть использовано для того, чтобы получить ссылку на вызываемый класс в контексте статического наследования. "Позднее связывание" отражает тот факт, что обращения через static:: не будут вычисляться по отношению к классу, в котором вызываемый метод определен, а будут вычисляться на основе информации в ходе исполнения.

# Использование static::

```php
<?php
class A {
    public static function who() {
        echo __CLASS__;
    }
    public static function test() {
        static::who(); // Здесь действует позднее статическое связывание
    }
}

class B extends A {
    public static function who() {
        echo __CLASS__;
    }
}

B::test();
?>
```

Позднее статическое связывание может использоваться, чтобы избежать дублирования кода из родительсикх классов в дочерние.

```php
abstract class DomainObject 
{
  public static function create () 
  {
    return new static ();
  }
class User extends DomainObject () 
{
}
class Document extends DomainObject () 
{
}
print_r(Document::create());
```

Ключевое слово static можно использовать не только для создания объектов. Так же, как и self и parent, его можно использовать как идентификатор для вызова статических методов даже из нестатического контекста.

```php
abstract class DomainObject
{
    private $group;
    public function __construct()
    {
        $this->group = static::getGroup();
    }
    public static function create(): DomainObject
    {
        return new static();
    }
    public static function getGroup(): string
    {
        return "default";
    }
}
class User extends DomainObject
{
}
class Document extends DomainObject
{
    public static function getGroup(): string
    {
        return "document";
    }
}
class SpreadSheet extends Document
{
}

print_r(User::create());
print_r(SpreadSheet::create());

```
