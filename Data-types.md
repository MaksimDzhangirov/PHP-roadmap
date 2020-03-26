# Типы данных

В таблице перечислены типы данных, используемые в PHP, а также соответствующие им функции проверки [http://php.net/manual/ru/language.types.intro.php](http://php.net/manual/ru/language.types.intro.php).

| Фукнция проверки            | Тип           |  Описание      |
| -----------------           | ------------- | -------------- |
| is_bool()                   | Boolean       | Одно из двух значений: true или false (истина или ложь). Скалярный тип данных |
| is_integer(), is_int(), is_long()    | Integer       | Целое число. Скалярный тип данных            |
| is_double(), is_float()  | Double       | Число с плавающей точкой. Скалярный тип данных            |
| is_string()   | String       | Символьные данные. Скалярный тип данных            |
| is_array()    | Array        | Массив. Смешанный тип данных            |
| is_object()   | Object       | Объект. Смешанный тип данных            |
| is_callable()   | Callable       | Функции обратного вызова (callback-функции). Смешанный тип данных            |
| is_iterable()   | Iterable       | Псевдотип, введенный в PHP 7.1. Он принимает любой массив или объект, реализующий интерфейс Traversable. Смешанный тип данных |
| is_resource()  | Resource       | Дескриптор, используемый для идентификации и работы с внешними ресурсами, такими как базы данных, файлы, области изображения. Специальных тип данных |
| is_null()       | Null           | Неинициализированное значение. Специальных тип данных |

Кроме того, существуют псевдотипы - слова, используемые в документации PHP, для обозначения типов или значений, какие могут принимать аргументы. К ним относятся [https://www.php.net/manual/ru/language.pseudo-types.php](https://www.php.net/manual/ru/language.pseudo-types.php)
- [mixed](https://www.php.net/manual/ru/language.pseudo-types.php#language.types.mixed)
- [number](https://www.php.net/manual/ru/language.pseudo-types.php#language.types.number)
- [callback (callable)](https://www.php.net/manual/ru/language.pseudo-types.php#language.types.callback)
- [array|object](https://www.php.net/manual/ru/language.pseudo-types.php#language.types.array-object)
- [void](https://www.php.net/manual/ru/language.pseudo-types.php#language.types.void)
и псевдопеременная [$...](https://www.php.net/manual/ru/language.pseudo-types.php#language.types.dotdotdot).
