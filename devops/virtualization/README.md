# Виртуализация

## Аппаратная виртуализация

Аппаратная виртуализация — виртуализация с поддержкой специальной процессорной архитектуры. В отличие от программной виртуализации, с помощью данной техники возможно использование изолированных гостевых систем, управляемых гипервизором напрямую.

Гостевая система не зависит от архитектуры хостовой платформы и реализации платформы виртуализации.

Аппаратная виртуализация обеспечивает производительность, сравнимую с производительностью невиртуализованной машины, что дает виртуализации возможность практического использования и влечет её широкое распространение. Наиболее распространены технологии виртуализации Intel-VT и AMD-V.

**Основные преимущества аппаратной виртуализации**

- Возможность создания множества виртуальных машин с различными операционными системами (включая Windows). Нет зависимости от единого ядра ОС. Пользователь может устанавливать собственные патчи на ядро при необходимости получения расширенной функциональности виртуального сервера.
- Виртуальные машины выглядят как обычный компьютер. Они содержат собственное виртуальное оборудование и программное обеспечение, которое может запускаться в виртуальных машинах без необходимости модификации.
- Виртуальные машины полностью изолированы друг от друга и от ОС сервера, где происходит запуск виртуальных машин (изоляция на уровне файловой системы, процессов, переменных sysctl).
- Благодаря использованию технологий виртуализации Intel и AMD производительность виртуальных серверов очень высока и приближена к производительности реального оборудования.

## Контейнеризация

Контейнеризация (виртуализация на уровне операционной системы, контейнерная виртуализация, зонная виртуализация) — метод виртуализации, при котором ядро операционной системы поддерживает несколько изолированных экземпляров пространства пользователя вместо одного. Эти экземпляры (обычно называемые контейнерами или зонами) с точки зрения пользователя полностью идентичны отдельному экземпляру операционной системы. Для систем на базе Unix эта технология похожа на улучшенную реализацию механизма chroot. Ядро обеспечивает полную изолированность контейнеров, поэтому программы из разных контейнеров не могут воздействовать друг на друга.

В отличие от аппаратной виртуализации, при которой эмулируется аппаратное окружение и может быть запущен широкий спектр гостевых операционных систем, в контейнере может быть запущен экземпляр операционной системы только с тем же ядром, что и у хостовой операционной системы (все контейнеры узла используют общее ядро). При этом при контейнеризации отсутствуют дополнительные ресурсные накладные расходы на эмуляцию виртуального оборудования и запуск полноценного экземпляра операционной системы, характерные при аппаратной виртуализации.

Т.о. приложение, запущенное в контейнере думает, что оно одно во всей ОС. Изоляция достигается за счет использования таких Linux-механизмов, как **namespaces** и **control groups**. Если говорить просто, то namespaces обеспечивают изоляцию в рамках ОС, а control groups устанавливают лимиты на потребление контейнером ресурсов хоста, чтобы сбалансировать распределение ресурсов между запущенными контейнерами.

Т.о. контейнеры сами по себе не являются чем-то новым, просто проект Docker, во-первых, скрыл сложные механизмы namespaces, control groups, а во-вторых, он окружен экосистемой, обеспечивающей удобное использование контейнеров на всех стадиях разработки ПО.  

**Основные преимущества контейнерной виртуализации**

- Контейнеры выполняются на одном уровне с физическими серверами. Отсутствие виртуализованного оборудования и использование реального оборудования и драйверов позволяют получить непревзойденную производительность.
- Каждый контейнер может масштабироваться до ресурсов целого физического сервера.
- Технология виртуализации на уровне ОС позволяет добиться высочайшей плотности, среди доступных среди решений виртуализации. Возможно создание и запуск сотен контейнеров на одном обычном физическом сервере.
- Контейнеры используют единую ОС, что делает их поддержку и обновление очень простым. Приложения могут быть также развернуты в отдельном окружении.
