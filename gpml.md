# GroupPrice Market Language

Формат выгрузки основан на [YML (Yandex Market Language)](https://yandex.ru/support/partnermarket/export/yml.html), [доп. описание полей](https://yandex.ru/support/marketplace/assortment/fields/index.html)

Но расширен тегами
* `variant` с вложениями `size`, `quantity` и `barcode`
* `vendorModel`

```xml
<!--
  Дата генерации выгрузки обязательна, если дата не актуальна более чем на 4 часа,
  товары закрываются автоматически.
-->
<yml_catalog date="2021-04-23 18:32">
  <shop>
    <name>Твой Стиль</name> <!-- Короткое название магазина, для покупателя. -->
    <company>ООО "Твой Стиль"</company> <!-- Полное наименование компании, владеющей магазином. -->
    <url>https://you-style.ru/</url> <!-- URL главной страницы магазина. -->
    <!-- Древовидный список категорий магазина. Подробнее https://yandex.ru/support/partnermarket/elements/categories.html -->
    <categories>
      <category id="1">Платья</category>
      <category id="11" parentId="1">Офисные</category>
      <category id="12" parentId="1">Вечерние</category>
      <category id="13" parentId="1">Вязаные</category>
      <category id="2">Блузки</category>
      <category id="3">Верхняя одежда</category>
      <category id="4">Френчи и Кардиганы</category>
      <category id="5">Юбки</category>
      <category id="6">Брюки</category>
    </categories>
    <offers>
      <!-- Список предложений. Подробнее https://yandex.ru/support/partnermarket/export/vendor-model.html -->
      <offer>
        <url>https://you-style.ru/products/2456</url> <!-- URL страницы товара на сайте -->
        <currencyId>RUR</currencyId> <!-- Валюта, в которой указана цена товара -->
        <categoryId>2</categoryId> <!-- Идентификатор категории товара -->
        <vendor>Твой Стиль</vendor> <!-- Бренд, название производителя -->
        <model>Блузка в полоску</model> <!-- Модель и название товара -->
        <vendorcode>1720000523</vendorcode> <!-- Артикул, код товара производителя -->
        <vendorModel>m-1</vendorModel> <!-- Идентификатор модели для группировки по цветам  -->
        <typePrefix>Блузка</typePrefix> <!-- Тип/категория товара - Брюки, платье, Футболка -->
        <price>2340</price> <!-- Оптовая цена товара -->
        <description> <!-- Описание -->
          Верх украшен кружевом, на талии бантик - смотрится изящно!
        </description>
        <country_of_origin>Россия</country_of_origin> <!-- Страна производства -->
        <!-- URL-ссылки на картинки товара -->
        <picture>https://you-style.ru/upload/f67f646484f8.jpeg</picture>
        <picture>https://you-style.ru/upload/s1of6464g6dr.jpeg</picture>
        <picture>https://you-style.ru/upload/a3hf646484f8.jpeg</picture>
        <!-- URL-ссылка на видео товара в формате MP4, MOV. Высота должна быть больше ширины и быть в диапазоне 800 - 2000px, размер файла не более 100 MB -->
        <video>https://you-style.ru/upload/trf646fj2e.mp4</video>
        <!-- Характеристики товара — цвет, размер, объем, материал, вес, возраст, пол, и т. д. -->
        <param name="Цвет">оранжевый</param>
        <param name="Ткань">атлас</param>
        <param name="Состав">полиэстер 97%, эластан 3%</param>
        <!-- Код ТН ВЭД,  может быть несколько <tn-ved-code>, каждый из которых содержит один из кодов товара. -->
        <tn-ved-codes>
          <tn-ved-code>8517610008</tn-ved-code>
        </tn-ved-codes>
        <!-- Габариты товара (длина, ширина, высота) в упаковке в сантиметрах. Формат: три положительных числа с точностью 0.001, разделитель целой и дробной части — точка. Числа должны быть                разделены символом «/» без пробелов.-->
        <dimensions>20/40.55/25</dimensions>
        <!-- Вес товара в килограммах с учетом упаковки. Вес можно указывать с точностью до тысячных (например, 1.001; разделитель целой и дробной части — точка). -->
        <weight>2.550</weight>
        <!-- Варианты товара, в карточке товара выберается пользователем -->
        <variant>
          <!-- (Необязателен) Уникальный идентификатор, возвращается в API -->
          <variantId>1720000523-56</variantId>
          <!-- Параметр варианта, для одежды - Размер, других видов товаров - длинна, диагональ -->
          <size name="Размер">56</size> 
          <!-- Специфичные характеристики в рамках варианта  -->
          <param name="Длина по спинке">60 см</param>
          <param name="Обхват бедер">90 см</param>
          <quantity>2</quantity> <!-- (Обязателен) Количество товара на складе у поставщика -->
          <barcode>65740266138</barcode> <!-- (Обязателен) Уникальный штрихкод, используется складом для оприходования товара, возвращается в API -->
        </variant>
      </offer>
      <offer>
        <url>https://you-style.ru/products/2345</url>
        <currencyId>RUR</currencyId>
        <categoryId>1</categoryId>
        <vendor>Твой Стиль</vendor>
        <model>Платье с брошкой</model>
        <vendorcode>1720000582</vendorcode>
        <vendorModel>m-2</vendorModel>
        <description>
          Трикотаж невероятно приятен к телу.
          С брошкой в комплекте.
        </description>
        <country_of_origin>Китай</country_of_origin> <!-- Страна производства -->
        <picture>https://you-style.ru/upload/54bf646484f8.jpeg</picture>
        <picture>https://you-style.ru/upload/54bf6464g6dr.jpeg</picture>
        <picture>https://you-style.ru/upload/74bf646484f8.jpeg</picture>
        <picture>https://you-style.ru/upload/8tbf64648de1.jpeg</picture>
        <picture>https://you-style.ru/upload/d4bf646484f8.jpeg</picture>
        <price>3 590</price>
        <typePrefix>Платье</typePrefix>
        <param name="Цвет">бежевый</param>
        <param name="Ткань">шифон</param>
        <param name="Состав">65 % вискоза 30 % полиэстр 5 % лайкра</param>
        <dimensions>20/20/20</dimensions>
        <weight>2</weight>
        <variant>
          <size name="Размер">44</size>
          <param name="Длина">70 см</param>
          <quantity>4</quantity>
          <barcode>6581400306131</barcode>
        </variant>
        <variant>
          <size name="Размер">46</size>
          <param name="Длина">71 см</param>
          <quantity>6</quantity>
          <barcode>125470306148</barcode>
        </variant>
        <variant>
          <size name="Размер">48</size>
          <param name="Длина">72 см</param>
          <quantity>2</quantity>
          <barcode>1254700306148</barcode>
        </variant>
        <variant>
          <size name="Размер">50</size>
          <param name="Длина">73 см</param>
          <quantity>4</quantity>
          <barcode>1254730306148</barcode>
        </variant>
        <variant>
          <size name="Размер">55</size>
          <param name="Длина">74 см</param>
          <quantity>3</quantity>
          <barcode>12543306148</barcode>
        </variant>
      </offer>
    </offers>
  </shop>
</yml_catalog>
```

# API для поставщика

API позволяет получить список текущих заказанных пользователями товаров, информацию по текущей/прошлой закупке, изменить остатки/цены. 
Используется для автоматического резервирования товара на стороне поставщика, рекомендуется делать запросы не реже
чем раз в пол часа. 

Все запросы выполняются с передачей токена доступа (`api_token`). Для его получения необходимо обратиться в отдел закупок - [opt@groupprice.ru](mailto:opt@groupprice.ru)

Взаимодействие с API реализуется посредством отправки REST-запросов в JSON-формате на один из адресов:
- Рабочая версия API - https://psupplier.groupprice.ru/api/v1/
- Тестовая версия - https://psupplier.groupprice.ru/api/test/

*Методы Api*

**1. Получение списка закупок /purchases**

Пример: https://psupplier.groupprice.ru/api/test/purchases?api_token=XXXX
```js
[
    {
        "id": 123, // Номер закупки
        "billed_at": "2021-06-12", // Дата окончания
        "created_at": "2021-06-08T10:38:05.487+03:00", // Дата cоздания
        "departure_at": "2021-06-14", // Дата забора ТК
        "stocked_at": "2021-06-16" // Дата поступления на склад Groupprice
    }
]
```

**2. Получение списка товаров по закупке /pre_order**

Метод имеет необязательный параметр `purchase_id`, при передаче которого будут возвращены товары по конкретной закупке.

Пример: https://psupplier.groupprice.ru/api/test/pre_order?api_token=XXXX

```js
{
    "line_items": [
        {
            "booked_at": "2021-04-27T10:10:52.231Z",
            "nomenclature": "a34596",
            "product_name": "Платье",
            "quantity": 1,
            "shop_barcode": "hfts57ld438",
            "shop_variant_id": "б0907-52",
            "variant_name": "Размер - 52"
        },
        {
            "booked_at": "2021-04-27T12:56:12.255Z",
            "nomenclature": "au75359",
            "product_name": "Платье",
            "quantity": 1,
            "shop_barcode": "gdkd642jdp0",
            "shop_variant_id": "б0407-50",
            "variant_name": "Размер - 50"
        },
        {
            "booked_at": "2021-04-27T14:19:44.374Z",  // Дата резервирования товара пользователем
            "nomenclature": "ab54673", // Артикул
            "product_name": "Костюм", // Название товара
            "quantity": 1, // Заказанное количество пользователям
            "shop_barcode": "jftsgd6pda3", // Штрихкод варианта
            "shop_variant_id": "у0624-48", // Уникальный идентификатор варианта
            "variant_name": "Размер - 48" // Название варианта
        }
    ],
    "purchase": {
        "id": 38943, 
        "billed_at": "2021-04-25", 
        "created_at": "2021-04-24T03:00:38.311+03:00", 
        "departure_at": "2021-04-26", 
        "stocked_at": "2021-05-04" 
    }
}
```

`billed_at = 2021-04-25` означает что 25 апреля в 3 часа ночи по мск закупка закроется, на почту будет отправлено письмо 
с csv файлом всех заказанных товаров в данной заупке, поставщику потребуется отравить эти товары на склад Groupprice.

После закрытия закупки `id = 38943` сразу же будет создана новая, и также начнет наполнятся товарами,
у неё уже будет другой номер, и другие даты.

В секции `line_items` один и тот же вариант-товар будет повторятся (`quantity` не будет увеличено), если он заказан несколькими пользователями
```js
{
    "booked_at": "2021-04-27T12:56:12.255Z",
    "nomenclature": "au75359",
    "product_name": "Платье",
    "quantity": 1,
    "shop_barcode": "gdkd642jdp0",
    "variant_name": "Размер - 50"
},
{
    "booked_at": "2021-04-27T14:26:53.629Z",
    "nomenclature": "au75359",
    "product_name": "Платье",
    "quantity": 1,
    "shop_barcode": "gdkd642jdp0",
    "variant_name": "Размер - 50"
},
```

Также товары в `line_items` могут удаляться, если пользователь отменил заказ, поэтому на стороне вызывающей API следует учесть уменьшение количества зарезервированных товаров

**3. Изменение остатков /stocks**

В метод передается массив струтур, содержажих поле `barcode` - штрихкод SKU, и `quantity` - остаток товара на складе поставщика. За один запрос можно изменить наличие не более 1000 SKU.

Пример: 

Запрос:
```bash
curl --location --request POST 'https://psupplier.groupprice.ru/api/test/stocks?api_token=XXXX' \
--header 'accept: application/json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "stocks": [
    {
      "barcode": "1005004632052714",
      "quantity": 1
    }
  ]
}'
```

Ответ:
```js
[
  {
    "barcode": "1005004632052714",
    "quantity": 3,
    "updated": true
  }
]
```

**4. Изменение цен /prices**

В метод передается массив струтур, содержажих поле `barcode` - штрихкод SKU, оптовую цену `price_supplier`. Также может содержать опционально текущую розничную `price_usual` и розничную без скидки `price_before_sale` цены
Пример: 

Запрос:
```bash
curl --insecure --location --request POST 'https://psupplier.groupprice.ru/api/test/prices?api_token=XXXX' \
--header 'accept: application/json' \
--header 'Content-Type: application/json' \
--data-raw '{
  "prices": [
    {
      "barcode": "1005004632052714",
      "price_supplier": 100,
      "price_usual": 200,
      "price_before_sale": 120
    }
  ]
}'
```

Ответ:
```js
[
  {
    "barcode": "1005004632052714",
    "price_supplier": "100.0",
    "price_usual": "200.0",
    "price_before_sale": "120.0",
    "updated": true
  }
]
```

# Интеграция через Webhooks
При данном виде интеграции идет моментальная отправка товара на резервирование сразу после создания заказа пользователем. API-сервис должен отвечать на три метода:
1) резервирование товара
2) отмена резерва
3) финализация отгрузки (закупки)

Примеры HTTP запросов на сервер поставщика можно сэмулировать утилитой https://httpie.io/docs#usage

```
http --json --verbose POST https://domain.ru/api_orders/reserve variant_id=12345 purchase_id=234
http --json --verbose POST https://domain.ru/api_orders/cancel_reserve variant_id=12345 purchase_id=234
http --json --verbose POST https://domain.ru/api_orders/finish_reserve purchase_id=234
```

- `variant_id` штрихкод товара поставщика, или ID варианта
- `purchase_id` - ID закупки groupprice.ru

Данные посылаются в `json` формате (`Content-Type: application/json`), в ответе сервер поставщика должен присылать `json` данные

При успешном резервировании в ответе должен быть http статус 200, `{ result: "ok" }`

При отсутствии товара на складе поставщика - http статус 422
```
{
  error_type: "product_not_available",
  error_message: "Товар не зарезервирован, на складе не достаточное количество"
}
```
