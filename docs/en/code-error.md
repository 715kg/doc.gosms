---
title: Error Codes
icon: material/alert-circle-outline
---




There are many error codes in the system. Below is the complete list of error codes and their descriptions.

| Code | Description |
|:-|:-|
| <kbd>1000</kbd> | [Unknown error](#1000) |
| <kbd>1001</kbd> | [Invalid Json request](#1001) |
| <kbd>1002</kbd> | [Api is inactive. Activate it in the control panel before using it.](#1002) |
| <kbd>1003</kbd> | [Api does not exist.](#1003) |
| <kbd>1004</kbd> | [You have not registered any devices. You can do this through the control panel in the "My devices" section.](#1004) |
| <kbd>1005</kbd> | [Sending SMS is not allowed for this API. Enable this option in your API settings.](#1005) |
| <kbd>1006</kbd> | [Maximum number of SMS on your tariff plan.](#1006) |
| <kbd>1007</kbd> | [Receiving information about SMS is not allowed for this API. Enable this option in your API settings.](#1007) |
| <kbd>1008</kbd> | [SMS with this id does not exist.](#1008) |


| Code | Description |
|:-|:-|
| <kbd>2001</kbd> | [Invalid phone number specified in the phone_number field.](#2001) |
| <kbd>2002</kbd> | [Invalid message text specified in the message field.](#2002) |
| <kbd>2003</kbd> | [Invalid id format.](#2003-2004-2005) |
| <kbd>2004</kbd> | [Invalid callback_id format.](#2003-2004-2005) |
| <kbd>2005</kbd> | [Invalid device_id format.](#2003-2004-2005) |


| Code | Description |
|:-|:-|
| <kbd>3000</kbd> | [Your account is blocked by the administration. Contact the project's technical support.](#error-3000) |

## Solutions for Errors

###### Error `1000`
An unknown error in the system. It occurs when some kind of failure happens, but a detailed description is not provided in the system. This error occurs very rarely, as developers try to describe all possible errors in the system. If the error still occurs at some stage of working with the services, it is better to contact the chat support in the [control panel](https://cms.gosms.ru).

###### Error `1001`
In this case, you should make sure that your JSON request is correctly structured. You can refer to the [documentation on using and working with JSON](https://developer.mozilla.org/en/docs/Learn/JavaScript/Objects/JSON).

###### Error `1002`
This error indicates an inactive API instance. To resolve this issue, go to the control panel, to the [API Integration](https://cms.gosms.ru/api) section, and activate the API instance you are working with.
![activate_api](https://media.gosms.ru/doc.gosms.ru/activate_api.png)

###### Error `1003`
This error occurs if you have deleted a previously used API but continue to authenticate under its token.

###### Error `1004`
This error occurs when trying to send an SMS. If there are no devices registered in your list of devices, the system will not allow you to send messages.
You need to register your devices in the control panel in the section - [My Devices](https://cms.gosms.ru/devices). First, download our mobile application [GoSMS](https://media.gosms.ru/gosms/files/app/v1.0/gosms.apk) for smartphones running on Android 7.0 and above. Install the application on your smartphone from which you plan to send SMS. The smartphone must be connected to mobile internet or Wi-Fi. Then in the control panel, click on the QR block on the image. Scan the QR code that appears in the mobile application.
![activate_api](https://media.gosms.ru/doc.gosms.ru/qr.png)
After the device is successfully displayed in the list of devices, you need to activate it.
![activate_api](https://media.gosms.ru/doc.gosms.ru/activatedevice.png)

###### Error `1005`
This error occurs when your API instance does not have permission to send SMS. To resolve this, go to the control panel, to the [API Integration](https://cms.gosms.ru/api) section. Click the (Edit) button on the API instance you are working with. In the access point (SMS) section, grant the permission (Can send messages).
![activate_api](https://media.gosms.ru/doc.gosms.ru/editApi.png)

###### Error `1006`
You will receive this error if you exceed the limit for sending messages via the API on your tariff plan. In this case, you can switch to a tariff plan with higher limits, or wait for the monthly limits to update if you are on a free tariff plan. You can monitor your limits in the control panel, in the [Subscription and Services](https://cms.gosms.ru/tariff) section.
![activate_api](https://media.gosms.ru/doc.gosms.ru/stats.png)

###### Error `1007`
This error occurs when your API instance does not have permission to read SMS. To resolve this, go to the control panel, to the [API Integration](https://cms.gosms.ru/api) section. Click the (Edit) button on the API instance you are working with. In the access point (SMS) section, grant the permission (Can see messages).
![activate_api](https://media.gosms.ru/doc.gosms.ru/getsms.png)

###### Error `1008`
This error occurs if you try to request information about an SMS from a database that does not exist or has been deleted.

###### Error `2001`
This error occurs if you do not adhere to the format when entering a phone number in the key value phone_number. 
The phone_number key value is a *required* string that can contain the following characters:
Digits from <kbd>0</kbd> to <kbd>9</kbd>
The length of the string should be from <kbd>3</kbd> to <kbd>30</kbd> characters.
"Example: <kbd>79929999999</kbd>

###### Error `2002`
This error occurs if you do not adhere to the format when entering a text message in the key value message. 
The message key value is a *required* string that can contain the following characters:
Latin letters (uppercase and lowercase) <kbd>A-Z</kbd>, <kbd>a-z</kbd>
Russian letters (uppercase and lowercase) <kbd>А-Я</kbd>, <kbd>а-я</kbd>
Digits <kbd>0</kbd>-<kbd>9</kbd>
Symbols <kbd>Ёё</kbd>
Additional allowed symbols: <kbd>-_/.,!+@=#$%^&*(){}[];"'<>?p{L}0-9p{P}s</kbd>
The length of the string should be from <kbd>1</kbd> to <kbd>300</kbd> characters.
"Backtick symbols, <kbd></kbd>, are not allowed.

###### Error `2003`, `2004`, `2005`
This error occurs when you try to enter a text value that differs from the primitive.ObjectID format in keys such as: <kbd>id</kbd>, <kbd>callback_id</kbd>, <kbd>device_id</kbd>  
The primitive.ObjectID value looks like this <kbd>6654a4e8f1527149588c89f2</kbd>.
And is regulated by the system with the regular expression <kbd>^ [0-9a-fA-F]{24}$</kbd>

###### Error `3000`
If you receive this error, in this case, we recommend contacting technical support chat through the [control panel](https://cms.gosms.ru)