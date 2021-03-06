# Анализатор HTTP логов

Считает статистику по записям в файле access_log.

Анализирует ~ 350 000 записей в минуту на Core i5.

## Использование
```bash
php parser.php access_log
```

## Вывод
```json
{
  "views": 16,
  "urls": 5,
  "traffic": 187990,
  "crawlers": {
      "Googlebot": 2
  },
  "statusCodes": {
      "200": 14,
      "301": 2
  }
}
```

## Тесты
```bash
./vendor/bin/phpunit tests
```

## Примечание
Для идентификации запросов от поисковиков используется [CrawlerDetect](https://github.com/JayBizzle/Crawler-Detect), 
который умеет определять более 1000 различных ботов.
Поэтому формат выходных данных в примере из задания немного нарушен, чтобы была возможность определять большее количество ботов.

## Производительность
Мое решение в первую очередь старается быть простым и расширяемым. Если говорить о производительности:
1. Вместо PHP лучше использовать, например, C++ или Go.
2. Инкрементальный анализ: можно обрабатывать записи по мере их появления в логе, а не все разом.
3. Снизить количество определяемых поисковиков, например, до четырех.
