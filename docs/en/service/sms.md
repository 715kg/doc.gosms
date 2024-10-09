---
title: SMS Messages
icon: material/message-processing
---

## Sending SMS

You should use `POST` `/sms/send` <div style="font-size:12px">For more detailed information, refer to the <a href="https://docs.gosms.ru/en/request" target="_blank">Requests</a></div><br>

#### Request Example

``` json title="POST: /sms/send"
{
  "message": "My message",  			// string (*required)
  "phone_number": "79999999999",  		// string (*required)
  "callback_id": "",  					// string (*optional)
  "device_id": ""  						// string (*optional)
}
```

|Key |Type |Marker | Values|
|:------------------------ |:- |:- |:- |
| `message`|string |<b style="color:#b13f3f">required</b> | The text of the message to be sent|
| `phone_number`|string |<b style="color:#b13f3f">required</b> | The phone number to which the message is being sent|
| `device_id`|string |`optional`| Contains the object ID of your device. You can find the device ID in the control panel under [My Devices](https://gosms.ru/devices). If this value is set, then only this device will handle the message. If the value is left empty or not passed at all, any device from your list of connected devices will handle the message. This way, you can specify which device processes a particular message. This is useful if you have at least two or more devices connected. Otherwise, leave the value empty or do not pass it at all.|
| `callback_id`|string |`optional` | Works similarly to `device_id`, allowing you to specify which Webhook will handle the event of this message. If the value is left empty or not passed at all, all webhooks with events for SMS message changes will be processed. You can find the Object ID value in the control panel under [Webhook](https://gosms.ru/webhook)|


#### Successful Response
<div style="font-size:12px">For more detailed information, you can find it in the <a href="https://docs.gosms.ru/en/responses" target="_blank">Responses</a></div>

Upon a successful response, the system will return a `200` code and the `ID` of the sent message, which can be used later for SMS operations within the system.


``` json title="HTTP 200 application-json"
{ 
    "id": "6654a4e8f1527149588c89f2"  // string 
}
```

> `String` The values are `id` corresponding `primitive.ObjectID`{.is-info}

## Requesting SMS Information

You should use `POST` `/sms/get`
<div style="font-size:12px">For more detailed information, you can find it in the <a href="https://docs.gosms.ru/request" target="_blank">Requests</a></div>

#### Request Example

``` json title="POST: /sms/get"
{    
    "id": "6654a4e8f1527149588c89f2"  //string (*required)
}
```

|Key |Type |Marker | Values|
|:- |:- |:- |:- |
| `id` |string |<b style="color:#b13f3f">*required</b> | The ID of the SMS request, corresponding to primitive.ObjectID, which was provided to you, for example, during [Sending SMS](#sending-sms) |



#### Successful Response
<div style="font-size:12px">For more detailed information, you can find it in the <a href="https://doc.gosms.ru/en/responses" target="_blank">Responses</a></div>

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

|Key |Type | Values|
|:- |:- |:- |
| `id`         |string | The ID of the SMS, corresponding to primitive.ObjectID |
| `message`    |string | The text of the message |
| `status`     |number | Numerical status of the message:<br> <kbd>0</kbd> - "waiting for processing",<br> <kbd>1</kbd> - "processing",<br> <kbd>2</kbd> - "sent",<br> <kbd>3</kbd> - "send error",<br> <kbd>4</kbd> - "delivered",<br> <kbd>5</kbd> - "delivery error" |
| `callback_id`|string | WebHook ID, corresponding to primitive.ObjectID |
| `device_id`  |string | Device ID, corresponding to primitive.ObjectID |
| `phone_number`|string | Phone number |
| `message_status`|string | Textual status of the SMS, corresponding to the <kbd>status</kbd> field |
| `time_create`|number | Time when the SMS was created, in Unix format|

## Deleting SMS

You should use `DELETE` `/sms/del`
<div style="font-size:12px">For more detailed information, you can find it 
  in the <a href="https://doc.gosms.ru/en/requests" target="_blank">Requests</a></div>
  

  
#### Request Example
  
``` json title="DELETE: /sms/del"
{	
    "id": "6654a4e8f1527149588c89f2"  // string (*required) 
}
```

|Key |Type |Marker | Values|
|:- |:- |:- |:- |
|`id`|string |<b style="color:#b13f3f">*required</b> | The ID of the SMS request, corresponding to primitive.ObjectID, provided to you, for example, during [Sending SMS](#sending-sms) |

#### Successful Response
<div style="font-size:12px">For more detailed information, you can find it in <a href="https://doc.gosms.ru/en/responses" target="_blank">Responses</a></div>

- <b style="color:rgb(29, 129, 39)">HTTP 204 </b><b>No Content</b>

## Request for SMS list

You should use `GET` `/sms`
<div style="font-size:12px">For more detailed information, you can find it in <a href="https://doc.gosms.ru/en/requests" target="_blank">Requests</a></div>

<br>

- Example GET request: `/sms?limit=5&offset=1&search=79999999999`

|Key |Type |Marker | Values|
|:- |:- |:- |:- |
|`limit`|number |<b style="color:#b13f3f">*required</b> | Indicates the number of records to retrieve. Minimum of <kbd>1</kbd> record and maximum of <kbd>100</kbd> records per page.|
|`offset`|number |`optional` | Specifies the offset relative to the beginning of the list. If the parameter is not specified, by default, it is <kbd>1</kbd>, meaning to display from the first page.|
|`search`|string |`optional` | Allows you to specify a set of characters to search for. The system searches for partial matches, regardless of case, in the fields: <kbd>message</kbd> - SMS text, <kbd>message_status</kbd> - SMS text status, <kbd>phone_number</kbd> - phone number.

#### Successful Response
<div style="font-size:12px">For more detailed information, you can find it in <a href="https://doc.gosms.ru/en/responses" target="_blank">Responses</a></div>

For example, you made a request `/sms?limit=2&offset=1`

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

|Key |Type | Values|
|:- |:- |:- |
|`pagination`|object | An object containing keys <kbd>total_records</kbd>, <kbd>limit</kbd>, <kbd>offset</kbd> |
|`total_records`|number | Indicates the total number of SMS in your database. |
|`limit`|number | Indicates the number of records currently returned. Corresponds to the specified parameter <kbd>limit</kbd>  |
|`offset`|number | Indicates the offset relative to the beginning of the list. Corresponds to the offset parameter  |
|`sms_list`|[]object | Represents an array of objects. Each element of the <kbd>sms_list</kbd> array represents one SMS message and contains various properties  |

## Request Errors

When making requests to resources, errors may occur. You can learn more about all possible errors and their scenarios on the [System Error Codes](https://docs.gosms.ru/en/code-error) page.