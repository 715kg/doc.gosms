---
title: Device Management
icon: material/cellphone-cog
---

## Retrieving Device Information

You should use the endpoint `POST` `/devices/get/info`. <div style="font-size:12px">For more detailed information, refer to the <a href="https://docs.gosms.ru/en/request" target="_blank">Requests</a></div>

<br>

#### Request Example

``` json title="POST: /devices/get/info"
{
  "id": "6622a8bbd963898821ebf934"  			// string (*required)
}
```

|Key |Type |Marker | Values|
|:------------------------ |:- |:- |:- |
| `id`|string |<b style="color:#b13f3f">*required</b> | The identifier of the device `primitive.ObjectID`. You can find it in the control panel under [My Devices](https://cms.gosms.ru/devices)|


#### Successful Response
<div style="font-size:12px">For more detailed information, refer to the <a href="https://docs.gosms.ru/en/responses" target="_blank">Responses</a></div>

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

|Key |Type | Values|
|:------------------------ |:- |:- |
| `id`|string | The identifier of the device `primitive.ObjectID`. |
| `device_id`|string | The identifier of your physical `Android` device with the `GoSMS` application installed. |
| `device_battery_state`|string | Battery charge percentage. |
| `device_name`|string | Device name, automatically determined. |
| `is_active`|boolean | Whether the device is activated. You can activate the device in the control panel under [My Devices](https://cms.gosms.ru/en/devices). |
| `is_charging`|boolean | Indicates if your device is currently charging. |
| `last_online_date`|string | The time of the device's last connection to our system. The device informs our system every 5 minutes if it is active. If more than 5 minutes have passed since this date, then for some reason, the device is not connecting to our system. |
| `console_data`|string | Device console. All information about recent actions and operations is displayed here. |


## Activation - Deactivation

You should use the endpoint `POST` `/devices/edit`. <div style="font-size:12px">For more detailed information, refer to the <a href="https://docs.gosms.ru/en/request" target="_blank">Requests</a></div>

<br>

#### Request Example

``` json title="POST: /devices/edit"
{
  "id": "6622a8bbd963898821ebf934",  			// string (*required)
  "is_active": true                       // boolean (optional)
}
```

|Key |Type | Marker | Values|
|:------------------------ |:- |:- |:- |
| `id`|string |<b style="color:#b13f3f">*required</b> | The identifier of the device `primitive.ObjectID`. You can find it in the control panel under [My Devices](https://cms.gosms.ru/devices)| 
| `is_active`|boolean |optional | To activate the device, you must pass a boolean value of `true`; for deactivation, pass `false`. Since this key is optional, you can make the request without it, and the system will interpret it as `false`, thus deactivating the device.|

#### Successful Response
<div style="font-size:12px">For more detailed information, refer to the <a href="https://docs.gosms.ru/en/responses" target="_blank">Responses</a></div>


- <b style="color:rgb(29, 129, 39)">HTTP 204 </b><b>No Content</b>


## Deletion

You should use `POST` `/devices/del` <div style="font-size:12px">For more detailed information, refer to the <a href="https://docs.gosms.ru/en/request" target="_blank">Requests</a></div>

<br>

#### Request Example

``` json title="POST: /devices/del"
{
  "id": "6622a8bbd963898821ebf934",  			// string (*required)
}
```

|Key |Type | Marker | Values|
|:------------------------ |:- |:- |:- |
| `id`|string |<b style="color:#b13f3f">*required</b> | The identifier of the device `primitive.ObjectID`. You can find it in the control panel under [My Devices](https://cms.gosms.ru/devices)|

#### Successful Response
<div style="font-size:12px">For more detailed information, refer to the <a href="https://docs.gosms.ru/en/responses" target="_blank">Responses</a></div>

- <b style="color:rgb(29, 129, 39)">HTTP 204 </b><b>No Content</b>