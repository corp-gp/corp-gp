## О компании
[GroupPrice.ru](https://groupprice.ru) – маркетплейс товаров, на площадке представлена продукция сотни поставщиков, основная специализация - женская одежда. Сборку заказа пользователя осуществляем на собственных площадях, складская логистика реализована по кросс-докинг модели (минимальные складские запасы). Загрузка товаров и синхронизация складских остатков происходит через [YML формат](http://https://yandex.ru/support/partnermarket/export/yml.html "YML формат").

- Компании 10 лет. ~ 2 млн. посетителей в месяц
- Общее количество сотрудников 100 человек.
- Свой склад площадью 14500 кв.м. и офисы 2800 кв.м.

## Технологический стек
- RoR 7
- Ruby 3.1
- Dry-rb
- Slim, SCSS
- Hotwire, Stimulus, Vite.JS
- Rspec
- PostgreSQL 15
- ClickHouse
- rubocop, eslint, slim-lint, stylelint, prettier

## Ключевая информация по организации работы

- Официальное трудоустройство по ТК РФ
- Гибкий график работы, но с 12 до 18 по мск нужно быть онлайн
- Офис в Твери. Но все кто в ИТ-отделе работают удаленно
- Для управления проектами используем свою тикет систему (`ptask`), которая тесно интегрирована с бизнес процессами
- Переписка и чаты в Telegram
- Ретроспективный еженедельный созвон, рассказываем о нововведениях, чтобы все были в курсе
- Оплата книг, курсов, билетов на конференции
- Собираемся на RubyRussia, вместе работаем одну неделю

## IT-инфраструктура
Помимо площадки продаж ведется разработка нескольких проектов-спутников:
- `ptask` - внутренняя тикет система, отражает коммуникационные связи организации (внутренние и внешние с поставщиками), интегрирована с Gitlab
- `pscheduler` - управляет запуском фоновых задач, в основе `delayed_job`
- `supplier` - личный кабинет поставщика, позволяет контрагентам контролировать выгрузку товаров, предоставляет статистику по продажам
- `tracer` - трекер ошибок (отлавливает все ошибки сайта), логирует все ответы сторонних API, хранит все изменения сущностей (Заказ, Товар...) - помогает быстро разбираться в проблемах
- `mailer` - управление email и push рассылками

## Работа над задачей
1. Задача создается в тикет системе (`ptask`), из которой можно сразу создать Merge Request в Gitlab.
1. Весь код проходит ревью. В проверке участвуют все сотрудники IT-отдела. Случайным образом выбираются 2 проверяющих (1 Senior и 1 Middle/Junior), которые автоматически добавляются к MR и получают уведомления о коммитах в Gitlab. В нем и проходит ревью кода.
1. Локально на каждый коммит запускаются линтеры: [rubocop](https://github.com/corp-gp/rubocop-gp), [slim-lint](https://github.com/sds/slim-lint), [eslint](https://github.com/eslint/eslint), [stylelint](https://github.com/stylelint/stylelint). Помимо этого в работе используется [соглашение о стилях](https://github.com/corp-gp/corp-gp/blob/main/STYLEGUIDE.md). 
1. Для деплоя используется Gitlab CI/CD. После аппрува MR запускаются линтеры и тесты, при успешном завершении происходит автоматический deploy в production.

## OpenSource
### Собственные репозитории (в том числе поддерживаемые форки)
- https://github.com/corp-gp/rails_string_enum
- https://github.com/corp-gp/activerecord-clean-db-structure
- https://github.com/corp-gp/lintbot
- https://github.com/corp-gp/rubocop-gp
- https://github.com/corp-gp/factory_bot-preload
- https://github.com/corp-gp/email_stylist


### Pull requests
https://github.com/dry-rb/dry-effects
- [@ermolaev - fix resolving dependencies via nested names](https://github.com/dry-rb/dry-effects/pull/81)

https://github.com/corp-gp/delayed_job
- [@xronos-i-am - Improve payload_object logging](https://github.com/collectiveidea/delayed_job/pull/1120)

https://github.com/corp-gp/mini_sql
- [@xronos-i-am - Fix symbol param encoder](https://github.com/discourse/mini_sql/pull/9)
- [@ermolaev - add query_array](https://github.com/discourse/mini_sql/pull/10)
- [@ermolaev - add query_decorator](https://github.com/discourse/mini_sql/pull/13)
- [@ermolaev - empty array encoding compatibility with Sequel and ActiveRecord](https://github.com/discourse/mini_sql/pull/14)
- [@ermolaev - improve test_query_decorator](https://github.com/discourse/mini_sql/pull/16)
- [@ermolaev - remove double checked empty params](https://github.com/discourse/mini_sql/pull/18)
- [@ermolaev - support prepared statements](https://github.com/discourse/mini_sql/pull/20)
- [@xronos-i-am & @ermolaev - Serializable materializer](https://github.com/discourse/mini_sql/pull/23)
- [@xronos-i-am - Compacted JSON serialization](https://github.com/discourse/mini_sql/pull/24)
- [@xronos-i-am - Marshallable serializer](https://github.com/discourse/mini_sql/pull/25)
- [@ermolaev - fix encode date](https://github.com/discourse/mini_sql/pull/28)
- [@ermolaev - real to_sql](https://github.com/discourse/mini_sql/pull/29)
- [@ermolaev - add query_array and group_by to builder](https://github.com/discourse/mini_sql/pull/31)
- [@xronos-i-am - Results equality](https://github.com/discourse/mini_sql/pull/33)
- [@xronos-i-am - allow multiple occurencies of builder statements](https://github.com/discourse/mini_sql/pull/50)

https://github.com/corp-gp/pronto-reek
- [@ermolaev - markdown message with link](https://github.com/prontolabs/pronto-reek/pull/25)

https://github.com/corp-gp/pronto-brakeman
- [@ermolaev - markdown message with link](https://github.com/prontolabs/pronto-brakeman/pull/22)

https://github.com/zaru/webpush
- [@xronos-i-am - Fix authorization header](https://github.com/zaru/webpush/pull/72)

https://github.com/github/view_component
- [@xronos-i-am - Move render check](https://github.com/github/view_component/pull/186)

https://github.com/mileszs/wicked_pdf
- [@xronos-i-am - Fix check webpacker version](https://github.com/mileszs/wicked_pdf/pull/964)

## Арихитектура Rails приложения
Все приложения реализуют серверный HTML рендеринг, в редких случаях результат отдается в JSON, с последующим рендерингом на клиенте. За счет этого имеются следующие преимущества:
- быстрое, удобное, при необходимости изолированное или полное тестирование страницы без браузера
- хорошее отслеживание ошибок (при возникновении в коде любой не понятной ситуации приложение должно падать, вместо проглатывания ошибки и некорректной тихой работы)
- при изменении HTML верстки не требуется полная перезагрузка страницы (если используется Turbolinks)

Бизнес-логика распределена по доменам, домены состоят из различных слоев: Services, Forms, Decorators, Repositories, Queries. Набор слоёв в каждом случае определяется относительно задачи, не стоит размазывать мелкую функциональность по всем слоям. Бизнес код - самая ценная и сложная часть приложения, для успешного решения задачи всегда надо понимать смысл решаемой задачи. В ИТ индустрии есть попытки формирования подхода к написанию бизнес кода:
- DDD
- Луковая (слоистая) архитектура

Если с философской точки зрения сообщество разработчиков более-менее в консенсусе, то предлагаемая практическая реализация, практически от любого автора, вызывает больше вопросов чем ответов. Поэтому окончательное решение за разработчиком, принятыми в команде соглашениями и подходами.

Переменные, методы, поля таблиц должны именоваться в терминах бизнеса, при изменении бизнес правил - переименовываться, дабы избежать путаницы, поддерживать общение с коллегами вне ИТ отдела на одном языке. Явная зависимость в коде (Inversion of Control Containers) почти всегда лучше неявной (Mixins).

## Работа с базой данных
Бизнес-логика и пользовательские интерфейсы эволюционируют довольно быстро, структурам данных и их отношениям это не свойственно. Правила предметной области, закодированные в модели данных имеют долгосрочный характер, и не теряются при изменениях в логике приложения. Потеря, порча, не консистентность данных самая страшная ошибка.

Для общения с Postgresql используются:
### ActiveRecord
- написания бизнес логики (в сервис объектах), удобно - построчное обновление с логированием всех изменений сущности, связи между объектами
- простые операции типа find, destroy, update_all

### [mini_sql](https://github.com/corp-gp/mini_sql)
- быстрая компиляция запроса в sql (builder от 3х быстрее ActiveRecord)
- быстрая сериализация данных из БД, экономия памяти. Быстрее, как создание объектов из строки, так и вызов методов у инстанса (быстрее ActiveRecord от 7х, если используются временные столбцы `timestamp`, преимущество 10x раз)
- ручной контроль prepared statements
- переиспользуется соединение с БД от ActiveRecord


## Frontend
Вся логика отображения хранится на сервере, пишется на slim шаблонизаторе, за счет использования `mini_sql` удается минимизировать время работы ruby кода, 90% всех действий это выборка объектов из БД и вызовы их методов.

Переходы внутри сайта работают быстро за счет https://github.com/turbolinks/turbolinks - не тратится время на компиляцию JS в браузере, CSS парсинга.

Логика на JS минимальна, используется минималистичный фреймворк https://stimulusjs.org совместимый с `turbolinks`. Новый код пишется на es6, без jquery, используются нативные методы и полифилы для них.

Для удобного переиспользования, простого тестирования и инкапсуляции шаблонов используется - https://github.com/github/view_component

## Производительность
Пользователю должно быть комфортно пользоваться сайтом на ПК и телефоне. Производительность важна как на бекенде, так и на форонтенде. Разработчику необходимо думать об оптимальности кода, разбираться в тонкостях БД, делать бенчмарки, иметь представление о работе ruby интерпретатора.

Существует исследование, которое выявило зависимость между временем реакции и субъективным восприятием пользователя:

Задержка реакции, мс |	Восприятие пользователем
------------ | -------------
0-100	| Мгновенная реакция
100-300	| Небольшая, но заметная задержка
300-1000	| Система работает, но нагружена
1000-10000	 | Вероятное переключение мыслей на другие задачи
10000 и более	| Задача отменяется (система не работает)

Среднее время ответа нашего бекенда 65 мс,учитывая что в основном каждый запрос отдает html, неплохой результат.
![image](https://user-images.githubusercontent.com/938305/120470716-8b12fa00-c3ac-11eb-9f5f-28f197fd97c9.png)

Половина времени уходит на выполнение SQL запросов, на страницах каталога сложные запросы для фильтрации, персональные сортировки, для обеспечения приемлемой производительности требуется глубокое понимание работы сайта - настройка nginx, кэши, защита от ddos, перезагрузка приложения без простоя, понимание работы rails, ruby, настройка параметров БД и знание подходов к оптимизации sql.

### PageSpeed Insights
Измерения необходимо проводить с одного и того же устройства, тестируется страница каталога - платье, как самая покупаемая вещь одежды
- [https://groupprice.ru/categories/platiya-jens](https://developers.google.com/speed/pagespeed/insights/?hl=RU&url=https%3A%2F%2Fgroupprice.ru%2Fcategories%2Fplatiya-jens&tab=mobile) - mobile 70, desktop 98
- [https://www.ozon.ru/category/platya-zhenskie-7502/](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fwww.ozon.ru%2Fcategory%2Fplatya-zhenskie-7502%2F&tab=mobile) - mobile 52, desktop 80
- [https://www.lamoda.ru/c/369/clothes-platiya/](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fwww.lamoda.ru%2Fc%2F369%2Fclothes-platiya%2F&tab=mobile) - mobile 29, desktop 68
- [https://www.wildberries.ru/catalog/zhenshchinam/odezhda/platya](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fwww.wildberries.ru%2Fcatalog%2Fzhenshchinam%2Fodezhda%2Fplatya&tab=mobile) - mobile 18, desktop 48
- [https://www.bonprix.ru/kategoriya/dlya-zhenshchin-odezhda-platya/](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fwww.bonprix.ru%2Fkategoriya%2Fdlya-zhenshchin-odezhda-platya%2F) - mobile 35, desktop 68

Знаете как сделать еще быстрее? Пишите https://t.me/a_ermolaev
