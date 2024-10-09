---
title: Работа с устройствами
icon: material/cellphone-cog
---

## Получение информации об устройстве

Вы должны использовать `POST` `/devices/get/info` <div style="font-size:12px">Более подробную информацию вы можете найти в <a href="https://docs.gosms.ru/request" target="_blank">Запросах</a></div>

<br>

#### Пример запроса

``` json title="POST: /devices/get/info"
{
  "id": "6622a8bbd963898821ebf934"  			// string (*required)
}
```

|Ключ |Тип |Маркер | Значения|
|:------------------------ |:- |:- |:- |
| `id`|string |<b style="color:#b13f3f">*обязательный</b> | Идентификатор устройства `primitive.ObjectID`. Посмотреть его можно в панели управления в разделе  - [Мои устройства](https://cms.gosms.ru/devices)|


#### Успешный ответ
<div style="font-size:12px">Более подробную информацию вы можете найти в <a href="https://docs.gosms.ru/responses" target="_blank">Ответах</a></div>

``` json title="HTTP 200 application-json"
{
    "id": "6622a8bbd963898821ebf934",
    "device_id": "65bbdaba833da513a46d36222",
    "device_battery_state": "57",
    "device_name": "Poco M3",
    "is_active": true,
    "is_charging": true,
    "last_online_date": "2024-02-01T17:54:02.668Z",
    "console_data": ""
}
```

|Ключ |Тип | Значения|
|:------------------------ |:- |:- |
| `id`|string | Идентификатор устройства `primitive.ObjectID`. |
| `device_id`|string | Идентификатор вашего физического `android` устройства, на котором установлено приложение `GoSMS`. |
| `device_battery_state`|string | Заряд аккумулятора в процентах. |
| `device_name`|string | Имя устройства, определяется автоматически. |
| `is_active`|boolean | Активировано ли устройство. Активировать устройство можно в панели управления в разделе - [Мои устройства](https://cms.gosms.ru/devices). |
| `is_charging`|boolean | Показывает, заряжается ли ваше устройство в данный момент. |
| `last_online_date`|string | Время последнего соединения устройства в нашей системе. Устройство раз в 5 минут дает нашей системе знать, активно ли оно. Можете ориентироваться по этому параметру, если с указанной даты прошло больше 5 минут, значит по каким то причинам, устройство не соединяется с нашей системой. |
| `console_data`|string | Консоль устройства. Вся информация о последних действиях и работе, отображается тут. |


## Активация - деактивация

Вы должны использовать `POST` `/devices/edit` <div style="font-size:12px">Более подробную информацию вы можете найти в <a href="https://docs.gosms.ru/request" target="_blank">Запросах</a></div>

<br>

#### Пример запроса

``` json title="POST: /devices/edit"
{
  "id": "6622a8bbd963898821ebf934",  			// string (*required)
  "is_active": true                             // boolean (optional)
}
```

|Ключ |Тип |Маркер | Значения|
|:------------------------ |:- |:- |:- |
| `id`|string |<b style="color:#b13f3f">*обязательный</b> | Идентификатор устройства `primitive.ObjectID`. Посмотреть его можно в панели управления в разделе  - [Мои устройства](https://cms.gosms.ru/devices)|
| `is_active`|boolean |`необязательный`| Для активации устройства, вы должны передать булевое значение `true` для деактивации `false`. Так как этот ключ необязательный, вы можете вызвать запрос и без него, тогда система будет это расценивать как `false` и устройство будет деактивированно.|

#### Успешный ответ
<div style="font-size:12px">Более подробную информацию вы можете найти в <a href="https://docs.gosms.ru/responses" target="_blank">Ответах</a></div>

- <b style="color:rgb(29, 129, 39)">HTTP 204 </b><b>No Content</b>


## Удаление

Вы должны использовать `POST` `/devices/del` <div style="font-size:12px">Более подробную информацию вы можете найти в <a href="https://docs.gosms.ru/request" target="_blank">Запросах</a></div>

<br>

#### Пример запроса

``` json title="POST: /devices/del"
{
  "id": "6622a8bbd963898821ebf934",  			// string (*required)
}
```

|Ключ |Тип |Маркер | Значения|
|:------------------------ |:- |:- |:- |
| `id`|string |<b style="color:#b13f3f">*обязательный</b> | Идентификатор устройства `primitive.ObjectID`. Посмотреть его можно в панели управления в разделе  - [Мои устройства](https://cms.gosms.ru/devices)|

#### Успешный ответ
<div style="font-size:12px">Более подробную информацию вы можете найти в <a href="https://docs.gosms.ru/responses" target="_blank">Ответах</a></div>

- <b style="color:rgb(29, 129, 39)">HTTP 204 </b><b>No Content</b>