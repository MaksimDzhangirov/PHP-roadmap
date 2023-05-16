[Оригинал](https://roadmap.sh/best-practices/api-security)

# Рекомендации по защите API

## Аутентификация

### Избегайте «базовой аутентификации» ('Basic Authentication'), используйте стандарты (например, JWT)
### Не изобретайте велосипед в механизмах аутентификации
### Используйте максимальное число неудачных попыток ('Max Retry') и функционал, осуществляющий блокировку, при определённом числе неудачных входов в систему
### Используйте шифрование для всех конфиденциальных данных

## JWT (JSON веб-токен)

### Используйте такой «JWT секретный ключ» ('JWT Secret'), который усложнит его подбор атакой методом «грубой силой» (полным перебором)
### Не извлекайте алгоритм из заголовка запроса, используйте бэкенд
### Делайте срок действия токена (TTL, RTTL) как можно короче
### Избегайте хранения конфиденциальных данных в полезной нагрузке JWT
### Старайтесь сделать полезную нагрузку небольшой, чтобы уменьшить размер JWT токена

## Контроль доступа

## OAuth

## Обработка

## Обработка входных данных

## Обработка выходных данных

## CI & CD

## Мониторинг

## Список рекомендованных ссылок по теме

* [Collection of Resources for Building APIs](https://github.com/yosriady/awesome-api-devtools)
* [CS253: Web Security](https://www.youtube.com/watch?v=5JJrJGZ_LjM&list=PL1y1iaEtjSYiiSGVlL1cHsXN_kvJOOhu-)
* [Securing Web Applications](https://www.youtube.com/watch?v=WlmKwIe9z1Q)
* [MIT 6.858: Computer Systems Security](https://www.youtube.com/watch?v=GqmQg-cszw4&list=PLUl4u3cNGP62K2DjQLRxDNRi0z2IRWnNh)
