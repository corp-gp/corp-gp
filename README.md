## О компании
[GroupPrice.ru](https://groupprice.ru "GroupPrice.ru") – маркетплейс товаров, на сайте предаставлена продукция сотни поставщиков. Сборка заказа пользователя осуществляется на собсвтвенных площадях. Складская логистика реализована по кросс-докинг модели (минимальные складские запасы). Загрузка товаров и синхронизация складских остатков происходит через [YML формат](http://https://yandex.ru/support/partnermarket/export/yml.html "YML формат").

Компании 9 лет. ~ 1.5 млн. посетителей в месяц, https://www.similarweb.com/website/groupprice.ru

## Технологический стек
- RoR 6
- Ruby 2.7
- Dry-rb
- Slim, SCSS
- Webpacker, Stimulus, ES6
- Rspec
- PostgreSQL
- rubocop, eslint, slim-lint, stylelint, prettier

## Ключевая информация по организации работы

- В команде 4 разработчика
- Официальное трудоустройство по ТК РФ (зарплата белая)
- Гибкий график работы, но с 12 до 18 по мск нужно быть онлайн
- Офис в Твери. Но все кто в ИТ-отделе работают удаленно
- Для управления проектами используем свою тикет систему, которая тесно интегрирована с бизнес процессами
- Переписка и чаты в Telegram
- Ретроспективный еженедельный созвон, рассказываем о выполненных нововведениях, чтобы все были в курсе
- Есть годовой бюджет на покупку книг, курсов, билетов на конференции на весь ИТ-отдел. Неиспользованные средства в конце года сгорают
- Собираемся на RubyRussia, вместе работаем одну неделю

## IT-инфраструктура
Помимо площадки продаж ведется разработка несколько-проектов спутников:
- ptask - внутренняя тикет система, отражает коммуникационные связи организации (внутренние и внешние с поставщиками), интегрирована с Gitlab
- pscheduler - управляет запуском фоновых тасков, в основе delayed_job
- supplier - личный кабинет поставщика, позволяет контрагентам контролировать выгрузку товаров, предоставляет статистику по продажам
- tracer - трекер ошибок, отлавливает все ошибки сайта, а также вспомогательные сообщения
- mailer - управление email и push рассылками

## Работа над задачей
Задача создается во тикет системе (ptask), из которой можно сразу создать Merge Request в Gitlab. После написания кода, он проходит ревью. В проверке участвуют все сотрудники по очереди. Случайным образом выбираются 2 проверяющих (1 Senior и 1 Middle/Junior), которые автоматически добавляются к MR и получают уведомления о коммитах в Gitlab. В нем и проходит ревью кода.

## OpenSource
### Собственные репозитории (в том числе поддерживаемые форки)
- https://github.com/corp-gp/rails_string_enum
- https://github.com/corp-gp/activerecord-clean-db-structure
- https://github.com/corp-gp/lintbot
### MR
https://github.com/corp-gp/delayed_job
 - [@xronos-i-am - Improve payload_object logging](https://github.com/collectiveidea/delayed_job/pull/1120)

https://github.com/corp-gp/mini_sql
 - [@xronos-i-am - Fix symbol param encoder](https://github.com/discourse/mini_sql/pull/9)
 - [@ermolaev - add query_array](https://github.com/discourse/mini_sql/pull/10)
 - [@ermolaev - add query_decorator](https://github.com/discourse/mini_sql/pull/13)
 - [@ermolaev - empty array encoding compatibility with Sequel and ActiveRecord](https://github.com/discourse/mini_sql/pull/14)
 - [@ermolaev - improve test_query_decorator](https://github.com/discourse/mini_sql/pull/16)
 - [@ermolaev - remove double checked empty params](https://github.com/discourse/mini_sql/pull/18)

https://github.com/corp-gp/pronto-reek
 - [@ermolaev - markdown message with link](https://github.com/prontolabs/pronto-reek/pull/25)

https://github.com/corp-gp/pronto-brakeman
 - [@ermolaev - markdown message with link](https://github.com/prontolabs/pronto-brakeman/pull/22)

https://github.com/zaru/webpush
- [@xronos-i-am - Fix authorization header](https://github.com/zaru/webpush/pull/72)

https://github.com/github/view_component
- [@xronos-i-am - Move render check](https://github.com/github/view_component/pull/186)

## Работа с базой данных
Для коммуницирования с Postgresql используются:
### ActiveRecord:
- написания бизнес логики (в сервис объектах), удобно - построчное обновление с логированием всех изменений сущности, связи между объектами
- простые операции типа find, destroy, update_all

### [mini_sql](https://github.com/corp-gp/mini_sql)
- быстрая компиляция запроса в sql (builder от 3х быстрее ActiveRecord)
- быстрая сериализация данных из БД, экономия памяти. Быстрее, как создание объектов из строки, так и вызов методов у инстанса (быстрее ActiveRecord от 7х, если используются временные столбцы `timestamp`, преимущество 10x раз)
- ручной контроль prepared statements
- переиспользуется соединение с БД от ActiveRecord


## Frontend
Вся логика отображения хранится на сервере, пишется на slim шаблонизаторе, за счет использования `mini_sql` удается минимизировать время работы ruby кода, 90% всех действий это выборка объектов из БД и вызова их методов

Логика на JS минимальна, используется минималистичный фреймворк https://stimulusjs.org. Новый код пишется на es6, без jquery, используются нативные методы и полифилы для них
