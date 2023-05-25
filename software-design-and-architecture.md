[Оригинал](https://roadmap.sh/software-design-architecture)

# Основные принципы проектирования программного обеспечения и виды архитектур приложений

## Принципы проектирования, базирующиеся на понятии «чистого кода»

Полезные ссылки:

* [Introduction to Clean Code & Software Design Principles](https://workat.tech/machine-coding/tutorial/introduction-clean-code-software-design-principles-nwu4qqc63e09)

### Будьте последовательны при написании кода

### Содержательные, понятные названия переменных, не требующие дополнительных комментариев

### Стиль программирования: отступы

### Старайтесь, чтобы создаваемые методы, классы, файлы, были как можно меньше

### Используйте чистые функции

### Минимизируйте цикломатическую сложность программы

### Старайтесь не передавать значения типа null и булевого типа

### Следите за тем, что код фреймворка был дистанцирован

### Используйте составляющие части вашей программы с умом

### Тесты должны выполняться быстро и быть независимыми

### Группируйте код вокруг а́ктора, к которому он относится

### Разделяйте команды и запросы

### Избегайте ненужной сложности и осуществляйте рефакторинг как можно чаще

## Парадигмы программирования

### Структурное программирование
### Процедурное программирование
### Объектно-ориентированное программирование
#### Модельно-ориентированный подход к проектированию
##### Модель предметной области
##### Анемичная модель
##### Многоуровневые архитектуры
##### Единый язык
##### Инварианты класса
#### Особенности парадигмы
##### Абстрактные классы
##### Реальные классы
##### Область видимости
##### Интерфейсы
#### Основные понятия
##### Наследование
##### Полиморфизм
##### Абстракция
##### Инкапсуляция

## Принципы проектирования программного обеспечения

### Используйте композицию, а не наследование

### Инкапсулируйте то, что изменяется

* [Почему нужно инкапсулировать то, что изменяется?](https://ru.stackoverflow.com/questions/499882/%D0%9F%D0%BE%D1%87%D0%B5%D0%BC%D1%83-%D0%BD%D1%83%D0%B6%D0%BD%D0%BE-%D0%B8%D0%BD%D0%BA%D0%B0%D0%BF%D1%81%D1%83%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D1%82%D1%8C-%D1%82%D0%BE-%D1%87%D1%82%D0%BE-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D1%8F%D0%B5%D1%82%D1%81%D1%8F)

### Пишите программы, основываясь на абстракциях

### Голливудский принцип

### SOLID

### DRY

### YAGNI

## Шаблоны проектирования

### GoF шаблоны проектирования
### PoSA шаблоны

## Архитектурные принципы

### Компонентно-ориентированное программирование

### Стратегия vs детали реализации

### Границы частей приложения

## Архитектурные стили

### по типу обмена сообщениями

#### основанный на событиях
#### издатель/подписчик

### по способу взаимодействия в распределенной сети

#### клиент-сервер
#### одноранговый, децентрализованный или пиринговый (peer-to-peer, P2P)

### по внутренней структуре

#### компонентно-ориентированный
#### монолитный
#### многоуровневый

## Архитектурные шаблоны

### SOA

### CQRS

### Предметно-ориентированное проектирование

### Модель-представление-контроллер (Model-View-Controller)

### Микросервисы

### Шаблон Blackboard («доска объявлений»)

### Микроядро

### Бессерверная архитектура

### Очереди сообщений / потоки

### Генерация событий

## Шаблоны корпоративных приложений

### Объекты переноса данных (DTOs)

### Коллекции объектов (Identity Maps)

### Частные случаи (Use Cases)

### Репозитории (Repositories)

### Преобразователи (Mappers)

### Сценарий транзакции (Transaction Script)

### Команды / Запросы (Commands / Queries)

### Объекты-значения (Value Objects)

### Модели предметной области (Domain Models)

### Сущности (Entities)

### Объектно-реляционные отображения (ORMs)

**Замечание.** Список, приведённый в данной дорожней карте, не является исчерпывающим. Здесь приведены лишь некоторые из наиболее важных тем, касающиеся каждого раздела.