---
title: Responses
icon: material/arrow-u-left-top
---

## Status Codes

Requests will return one of the following HTTP response status codes:

|Status|Description|
|:---------------------------|:----------------------------------------------------|
|`200 OK`|The action on the resource was successfully executed.|
|`201 Created`|The resource was successfully created. The resource may be ready for use or in the process of starting.|
|`204 No Content`|The action on the resource was successfully executed, and the response does not contain additional information in the body.|
|`400 Bad Request`|An invalid request was sent, for example, it lacks mandatory parameters, etc. The response body will contain additional error information.|
|`401 Unauthorized`|Authentication error.|
|`403 Forbidden`|Authentication succeeded, but there are insufficient permissions to perform the action.|
|`404 Not Found`|The requested resource was not found.|
|`429 Too Many Requests`|The request limit for the time period has been reached.|
|`500 Internal Server Error`|Some internal error occurred while processing the request. To resolve this issue, it's best to contact support through the control panel.|

## Successful Response

All endpoints will return data in `JSON` format.

##### Structure of 200 OK Response
``` json title="HTTP/2.0 200 OK"
// (1)
{
    "id":"6654a4e8f1527149588c89f2",                       
    "message": "test", 					            
    "status": 0, 							      
    "callback_id": "", 					         
    "device_id": "",                              
    "phone_number": "79999999999",                  
    "message_status": "Ждет обработки",             
    "time_create": 1716812679                   
}
```

1. This structure may vary depending on the requested resource.

## Error Response

|Field Name  |Type  |Description|
|:--------------|:------|:-------|
| `errors` | object | An object containing nested keys "code" and "message". |
|`code` | number | A short numerical error identifier. |
|`message` | string | Optional. In most cases, the response will contain a human-readable detailed description of the error(s) to help understand what needs to be corrected. |

##### Structure of 400 Bad Request Response
```json title="HTTP/2.0 400 Bad Request"
// (1)
{
    "errors": {
        "code": 2008,
        "message": "Неверно указан номер телефона в поле phone_number.",     
        "hash":"6654a4e8f152"
    }
}
```

1. The structure is the same for all error responses.

## Resource Statuses

It is important to note that when creating most resources within the platform, you will immediately receive a server response with status `200 OK` or `201 Created` and the identifier of the created resource in the response body. However, this resource may still be in a starting state. The list of statuses will vary depending on the resource type. You can view the supported list of statuses in the description of each specific resource.