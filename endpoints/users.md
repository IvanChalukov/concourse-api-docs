# Users

### Get current user info

<details open>
 <summary><code>GET</code> <code><b>/api/v1/user</b></code> <code>(retrieves the current user info)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |

##### Responses

| HTTP Code | Content-Type       | Response Example |
|:---------:|:------------------:|:----------------------:|
| `200`     | `application/json` | See JSON example below |
| `401`     | text/plain; charset=utf-8 | not authorized  |

<details>
<summary>JSON Example for 200 Response</summary>

```json
{
  "sub": "CgR0ZXN0EgVsb2NhbA",
  "name": "test",
  "user_id": "test",
  "user_name": "",
  "email": "test",
  "is_admin": true,
  "is_system": false,
  "teams": {
    "main": [
      "owner"
    ]
  },
  "connector": "local",
  "display_user_id": "test"
}
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url http://localhost:8080/api/v1/user \
  --header 'authorization: Bearer <token>'
```
</details>

---

### List active users since timestamp

<details open>
 <summary><code>GET</code> <code><b>/api/v1/users</b></code> <code>(Gets active users since a given timestamp)</code></summary>

##### Headers
> | name           |  type     | data type                | description                                                           |
> |----------------|-----------|--------------------------|-----------------------------------------------------------------------|
> | Authorization  |  required | string                   | Bearer auth header with the access token                              |

##### Query Parameters
> | name        |  type     | data type | description                                           |
> |-------------|-----------|-----------|-------------------------------------------------------|
> | since       |  optional | string    | The timestamp (YYYY-MM-DD) to list active users since |

##### Responses
| HTTP Code | Content-Type       | Response Example |
|:---------:|:------------------:|:----------------------:|
| `200`     | `application/json` | See JSON example below |
| `401`     | text/plain; charset=utf-8 | not authorized  |

<details>
<summary>JSON Example for 200 Response</summary>

```json
[
  {
    "id": 1,
    "last_login": 1763631929
  },
  {
    "id": 2,
    "username": "test",
    "connector": "local",
    "last_login": 1763632137
  }
]
```
</details>

##### Example cURL
```shell
curl --request GET \
  --url 'http://localhost:8080/api/v1/users?since=1970-01-01' \
  --header 'authorization: Bearer <token>'
```
</details>

---