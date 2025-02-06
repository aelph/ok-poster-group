# Форк плагина автопостинга OkPoster из WordPress.

Опробован на WordPress 6.7.1, PHP 7.4, MySQL 8.0.

При постинге записи в группу Одноклассники возникла ошибка:

```
PHP Fatal error:  Uncaught Error: Cannot use object of type WP_Error as array in /home/site.ru/public_html/wp-content/plugins/ok-poster-group/inc/okp-function-class.php:135
...
```

После обновления WordPress до версии 6.7.1 и обновления MySQL до версии 8.0.0 ошибка стала появляться после каждого поста.

Что было исправлено:

1. Добавлена корректная обработка ошибок при неудачном запросе к API OK.ru
2. Использована безопасная функция wp_remote_retrieve_body() для получения тела ответа
3. Добавлены проверки на пустой ответ и некорректный JSON
4. Добавлены информативные сообщения об ошибках на русском языке
5. Увеличен таймаут запроса до 15 секунд (по умолчанию было 5)
6. Отключена проверка SSL-сертификатов, так как иногда это может быть причиной задержек.
7. Вынесены параметры запроса в отдельный массив для лучшей читаемости.

Все ошибки теперь корректно записываются в журнал плагина и выводятся на соответствующей вкладке.