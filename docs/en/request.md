---
title: Requests
description: Executing requests, URL, parameters.
icon: material/arrow-horizontal-lock
---

## Request Execution

> Requests must be made over HTTPS to the server address https://api.gosms.ru/v1/ to ensure transaction encryption. The following request methods are supported:

| Method       | Description                          |
| :-------------- | :--------------------------------------------------------------------------------------------------------------- |
| `GET`       | :material-check: Retrieves data about collections and individual resources.|
| `POST`       | :material-check: For collections, creates a new resource of that type. Also used to perform actions on a specific resource.  |
| `PUT`       | :material-check-all: Updates an existing resource. |
| `DELETE`    | :material-close:     Deletes a resource. |

`POST`, `PUT`, and `DELETE` methods may include an object in the request body (Body raw) with the content type `application/json`.

## Parameters in Requests

Some collections support pagination, search, or sorting in requests.  
The following parameters need to be included in the request:

- `limit`: Indicates the number of records to return.
- `offset`: Specifies the offset relative to the beginning of the list.
- `search`: Allows specifying a set of characters to search for.
