# ClickHouse

## Колоночные БД

С выполнением SQL запросов на больших объемах данных стандартные СУБД справляются все хуже, т.к. объемы данных все растут и растут. На таблицах с парой десятков тысяч записей уже нужно создавать [индексы](https://ruhighload.com/%d0%98%d0%bd%d0%b4%d0%b5%d0%ba%d1%81%d1%8b+%d0%b2+mysql), чтобы получить приемлемую производительность. Не говоря уже о том, что добавить или удалить колонку в большую таблицу практически невозможно и это требует специальных техник. 

Колоночные базы данных адресуют две проблемы — скорость сложных запросов на больших объемах и изменение структуры таблиц с данными.

Колоночные базы данных позволяют эффективно делать сложные выборки на больших таблицах. Изменение структуры больших таблиц происходит мгновенно, а сжатие данных позволяет сэкономить кучу места. Однако не следует использовать колоночные базы для случаев с обычными выборками по ключу и известными структурами запросов. Для этого лучше подойдут обычные (строчные) СУБД.

Колоночные базы так и называются потому, что хранят данные не в строках а в колонках. Каждая колонка — это как бы отдельная таблица из одной колонки, которая хранит только свои значения. И значения primary key.

Классические БД - **OLTP** (Online Transaction Processing) — обработка транзакций в реальном времени. Способ организации БД, при котором система работает с небольшими по размерам транзакциями, но идущими большим потоком, и при этом клиенту требуется от системы максимально быстрое время ответа. 

А колоночные - **OLAP** (англ. online analytical processing, аналитическая обработка в реальном времени) — технология обработки информации, включающая составление и динамическую публикацию отчётов и документов. Используется аналитиками для быстрой обработки сложных запросов к базе данных. Служит для подготовки бизнес-отчётов по продажам, маркетингу, в целях управления, т. н. data mining — добыча данных (способ анализа информации в базе данных с целью отыскания аномалий и трендов без выяснения смыслового значения записей).

OLAP делает мгновенный снимок реляционной БД и структурирует её в пространственную модель для запросов. Заявленное время обработки запросов в OLAP составляет около 0,1 % от аналогичных запросов в реляционную БД.

OLAP-структура, созданная из рабочих данных, называется OLAP-куб. Куб создаётся из соединения таблиц с применением схемы звезды или схемы снежинки. В центре схемы звезды находится таблица фактов, которая содержит ключевые факты, по которым делаются запросы. Множественные таблицы с измерениями присоединены к таблице фактов. Эти таблицы показывают, как могут анализироваться агрегированные реляционные данные. Количество возможных агрегирований определяется количеством способов, которыми первоначальные данные могут быть иерархически отображены.

## Когда использовать

Адресуемые проблемы колоночных баз данных очень тесно связаны с аналитическими и Big Data системами. Соответственно применять колоночные базы лучше всего на таких таблицах:

- Событийные таблицы, над которыми выполняются сложные выборки (агрегации, фильтры, сортировки). Например, добавление товаров в корзину в Интернет магазине.
- Агрегатные таблицы с большим количеством данных для аналитических выборок. Это часто таблицы, которые строятся из событийных таблицы. Это может быть таблицы со статистикой добавления товаров в корзину по дням, категориям, ценам и другим параметрам.

Однако обычные строчные базы данных остаются лучшим решением для продуктовых задач:

- Таблицы с доступом по ключу (id) — пользователи, товары, комментарии.
- Таблицы с заранее известной структурой запросов. Например, мы знаем, что будем делать выборку из таблицы статей, сортируя их по дате.



## ClickHouse

 Что такое ClickHouse?

- Это столбцовая column-oriented база данных, которая позволяет очень быстро выполнять аналитические и интерактивные запросы.

- Язык запросов – это SQL с расширениями.

- Плохо подходит для OLTP, потому что транзакций нет. Key-Value, потому что у нас разреженный индекс. Если вам нужна одна строчка, то вы много чего лишнего прочитаете. И если у вас Key-Value с большими blob, то это вообще будет плохо работать.

- Линейно масштабируется, если шардировать и использовать distributed таблицы.

- Отказоустойчивая, если использовать replicate таблицы.

  

***Дополнительно:***

- [Что нужно знать об архитектуре ClickHouse, чтобы его эффективно использовать](https://habr.com/ru/post/509540/)

- [Колоночные БД](https://highload.today/kolonochnye-bazy-dannykh/)

- https://habr.com/post/95181/

- https://habr.com/post/413051/

- https://habr.com/post/322724/

  