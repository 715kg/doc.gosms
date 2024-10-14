---
title: Сообщения SMS
icon: material/message-processing
---

## Отправка СМС

Вы должны использовать `POST` `/sms/send` <div style="font-size:12px">Более подробную информацию вы можете найти в <a href="https://docs.gosms.ru/request" target="_blank">Запросах</a></div><br>

#### Пример запроса

``` json title="POST: /sms/send"
{
  "message": "My message",  			// string (*required)
  "phone_number": "79999999999",  		// string (*required)
  "callback_id": "",  					// string (*optional)
  "device_id": ""  						// string (*optional)
}
```

|Ключ |Тип |Маркер | Значения|
|:------------------------ |:- |:- |:- |
| `message`|string |<b style="color:#b13f3f">*обязательный</b> | Текст отправляемого сообщения|
| `phone_number`|string |<b style="color:#b13f3f">*обязательный</b> | Номер на который отправляется сообщения|
| `device_id`|string |`необязательный`| Cодержит object ID вашего устройства. Посмотреть ID устройства можно в панели управления в разделе **([Мои устройства](https://gosms.ru/devices))**. Если данное значение установлено, то обработкой данным смс займется именно это устройства и не какое больше. Если значение остается пустым или не передается вовсе, обработкой смс займется любое устройства из вашего списка подключенных устройств. Тем самым вы можете сами задавать какому устройству обрабатывать то или иное сообщение. Это полезно, если у вас подключено хотя-бы два или более устройств. В противном случаи, оставьте значение пустым или не передавайте его вовсе.|
| `callback_id`|string |`необязательный` | Работает аналогично `device_id`, вы сами можете указать, какой Webhook возьмет в обработку событие данного сообщение. Если значение оставить пустым, или не передавать вовсе, будут отрабатывать все веб хуки, у которых включены события на изменения смс сообщений. Object ID значение, вы можете посмотреть в панели управления, пункт меню **([Webhook](https://gosms.ru/webhook))**|


#### Успешный ответ
<div style="font-size:12px">Более подробную информацию вы можете найти в <a href="https://docs.gosms.ru/responses" target="_blank">Ответах</a></div>


При успешном ответе, система вернет вам код `200` и `id` отправленного сообщения, который можно использовать в дальнейшем для работы с смс в системе.


``` json title="HTTP 200 application-json"
{ 
    "id": "6654a4e8f1527149588c89f2"  // string 
}
```

> `String` значения `id` является соответствием `primitive.ObjectID`{.is-info}

## Запрос информации об СМС

Вы должны использовать `POST` `/sms/get`
<div style="font-size:12px">Более подробную информацию вы можете найти в <a href="https://docs.gosms.ru/request" target="_blank">Запросах</a></div>

#### Пример запроса

``` json title="POST: /sms/get"
{    
    "id": "6654a4e8f1527149588c89f2"  //string (*required)
}
```

|Ключ |Тип |Маркер | Значения|
|:- |:- |:- |:- |
| `id`|string |<b style="color:#b13f3f">*обязательный</b> | Идентификатор запроса СМС, в соответствии primitive.ObjectID, который выдавался вам например при [Отправки СМС](#отправка-смс) |



#### Успешный ответ
<div style="font-size:12px">Более подробную информацию вы можете найти в <a href="https://doc.gosms.ru/responses" target="_blank">Ответах</a></div>


``` json title="HTTP 200 application-json"
{
    "id": "6654a4e8f1527149588c89f2",      // string    
    "message": "test",                     // string    
    "status": 0,                           // number    
    "callback_id": "",                     // string    
    "device_id": "",                       // string    
    "phone_number": "79999999999",         // string    
    "message_status": "Ждет обработки",    // string    
    "time_create": 1716812679              // number
}
```

|Ключ |Тип | Значения|
|:- |:- |:- |
| `id`      |string | Идентификатор СМС, в соответствии primitive.ObjectID |
| `message` |string | Текст сообщения |
| `status`  |number | Числовой статус сообщения.<br> <kbd>0</kbd> - "ждет обработки",<br> <kbd>1</kbd> - "взято в обработку",<br> <kbd>2</kbd> - "отправлено",<br> <kbd>3</kbd> - "ошибка отправки",<br> <kbd>4</kbd> - "доставлено",<br> <kbd>5</kbd> - "ошибка доставки" |
| `callback_id`     |string | Идентификатор WebHook, в соответствии primitive.ObjectID |
| `device_id`       |string | Идентификатор Устройства, в соответствии primitive.ObjectID |
| `phone_number`    |string | Номер телефона |
| `message_status`  |string | Текстовый статус смс, в соответствии с <kbd>status</kbd> |
| `time_create`     |number | Время создания СМС, не путать с доставкой, отправкой и другими статусами. Формат Unix|

## Удаление СМС

Вы должны использовать `DELETE` `/sms/del`
<div style="font-size:12px">Более подробную информацию вы можете найти в 
  <a href="https://doc.gosms.ru/requests" target="_blank">Запросах</a></div>
  

  
#### Пример запроса
  
``` json title="DELETE: /sms/del"
{	
    "id": "6654a4e8f1527149588c89f2"  // string (*required) 
}
```

|Ключ|Тип|Маркер|Значения|
|:- |:- |:- |:- |
|`id`|string |<b style="color:#b13f3f">*обязательный</b> | Идентификатор запроса СМС, в соответствии primitive.ObjectID, который выдавался вам например при [Отправки СМС](#отправка-смс) |

#### Успешный ответ
<div style="font-size:12px">Более подробную информацию вы можете найти в <a href="https://doc.gosms.ru/responses" target="_blank">Ответах</a></div>

- <b style="color:rgb(29, 129, 39)">HTTP 204 </b><b>No Content</b>

## Запрос списка СМС

Вы должны использовать `GET` `/sms`
<div style="font-size:12px">Более подробную информацию вы можете найти в <a href="https://doc.gosms.ru/requests" target="_blank">Запросах</a></div>

<br>

- Пример запроса GET: `/sms?limit=5&offset=1&search=79999999999`

|Ключ |Тип |Маркер | Значения|
|:- |:- |:- |:- |
|`limit`|number |<b style="color:#b13f3f">*обязательный</b> | Обозначает количество записей, которое необходимо вернуть. Минимум <kbd>1</kbd> запись и максимум <kbd>100</kbd> записей нас траницу.|
|`offset`|number |`необязательный` | Указывает на смещение, относительно начала списка. Если параметр не задан, поумолчанию <kbd>1</kbd>, то есть, выводить с первой страницы.|
|`search`|string |`необязательный` | Позволяет указать набор символов для поиска. Система ищет частичные совпадения, без учета регистра по полям: <kbd>message</kbd> - текст смс, <kbd>message_status</kbd> - текстовый статус смс, <kbd>phone_number</kbd> - номер телефона.



#### Успешный ответ
<div style="font-size:12px">Более подробную информацию вы можете найти в <a href="https://doc.gosms.ru/responses" target="_blank">Ответах</a></div>


К примеру, вы выполнили запрос `/sms?limit=2&offset=1`

``` json title="HTTP 200 application-json"
{
  "pagination": {
    "total_records": 95,
    "limit": 2,
    "offset": 1
  },
  "sms_list": [
    {
      "id": "6658053caa16b5ca5c5d72fc",
      "message": "Hello my friends",
      "status": 0,
      "callback_id": "",
      "device_id": "",
      "phone_number": "79929999999",
      "message_status": "Ждет обработки",
      "time_create": 1717044540
    },
    {
      "id": "665727c04a5fad164ea38bb2",
      "message": "Hello World",
      "status": 4,
      "callback_id": "",
      "device_id": "",
      "phone_number": "79929999988",
      "message_status": "Доставлено",
      "time_create": 1716987840
    }
  ]
}
```

|Ключ |Тип | Значения|
|:- |:- |:- |
| `pagination`|object | Обьект, содержащий в себе ключи <kbd>total_records</kbd>, <kbd>limit</kbd>, <kbd>offset</kbd> |
| `total_records`|number | Указывает на общее количество смс у вас в базе. |
| `limit`|number | Указывает на количество записей, которое в данный момент возвращено. Соответствует указанному параметру <kbd>limit</kbd>  |
| `offset`|number | Указывает на смещение, относительно начала списка. Соответствует параметру offset  |
| `sms_list`|[]object | Представляет собой массив обьектов. Каждый элемент массива <kbd>sms_list</kbd> представляет одно SMS сообщение и содержит различные свойства  |

## Ошибки в запросах

При выполнении запроса к ресурсам, могут возникать ошибки. Более подробно ознакомиться со всеми возможными ошибками и их сценариями, вы можете на странице [Коды ошибок системы](https://docs.gosms.ru/code-error)