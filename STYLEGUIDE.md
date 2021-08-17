# Ruby
### Другие стайлгайды
https://github.com/thoughtbot/guides/blob/master/rails/README.md

### Именование хешей `value(s)_by_key`

сразу видно что это хеш и что в нем

часто образуется от методов:

```ruby
user_by_product_id = users.index_by(&:product_id)
users_by_product_id = users.group_by(&:product_id)
```

### Именование методов, которые присваивают аттрибуты, начинаются с assign

```
class TaskForm
  
  def create(params)
    self.attributes = params
    assign_owner
    save
  end
  
  private def assign_owner
    self.owner_id = 1
  end

end
```


### Установка инстанс переменных в контроллере
только явное присвоение

#### плохо
```
class TaskController < ApplicationController
  before_action :show, :edit
  
  def show; end
  def edit; end
  
  private def set_task
    @task = Task.find(params[:id])
  end
end
```

#### хорошо
```
class TaskController < ApplicationController
  
  def show
    @task = fetch_task
  end
  
  def edit
    @task = fetch_task
  end
  
  private def fetch_task
    Task.find(params[:id])
  end
end
```

### Именование временных полей в бд, переменных
- Временная метка с секундами `(datetime)` с суффиксом  - `_at`
- Время до дня `(date)` с суффиксом - `_on`
- Время суток без даты с суффиксом `_time`.

# Ruby Profiling

- https://github.com/tmm1/stackprof
- https://github.com/SamSaffron/flamegraph
- https://github.com/tmm1/rbtrace
- https://samsaffron.com/archive/2018/01/18/my-production-ruby-on-rails-cpu-is-at-100-now-what
- https://www.justinweiss.com/articles/how-to-debug-ruby-performance-problems-in-production/
- https://github.com/MiniProfiler/rack-mini-profiler

# Rails PG Migrations
- https://docs.gitlab.com/ee/development/migration_style_guide.html#multi-threading
- https://gitlab.com/gitlab-org/gitlab-foss/-/blob/master/lib/gitlab/database/migration_helpers.rb
- https://github.com/ankane/strong_migrations
- https://github.com/gocardless/nandi


# StimulusJS
- https://github.com/skatkov/awesome-stimulusjs
- https://www.betterstimulus.com/
- https://github.com/stimulus-use/stimulus-use

# CSS
Пример оформления CSS классов
- классы компонентов начинаются с нижнего подчеркивания `_subscribe-user--widget`, `_order-new`
- во всех названиях класса должен использоваться только `-` (kebab-case, удобно искать так как нет персесечения с js, ruby кодом)
- класс верхнего уровня - минимум 2 слова полученных от нижних уровней дерева каталогов (по аналогии со stimulus контроллером, `--` между директориями)
- в идеале не должно быть переопределений общих классов, или классов от других компонентов (когда компонет внутри компонента)

```scss
._order-new {
  ._payment { }
  ._delivery { }
  ._line-items { }
  ._button { }
}
```

# SQL
### Другие стайлгайды
https://www.sqlstyle.guide/ru/
https://docs.telemetry.mozilla.org/concepts/sql_style.html

### Типовое оформление запроса

```sql
SELECT
  line_items.id,
  line_items.user_id,
  COALESCE(warehouse_storehouses.total_remainders - warehouse_storehouses.total_in_delivery, 0) AS available_main_storehouse,
  (
    CASE
    WHEN line_items.state != 'choice' THEN true
    WHEN warehouses.limit_quantity_supplier > warehouses.total_ordered THEN true
    WHEN warehouse_storehouses.total_remainders > warehouse_storehouses.total_in_delivery THEN true
    ELSE false
    END
  ) AS is_cart_available,
  GREATEST(
    warehouses.limit_quantity_supplier - warehouses.total_ordered,
    COALESCE(warehouse_storehouses.total_remainders - warehouse_storehouses.total_in_delivery, 0)
  ) AS max_cart_available,
FROM
  line_items
  INNER JOIN warehouses
          ON warehouses.id = line_items.warehouse_id
  INNER JOIN products
          ON products.id = warehouses.product_id
  INNER JOIN brands
          ON brands.id = products.brand_id
  LEFT JOIN warehouse_storehouses
         ON warehouse_storehouses.storehouse_id = 1
        AND warehouse_storehouses.warehouse_id = warehouses.id
  LEFT JOIN purchases
         ON purchases.id = line_items.purchase_id
         OR ( line_items.purchase_id IS NULL AND purchases.supplier_id = products.supplier_id AND purchases.state = 'created' )
WHERE
      line_items.deleted_at IS NULL
  AND line_items.state IN (:cart_items_states)
  AND line_items.order_id IS NULL
ORDER BY
  line_items.state ASC,
  is_cart_available DESC,
  line_items.id DESC
```


```sql
SELECT
  *
FROM
  properties
WHERE
     properties.prototype_id = 1
  OR properties.id IN (2, 3, 8)
  OR (
    properties.prototype_id = :prototype_id
    AND (
      properties.ptype_property_list_ids = '{}'
      OR
      properties.ptype_property_list_ids && ARRAY[123]::int[]
    )
  )
```
