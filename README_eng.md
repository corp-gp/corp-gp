## About the Company
[GroupPrice.ru](https://groupprice.ru) – a marketplace for goods, featuring products from hundreds of suppliers, with the main specialization in women's clothing. We assemble user orders on our own premises, warehouse logistics is implemented using a cross-docking model (minimal warehouse stocks). Uploading goods and synchronizing warehouse balances occurs through [YML format](http://https://yandex.ru/support/partnermarket/export/yml.html "YML format").

- The company is 14 years old. ~ 2 million visitors per month
- Total number of employees: 100 people.
- Own warehouse with an area of 14,500 sq.m. and offices of 2,800 sq.m.

## Technology Stack
- RoR 8
- Ruby 3.4
- Dry-rb
- Slim, SCSS
- Hotwire, Stimulus, Vite.JS, Tailwind
- Rspec
- PostgreSQL 18
- ClickHouse
- rubocop, eslint, slim-lint, stylelint, prettier
- kamal

## Key Information on Work Organization

- Official employment under the Labor Code of the Russian Federation
- Flexible work schedule, but you need to be online from 12 to 18 Moscow time
- Office in Tver. But everyone in the IT department works remotely
- For project management, we use our own ticket system (`ptask`), which is tightly integrated with business processes
- Correspondence and chats in Telegram
- Retrospective weekly call, we talk about innovations so that everyone is informed
- Payment for books, courses, conference tickets
- We gather at RubyRussia, work together for one week

## IT Infrastructure
In addition to the sales platform, development of several satellite projects is underway:
- `ptask` - internal ticket system, reflects the organization's communication links (internal and external with suppliers), integrated with Gitlab, telegram
- `psupplier` - supplier's personal account, allows contractors to control product uploads, provides sales statistics, work with ozon, wb, yandex
- `tracer` - error tracker (catches all site errors), logs all responses from third-party APIs, stores all entity changes (Order, Product...) - helps to quickly resolve issues
- `mailer` - management of email and push mailings

## Working on a Task
1. The task is created in the ticket system (`ptask`), from which you can immediately create a Merge Request in Gitlab.
1. All code undergoes review. All IT department employees participate in the review. Two reviewers are randomly selected (1 Senior and 1 Middle/Junior), who are automatically added to the MR and receive notifications about commits in Gitlab. The code review takes place there.
1. Locally, linters are run on each commit: [rubocop](https://github.com/corp-gp/rubocop-gp), [slim-lint](https://github.com/sds/slim-lint), [eslint](https://github.com/eslint/eslint), [stylelint](https://github.com/stylelint/stylelint). In addition, a [style agreement](https://github.com/corp-gp/corp-gp/blob/main/STYLEGUIDE.md) is used in the work. 
1. For deployment, Gitlab CI/CD is used. After MR approval, linters and tests are run, upon successful completion, automatic deploy to production occurs.

## OpenSource
### Own Repositories (including maintained forks)
- https://github.com/corp-gp/active_dry_form
- https://github.com/corp-gp/enum_machine
- https://github.com/corp-gp/active_dry_deps
- https://github.com/corp-gp/active_typed_store
- https://github.com/corp-gp/activerecord-clean-db-structure
- https://github.com/corp-gp/lintbot
- https://github.com/corp-gp/rubocop-gp
- https://github.com/corp-gp/fixture_bot
- https://github.com/corp-gp/email_stylist
- and others https://github.com/corp-gp

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

## Rails Application Architecture
All applications implement server-side HTML rendering, in rare cases the result is returned in JSON, with subsequent rendering on the client. This provides the following advantages:
- fast, convenient, if necessary, isolated or full page testing without a browser
- good error tracking (if any unclear situation occurs in the code, the application should crash instead of swallowing the error and working incorrectly quietly)
- when changing HTML layout, a full page reload is not required (if Turbo is used)

Business logic is distributed across domains, domains consist of various layers: Services, Forms, Decorators, Repositories, Queries. The set of layers in each case is determined relative to the task, do not spread small functionality across all layers. Business code is the most valuable and complex part of the application, to successfully solve the task, you always need to understand the meaning of the task being solved. In the IT industry, there are attempts to form an approach to writing business code:
- DDD
- Onion (layered) architecture

From a philosophical point of view, the developer community is more or less in consensus, but the proposed practical implementation from almost any author raises more questions than answers. Therefore, the final decision is up to the developer, the agreements and approaches accepted in the team.

Variables, methods, table fields should be named in business terms, when business rules change - renamed to avoid confusion, maintain communication with colleagues outside the IT department in the same language. Explicit dependency in code (Inversion of Control Containers) is almost always better than implicit (Mixins).

## Working with the Database
Business logic and user interfaces evolve quite quickly, data structures and their relationships do not. Domain rules encoded in the data model have a long-term nature and are not lost when application logic changes. Loss, corruption, data inconsistency is the worst error.

For communication with Postgresql, the following are used:
### ActiveRecord
- writing business logic (in service objects), convenient - line-by-line update with logging of all entity changes, relationships between objects
- simple operations like find, destroy, update_all

### [mini_sql](https://github.com/corp-gp/mini_sql)
- fast compilation of the query into sql (builder is 3x faster than ActiveRecord)
- fast data serialization from the DB, memory saving. Faster both creating objects from a string and calling instance methods (faster than ActiveRecord by 7x, if temporary `timestamp` columns are used, advantage 10x)
- manual control of prepared statements
- reuses the DB connection from ActiveRecord


## Frontend
All display logic is stored on the server, written in the slim templater, thanks to the use of `mini_sql`, it is possible to minimize the runtime of ruby code, 90% of all actions are selecting objects from the DB and calling their methods.

Transitions within the site work quickly thanks to [https://github.com/turbolinks/turbolinks](https://github.com/hotwired/turbo) - no time is spent on JS compilation in the browser, CSS parsing.

Logic on JS is minimal, a minimalist framework https://stimulusjs.org compatible with `turbo` and turbo frames/tags is used. New code is written in es6 and typescript, native methods are used.

For convenient reuse, simple testing, and template encapsulation - https://github.com/github/view_component is used.

## Performance
The user should be comfortable using the site on PC and phone. Performance is important both on the backend and frontend. The developer needs to think about code optimality, understand DB subtleties, do benchmarks, have an idea of the ruby interpreter's work.

There is a study that revealed the dependence between reaction time and the user's subjective perception:

Reaction delay, ms |	User Perception
------------ | -------------
0-100	| Instant reaction
100-300	| Small but noticeable delay
300-1000	| System is working but loaded
1000-10000	 | Likely switching thoughts to other tasks
10000 and more	| Task is canceled (system not working)

Our backend's average response time is 65 ms, considering that mainly each request returns html, a good result.
![image](https://user-images.githubusercontent.com/938305/120470716-8b12fa00-c3ac-11eb-9f5f-28f197fd97c9.png)

Half the time is spent on executing SQL queries, on catalog pages there are complex queries for filtering, personal sorting, to ensure acceptable performance, a deep understanding of the site's work is required - nginx setup, caches, ddos protection, application restart without downtime, understanding of rails, ruby work, DB parameter setup, and knowledge of sql optimization approaches.

### PageSpeed Insights
Measurements must be taken from the same device, the catalog page - dress, as the most purchased clothing item is tested
- [https://groupprice.ru/categories/platiya-jens](https://developers.google.com/speed/pagespeed/insights/?hl=RU&url=https%3A%2F%2Fgroupprice.ru%2Fcategories%2Fplatiya-jens&tab=mobile) - mobile 70, desktop 98
- [https://www.ozon.ru/category/platya-zhenskie-7502/](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fwww.ozon.ru%2Fcategory%2Fplatya-zhenskie-7502%2F&tab=mobile) - mobile 52, desktop 80
- [https://www.lamoda.ru/c/369/clothes-platiya/](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fwww.lamoda.ru%2Fc%2F369%2Fclothes-platiya%2F&tab=mobile) - mobile 29, desktop 68
- [https://www.wildberries.ru/catalog/zhenshchinam/odezhda/platya](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fwww.wildberries.ru%2Fcatalog%2Fzhenshchinam%2Fodezhda%2Fplatya&tab=mobile) - mobile 18, desktop 48
- [https://www.bonprix.ru/kategoriya/dlya-zhenshchin-odezhda-platya/](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fwww.bonprix.ru%2Fkategoriya%2Fdlya-zhenshchin-odezhda-platya%2F&tab=mobile) - mobile 35, desktop 68

Know how to make it even faster? Write to https://t.me/a_ermolaev
