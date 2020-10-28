## Наследование vs Композиция vs Агрегация

[Смотри также](http://sergeyteplyakov.blogspot.com/2012/12/vs-vs.html)

Между двумя классами/объектами существует разные типы отношений. Самым базовым типом отношений является ассоциация (*association*), 
это означает, что два класса как-то связаны между собой. Обычно это отношение используется на ранних этапах дизайна, чтобы показать
существующую зависимость между классами.

Более точным типом отношений является отношение *открытого наследования* (отношение «является», IS A Relationship),
которое говорит, что все, что справедливо для базового класса справедливо и для его наследника. 
Именно с его помощью мы получаем полиморфное поведение, абстрагируемся от конкретной реализации классов, 
имея дело лишь с абстракциями (интерфейсами или базовыми классами) и не обращаем внимание на детали реализации.

```php
<?php declare(strict_types=1);

abstract class AbstractRepository
{
    abstract public function save(): void;
}

class SqlRepository extends AbstractRepository
{
    public function save(): void
    {
        echo "Save something in db\n";
    }
}

$repo = new SqlRepository();
$repo->save();
```

И хотя наследование является отличным инструментом, его явно недостаточно для решения всех типов задач.
Во-первых, далеко не все отношения между классами определяются отношением «является», а во-вторых,
наследование является самой сильной связью между двумя классами, которую невозможно разорвать во время исполнения.

В этом случае нам на помощь приходит другая пара отношений: композиция (**composition**) и агрегация (**aggregation**).
Оба они моделируют отношение «является частью» (HAS-A Relationship) и обычно выражаются в том,
что класс целого содержит поля (или свойства) своих составных частей. Грань между ними достаточно тонкая,
но важная, особенно в контексте управления зависимостями.

Разница между композицией и агрегацией заключается в том, что **в случае композиции целое явно контролирует время жизни своей составной части**
(часть не существует без целого), а **в случае агрегации целое хоть и содержит свою составную часть, время их жизни не связано**
(например, составная часть передается через параметры конструктора).

```php
<?php declare(strict_types=1);

class CustomRepository
{
    public function save(): void
    {
        echo "Save something in db\n";
    }
}

class CompositeCustomService
{
    private $customRepository;
    // Композиция
    public function __construct()
    {
        $this->customRepository = new CustomRepository();
    }

    public function doSomething(): void
    {
        // do some work
        echo "Do some work\n";
        // save data
        $this->customRepository->save();
    }
}

$service = new CompositeCustomService();
$service->doSomething();

class AggregatedCustomService
{ 
    // Агрегация
    private $customRepository;
    public function __construct(CustomRepository $customRepository)
    {
        $this->customRepository = $customRepository;
    }

    public function doSomething(): void
    {
        // do some work
        echo "Do some work\n";
        // save data
        $this->customRepository->save();
    }
}

$repo = new CustomRepository();
$service = new AggregatedCustomService($repo);
$service->doSomething();
```

**CompositeCustomService** для управления своими составными частями использует композицию, а **AggregatedCustomService** – агрегацию.
При этом явный контроль времени жизни обычно приводит к более высокой связанности между целым и частью, поскольку используется конкретный тип,
тесно связывающий участников между собой.

Мы можем использовать композицию и контролировать время жизни объекта, не завязываясь на конкретные типы. Например, с помощью фабричного метода:

```php
<?php declare(strict_types=1);

interface DbConnectionInterface
{
    public function connect(): void;
    public function close(): void;
}

interface DbConnectionFactoryInterface
{
    public static function factory(string $type): DbConnectionInterface;
}

abstract class AbstractConnectionFactory implements DbConnectionFactoryInterface
{    
}

class ConnectionFactory extends AbstractConnectionFactory
{
    public static function factory(string $type): DbConnectionInterface
    {
        if ($type == 'mysql') {
            return new MySqlConnection();
        } elseif ($type == 'postgresql') {
            return new PostgreSqlConnection();
        }

        throw new InvalidArgumentException('Unknown format given');
    }
}

class MySqlConnection implements DbConnectionInterface
{
    public function connect(): void
    {
        echo "Connect to MySQL server\n";
    }

    public function close(): void
    {
        echo "Disconnect from MySQL server\n";
    }
}

class PostgreSqlConnection implements DbConnectionInterface
{
    public function connect(): void
    {
        echo "Connect to PostgreSql server\n";
    }

    public function close(): void
    {
        echo "Disconnect from PostgreSql server\n";
    }
}

class CustomService
{ 
    const DB_TYPE = 'mysql';
    private $connectionFactory;
    public function __construct(DbConnectionFactoryInterface $connectionFactory)
    {
        $this->connectionFactory = $connectionFactory;
    }

    public function doSomething(): void
    {
        // Композиция
        $dbConnection = $this->connectionFactory::factory(self::DB_TYPE);
        $dbConnection->connect();
        // do some work
        echo "Do some work\n";
        $dbConnection->close();
    }
}

$factory = new ConnectionFactory();
$service = new CustomService($factory);
$service->doSomething();
```

Задачу с сервисами и репозиториями можно решить как с помощью наследования, так и с помощью агрегации. Каждый вариант
приводит к одному и тому же конечному результату, при этом связанность изменяется от очень высокой (при наследовании)
к очень слабой (при агрегации).

В большинстве случаев следует предпочесть агрегацию наследованию, поскольку первая дает большую гибкость и динамичность во время исполнения.
