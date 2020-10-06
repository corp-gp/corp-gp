## О компании
[GroupPrice.ru](https://groupprice.ru "GroupPrice.ru") – маркетплейс товаров, на сайте предаставлена продукция сотни поставщиков. Сборка заказа пользователя осуществляется на собсвтвенных площадях. Складская логистика реализована по кросс-докинг модели (минимальные складские запасы). Загрузка товаров и синхронизация складских остатков происходит через [YML формат](http://https://yandex.ru/support/partnermarket/export/yml.html "YML формат").

- Компании 9 лет. ~ 1.5 млн. посетителей в месяц, https://www.similarweb.com/website/groupprice.ru
- Общее количество сотрудников 80 человек.
- Свой склад площадью 14500 кв.м. и офисы 2800 кв.м.

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
- Ретроспективный еженедельный созвон, рассказываем о нововведениях, чтобы все были в курсе
- Есть годовой бюджет на покупку книг, курсов, билетов на конференции на весь ИТ-отдел
- Собираемся на RubyRussia, вместе работаем одну неделю

## IT-инфраструктура
Помимо площадки продаж ведется разработка нескольких проектов-спутников:
- ptask - внутренняя тикет система, отражает коммуникационные связи организации (внутренние и внешние с поставщиками), интегрирована с Gitlab
- pscheduler - управляет запуском фоновых тасков, в основе `delayed_job`
- supplier - личный кабинет поставщика, позволяет контрагентам контролировать выгрузку товаров, предоставляет статистику по продажам
- tracer - трекер ошибок (отлавливает все ошибки сайта), логирует все ответы сторонних API, хранит все изменения сущностей (Заказ, Товар...) - помогает быстро разбираться в проблемах
- mailer - управление email и push рассылками

## Работа над задачей
Задача создается в тикет системе (ptask), из которой можно сразу создать Merge Request в Gitlab. После написания кода, он проходит ревью. В проверке попеременно участвуют все сотрудники IT-отдела. Случайным образом выбираются 2 проверяющих (1 Senior и 1 Middle/Junior), которые автоматически добавляются к MR и получают уведомления о коммитах в Gitlab. В нем и проходит ревью кода. Каждый коммит проходит автоматическую валидацию при помощи [rubocop](https://github.com/rubocop-hq/rubocop), [slim-lint](https://github.com/sds/slim-lint), [eslint](https://github.com/eslint/eslint), [stylelint](https://github.com/stylelint/stylelint). Помимо этого в работе используется [соглашение о стилях](https://github.com/corp-gp/styleguide/blob/main/README.md). Для деплоя используется Gitlab CI/CD. После аппрува MR запускается lint и прогоняются тесты, при успешном завершении происходит автоматический deploy в production.

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

## Производительность
Пользователю должно быть комфортно пользоваться сайтом на ПК и телефоне. Производительность важна как на бекенде, так и на форонтенде, разработчику необходимо думать об оптимальности кода, разбираться в тонкостях БД, делать бенчмарки, иметь представление о работе ruby интерпретатора.

Среднее время ответа нашего бекенда 115мс (учитывая что весь html генерится на сервере это очень хороший результат)
![image](https://user-images.githubusercontent.com/938305/95205175-af9ede00-07ed-11eb-84cd-dc52d5daf071.png)

Половина времени уходит на выполнение sql запросов, на страницах каталога сложные запросы для фильтрации, персональные сортировки, для обеспечения приемлемой производительности требуется глубокое понимание работы сайта - настройка nginx, кэши, защита от ddos, перезагрузка приложения без простоя, понимание работы rails, ruby, настройка параметров БД и знание подходов к оптимизации sql.

### PageSpeed Insights
Измерения необходимо проводить с одного и того же устройства, тестируется страница каталога - платье, как самая покупаемая вещь одежды
- [https://groupprice.ru/categories/platiya-jens](https://developers.google.com/speed/pagespeed/insights/?hl=RU&url=https%3A%2F%2Fgroupprice.ru%2Fcategories%2Fplatiya-jens&tab=mobile) - mobile 49, desktop 87
- [https://www.ozon.ru/category/platya-zhenskie-7502/](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fwww.ozon.ru%2Fcategory%2Fplatya-zhenskie-7502%2F&tab=mobile) - mobile 28, desktop 56
- [https://www.lamoda.ru/c/369/clothes-platiya/](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fwww.lamoda.ru%2Fc%2F369%2Fclothes-platiya%2F&tab=mobile) - mobile 19, desktop 78
- [https://www.wildberries.ru/catalog/zhenshchinam/odezhda/platya](https://developers.google.com/speedpagespeed/insights/?url=https%3A%2F%2Fwww.wildberries.ru%2Fcatalog%2Fzhenshchinam%2Fodezhda%2Fplatya&tab=mobile) - mobile 6, desktop 70
- [https://www.kupivip.ru/catalog/zhenschinam/odezhda/platya-i-sarafany](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fwww.kupivip.ru%2Fcatalog%2Fzhenschinam%2Fodezhda%2Fplatya-i-sarafany&tab=mobile) - mobile 18, desktop 40
- [https://www.bonprix.ru/kategoriya/dlya-zhenshchin-odezhda-platya/](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fwww.bonprix.ru%2Fkategoriya%2Fdlya-zhenshchin-odezhda-platya%2F) - mobile 31, desktop 59

Знаете как сделать еще быстрее? Пишите https://t.me/a_ermolaev
